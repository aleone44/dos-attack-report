# dos-attack-report

================================================================================
LABORATORIO DI SICUREZZA DELLE RETI
SIMULAZIONE E MITIGAZIONE DI UN ATTACCO DOS APPLICATIVO (LAYER 7)
================================================================================

INDICE
1. Introduzione e Contesto Teorico
2. Architettura del Laboratorio Docker
3. Prerequisiti di Sistema
4. Guida Operativa Passo-Passo
   - Passo 1: Creazione dell'Infrastruttura Docker (docker-compose.yml)
   - Passo 2: Configurazione della Baseline Vulnerabile (nginx.conf)
   - Passo 3: Configurazione dei Terminali di Monitoraggio
   - Passo 4: Esecuzione del Test 1 (Saturazione e DoS)
   - Passo 5: Applicazione delle Contromisure (Mitigazione Layer 7)
   - Passo 6: Esecuzione del Test 2 (Verifica della Mitigazione)
5. Tabella Comparativa dei Risultati Sperimentali
6. Struttura Consigliata per il Report Universitario (Framework NIST SP 800-61)
7. Pulizia dell'Ambiente di Test

--------------------------------------------------------------------------------
1. INTRODUZIONE E CONTESTO TEORICO
--------------------------------------------------------------------------------
Gli attacchi di tipo Denial of Service (DoS) e Distributed Denial of Service
(DDoS) mirano a compromettere la Disponibilita di un sistema o servizio di rete,
uno dei tre pilastri fondamentali della sicurezza informatica (triade CIA:
Confidenzialita, Integrita, Disponibilita).

Il principio cardine su cui poggia qualsiasi vettore DoS e l'asimmetria delle
risorse:
- Il costo computazionale, di memoria o di banda per generare una richiesta o
  un pacchetto da parte del client e trascurabile.
- Il costo sostenuto dal server per elaborare la richiesta, mantenere aperto
  il descrittore di socket o interrogare il database e notevolmente superiore.

In questo laboratorio l'attenzione e focalizzata sugli attacchi a livello
applicativo (Layer 7 del modello OSI), in particolare sulle varianti di tipo
HTTP Flood. A differenza dei flood volumetrici Layer 3/4 (es. UDP Flood o SYN
Flood), un attacco Layer 7 genera traffico sintatticamente conforme e
formalmente legittimo, saturando i processi operativi (worker) e i thread
del server web fino a impedire l'evasione delle richieste legittime.

--------------------------------------------------------------------------------
2. ARCHITETTURA DEL LABORATORIO DOCKER
--------------------------------------------------------------------------------
L'esperimento e progettato per essere eseguito all'interno di una rete virtuale
Docker bridge completamente isolata (internal: true), priva di instradamento
verso la rete esterna o Internet.

L'infrastruttura comprende due nodi:
1. lab_target (Indirizzo IP: 172.28.1.10):
   Server web basato su Nginx (Alpine Linux) con quote di risorse hardware
   rigidamente limitate (0.25 vCPU, 64 MB di memoria RAM). Questa limitazione
   consente di evidenziare sperimentalmente il punto di saturazione delle risorse
   senza impattare l'hardware dell'host.
2. lab_tester (Indirizzo IP: 172.28.1.20):
   Container Alpine Linux contenente la suite apache2-utils (nello specifico lo
   strumento di benchmarking ApacheBench "ab") e curl, utilizzato per generare
   carico controllato e campionare i tempi di risposta.

--------------------------------------------------------------------------------
3. PREREQUISITI DI SISTEMA
--------------------------------------------------------------------------------
Prima di avviare il laboratorio, verificare la presenza sulla macchina host di:
- Docker Engine (versione 20.10 o superiore)
- Docker Compose v2

Verifica da terminale:
$ docker --version
$ docker compose version

--------------------------------------------------------------------------------
4. GUIDA OPERATIVA PASSO-PASSO
--------------------------------------------------------------------------------

PASSO 1: CREAZIONE DELL'INFRASTRUTTURA DOCKER
--------------------------------------------------------------------------------
Creare una directory dedicata per il progetto universitario e posizionarsi al
suo interno:

$ mkdir lab-dos-univ && cd lab-dos-univ

Creare il file "docker-compose.yml" con il seguente contenuto esatto:

services:
  web_target:
    image: nginx:alpine
    container_name: lab_target
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    networks:
      isolated_lab:
        ipv4_address: 172.28.1.10
    deploy:
      resources:
        limits:
          cpus: '0.25'
          memory: 64M

  load_generator:
    image: alpine:latest
    container_name: lab_tester
    command: sh -c "apk add --no-cache apache2-utils curl && tail -f /dev/null"
    networks:
      isolated_lab:
        ipv4_address: 172.28.1.20

