# Esercizio Guidato: Audit di Conformità GDPR di un Sito Web

Il presente documento definisce le specifiche operative per l'esecuzione di un audit tecnico e documentale finalizzato alla verifica della conformità di un sito web rispetto al Regolamento Generale sulla Protezione dei Dati (GDPR - Regolamento UE 2016/679) e alla direttiva ePrivacy.

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


































---
### Sezione dettagliata della guida 
# Laboratorio di Verifica Tecnica e Normativa: Audit di Conformità GDPR e Direttiva ePrivacy

Il presente documento definisce le specifiche operative per l'esecuzione di un'analisi di conformità (Audit) su un'applicazione web pubblica. L'attività richiede l'esame congiunto dei presidi tecnico-informatici e della documentazione legale esposta dal sito, al fine di determinare l'aderenza al Regolamento (UE) 2016/679 (GDPR), alla Direttiva 2002/58/CE (ePrivacy), al D.Lgs. 196/2003 novellato dal D.Lgs. 101/2018 e alle "Linee guida cookie e altri strumenti di tracciamento" emanate dal Garante per la protezione dei dati personali (Provvedimento del 10 giugno 2021).

Il documento è suddiviso in due sezioni:
* **Sezione 1:** Protocollo di Verifica (Quadro sinottico delle aree di analisi).
* **Sezione 2:** Manuale Operativo Passo-Passo (Procedure tecniche dettagliate per l'esecuzione dei test).

---

## SEZIONE 1: Protocollo di Verifica

### 1.1 Obiettivi Tecnici e Formativi
Al termine dell'attività di verifica, l'analista dovrà essere in grado di:
1. Valutare la conformità formale e sostanziale dell'informativa sul trattamento dei dati personali ai sensi degli artt. 13 e 14 del GDPR.
2. Analizzare l'architettura delle piattaforme di gestione del consenso (CMP - *Consent Management Platform*) in relazione ai principi di *Privacy by Design* e *Privacy by Default* (art. 25 GDPR).
3. Intercettare e classificare i cookie, gli oggetti di archiviazione locale (*Local Storage*, *Session Storage*) e le richieste di rete (*Network Requests*) verso domini di terze parti prima e dopo la manifestazione del consenso.
4. Verificare la corretta implementazione dei punti di raccolta dati (form HTML) rispetto ai principi di minimizzazione (art. 5, par. 1, lett. c) e granularità del consenso (art. 7 e Considerando 32 e 43).
5. Redigere un rapporto tecnico di audit contenente le evidenze raccolte, la valutazione del rischio e il piano di rientro (*Remediation Plan*).

### 1.2 Prerequisiti e Strumentazione Tecnica
* **Browser Web aggiornato** (Google Chrome, Mozilla Firefox o Microsoft Edge) avviato in sessione isolata (Modalità Incognito / Navigazione Privata) con qualsiasi blocco di tracciamento nativo o estensione *AdBlocker* disabilitati, per non falsare le rilevazioni sul comportamento nativo del sito.
* **Strumenti di sviluppo integrati (Browser DevTools)** per l'ispezione del DOM, dello storage client-side e del traffico HTTP/HTTPS.
* **Utility di interrogazione di rete e DNS** (terminale con `curl`, `openssl`, `nslookup` o `dig`, oppure analizzatori passivi equivalenti).

---

## SEZIONE 2: Manuale Operativo Passo-Passo

Questa sezione illustra nel dettaglio le procedure tecniche da eseguire per ciascuna fase dell'audit. Seguire rigorosamente l'ordine cronologico indicato per non contaminare lo stato della sessione del browser.

---

### FASE 1: Sicurezza del Trasporto e Configurazione di Rete (Art. 32 GDPR)

L'art. 32 del GDPR impone l'adozione di misure tecniche adeguate a garantire la sicurezza dei dati, inclusa la cifratura dei dati in transito.

#### Passo 1.1: Preparazione dell'ambiente sterile
1. Avviare il browser in **Modalità di Navigazione in Incognito** (`Ctrl+Shift+N` su Chrome/Edge, `Ctrl+Shift+P` su Firefox).
2. Disattivare temporaneamente eventuali protezioni antitracciamento integrate nel browser (es. "Protezione antitracciamento avanzata" di Firefox impostata su "Personalizzata" deselezionando i blocchi cookie) per osservare il reale comportamento del sito per un utente standard.
3. Prima di digitare l'URL del sito da analizzare, aprire una scheda vuota, premere `F12` per avviare i **DevTools**, selezionare la scheda **Network** (Rete) e attivare la casella **Preserve log** (Mantieni log). Questo impedirà la cancellazione delle tracce in caso di reindirizzamenti (HTTP 301/302).

#### Passo 1.2: Verifica della forzatura HTTPS e dell'header HSTS
1. Nella barra degli indirizzi, digitare esplicitamente l'URL del sito utilizzando il protocollo non sicuro: `http://www.nomesito.it` e premere Invio.
2. Osservare la prima riga nella scheda **Network** dei DevTools:
   * **Comportamento conforme:** Il server risponde con uno stato `301 Moved Permanently` o `307 Internal Redirect` (o `308 Permanent Redirect`) reindirizzando immediatamente il client verso `https://www.nomesito.it`.
   * **Comportamento non conforme:** La pagina viene renderizzata rimanendo su protocollo `http://` (stato `200 OK` su porta 80), esponendo la navigazione e gli eventuali form a intercettazioni *Man-in-the-Middle*.
3. Cliccare sulla prima richiesta con protocollo `https://` nella scheda **Network** e selezionare il pannello **Headers** (Intestazioni) -> **Response Headers** (Intestazioni di risposta).
4. Cercare l'header `Strict-Transport-Security` (HSTS). La sua presenza (es. `max-age=31536000; includeSubDomains`) garantisce che il browser rifiuti connessioni HTTP future verso quel dominio. Annotare la presenza o l'assenza di tale header.

#### Passo 1.3: Ispezione del Certificato TLS
1. Cliccare sull'icona di stato della connessione a sinistra dell'URL nella barra degli indirizzi -> **La connessione è sicura** -> **Il certificato è valido** (oppure utilizzare la scheda **Security** nei DevTools).
2. Verificare che il certificato non sia scaduto, che il *Common Name* (CN) o il *Subject Alternative Name* (SAN) corrisponda al dominio visitato e che il protocollo negoziato sia **TLS 1.2** o **TLS 1.3** (i protocolli TLS 1.0 e 1.1 sono deprecati e non conformi agli standard di sicurezza attuali).

---

### FASE 2: Verifica Tecnica della CMP e dei Tracciatori (Direttiva ePrivacy e Linee Guida Garante)

**ATTENZIONE:** In questa fase iniziale **non interagire con la pagina**, non scorrere (*scroll*) e non cliccare su alcun pulsante del Cookie Banner.

#### Passo 2.1: Analisi dell'interfaccia del Cookie Banner (Design e Dark Pattern)
Esaminare visivamente e tramite l'ispettore DOM (`Ctrl+Shift+C`) il banner di primo livello presentato all'utente:
1. **Presenza del comando di rifiuto/chiusura:** Verificare l'esistenza di una "X" in alto a destra o di un pulsante esplicito "Rifiuta" / "Continua senza accettare".
2. **Simmetria visiva:** Con lo strumento di selezione elemento (`Inspect`), cliccare sul pulsante "Accetta" e successivamente sul pulsante "Rifiuta" (o sulla "X"). Nel pannello **Styles / Computed** dei DevTools, confrontare:
   * `font-size` (dimensione del carattere)
   * `background-color` e `color` (contrasto cromatico)
   * Dimensioni del box (`width`, `height`, `padding`).
   * *Nota di conformità:* Se il pulsante "Accetta" è un bottone ad alto contrasto mentre l'opzione di rifiuto è un semplice link testuale sbiadito o nascosto nel testo, oppure richiede di aprire il pannello "Personalizza" (secondo livello) per poter negare il consenso, si configura un *Dark Pattern* non conforme alle Linee Guida del Garante.
3. **Verifica assenza di Cookie Wall:** Verificare se il sito impedisce completamente l'accesso ai contenuti a meno che non si clicchi su "Accetta" (pratica illecita, salvo rari casi di modello *Pay or Okay* regolamentati specificamente per grandi editori con alternativa di abbonamento equa).
4. **Test dello Scroll:** Effettuare uno scorrimento della pagina verso il basso con la rotellina del mouse. Il banner non deve scomparire interpretando lo scroll come consenso implicito (il consenso mediante semplice *scrolling* è vietato, salvo sia inserito in un processo documentabile e inequivocabile ormai in disuso).

#### Passo 2.2: Ispezione dello Storage Client-Side (Pre-Consenso)
Senza aver ancora interagito con il banner, verificare se il sito ha già installato tracciatori non tecnici:
1. Nei DevTools, selezionare la scheda **Application** (su Chrome/Edge) o **Archiviazione** (su Firefox).
2. Nel menu laterale sinistro, espandere la voce **Cookies** e selezionare il dominio del sito (e gli eventuali sottodomini o domini di terze parti elencati).
3. Esaminare la tabella dei cookie presenti (colonne `Name`, `Domain`, `Value`, `Expires / Max-Age`).
4. Cercare la presenza di cookie analitici non anonimizzati o di profilazione/marketing prima del consenso. Di seguito i più comuni da ricercare:
   * **Google Analytics / Ads:** `_ga`, `_gid`, `_gat`, `_gcl_au`, `IDE`, `test_cookie` (dominio `.doubleclick.net`).
   * **Meta (Facebook / Instagram):** `_fbp`, `_fbc`, `fr` (dominio `.facebook.com`).
   * **TikTok:** `_ttp`, `_tt_enable_cookie`.
   * **Hotjar / Clarity / Mouseflow:** `_hjSessionUser_*`, `_hjSession_*`, `_clck`, `_clsk`.
   * **LinkedIn / HubSpot / Criteo:** `bcookie`, `li_sugr`, `UserMatchHistory`, `__hssc`, `__hstc`, `hubspotutk`, `uid`.
5. Espandere anche le voci **Local Storage** e **Session Storage** nel menu laterale della scheda **Application**. Molti script moderni salvano identificatori univoci di tracciamento nel Local Storage invece che nei cookie per eludere i controlli superficiali (la normativa si applica identicamente anche al Local Storage).
6. **Valutazione:** Se in questa fase (prima del clic) è presente anche un solo cookie o elemento di storage appartenente alle categorie di marketing/profilazione o analitici di terze parti non adeguatamente mascherati, **il sito è in violazione diretta dell'art. 122 del Codice Privacy e dell'art. 25 del GDPR** (mancato blocco preventivo).

#### Passo 2.3: Ispezione del Traffico di Rete (Network) Pre-Consenso
Anche se un sito non salva cookie sul browser, potrebbe comunque inviare l'indirizzo IP dell'utente e i parametri di navigazione a server di terze parti tramite *tracking pixel* o API (es. *Google Consent Mode* configurata senza anonimizzazione o *Meta Pixel* attivo).
1. Portarsi nella scheda **Network** dei DevTools.
2. Nella barra **Filter** (Filtro) in alto a sinistra, digitare uno alla volta i seguenti termini chiave per verificare se sono partite chiamate HTTP/HTTPS verso server di tracciamento prima del consenso:
   * `collect` (identifica chiamate verso Google Analytics: `google-analytics.com/g/collect`).
   * `tr?` o `fbevents` (identifica chiamate verso Meta/Facebook: `facebook.com/tr?id=...`).
   * `adsct` o `pagead` (identifica chiamate pubblicitarie Google/Twitter).
   * `clarity` o `hotjar` (identifica session recording).
3. *Approfondimento su Google Consent Mode v2:* Se si individua una chiamata verso `google-analytics.com/g/collect` prima del consenso, cliccarci sopra e aprire la sottoscheda **Payload** (Parametri). Cercare il parametro `gcs` (Google Consent State):
   * Se `gcs=G100`, significa che sia `ad_storage` che `analytics_storage` sono negati (`00`), ma il sito sta comunque inviando *cookieless pings* a Google (comportamento comunque discusso dalle autorità europee perché trasmette l'indirizzo IP a server terzi senza consenso).
   * Se `gcs=G111` prima del clic sul banner, il sito sta trasmettendo dati con flag di consenso attivo in modo illecito.

#### Passo 2.4: Verifica del Rifiuto del Consenso
1. Cliccare sul pulsante **"Rifiuta tutti"** o sulla **"X"** di chiusura del banner.
2. Osservare nuovamente la scheda **Application -> Cookies** e la scheda **Network**:
   * Deve comparire esclusivamente un cookie tecnico (o una chiave nel Local Storage) che memorizza la scelta negativa dell'utente (es. `CookieConsent`, `euconsent-v2`, `cmplz_banner-status=dismissed`, `iub_cs-*`).
   * Non deve essere generata alcuna nuova richiesta verso tracker pubblicitari né installato alcun cookie di profilazione.

#### Passo 2.5: Verifica dell'Accettazione e della Revocabilità (Art. 7, par. 3 GDPR)
1. Cancellare tutti i dati del sito: nei DevTools, andare su **Application -> Storage** (nel menu a sinistra) e cliccare sul pulsante **Clear site data** (Cancella dati sito), quindi ricaricare la pagina (`F5`) per far riapparire il banner.
2. Cliccare su **"Accetta tutti"** e annotare tutti i cookie di profilazione/analitici che vengono ora installati nella scheda **Cookies**.
3. Individuare nella pagina (solitamente in basso a sinistra/destra come icona fluttuante, oppure come link testuale nel footer denominato *"Preferenze Cookie"*, *"Gestisci consenso"* o *"Rivedi scelte cookie"*) lo strumento per riaprire il banner.
   * *Nota:* Se una volta chiuso il banner non esiste alcun modo per riaprirlo senza dover cancellare manualmente i cookie dal browser, il sito **non è conforme** all'art. 7, par. 3 del GDPR ("È. facile revocare il consenso tanto quanto darlo").
4. Riaprire il pannello tramite il link/icona, revocare tutti i consensi (o cliccare su "Rifiuta tutti") e salvare.
5. Tornare su **Application -> Cookies** e ricaricare la pagina: verificare se i cookie di profilazione installati al punto 2 sono stati effettivamente rimossi o se i relativi script hanno cessato di trasmettere dati nella scheda **Network**.

---

### FASE 3: Analisi Legale e Strutturale dell'Informativa (Artt. 12, 13 e 14 GDPR)

Individuare i link alla **Privacy Policy** e alla **Cookie Policy** (verificando che siano visibili e accessibili da ogni pagina del sito, tipicamente nel footer, e che non siano rotti o restituiscano errori `404`).

Eseguire un controllo incrociato del testo ricercando i seguenti 8 elementi obbligatori (utilizzare `Ctrl+F` nella pagina della policy per velocizzare l'individuazione dei termini):

#### Passo 3.1: Identità e dati di contatto del Titolare (Art. 13, par. 1, lett. a)
* **Cosa cercare:** Ragione sociale completa dell'azienda (o nome e cognome se persona fisica/ditta individuale), indirizzo della sede legale, Partita IVA/Codice Fiscale e un recapito di contatto diretto (indirizzo email ordinario e/o PEC).
* **Errore comune di non conformità:** Informative generate con template automatici in cui è rimasto un segnaposto vuoto, oppure in cui è indicato solo il nome commerciale del sito (es. *"Il Titolare è lo staff di NomeSito.it"*) senza alcuna entità giuridica identificabile.

#### Passo 3.2: Dati di contatto del DPO / RPD (Art. 13, par. 1, lett. b)
* **Cosa cercare:** Se il sito appartiene a un ente pubblico, a una struttura sanitaria, a un istituto bancario/assicurativo o a un'azienda che effettua monitoraggio regolare e sistematico su larga scala (art. 37 GDPR), deve essere indicato il contatto del *Data Protection Officer* (es. `dpo@azienda.it`).

#### Passo 3.3: Matrice Finalità / Base Giuridica (Art. 13, par. 1, lett. c)
* **Cosa verificare:** L'informativa non deve elencare le finalità in un blocco unico e le basi giuridiche in un altro blocco indistinto. Per ogni singolo trattamento deve essere chiaro quale delle 6 basi giuridiche dell'art. 6 GDPR viene applicata:
  1. *Risposta a richieste di contatto / preventivi:* Esecuzione di misure precontrattuali (art. 6.1.b).
  2. *Vendita prodotti e spedizione (e-commerce):* Esecuzione di un contratto (art. 6.1.b).
  3. *Fatturazione e adempimenti fiscali:* Obbligo legale (art. 6.1.c).
  4. *Invio di newsletter promozionali / DEM / Profilazione:* Consenso specifico dell'interessato (art. 6.1.a).
  5. *Sicurezza informatica e prevenzione frodi:* Legittimo interesse del titolare (art. 6.1.f).
* **Errore comune di non conformità:** Citare ancora l'*"Art. 23 del D.Lgs. 196/2003"* non aggiornato, oppure dichiarare di basare il marketing diretto o la profilazione sul "Legittimo Interesse" o sull'"Esecuzione del contratto" anziché sul consenso (salvo il caso specifico di *Soft Spam* ex art. 130 comma 4 del Codice Privacy per clienti già acquisiti).

#### Passo 3.4: Destinatari dei dati e Fornitori Terzi (Art. 13, par. 1, lett. e)
* **Cosa verificare:** L'informativa dichiara a quali soggetti o categorie di soggetti vengono comunicati i dati? Confrontare quanto dichiarato nella policy con quanto rilevato tecnicamente nella Fase 2:
  * Se nella Fase 2 sono state rilevate chiamate a *Google Analytics*, *Meta Pixel*, *Mailchimp*, *Stripe* o *HubSpot*, tali fornitori (o le rispettive categorie specifiche) devono essere menzionati nella Privacy/Cookie Policy. Se un tracker è presente sul sito ma non è citato nella documentazione, l'informativa è incompleta e mendace.

#### Passo 3.5: Trasferimento di dati verso Paesi Terzi Extra-SEE (Art. 13, par. 1, lett. f e Artt. 44-49)
* **Cosa cercare:** Cercare nel testo parole come *"Trasferimento"*, *"Extra-UE"*, *"Stati Uniti"*, *"USA"*.
* **Cosa verificare:** Se il sito utilizza servizi statunitensi (Google, Meta, AWS, Cloudflare, Mailchimp), deve dichiarare su quale strumento giuridico si basa il trasferimento:
  * **Conforme:** Riferimento alla Decisione di Adeguatezza della Commissione Europea del 10 luglio 2023 (**EU-U.S. Data Privacy Framework - DPF**) o alla stipula di **Clausole Contrattuali Standard (SCC)** ex art. 46 GDPR.
  * **Gravemente non conforme (Obsoleto):** Riferimento al **Privacy Shield** (invalidato dalla Corte di Giustizia UE con la sentenza *Schrems II* nel luglio 2020) o al **Safe Harbor** (invalidato nel 2015).

#### Passo 3.6: Periodo di conservazione dei dati - Data Retention (Art. 13, par. 2, lett. a)
* **Cosa verificare:** Per ciascuna finalità deve essere indicato un termine temporale preciso o il criterio oggettivo per determinarlo:
  * *Dati di fatturazione:* 10 anni (ex art. 2220 Codice Civile).
  * *Dati di contatto per preventivo non seguito da contratto:* es. 6 mesi o 1 anno.
  * *Dati per finalità di marketing/profilazione:* Periodo definito e proporzionato (es. 24 mesi per il marketing, 12 mesi per la profilazione secondo la prassi del Garante, o comunque un termine temporale definito sottoposto a verifica periodica).
* **Errore comune:** La dicitura generica *"I dati saranno conservati per il tempo strettamente necessario al raggiungimento delle finalità"* senza alcuna quantificazione temporale, oppure *"I dati saranno conservati fino a revoca del consenso"* come unica indicazione per tutti i trattamenti.

#### Passo 3.7: Diritti dell'Interessato e Reclamo al Garante (Art. 13, par. 2, lett. b, d)
* **Cosa verificare:** Presenza dell'elenco completo dei diritti previsti dagli artt. 15-22 del GDPR (accesso, rettifica, cancellazione/oblio, limitazione del trattamento, portabilità dei dati, opposizione al trattamento) con l'indicazione pratica di come esercitarli (es. invio email all'indirizzo del Titolare).
* Deve essere esplicitamente menzionato il diritto di proporre reclamo all'**Autorità Garante per la protezione dei dati personali** (art. 77 GDPR).

#### Passo 3.8: Tabella Analitica dei Cookie (Cookie Policy)
* **Cosa verificare:** La Cookie Policy (integrata nella Privacy Policy o su pagina dedicata) deve contenere un elenco aggiornato dei cookie effettivamente utilizzati dal sito, suddivisi per categoria (Tecnici, Analitici, Profilazione/Marketing), indicando per ciascuno: **Nome del cookie**, **Fornitore (Prima o Terza parte)**, **Finalità** e **Durata (Scadenza)**.
* Confrontare questa tabella con i cookie effettivamente rilevati nei DevTools durante la Fase 2.5 (dopo aver cliccato su "Accetta tutti").

---

### FASE 4: Verifica dei Moduli di Raccolta Dati - Form HTML (Artt. 5, 7 e 32 GDPR)

Navigare sul sito alla ricerca di tutti i punti di immissione dati: pagina *"Contatti"*, box *"Iscriviti alla Newsletter"*, pagina *"Lavora con noi"*, pagina *"Registrazione / Checkout"*.

#### Passo 4.1: Verifica del Principio di Minimizzazione (Art. 5, par. 1, lett. c)
1. Osservare i campi del form e distinguere quelli obbligatori (contrassegnati da asterisco `*` o dall'attributo HTML `required` verificabile con tasto destro -> **Ispeziona** sul campo `<input>`) da quelli facoltativi.
2. Valutare la pertinenza rispetto alla finalità:
   * **Esempio in un form Newsletter:** L'unico dato strettamente necessario per inviare un'email è l'indirizzo email (eventualmente il nome per personalizzare il saluto, ma preferibilmente facoltativo). Se il form obbliga l'utente a inserire *Cognome, Data di nascita, Indirizzo fisico, Numero di cellulare o Professione* per ricevere una semplice newsletter, viola il principio di minimizzazione.
   * **Esempio in un form di Contatto rapido:** Rendere obbligatorio il *Codice Fiscale* o l'*Indirizzo di residenza* per una semplice richiesta di informazioni generali è non conforme.

#### Passo 4.2: Verifica dell'Informativa Breve e del Link di Rinvio
1. Subito sotto i campi di input (prima del pulsante di invio `Submit`), verificare che sia presente una dicitura che rimandi con un link cliccabile alla Privacy Policy completa (es. *"Ho letto l'Informativa Privacy..."* o *"Inviando il modulo dichiari di aver preso visione dell'Informativa sulla Privacy"*).
2. *Nota giuridica importante:* Per un semplice **form di contatto** (dove l'utente scrive per chiedere informazioni), la base giuridica corretta è l'esecuzione di misure precontrattuali su richiesta dell'interessato (art. 6, par. 1, lett. b). Pertanto, non sarebbe nemmeno necessario un checkbox di "consenso" per rispondere alla richiesta, ma solo la presa visione dell'informativa. Tuttavia, molti siti inseriscono un checkbox di presa visione: ciò è tollerato purché sia distinto da eventuali consensi marketing.

#### Passo 4.3: Verifica della Granularità e Libertà del Consenso (Art. 7 e Cons. 43)
Se il form raccoglie dati anche per finalità ulteriori (es. iscrizione alla newsletter, invio di comunicazioni commerciali, profilazione o comunicazione dei dati a partner terzi):
1. **Separazione dei Checkbox (Granularità):** Deve esserci un checkbox dedicato e separato per **ciascuna** finalità distinta:
   * Checkbox 1: Presa visione informativa / gestione richiesta contatto.
   * Checkbox 2 (Opzionale): *"Acconsento al trattamento dei dati per l'invio di comunicazioni promozionali e newsletter"*.
   * Checkbox 3 (Opzionale): *"Acconsento alla comunicazione dei miei dati a società terze partner per loro finalità di marketing"*.
2. **Test di Invio (Verifica assenza di "Bundled Consent"):** Provare a compilare il form (con dati di test o verificando il blocco client-side) **senza spuntare** i checkbox di marketing (Checkbox 2 e 3).
   * Se il form blocca l'invio mostrando un messaggio di errore (o se l'elemento `<input type="checkbox">` del marketing possiede l'attributo HTML `required`), il consenso è **estorto/condizionato** e quindi **nullo e illecito** ai sensi dell'art. 7, par. 4 del GDPR.
   * **Gravemente non conforme:** Un unico checkbox con una frase cumulativa come *"Accetto la Privacy Policy e acconsento a ricevere comunicazioni promozionali"*. In questo caso l'utente non può inviare una richiesta di contatto senza iscriversi forzatamente al marketing.
3. **Verifica assenza di caselle pre-spuntate (No Pre-ticked Boxes):** Ricaricare la pagina e osservare i checkbox prima di toccarli (o ispezionare il codice HTML verificando l'assenza dell'attributo `checked`). Nessuna casella di consenso deve essere pre-selezionata di default (sentenza *Planet49* della Corte di Giustizia UE).

---

### FASE 5: Inclusione di Risorse Esterne e Servizi di Terze Parti (Art. 25 e 44 GDPR)

Quando un browser carica un font, una mappa interattiva, un video o una libreria JavaScript da un server esterno (CDN), trasmette automaticamente a quel server terzo l'**indirizzo IP dell'utente** (che è un dato personale ai sensi del GDPR), oltre a *User-Agent* e *Referer* header.

#### Passo 5.1: Rilevamento delle Connessioni a Domini Terzi
1. Tornare in una sessione in incognito pulita (senza aver accettato il cookie banner).
2. Aprire i DevTools -> scheda **Sources** (Origini) -> pannello **Page** (Pagina) a sinistra.
3. Qui è visibile l'albero di tutti i domini da cui la pagina corrente sta scaricando file. Qualsiasi dominio diverso da quello del sito analizzato rappresenta una connessione verso terze parti avvenuta **senza consenso**.
4. In alternativa, nella scheda **Network**, cliccare con il tasto destro sull'intestazione delle colonne della tabella (dove c'è scritto *Name, Status, Type*) e spuntare la voce **Domain** per visualizzare chiaramente il dominio di destinazione di ogni singola richiesta.

#### Passo 5.2: Verifica di Google Fonts / Adobe Fonts
1. Nella lista dei domini (scheda **Sources** o colonna **Domain** in **Network**), cercare `fonts.googleapis.com`, `fonts.gstatic.com` o `use.typekit.net`.
2. **Valutazione:**
   * **Conforme (Self-Hosting):** I file dei caratteri (`.woff2`, `.ttf`) vengono caricati direttamente dal dominio del sito stesso (es. `www.nomesito.it/wp-content/uploads/fonts/...`). Nessun dato viene inviato a Google.
   * **Criticità / Rischio (Remote Loading):** I font vengono scaricati in tempo reale dai server di Google/Adobe al caricamento della pagina, esponendo l'IP del visitatore prima di qualsiasi consenso (pratica sanzionata da diversi tribunali europei, es. LG München I, in quanto tecnicamente evitabile tramite l'hosting locale dei font).

#### Passo 5.3: Verifica di Iframe Incorporati (YouTube, Vimeo, Google Maps, Social Widget)
1. Cercare nel sito (spesso nella homepage o nella pagina "Contatti") eventuali video incorporati o mappe stradali interattive.
2. Ricaricare la pagina rifiutando i cookie nel banner iniziale.
3. **Comportamento Conforme (Blocco Preventivo / Placeholder):** Al posto della mappa di Google Maps o del video di YouTube viene mostrato un riquadro statico (un'immagine segnaposto ospitata localmente) con un avviso del tipo: *"Per visualizzare la mappa/il video è necessario accettare i cookie di terze parti. Clicca qui per abilitare"*. Nessuna chiamata verso `youtube.com`, `googlevideo.com` o `maps.googleapis.com` appare nella scheda **Network** finché l'utente non clicca.
   *(Nota per YouTube: anche l'uso del dominio `youtube-nocookie.com`, pur riducendo i cookie iniziali, carica comunque script e font dai server Google ed è preferibile che sia sottoposto a blocco preventivo o click-to-load).*
4. **Comportamento Non Conforme:** La mappa interattiva o il player di YouTube vengono caricati immediatamente anche se l'utente ha rifiutato i cookie, installando cookie e oggetti di storage di Google (`PREF`, `VISITOR_INFO1_LIVE`, `YSC`) senza consenso.

#### Passo 5.4: Verifica di Sistemi Anti-Bot (Google reCAPTCHA)
1. Nei form di contatto (Fase 4), verificare se viene utilizzato **Google reCAPTCHA** (visibile tramite il badge in basso a destra o la casella *"Non sono un robot"*).
2. Controllare nella scheda **Network** e **Cookies** se `www.google.com/recaptcha` viene caricato su tutte le pagine del sito anziché solo sulla pagina del form, e verificare nella Privacy Policy se l'utilizzo di reCAPTCHA è dichiarato (specificando se viene usato per sicurezza informatica ed evitando che Google utilizzi i dati di impronta digitale del browser per finalità pubblicitarie senza consenso).

---

## SEZIONE 3: Modello di Rapporto di Audit (Deliverable)

Al termine delle 5 fasi di ispezione, compilare il seguente rapporto tecnico. Ogni non conformità segnalata con `[NON CONFORME]` o `[PARZIALE]` deve essere supportata da evidenze oggettive (nomi esatti dei cookie rilevati, URL delle chiamate di rete, citazioni testuali dalla Privacy Policy o riferimenti a screenshot allegati).

---

### Rapporto Tecnico di Verifica GDPR / ePrivacy

* **Target di Analisi (URL):** `[Inserire URL completo]`
* **Titolare del Trattamento individuato:** `[Inserire Ragione Sociale e P.IVA se presenti, altrimenti indicare "Non rilevabile"]`
* **Piattaforma CMS e CMP rilevati:** `[Es. WordPress + Complianz / Cookiebot / Iubenda / Nessuna CMP]`
* **Data e Ora di esecuzione del test:** `[GG/MM/AAAA - HH:MM]`
* **Analista / Gruppo di Lavoro:** `[Nome e Cognome]`

#### 3.1 Matrice di Conformità Analitica

*(Legenda Stati: **CONFORME** = Requisito pienamente soddisfatto | **PARZIALE** = Presidio presente ma incompleto o impreciso | **NON CONFORME** = Violazione diretta o assenza totale del presidio | **N/A** = Non applicabile al sito in esame)*

| ID | Area di Controllo | Riferimento Normativo | Parametro Verificato | Stato | Evidenze Tecniche / Note Analitiche |
| :--- | :--- | :--- | :--- | :---: | :--- |
| **1.1** | Sicurezza Trasporto | Art. 32 GDPR | Cifratura TLS (1.2/1.3) valida e redirect automatico `HTTP -> HTTPS` | | *Es: Redirect 301 attivo, TLS 1.3 valido.* |
| **1.2** | Sicurezza Trasporto | Art. 32 GDPR | Presenza dell'header di sicurezza `Strict-Transport-Security` (HSTS) | | |
| **2.1** | CMP & Cookie Banner | Linee Guida Garante 2021 | Presenza del pulsante di rifiuto/chiusura ("X") sul primo livello | | |
| **2.2** | CMP & Cookie Banner | Linee Guida Garante 2021 | Simmetria visiva (font, colori, dimensioni) tra "Accetta" e "Rifiuta" (Assenza Dark Pattern) | | |
| **2.3** | Tracciatori Pre-Consenso | Art. 122 Cod. Privacy / Art. 25 GDPR | Assenza di cookie analitici non anonimizzati o di profilazione prima del consenso | | *Elencare i nomi esatti dei cookie trovati prima del clic.* |
| **2.4** | Tracciatori Pre-Consenso | Art. 122 Cod. Privacy / Art. 25 GDPR | Assenza di chiamate di rete (Network) verso pixel di tracciamento prima del consenso | | *Elencare gli endpoint contattati (es. `facebook.com/tr`).* |
| **2.5** | Gestione Consenso | Linee Guida Garante 2021 | Efficacia del comando di rifiuto (nessun tracker attivato dopo il clic su "Rifiuta") | | |
| **2.6** | Gestione Consenso | Art. 7, par. 3 GDPR | Presenza e funzionamento del meccanismo permanente di revoca/modifica del consenso | | |
| **3.1** | Privacy Policy | Art. 13, par. 1, lett. a-b GDPR | Indicazione completa del Titolare del trattamento (e del DPO, ove applicabile) | | |
| **3.2** | Privacy Policy | Art. 13, par. 1, lett. c GDPR | Corretta associazione tra ciascuna finalità del trattamento e la relativa base giuridica | | |
| **3.3** | Privacy Policy | Art. 13, par. 1, lett. e GDPR | Coerenza tra i fornitori/terze parti dichiarati nella policy e quelli rilevati nei DevTools | | |
| **3.4** | Privacy Policy | Artt. 13.1.f e 44-49 GDPR | Indicazione dei trasferimenti Extra-SEE e delle garanzie applicate (es. DPF / SCC) | | |
| **3.5** | Privacy Policy | Art. 13, par. 2, lett. a GDPR | Specificazione di tempi di conservazione definiti per ciascuna finalità (Data Retention) | | |
| **3.6** | Privacy Policy | Art. 13, par. 2, lett. b, d GDPR | Elenco completo dei diritti dell'interessato (artt. 15-22) e diritto di reclamo al Garante | | |
| **3.7** | Cookie Policy | Linee Guida Garante 2021 | Censimento tabellare accurato dei cookie (nome, fornitore, scopo, scadenza) | | |
| **4.1** | Form di Raccolta Dati | Art. 5, par. 1, lett. c GDPR | Rispetto del principio di minimizzazione sui campi contrassegnati come obbligatori | | |
| **4.2** | Form di Raccolta Dati | Artt. 7 e 13 GDPR | Link all'informativa presente e separazione granulare dei checkbox per finalità diverse | | |
| **4.3** | Form di Raccolta Dati | Art. 7, par. 4 e Cons. 32 GDPR | Assenza di caselle pre-spuntate e libertà di inviare il form senza accettare il marketing | | |
| **5.1** | Risorse Terze Parti | Artt. 25 e 44 GDPR | Hosting locale dei web font (assenza di chiamate dirette a `fonts.googleapis.com`) | | |
| **5.2** | Risorse Terze Parti | Linee Guida Garante 2021 | Blocco preventivo di iframe esterni (YouTube, Google Maps, Social) prima del consenso | | |

---

#### 3.2 Valutazione Complessiva del Rischio e Piano di Rientro (Remediation Plan)

Redigere una relazione conclusiva strutturata nei seguenti tre paragrafi:

1. **Indice di Rischio Sanzionatorio e Sintesi Esecutiva:**
   Esprimere un giudizio sintetico sul livello di esposizione al rischio legale e sanzionatorio del Titolare del trattamento (**Basso**, **Medio**, **Alto** o **Critico**), motivando la scelta sulla base della gravità delle non conformità riscontrate.
2. **Analisi delle Principali Non Conformità (Top 3 Vulnerabilità):**
   Descrivere nel dettaglio le tre violazioni più critiche individuate durante l'audit, spiegando quale impatto concreto hanno sui diritti e sulle libertà degli utenti che navigano sul sito (es. tracciamento occulto, impossibilità di negare il consenso, raccolta eccessiva di dati personali).
3. **Piano di Rientro Tecnico e Organizzativo (Remediation Plan):**
   Fornire un elenco puntato di interventi correttivi concreti, ordinati per priorità, che gli sviluppatori web e i consulenti legali del sito devono attuare per sanare le irregolarità rilevate (es. *"Configurare Google Tag Manager per subordinare il tag di Meta Pixel al trigger di consenso marketing della CMP"*, *"Scaricare i file .woff2 di Google Fonts sul server locale e modificare il foglio di stile CSS"*, *"Separare l'unico checkbox del form contatti in due opzioni distinte e rimuovere l'attributo required dal consenso newsletter"*).
