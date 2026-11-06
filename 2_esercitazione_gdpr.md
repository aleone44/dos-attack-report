# Esercizio Guidato: Audit di Conformità GDPR di un Sito Web

Il presente documento definisce le specifiche operative per l'esecuzione di un audit tecnico e documentale finalizzato alla verifica della conformità di un sito web rispetto al Regolamento Generale sulla Protezione dei Dati (GDPR - Regolamento UE 2016/679) e alla normativa ePrivacy.

---

## 1. Obiettivi di Apprendimento

Il laboratorio si prefigge il conseguimento delle seguenti competenze:
* Analisi strutturata della documentazione informativa (Privacy e Cookie Policy) ai sensi degli artt. 13 e 14 del GDPR.
* Verifica dell'adozione del principio di *Privacy by Default* (art. 25) in relazione alla gestione del consenso preventivo.
* Utilizzo degli strumenti di ispezione di rete e storage dei browser (DevTools) per il monitoraggio dei tracker e dei cookie persistenti.
* Valutazione dei moduli di acquisizione dati (form di contatto, newsletter, aree riservate) in merito alla minimizzazione e alla granularità del consenso.
* Redazione di un report di conformità strutturato secondo standard professionali.

---

## 2. Requisiti Tecnici e Strumenti di Analisi

* **Browser Web** (Google Chrome, Mozilla Firefox o Microsoft Edge) configurato in modalità di navigazione in incognito per garantire l'assenza di sessioni o cookie pregressi.
* **Developer Tools (DevTools)** integrati nel browser (shortcuts: `F12` o `Ctrl+Shift+I` / `Cmd+Option+I`).
* **Tool di supporto opzionali:**
  * Blacklight (The Markup) per l'analisi dei tracker di terze parti.
  * Webbkoll per la verifica delle chiamate di rete e degli header di sicurezza HTTP.

---

## 3. Metodologia di Analisi Operativa

L'audit deve essere condotto procedendo attraverso cinque fasi sequenziali su un target di analisi designato (es. portale e-commerce, testata giornalistica o applicativo web).

### Fase 1: Verifica dei Protocolli di Trasporto
1. Avviare una nuova sessione in navigazione in incognito.
2. Verificare che l'infrastruttura utilizzi esclusivamente il protocollo **HTTPS** con certificato SSL/TLS valido.
3. Testare il reindirizzamento automatico da richieste effettuate su protocollo non sicuro (`http://`) verso l'endpoint cifrato.

### Fase 2: Ispezione del Meccanismo di Gestione del Consenso (Cookie Banner)
*Nota: Non interagire con l'interfaccia grafica prima di aver completato le verifiche tecniche preliminari.*
1. **Analisi dell'interfaccia utente:**
   * Presenza e accessibilità del banner di notifica.
   * Verifica del rispetto del principio di simmetria visiva tra le opzioni di accettazione e rifiuto (medesima evidenza tipografica, dimensionale e cromatico-contrastante).
2. **Analisi tecnica pre-consenso:**
   * Ispezionare la sezione **Application** (o **Archiviazione**) dei DevTools per rilevare l'installazione di cookie non tecnici prima di qualsiasi azione dell'utente.
   * Monitorare la scheda **Network** per intercettare chiamate asincrone verso domini di terze parti (es. analytics, pixel di tracciamento) prima dell'espressione del consenso.
3. **Test di revoca e opposizione:**
   * Validare l'efficacia del comando di rifiuto o chiusura forzata.
   * Verificare la presenza di un meccanismo permanente di revoca o modifica del consenso all'interno del layout di pagina.

