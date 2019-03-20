# Come raccogliere dati geolocalizzati

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue:

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



to be continued...