networks:
  isolated_lab:
    driver: bridge
    internal: true
    ipam:
      config:
        - subnet: 172.28.1.0/24


PASSO 2: CONFIGURAZIONE DELLA BASELINE VULNERABILE (nginx.conf)
--------------------------------------------------------------------------------
Creare il file "nginx.conf" configurato senza alcun meccanismo di limitazione
della frequenza delle richieste (Rate Limiting) e con una capacita di gestione
delle connessioni volutamente ridotta (worker_connections 32):

worker_processes 1;

events {
    worker_connections 32;
}

http {
    server {
        listen 80;
        server_name localhost;

        location / {
            return 200 "Risposta dal server: Servizio Attivo\n";
        }
    }
}

Avviare i container in modalita disaccoppiata (background):
$ docker compose up -d

Verificare che entrambi i container siano nello stato "Up":
$ docker ps


PASSO 3: CONFIGURAZIONE DEI TERMINALI DI MONITORAGGIO
--------------------------------------------------------------------------------
Per raccogliere le evidenze empiriche necessarie alla documentazione accademica,
aprire tre sessioni di terminale indipendenti e affiancate sullo schermo:

- TERMINALE 1 (Monitoraggio metriche hardware in tempo reale):
  $ docker stats lab_target

- TERMINALE 2 (Flusso dei log del web server Nginx):
  $ docker logs -f lab_target

