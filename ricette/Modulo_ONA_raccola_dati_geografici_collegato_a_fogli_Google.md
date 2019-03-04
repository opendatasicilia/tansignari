# Creare moduli di raccolta dati geografici online con ONA e metterli in collegamento automatico con fogli Google
## (e avere dati agiornati al minuto)


<!-- TOC -->

- [Creare moduli di raccolta dati geografici online con ONA e metterli in collegamento automatico con fogli Google](#creare-moduli-di-raccolta-dati-geografici-online-con-ona-e-metterli-in-collegamento-automatico-con-fogli-google)
    - [(e avere dati agiornati al minuto)](#e-avere-dati-agiornati-al-minuto)
    - [1 - Creare un modulo per raccolta dati in mobilità](#1---creare-un-modulo-per-raccolta-dati-in-mobilità)
        - [Alcune poche cose importanti da sapere sul database generato dalla compilazione del modulo di "ONA":](#alcune-poche-cose-importanti-da-sapere-sul-database-generato-dalla-compilazione-del-modulo-di-ona)
    - [2 - Le API di ONA](#2---le-api-di-ona)
    - [3 - Ottenere un foglio dati di Google con i dati aggiornati ad 1 minuto da quando vengono raccolti con il modulo ONA](#3---ottenere-un-foglio-dati-di-google-con-i-dati-aggiornati-ad-1-minuto-da-quando-vengono-raccolti-con-il-modulo-ona)

<!-- /TOC -->


## 1 - Creare un modulo per raccolta dati in mobilità


Questa ricetta nasce dalla necessità di disporre di un modulo di raccolta dati/informazioni online, dove fosse possibile inserire dati geografici, quindi ad esempio dati di latitudine e longitudine per un determinato punto. Pensiamo ad un modulo, ad esempio, in cui è possbile censire elementi di arredo urbano, casi di tombini otturati, marcipiedi dissestati o buche su strada, barriere architettoniche varie, o anche per censire semplicemente luoghi di interesse.

Precedentemente alla realizzazione di questa ricetta è stata aperta questa [**issue**](https://github.com/opendatasicilia/tansignari/issues/25) in cui sono seguite alcune procedure per capire come collegare i dati derivanti dalla compilazione del modulo fornito dal servizio "ONA" con i fogli di Google, comodo strumento per costruire ad esempio mappe online. Ed in particolare **come fare in modo che, dopo aver inserito i dati nel modulo ONA, un minuto dopo questi dati possano essere già disponibili nel foglio Google**.

Tra i vari servizi online gratuiti di raccolta dati grazie ad un modulo va menzionato https://ona.io/. Molto interessante perchè semplice da utilizzare (a portata di mano di chi non ha competenze da sviluppatore) e perchè il modulo generato è responsive quindi comodamente fruibile su dispositivi mobili.
Dopo essersi registrati sulla piattaforma, creando un account, si accede ad una sezione in cui è possibile costruire un modulo. 

Possiamo scegliere un progetto pubblico, con dati visibili a tutti, oppure privato, con dati visibili solo a noi creatori del modulo. 

Cliccando su "new project" si sceglie un nome ed appare una pagina in cui si può scegliere tra diverse opzioni per cominciare ad inserire elementi. Scegliamo quello interno al sito che prend il nome di "**Form builder**". 
![image](https://raw.githubusercontent.com/opendatasicilia/tansignari/master/static/ricette/Ona-Google_sheet/formbuilder.JPG)

Qui possiamo inserire vari elementi che rappresentano le domande da porre nel modulo online:
- domande a risposta multipla
- domande a singola risposta
- note 
- dati geografici (qui si apre una mappa nel modulo online)
- possibilità di inserire foto, video, audio
- data
- orario
- ecc.

Una cosa **importante** per l'elemento "**mappa**" è dare all'elemento "mappa" il seguente codice nel campo "**Appearance (Advanced):**" 
`maps hide-input`. Questo permetterà a chi usa il modulo di posizionare il puntatore anche manualmente sulla mappa per una localizzazione precisa, nel caso in cui il gps dello smartphone/tablet/dispositivo mobile non dovesse localizzare il punto oggetto di interesse in maniera precisa!

Per i restanti elementi da inserire, la cosa è molto facile, in quanto basta soltanto editare il nome della domanda che poi vogliamo sia visulizzato nel modulo online.

Una volta terminata la procedura di inserimento elementi nel modulo si salva attraverso il relativo pulsante "save" in alto a destra.
Durante le fasi di inserimento degli elementi, cliccando sull'icona a forma di occhio nella barra in alto degli strumenti, è possibile visualizzare che aspetto avrà il modulo che stiamo preparando.

Una volta salvato il modulo, andando nella sezione della piatatforma dove sono i nostri progett, troveremo il primo progetto generato e cliccandoci sopra si aprirà un pannello di visualizzazione dati in cui c'è anche la sezione "**submit data**"

![image](https://raw.githubusercontent.com/opendatasicilia/tansignari/master/static/ricette/Ona-Google_sheet/linkmodulo.JPG) 

in cui leggiamo il link al modulo che è pronto per essere usato online. Vediamo questo che ho creato come prova: https://enketo.ona.io/x/#iuYQFAYj.

Abbiamo creato un modulo online pronto da usare per raccogliere dati in mobilità.




### Alcune poche cose importanti da sapere sul database generato dalla compilazione del modulo di "ONA":

- i dati generati dalla compialzione del modulo confluiscono in un database ospitato nei server della piattaforma ONA: [qui](https://ona.io/cirospat/81378/387318#/table) possiamo vedere il database generato dalla compilazione (è solo un test) di questo [modulo](https://enketo.ona.io/x/#iuYQFAYj). 
- la piattaforma ONA espone le cosiddette API [Application Programming Interfaces](https://it.wikipedia.org/wiki/Application_programming_interface#Finalit%C3%A0), interfaccie che consentono di fare dialogare i dati raccolti con i moduli ONA con altri servizi e software online di terze parti. E come dice Andrea Borruso (!), quando un servizio online espone le API [ci si può fare la guerra](https://github.com/opendatasicilia/tansignari/issues/25#issuecomment-468945094), in termini di riutilizzo dei dati. 


Quindi se i dati raccolti col modulo sono supportati dalle API, allora ce li possiamo trattare in tanti modi, ad esempio:

- sulla piattaforma/repository di [**Data.World**](https://data.world/cirospat/importfromona/workspace/file?filename=387318.csv);

- oppure sui [**Fogli di Google**](https://docs.google.com/spreadsheets/d/1JaaG60FgQZf8Z2zaQzyEFbyQJ11yQVinrmV1QpZ1YLg/edit#gid=0) (vedi "Foglio1").

Questi esempi di disponibilità dei dati su altre piattaforme, esterne al servizio web di ONA, sono estremamente importanti per chi vuole riusare i dati per diversi scopi, ad esempio per fare mappe che filtrano gli stessi dati per criteri specifici (ad esempio fammi vedere un livello di mappa con i tombini otturati o fammi vedere un livello di mappa con le sole buche nelle strade, ecc, oppure per realizzare infografiche).

Fino a qui ci siamo concentrati su quello che è possibile fare sulla (e con la) piattaforma di https://ona.io/ (costruire il modulo raccolta dati e visualizzare i dati su un database interno a ONA).


|


## 2 - Le API di ONA


ONA ha le API, [qui](https://api.ona.io/static/docs/index.html) la documentazione per l'uso.

Qui un primo esempio di uso delle API: con https://api.ona.io/api/v1/data?owner=nomeutente si ha la lista dei progetti pubblici del signor "nomeutente".

Nel caso del modulo che abbiamo usato come test sopra abbiamo: https://api.ona.io/api/v1/data/387318.csv, in pratica dopo `data` abbiamo il numero del progetto che abbiamo creato su ONA, seguito dal suffisso `.csv`.
Abbastanza semplice.


|


## 3 - Ottenere un foglio dati di Google con i dati aggiornati ad 1 minuto da quando vengono raccolti con il modulo ONA

Dopo aver creato un foglio Google sulla prima cella (A1) impostiamo la funzione =importdata("https://api.ona.io/api/v1/data/387318.csv") e avremo i dati direttamente da ONA, grazie alle API.

Ora andiamo sulla barra degli strumenti in alto e clicchiamo su "**strumenti**" e dopo su "**< > editor di script**". Si aprirà lo strumento per creare uno **script**. Si tratta di un piccolo servizio che svolge una determinata funzione all'interno del foglio Google. La funzione la stabiliamo noi con le istruzioni che diamo con la sintassi del codice.

Diamo innanzitutto un nome allo script (io ho dato "updateCSVeveryminute"). Poi nello spazio dedicato alla sintassi scriviamo il seguente codice:

```
function importData() 
{
  var csvUrl = "https://api.ona.io/api/v1/data/387318.csv";
  var csvContent = UrlFetchApp.fetch(csvUrl).getContentText();
  var csvData = Utilities.parseCsv(csvContent);
  
  var sheet = SpreadsheetApp.getActive().getSheetByName('Foglio1')
  sheet.getRange(1, 1, csvData.length, csvData[0].length).setValues(csvData);
}
```

Successivamente clicchiamo sull'icona a forma di cerchio di orologio (passando sopra il mouse leggiamo: "**trigger del progetto corrente**"). Clicchiamo sul nome dello script (nel mio caso "Modifica Attivatore per updateCSVeveryminute"). 

A questo punto abbiamo una pagina in cui dobbiamo settare le seguenti impostazioni:

- Scegli quale funzione eseguire: **importdata**
- Viene eseguito durante il deployment: **head**
- Seleziona l'origine dell'evento: **evento vincolato a specifiche temporali**
- Seleziona il tipo di attivatore basato sull'orario: **timer in minuti**
- Seleziona intervallo in minuti: **ogni minuto**
- Impostazioni di notifica di errore: **invia una notifica immediatamente** (opzionale, serve solo ad essere informati tramite notifica in caso di errori

In questa maniera lo script attiverà una verifica di presenza di nuovi dati (dalla fonte CSV pre impostata nello script, cioè da https://api.ona.io/api/v1/data/387318.csv) con una frequenza temporale del singolo minuto. Abbiamo ottenuto, così, una sorta di database (foglio Google) con dati provenienti dal modulo ONA in tempo quasi reale!

Arivato a questo punto il lavoro che consente al foglio Google di aggiornarsi in tempo quasi reale grazie alle API di ONA e allo script creato è completato.

**Una cosa che noterete**: [nella cella **A1** del foglio Google](https://docs.google.com/spreadsheets/d/1JaaG60FgQZf8Z2zaQzyEFbyQJ11yQVinrmV1QpZ1YLg/edit#gid=0) dove avevamo inizialmente impostato la funzione `=importdata("https://api.ona.io/api/v1/data/387318.csv")` se ora andiamo a controllare non ci sarà più. Questa verifica sarà la conferma che lo script funziona. 

Un grazie ad **Andrea Borruso** per la realizzazione dello script e a **Gianni Vitrano** per il supporto (e per sopportarmi) che mi ha dato per la comprensione dell'intero processo appena illustrato in questa ricetta. E anche a **Totò Fiandaca** perchè ormai per fare certe cose insieme partiamo sempre in 4 !!!

