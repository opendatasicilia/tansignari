Creare moduli di raccolta dati geografici con ONA e metterlo in collegamento automatico con Google sheet
========================================================================================================

Questa ricetta nasce dalla necessità di disporre di un modulo di raccolta dati/informazioni online, dove fosse possibile inserire dati geografici, quindi ad esempio dati di latitudine e longitudine per un determinato punto. Pensiamo ad un modulo, ad esempio, in cui è possbile censire elementi di arredo urbano, casi di tombini otturati, marcipiedi dissestati o buche su strada, barriere architettoniche varie, o anche per censire semplicemente luoghi di interesse.

Precedentemente ala realizzazione di questa ricetta è stata aperta questa [issue](https://github.com/opendatasicilia/tansignari/issues/25) in cui sono seguite alcune procedure per capire come collegare i dati derivanti dalla compilazione del modulo fornito dal servizio "ONA" con i fogli di Google, comodo strumento per costruire ad esempio mappe online. Ed in particolare **come fare in modo che, dopo aver inserito i dati nel modulo ONA, un minuto dopo questi dati possano essere già disponibili nel foglio Google**.

Tra i vari servizi online gratuiti di raccolta dati grazie ad un modulo va menzionato https://ona.io/. Molto interessante perchè semplice da utilizzare (anche a portata di mano di chi non ha competenze da sviluppatore) e perchè il modulo generato è responsive quindi comodamente fruibile su dispositivi mobili.
Dopo essersi registrati, creando un account, si accede ad una sezione in cui è possibile costruire un modulo. 

Possiamo scegliere un progetto pubblico, con dati visibili a tutti, oppure privato, con dati visibili solo a noi creatori del modulo. 

Cliccando su "new project" si sceglie un nome ed appare una pagina in cui si può scegliere tra diverse opzioni per cominciare ad inserire elementi. Scegliamo quello interno al sito che prend il nome di "Form builder". 
![image](https://raw.githubusercontent.com/opendatasicilia/tansignari/master/static/ricette/Ona-Google_sheet/formbuilder.JPG)

Qui possiamo inserire vari elementi che rappresentano le domande da porre nel modulo online:
- domande a risposta multipla
- note 
- dati geografici (qui si apre una mappa nel modulo online)
- possibilità di inserire foto, video, audio
- data
- orario
- ecc.

Una cosa **importante** per l'elemento "mappa" è dare all'elemento "mappa" il seguente codice nel campo "**Appearance (Advanced):**" 
`maps hide-input`. Questo permetterà a chi usa il modulo di posizionare il puntatore anche manualmente sulla mappa per una localizzazione precisa, nel caso in cui il gps dello smartphone/tablet/dispositivo mobile non dovesse localizzare il punto oggetto di interesse in maniera precisa!

Per i restanti elementi da inserire, la cosa è molto facile, in quanto basta soltanto editare il nome della domanda che poi vogliamo sia visulizzato nel modulo online.






...
to-be-continued