- TERMINALE 3 (Console operativa per l'invio dei test di carico):
  Utilizzata per l'esecuzione dei comandi nei passi successivi.


PASSO 4: ESECUZIONE DEL TEST 1 (SATURAZIONE E DOS)
--------------------------------------------------------------------------------
Dal TERMINALE 3, verificare innanzitutto il comportamento di base (baseline)
inviando una singola richiesta:
$ docker exec -it lab_tester ab -n 1 -c 1 http://172.28.1.10/

Successivamente, avviare un carico ad alta concorrenza composto da 2000 richieste
totali con 100 richieste concorrenti simultanee (valore ampiamente superiore ai
32 slot di connessione allocati nel worker di Nginx):
$ docker exec -it lab_tester ab -n 2000 -c 100 http://172.28.1.10/

Evidenze da rilevare e annotare:
1. Nel Terminale 1 (docker stats): incremento immediato dell'utilizzo della CPU
   verso il tetto massimo del 25% assegnato al container.
2. Nel Terminale 2 (docker logs): comparsa di avvisi critici di sistema, tra cui:
   "[alert] 32 worker_connections are not enough while connecting to upstream"
   Questa voce attesta l'avvenuta saturazione della coda delle connessioni.
3. Nel Terminale 3 (output ApacheBench): incremento drastico della metrica
   "Time per request" e presenza di "Failed requests".


PASSO 5: APPLICAZIONE DELLE CONTROMISURE (MITIGAZIONE LAYER 7)
--------------------------------------------------------------------------------
Intervenire sul file di configurazione "nginx.conf" introducendo:
- Aumento della tabella worker_connections a 512 unita.
- Implementazione dell'algoritmo Leaky Bucket tramite direttiva "limit_req_zone"
  (soglia massima di 5 richieste al secondo per singolo indirizzo IP).
- Implementazione del limite di connessioni simultanee per IP con "limit_conn_zone".
- Riduzione dei timeout applicativi (client_header_timeout, client_body_timeout)
  per neutralizzare attacchi di tipo slow-rate (es. Slowloris).

Sostituire integralmente il contenuto di "nginx.conf" con il seguente:

worker_processes 1;

events {
    worker_connections 512;
}

http {
    # Allocazione zona di memoria (10MB) per tracciare il rate per IP: 5 richieste/secondo
    limit_req_zone $binary_remote_addr zone=req_limit_per_ip:10m rate=5r/s;

    # Allocazione zona di memoria per monitorare il numero di connessioni per IP
    limit_conn_zone $binary_remote_addr zone=conn_limit_per_ip:10m;

    # Timeout ridotti per mitigare connessioni incomplete o frammentate
    client_body_timeout 5s;
    client_header_timeout 5s;
    keepalive_timeout 5s;

    server {
        listen 80;
        server_name localhost;

        location / {
            # Ammette un picco (burst) massimo di 10 richieste; le eccedenze vengono
            # scartate all'istante (nodelay) restituendo lo stato HTTP 429
            limit_req zone=req_limit_per_ip burst=10 nodelay;
            limit_req_status 429;

            # Limite massimo di 10 connessioni contemporanee dallo stesso IP
            limit_conn conn_limit_per_ip 10;
            limit_conn_status 429;

            return 200 "Risposta dal server: Servizio Attivo\n";
        }
    }
}

Applicare la nuova configurazione a caldo senza riavviare il container:
$ docker exec -it lab_target nginx -s reload


PASSO 6: ESECUZIONE DEL TEST 2 (VERIFICA DELLA MITIGAZIONE)
--------------------------------------------------------------------------------
Dal TERMINALE 3, ripetere esattamente il medesimo test di stress eseguito al
Passo 4:
$ docker exec -it lab_tester ab -n 2000 -c 100 http://172.28.1.10/

Evidenze da rilevare e annotare:
1. Nel Terminale 3 (output ApacheBench): comparira la voce "Non-2xx responses",
   con un conteggio di circa 1985-1990 risposte scartate con codice HTTP 429
   (Too Many Requests). Soltanto le prime 10-15 richieste (rientranti nella
   tolleranza della soglia di rate e del burst) riceveranno il codice 200 OK.
2. Nel Terminale 2 (docker logs): comparsa di log operativi di rigetto:
   "[error] limiting requests, excess: ... by zone 'req_limit_per_ip'"
   I worker non esauriscono la memoria interna poiche le connessioni in eccesso
   vengono troncate immediatamente.
3. Il tempo complessivo di evasione del benchmark risulta drasticamente inferiore
   rispetto al Test 1, dimostrando che il server preserva la propria reattivita.

--------------------------------------------------------------------------------
5. TABELLA COMPARATIVA DEI RISULTATI SPERIMENTALI
--------------------------------------------------------------------------------

+-----------------------------------+--------------------+--------------------+
| Metrica Rilevata                  | Test 1 (Baseline)  | Test 2 (Mitigato)  |
+-----------------------------------+--------------------+--------------------+
| Richieste Totali Inviate          | 2000               | 2000               |
| Livello di Concorrenza            | 100 connessioni    | 100 connessioni    |
| Risposte elaborate (200 OK)       | ~1900 - 2000       | ~10 - 15 (Burst)   |
| Risposte bloccate (HTTP 429)      | 0                  | ~1985 - 1990       |
| Errori dei Worker nei log         | Presenti (alert)   | Assenti            |
| Degradazione delle Risorse (CPU)  | Elevata / Saturaz. | Bassa / Controllata|
| Stato complessivo del servizio    | Denial of Service  | Disponibile        |
+-----------------------------------+--------------------+--------------------+

--------------------------------------------------------------------------------
6. STRUTTURA CONSIGLIATA PER IL REPORT UNIVERSITARIO (FRAMEWORK NIST SP 800-61)
--------------------------------------------------------------------------------
Per la formalizzazione accademica del lavoro svolto, si consiglia di articolare
l'elaborato scritto secondo le seguenti macro-sezioni:

1. EXECUTIVE SUMMARY:
   Sintesi dell'obiettivo del laboratorio, descrizione concisa del vettore di
   minaccia testato (HTTP Flood Layer 7) e riassunto numerico dell'efficacia
   delle policy di mitigazione.

2. ANALISI TEORICA DEL VETTORE DI ATTACCO:
   - Definizione dell'attacco DoS/DDoS e collocazione nel modello CIA.
   - Analisi dell'asimmetria delle risorse (computazione vs generazione pacchetti).
   - Differenze tra attacchi volumetrici (L3/L4) e applicativi (L7).
   - Meccanica dell'esaurimento delle connessioni (socket table exhaustion).

3. METODOLOGIA E CONFIGURAZIONE SPERIMENTALE:
   - Architettura della rete virtuale isolata in ambiente containerizzato.
   - Quote di allocazione risorse assegnate a Nginx (cgroups / CPU quota).
   - Parametrizzazione dello strumento di benchmark ApacheBench.

4. VALUTAZIONE DEI RISULTATI (BASELINE VS MITIGAZIONE):
   - Inserimento dei dati estratti da ApacheBench (Tempi di latenza, RPS, errori).
   - Tracciati dei log di Nginx attestanti l'evento anomalo e il successivo blocco.
   - Discussione comparativa basata sulla tabella dei risultati.

5. ARCHITETTURA DI DIFESA E LEZIONI APPRESE (POST-INCIDENT / HARDENING):
   - Funzionamento matematico dell'algoritmo Leaky Bucket / Token Bucket.
   - Limiti intrinseci della mitigazione su singolo host (saturazione della banda
     di uplink a monte dell'host).
   - Soluzioni architetturali per contesti Enterprise distribuiti:
     * Content Delivery Network (CDN) e routing Anycast.
     * Web Application Firewall (WAF) con analisi euristica e reputazionale.
     * Parametri di kernel tuning Linux (/etc/sysctl.conf: TCP SYN Cookies).

--------------------------------------------------------------------------------
7. PULIZIA DELL'AMBIENTE DI TEST
--------------------------------------------------------------------------------
Una volta raccolte le schermate e i log necessari alla redazione del report,
arrestare i servizi ed eliminare i container e la rete virtuale associata
eseguendo:

$ docker compose down
================================================================================
