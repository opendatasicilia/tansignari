Creare moduli di raccolta dati geografici con ONA e metterlo in collegamento automatico con Google sheet
========================================================================================================

Questa ricetta nasce dalla necessità di disporre di un modulo di raccolta dati/informazioni online, dove fosse possibile inserire dati geografici, quindi ad esempio dati di latitudine e longitudine per un determinato punto. Pensiamo ad un modulo, ad esempio, in cui è possbile censire elementi di arredo urbano, casi di tombini otturati, marcipiedi dissestati o buche su strada, barriere architettoniche varie, o anche per censire semplicemente luoghi di interesse.

Precedentemente alla realizzazione di questa ricetta è stata aperta questa [issue](https://github.com/opendatasicilia/tansignari/issues/25) in cui sono seguite alcune procedure per capire come collegare i dati derivanti dalla compilazione del modulo fornito dal servizio "ONA" con i fogli di Google, comodo strumento per costruire ad esempio mappe online. Ed in particolare **come fare in modo che, dopo aver inserito i dati nel modulo ONA, un minuto dopo questi dati possano essere già disponibili nel foglio Google**.

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

Una volta slavato il modulo, andando nella sezione della piatatforma dove sono i nostri progetti, troveremo il primo progetto generato e cliccandoci sopra si aprirà un pannello di visualizzazione dati in cui c'è anche "**submit data**"

![image](https://raw.githubusercontent.com/opendatasicilia/tansignari/master/static/ricette/Ona-Google_sheet/linkmodulo.JPG) 

in cui leggiamo il link al modulo che è pronto per essere usato online. Vediamo questo che ho creato come prova: https://enketo.ona.io/x/#iuYQFAYj.

Abbiamo creato un modulo online pronto sa usare.

**Alcune poche cose importanti da sapere sul database generato dalla compilazione del modulo di "ONA"**:

- i dati generati dalla compialzione del modulo confluiscono in un database ospitato nei server della piattaforma ONA: [qui](https://ona.io/cirospat/81378/387318#/table) possiamo vedere il database generato dalla compilazione (è solo un test) di questo [modulo](https://enketo.ona.io/x/#iuYQFAYj). 
- la piattaforma ONA espone le cosiddette API [Application Programming Interfaces](https://it.wikipedia.org/wiki/Application_programming_interface#Finalit%C3%A0), interfaccie che consentono di fare dialogare i dati raccolti con i moduli ONA con altri servizi e software online di terze parti. E come dice Andrea Borruso (!), quando un servizio online espone le API [ci si può fare la guerra](https://github.com/opendatasicilia/tansignari/issues/25#issuecomment-468945094), in termini di riutilizzo dei dati. 

Quindi se i dati raccolti col modulo sono supportati dalle API, allora ce li possiamo trattare in tanti modi:
1- sulla piattaforma/repository di [DataWorld](https://data.world/cirospat/importfromona/workspace/file?filename=387318.csv)
2- oppure sui [fogli di Google](https://docs.google.com/spreadsheets/d/1JaaG60FgQZf8Z2zaQzyEFbyQJ11yQVinrmV1QpZ1YLg/edit#gid=0) (vedi "Foglio1").

Questi esempi di disponibilità dei dati su altre piattaforme ...








...
to-be-continued