### Fase 3: Valutazione della Informativa sul Trattamento dei Dati (Art. 13 GDPR)
Esaminare il testo della Privacy Policy verificando la presenza dei seguenti elementi obbligatori:
1. **Identificazione del Titolare:** Estremi identificativi completi, ragione sociale, sede legale e recapiti di contatto (inclusa PEC).
2. **Responsabile della Protezione dei Dati (DPO):** Indicazione dei canali di contatto dedicati, ove obbligatorio per legge.
3. **Finalità e Basi Giuridiche:** Corresponsione puntuale tra ogni trattamento dichiarato e la relativa base giuridica di cui all'art. 6 del GDPR.
4. **Destinatari e Trasferimenti Extra-UE:** Specificazione dei responsabili esterni del trattamento e garanzie giuridiche adottate per il trasferimento di dati verso paesi terzi (es. Data Privacy Framework o Clausole Contrattuali Standard).
5. **Periodo di Conservazione (Data Retention):** Criteri determinati per la conservazione dei dati per ciascuna finalità.
6. **Diritti dell'Interessato:** Esplicitazione dei diritti di cui agli artt. 15-22 del GDPR e riferimento all'autorità di controllo competente (Garante per la Protezione dei Dati Personali).

### Fase 4: Analisi dei Moduli di Raccolta Dati (Form)
1. **Minimizzazione dei dati (Art. 5.1.c):** Accertarsi che i campi obbligatori siano strettamente proporzionati alla finalità del servizio offerto.
2. **Granularità del consenso:**
   * Presenza di checkbox separate per finalità distinte (es. esecuzione contrattuale vs. attività promozionali/marketing).
   * Verifica del divieto di pre-spuntatura delle caselle di consenso (*opt-in* attivo obbligatorio).

### Fase 5: Integrazione di Risorse Esterne
* Verificare tramite i DevTools se font, librerie, widget di geolocalizzazione o streaming multimediale vengono caricati da server di terze parti senza il preventivo mascheramento dell'indirizzo IP o l'ottenimento del consenso informato.

---

## 4. Deliverable: Scheda di Valutazione e Report di Conformità

Il risultato dell'audit deve essere formalizzato compilando la seguente griglia di riscontro, associando a ciascun parametro lo stato di conformità corrispondente: **Conforme**, **Parzialmente Conforme**, oppure **Non Conforme**.

### Tabella di Riepilogo delle Evidenze

* **URL Target:** `[Inserire URL]`
* **Data di Esecuzione:** `[GG/MM/AAAA]`
* **Gruppo / Auditor di Riferimento:** `[Inserire Identificativo]`

| Area di Verifica | Parametro di Controllo | Stato | Note Tecniche ed Evidenze |
| :--- | :--- | :--- | :--- |
| **Infrastruttura** | Attivazione e forzatura protocollo HTTPS | | |
| **Consenso (Banner)** | Assenza di cookie di profilazione pre-consenso | | |
| **Consenso (Banner)** | Simmetria visiva tra opzioni di accettazione e rifiuto | | |
| **Consenso (Banner)** | Disponibilità di un sistema di revoca permanente | | |
| **Trasparenza (Policy)** | Completezza dei dati identificativi del Titolare | | |
| **Trasparenza (Policy)** | Esplicitazione delle basi giuridiche per finalità | | |
| **Trasparenza (Policy)** | Definizione dei termini di conservazione dei dati | | |
| **Trasparenza (Policy)** | Indicazione dei trasferimenti Extra-UE | | |
| **Raccolta Dati (Form)**| Applicazione del principio di minimizzazione | | |
| **Raccolta Dati (Form)**| Separazione e granularità dei consensi | | |
| **Raccolta Dati (Form)**| Assenza di meccanismi di pre-flagging | | |
| **Risorse Esterne** | Blocco preventivo di widget e font remoti | | |

---

### Conclusioni e Piano di Azione Correttiva (Remediation Plan)

La redazione del report deve concludersi con una sintesi tecnica (circa 15-20 righe) contenente:
1. **Valutazione di rischio complessiva** dell'infrastruttura esaminata.
2. **Elenco delle criticità prioritarie** riscontrate in ordine di gravità normativa.
3. **Proposta di interventi correttivi** di natura tecnica e legale necessari al raggiungimento della piena conformità.
