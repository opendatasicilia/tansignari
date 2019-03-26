# Come raccogliere dati geolocalizzati

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue:

Indice

   * [Come raccogliere dati geolocalizzati](#)
       * [ODK](#odk)
   * [ona.io](#ona-io)
        * [Registrazione](#registrazione)
        * [New Projects](#new-projects)
        * [Costruire il form con Form builder](#costruire-il-form-con-form-builder)
        * [Costruire il form utilizzando i file XLS](#costruire-il-form-utilizzando-i-file-xls)
   * [Il contenitore dei dati](#il-contenitore-dei-dati)
        * [Come si scaricano i dati…?](#come-si-scaricano-i-dati)
   * [Ona API](#ona-api)
   * [Usare Google sheet per gestire i dati](#usare-google-sheet-per-gestire-i-dati)
        * [Come attivare lo script…?](#come-attivare-lo-script)
   * [Open Data Kit di Ona (odk.ona.io)](#open-data-kit-di-ona-odk-ona-io)
   * [Interfaccia web – Demo](#interfaccia-web-demo)
   * [No costi di licenza](#no-costi-di-licenza)
   * [QgisODK](#qgisodk)
   * [Alternativa a ODK](#alternativa-a-odk)

---

E’ possibile raccogliere dati geolocalizzati, ordinati secondo uno schema,  che ci consente di mappare (in tempo reale) tutto quello che ci circonda…? e che sia anche una soluzione a basso costo e semplice da usare in mobile/computer…?

## ODK
**Si… la risposta è SI…** Tutto questo ed anche di più è possibile realizzarlo con [Open Data Kit](https://opendatakit.org/) un progetto “open” che consente l’impostazione di sistemi client-server di raccolta e archiviazione di dati da parte di operatori sul campo tramite dispositivi mobili.

Cit. dal blog [TANTO – Raccolta dati per tutti: GeoODK e smartphones per sensori urbani (parte I)](http://blog.spaziogis.it/index.html_p=6786.html).

[Open Data Kit](https://opendatakit.org/) (ODK) consente di:
* costruire una form (o “questionario”) di raccolta dati;
* raccogliere dati su di un dispositivo mobile;
* aggregare i dati raccolti su di un server ed estrarli in formati utilizzabili.

Il sistema richiede diversi elementi da integrare.

Innanzitutto una *form*, ovvero il questionario da sviluppare.

Una **‘piattaforma’ per la raccolta dei dati**: qui ci viene in aiuto [enketo.org](https://enketo.org/) per la realizzazione di una **webform** compilabile da (virtualmente) qualsiasi dispositivo, oppure un’**app** da caricare su dispositivo mobile. Diverse app sono state sviluppate: [ODK Collect](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=2ahUKEwjh6PWy7ojhAhXqsaQKHRhLCCEQFjAAegQIBxAB&url=https%3A%2F%2Fplay.google.com%2Fstore%2Fapps%2Fdetails%3Fid%3Dorg.odk.collect.android%26hl%3Dit&usg=AOvVaw24t_x8wIkiQj7jI7z-8cvB) e [KoBo Collect](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=2ahUKEwidmqvC7ojhAhXFGuwKHZe4B68QFjAAegQIAxAB&url=https%3A%2F%2Fwww.kobotoolbox.org%2F&usg=AOvVaw0mpRrQ9A3VHIKgZRP547tB), solo per citarne un paio, soprattutto nell’ambito di progetti a contenuto umanitario o sviluppati apposta per scopi educativi.

Un server, ovvero un sistema centralizzato in cui salvare i dati immessi. Senza ricorrere a un nostro server si può fare riferimento alle piattaforme [ODK aggregate](https://docs.opendatakit.org/aggregate-intro/) e [Ona.io](https://ona.io/home/) (nel nostro caso).

Per capire meglio il funzionamento del **sistema di raccolta dati** di [Open Data Kit](https://opendatakit.org/) vi invito a leggere l’articolo su [TANTO – Raccolta dati per tutti: GeoODK e smartphones per sensori urbani (parte I)](http://blog.spaziogis.it/index.html_p=6786.html). In questo post mi limiterò a descrivere il procedimento che ci ha permesso di realizzare i diversi form per la raccolta dati, l’archiviazione e l’estrazione dei dati per la pubblicazione e l’interfaccia web per esporli già mappati. (ricerca e sviluppo di opendatasicilia.it)

---

## ona.io

### Registrazione

La prima cosa da fare è scegliere il server/piattaforma che ospiterà i dati da noi raccolti, noi abbiamo scelto **[Ona.io](https://ona.io/home/)**, la stessa cosa si può fare con [kobotoolbox.org](https://www.kobotoolbox.org/), [mapyourworld.org](http://mapyourworld.org/), [datawinners.com](https://www.datawinners.com/) e tante altre piattaforme, tutti servizi online free e basati sulle **webform** di [enketo.org](https://enketo.org/).

![](/img/odk_ona/ona_register.jpg)

[Registazione alla Piattaforma ona.io](https://ona.io/join)

Dopo la registrazione per prima, di iniziare un nuovo progetto,  sarebbe opportuno entrare nel **Settings** del proprio profilo e impostare **Require Phone Authentication?**, ovvero decidere se limitare o meno l’invio dei moduli solo ad utenti registrati.

![](/img/odk_ona/ona_settings.jpg)

---

### New Projects
Ora siamo pronti per aprire/impostare un nuovo progetto, direttamente nella home page, cliccate sul pulsante **New Projects**

![](/img/odk_ona/ona_new.png)

Dopo aver cliccato sul pulsante **New Porject**, si apre una tendina che ci permette di creare il nuovo progetto, al punto (1) scrivere il titolo del progetto, al punto (2) selezionare la categoria.

![](/img/odk_ona/ona_new2.png)

Se il vostro è un profilo free, tutti i nuovi progetti, tranne 1 che può essere impostato come privato,  saranno pubblici.

![](/img/odk_ona/nuovo_form.png)

Come si vede dall’immagine, ogni progetto può ospitare più form. Come aggiungere un nuovo form al progetto?
Possiamo aggiungere un nuovo form in due modi diversi:

    caricare il questionario/form in formato .xls (file di excel) tramite il tasto **Add a form** (1)
    costruire il form utilizzando gli strumenti forniti da **[Ona.io](https://ona.io/home/)** il **Form builder** (2)

Costruire il form utilizzando un file .xls ci da molta più libertà nella progettazione, ma è necessario conoscere qualche regola di base, a seguire due guide molte utili per la costruzione di un modello .xls,  [Ona Help Center](https://help.ona.io/knowledge-base/are-there-xlsforms-to-use-as-a-starting-point-for-form-authoring/) e [xlsform.org](http://xlsform.org/) che approfondiremo dopo.
Viceversa usare il **Form builder** è un po più vincolante, ma ci permette di partire subito.

---

### Costruire il form con Form builder

Iniziamo con la Form builder, cliccando sul pulsate Form builder si apre una nuova pagina dedicata alla costruzione del form.

![](/img/odk_ona/form.png)

Inserire il **nome** del form (1) e cliccare sulla crocetta (2) per aggiungere un nuovo **componente** al form, cosi facendo viene mostrato il pulsante **+ Add Question**,

![](/img/odk_ona/form1.png)

con un ulteriore click su quest’ultimo pulsante e si apre al console degli strumenti del Form builder

![](/img/odk_ona/form2.png)

Da questa console possiamo aggiungere tutti i blocchi utili al nostro form,

* dati geografici come lat. e long. (blocco GPS)
* domande a risposta multipla
* domande a singola risposta
* note
* foto, video, audio
* data
* orario
* e tanto altro

Per aggiungere una mappa, che permette all’utente di inviarci le coordinate di un punto, basta cliccare sull’icona del geo markers GPS (‘geopoint’).

![](/img/odk_ona/form3.png)

adesso non resta che configurare i parametri, per farlo, cliccare sull’icona a forma di ingranaggio (1)

![](/img/odk_ona/form4.png)

1. nome del blocco
2. nome da assegnare alle relative colonne nella tabella dei dati
3. descrizione/suggerimento per la domanda
4. spuntare, in caso sia obbligatorio rispondere al quesito
5. aspetto (avanzato), ulteriore regola per migliorare il blocco

![](/img/odk_ona/form5.png)

Ecco pronto e ottimizzato il blocco per l’inserimento della posizione (‘**geopoint**’).
Come si può notare abbiamo aggiunto ad **Appearance (advanced)** la regola **maps hide-input** questo permetterà alla mappa di essere visibile anche in modalità mobile.
Questa ed altre regole si trovano in un form demo sul sito **[enketo.org](https://enketo.org/)** , na seguire il link del form con i **[Widgets](https://enke.to/x/#widgets)** dove vengono mostrati i diversi  widgets disponibili e il relativo file **[XLS sorgente](https://docs.google.com/spreadsheets/d/1KLQiQyQ5BlN_wd-83p8Eb6xIU-TZp-yvzgrm20HecRI/edit#gid=0)**.

Per salvare il form, ovviamente bisogna cliccare il tasto **SAVE** 🙂

A questo punto costruire un form/questionario diventa semplicissimo, anche per gli altri blocchi il procedimento per la configurazione è molto simile a quello appena visto.

![](/img/odk_ona/form_mod.png)

Il form può essere modificato velocemente in qualsiasi momento, selezionando Edit form dal menù a tendina delle opzioni del form stesso, posizionato a destra della pagina.

---

### Costruire il form utilizzando i file XLS
Come si può notare dal file [XLS sorgente](https://docs.google.com/spreadsheets/d/1KLQiQyQ5BlN_wd-83p8Eb6xIU-TZp-yvzgrm20HecRI/edit#gid=0) di [enketo.org](https://enketo.org/) è formato da tre fogli di lavoro, obbligatoriamente denominati ‘**survey**’ , ‘**choices**’ e ‘**settings**’.
Nel foglio ‘**survey**’ c’è la griglia di domande e informazioni da raccogliere, impostate in ordine ben preciso.
Nel foglio ‘**choices**’ vanno inserite le griglie di risposte possibili alle varie domande poste nel foglio ‘**survey*’.
Nel foglio ‘**settings**’ troviamo la descrizione del form, se non è presente questo foglio, il questionario avrà lo stesso nome dato al file .xls che verrà caricato sul sito.

Per maggiori dettagli sull’impostazione del file XLS vi invito a leggere il secondo articolo su [TANTO – Raccolta dati per tutti: GeoODK e smartphones per sensori urbani (parte II)](http://blog.spaziogis.it/index.html_p=6834.html).

---

## Il contenitore dei dati
Dopo aver costruito il nostro questionario, è arrivato il momento dare uno sguardo al luogo dove saranno caricati e archiviati i dati, e dove sarà possibile effettuare delle operazioni, come visualizzare i dati in forma di tabella o sotto forma di mappa, dove sarà possibile caricare eventuali file multimediali (come ad esempio immagini o video registrati) nonché dei report sulle attività (es. delle statistiche sulle acquisizioni di dati, ecc.) e scaricare i dati in vari formati una volta raccolti.

![](/img/odk_ona/form6.png)

Per accedere a questo spazio ci sono due modi, o cliccate sul **nome del form** interessato, o sempre da menù a tendina, posto a destra della pagina, cliccate su **Settings**.

![](/img/odk_ona/form8.png)

Subito dopo aver cliccato su **Settings**, si apre la pagina dedicata ai dati del form, ci sono 7 schede, tutte utili a gestire i dati che man mano vengono caricati, nell’immagine in alto vediamo la tabella che si è generata automaticamente alla ricezione dei dati.

In basso la scheda con le varie foto associate.

![](/img/odk_ona/form10.png)

La scheda Settings, utilissima per modificare le informazioni sul form, per aggiungere una nuova base mappa tipo [Mapbox](https://www.mapbox.com/) per collegare applicazioni esterne come google sheet, tableau public, ottime per scaricare ed analizzare i dati raccolti. Fino alla data di pubblicazione di questo post, non è stato possibile collegare google sheet ad **[Ona.io](https://ona.io/home/)**, ma [@aborruso](https://twitter.com/aborruso) ha risolto brillantemente il problema utilizzando le API di **[Ona.io](https://ona.io/home/)**, più avanti il procedimento verrà descritto.

![](/img/odk_ona/form11.png)

Attraverso la scheda **Settings** possiamo caricare file multimediali, un piccolo esempio pratico, se desideriamo aggiungere un logo al nostro form/questionario, basta caricare, un file denominato **form_logo.png** nella sezione Form Media Files (1) attraverso il tasto **Select file uplodad** (2)

![](/img/odk_ona/form12.png)

Esempio di form con logo inserito

![](/img/odk_ona/form13.png)

---

### Come si scaricano i dati…?

Nella scheda Overview si trova il pannello **Data Exports** (1)  all’interno del quale si trova il pulsante **Prepare Data Export** (2) al click si apre una tendina dove vengono mostrate tutti i possibili formati in cui si possono esportare i dati.

![](/img/odk_ona/form15.png)

Supponendo di voler esportare i dati in formato csv, selezioniamo la voce CSV

![](/img/odk_ona/form16.png)

Si apre un ulteriore pannello (1), dove è possibile selezionare le opzioni per l’esportazione, dopo aver selezionato le opzione non ci resta che esportare il file (2).

![](/img/odk_ona/form18.png)

**Attenzione** i dati esportati con questo metodo, sono come delle foto istantanee, congelano il momento, restituiscono i dati presenti nell’archivio fino al momento in cui vengono richiesti, e non vengono più aggiornati.

---

## Ona API
Per avere dati sempre aggiornati bisogna utilizzare le Ona API il funzionamento è semplicissimo, basta seguire la guida

Per conoscere i progetti di un utente con **https://api.ona.io/api/v1/data?owner=nomeutente**  si ha la lista dei progetti pubblici del signor “nomeutente”.

Ad esempio il mio **https://api.ona.io/api/v1/data?owner=gbvitrano** restituisce:


```
{
"id": 386586,
"id_string": "aKumLRpod6BV9NP5viye2u",
"title": "Geolocalizza (form test)",
"description": "form test per progetto Geolocalizza",
"url": "https://api.ona.io/api/v1/data/386586"
},
{
"id": 386670,
"id_string": "aVXogAibtRyPggq7PhjF7v",
"title": "Geolocalizzazione di...",
"description": "",
"url": "https://api.ona.io/api/v1/data/386670"
},
{
"id": 387237,
"id_string": "imp_publ_01",
"title": "imp_publ",
"description": "",
"url": "https://api.ona.io/api/v1/data/387237"
}
```

[@aborruso](https://twitter.com/aborruso) docet [#issue 25](https://github.com/opendatasicilia/tansignari/issues/25) tansignari

Se sono interessato ai dati in CSV del progetto **Geolocalizza (form test)** (il primo), bisogna prendere il valore di **ulr** e aggiungere .csv, quindi **https://api.ona.io/api/v1/data/386586.csv**, questo CSV sarà sempre quello aggiornato e potrà fare da source ad applicazione esterne, come Google sheet, [tableau public](https://public.tableau.com/en-us/s/) o se preferite ad un dataset di [data.world](https://data.world/).
Utilizzando le [Ona API](https://api.ona.io/static/docs/index.html) si possono ottenere i dati anche in altri formati come [json](https://api.ona.io/static/docs/data.html#get-json-list-of-data-end-points-using-limit-operators), [geojson](https://api.ona.io/static/docs/data.html#geojson) e [OSM](https://api.ona.io/static/docs/data.html#osm)

---

## Usare Google sheet per gestire i dati
Usando la funzione **[IMPORTDATA](https://support.google.com/docs/answer/3093335?hl=en)** di Google sheet possiamo  caricare i dati in un nuovo foglio di lavoro (sheet), ricordiamoci prima di settare le **[impostazioni del foglio di lavoro](https://support.google.com/docs/answer/58515?co=GENIE.Platform%3DDesktop&hl=it)**, dal menu File.

![](/img/google/google_sheet.png)

Nella scheda Generale selezionare **Regno Unito** per le Impostazioni internazionali e spuntare **Usa sempre nomi di funzioni inglesi**, nella scheda Calcolo selezionare **A ogni modifica** nelle impostazioni del Ricalcolo, in caso contrario verranno restituiti valori errati di Latitudine e Longitudine, di conseguenza non riusciremo a mappare i nostri dati.

![](/img/google/google_sheet2.png)

Nota sull’aggiornamento dati: la funzione **IMPORTDATA()** by default aggiorna i dati ogni ora, ma se avete l’esigenza di avere i dati in tempo reale o quasi, durante una campagna di rilievi, esiste una opzione per forzare l’aggiornamento della funzione anche ad ogni minuto, come spiegato da  [@aborruso](https://twitter.com/aborruso) docet [#issue 25](https://github.com/opendatasicilia/tansignari/issues/25) di tansignari. *Come si fà…?* semplice, siamo uno *script* 🙂

![](/img/google/google_sheet3.png)

Dal menù **strumenti** (1) cliccare su **Editor di script** (2)

![](/img/google/google_sheet7.png)

```
{
// ATTENZIONE "dati_ona" è il nome del foglio di lavoro dove verranno caricati i dati

var csvUrl = “https://api.ona.io/api/v1/data/388501.csv”;
var csvContent = UrlFetchApp.fetch(csvUrl).getContentText();
var csvData = Utilities.parseCsv(csvContent);

var sheet = SpreadsheetApp.getActive().getSheetByName(‘dati_ona’)
sheet.getRange(1, 1, csvData.length, csvData[0].length).setValues(csvData);
}
```
**Attenzione** modificate il nome del foglio di lavoro inserito nello script “dati_ona” con il nome del vostro foglio di lavoro, se il nome del foglio di lavoro inserito nello script non esiste, lo script non si avvia e vi restituisce un errore.

### Come attivare lo script…? 
Si attiva semplicemente cliccando su **esegui** (icona play), la prima volta che lo eseguite vi chiederà l’autorizzazione, verrà visualizzato il messaggio che l’applicazione non è autenticata, non è  sicura etc etc…per bypassare tutto questo, cliccare su **applicazione avanzate** e confermare i permessi per poter lavorare…

![](/img/google/google_sheet5.png)

Come si può notare nelle script non c’è nessun riferimento al tempo. L’intervallo di tempo di lancio dello script si imposta da **Trigger**

![](/img/google/google_sheet8.png)

Per personalizzare i valori del **Trigger**, bisogna cliccare su **I miei attivatori** e selezionare quello dedicato allo script appena creato **importData()** e modificarne i valori. In questa modo lo script attiverà una verifica di nuovi dati (dalla fonte CSV pre impostata nel trigger) con una frequenza temporale del singolo minuto.

![](/img/google/google_sheet9.png)

Se tutto è andato a buon fine, la funzione ``` =IMPORTDATA(“https://api.ona.io/api/v1/data/388501.csv”)``` che abbiamo scritto precedentemente nella cella A1 sarà sparita, in quanto adesso è lo script a gestire tutto, e come programmato nel **Trigger** i dati verranno aggiornati ogni minuto.

---

**Si possono controllare allo stesso tempo più form/questionari anche di argomenti diversi…?**

Si lo script proposto da [@aborruso](https://twitter.com/aborruso) permette anche questo, con qualche piccola modifica alle variabili, come si può osservare nell’immagine in basso.

![](/img/google/google_sheet11.png)

Si potrebbe fare un *array* e fare un *loop*, ma anche cosi funziona e a noi va bene così 🙂

---

## Open Data Kit di Ona (odk.ona.io)
Con le stesse credenziali di accesso a  [Ona.io](https://ona.io/home/), possiamo accedere anche al profilo [odk.ona.io](https://odk.ona.io/) con un URL del tipo **https://odk.ona.io/nomeutente/** da questo link chiunque può visualizzare/scaricare le mappe e i dati delle form/questionari e persino scaricare XLSForm del questionario.

![](/img/odk_ona/ona_01.png)

---

## Interfaccia web – Demo
Adesso che siamo in grado di  costruire un form/questionario, sappiamo scaricare e gestire i dati, **come li usiamo…? come li comunichiamo all’esterno…?**

Noi di [OpenDataSicilia.it](http://opendatasicilia.it/) abbiamo pensato di usare un semplice [sito web](https://opendatasicilia.github.io/Geo_Form/) dove chiunque trova il [form/questionario](https://opendatasicilia.github.io/Geo_Form/#portfolio) lo compila e dopo qualche minuto di attesa può vedere la sua segnalazione geolocalizzata in una [mappa](https://opendatasicilia.github.io/Geo_Form/#maps).

![](/img/odk_ona/demo_01.png)

Demo per un progetto di raccolta dati (georeferenziati) sul terreno, per progetti di ricerca o di pubblica utilità, con il coinvolgimento attivo da parte dei cittadini. 

![](/img/odk_ona/demo_02.png)

Il webform può essere compilato anche in caso di assenza di rete. I dati vengono salvati nel browser (anche spegnendo il mobile/computer o effettuando la disconnessione) finché non sarà disponibile una connessione Internet per caricali automaticamente, in background, sui server di [ona.io](https://ona.io/)

![](/img/odk_ona/demo_03.png)

I dati raccolti vengono indirizzati su [uMap](http://u.osmfr.org/m/298837/) per realizzare la mappa

![](/img/odk_ona/demo_04.png)

Dettaglio di una segnalazione e scheda dati.

---

## No costi di licenza
Utilizzando piattaforme [Open Data Kit](https://opendatakit.org/) come [ona.io](https://ona.io/) e [enketo.org](https://enketo.org/), che consentono di raccogliere, gestire e utilizzare i dati senza costi di licenza e con un limitato ricorso a doti di programmazione, con qualche ora di studio e un pizzico di buona volontà, abbiamo realizzato un sistema di raccolta dati georeferenziati a costo zero per l’utilizzo di hardware e software di gestione dati.
Anche Google sheet e [uMap](http://umap.openstreetmap.fr/it/) non hanno costi di licenza.
La demo del [sito web](https://opendatasicilia.github.io/Geo_Form/) è ospitata nel [repository Github](https://github.com/opendatasicilia/Geo_Form) di [Open Data Sicilia](https://github.com/opendatasicilia) e non ha costi di licenza
Il template usato per realizzare la demo è  [Start Bootstrap – Creative](https://startbootstrap.com/template-overviews/creative/) rilasciato con [licenza CC BY 4.0](http://creativecommons.org/licenses/by/4.0/) anche in questo caso non ci sono costi di licenza.

---
## QgisODK
Chiudo la ricetta, ricordandovi che è disponibile per **QGIS 2.x** un plugin, **[QgisODK](https://github.com/enricofer/QgisODK)** di [Enrico Ferreguti](mailto:enricofer@gmail.com). Il plugin QGIS consente di costruire un sondaggio mobile ‘sul campo’ in pochi minuti a partire da uno strato QGIS e recuperare i dati raccolti con l’aiuto degli strumenti e dei servizi Open Data Kit.

![](/img/odk_ona/ona_qgis.png)

Grazie a [@aborruso](https://twitter.com/aborruso) per tutte le info e la pazienza 🙂

---

## Alternativa a ODK
Come suggerito da [@napo (Maurizio Napolitano)](https://www.facebook.com/groups/opendatasicilia/permalink/2061448710640440/) nel post del [gruppo facebook opendatasicilia](https://www.facebook.com/groups/opendatasicilia/permalink/2061448710640440/), una valida alternativa ad [ODK](https://opendatakit.org/) è [EpiCollect](http://www.epicollect.net/).
