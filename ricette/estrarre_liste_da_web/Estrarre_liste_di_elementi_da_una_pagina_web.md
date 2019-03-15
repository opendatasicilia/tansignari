## Come estrarre liste di elementi da una pagina web 

- issue correlata: [#29](https://github.com/opendatasicilia/tansignari/issues/29)
- autore: [Lorenzo Perone](https://github.com/lorenzoperone); fornitore della ricetta: [Andrea Borruso](https://github.com/aborruso); 
---

![image](./demetra_articolo.png)

Per estrarre un elenco di elementi utili da una lunga pagina web come quella di una legge, è possibile utilizzare una tecnica replicabile modificando solo il riferimeno all'elemento **css** da scaricare.

Utilizziamo [questa pagina](https://demetra.regione.emilia-romagna.it/al/articolo?urn=er%3Aassemblealegislativa%3Alegge%3A2005%3B13&dl_t=text%2Fxml&dl_a=y&dl_id=10&pr=idx%2C0%3Bartic%2C0%3Barticparziale%2C1&anc=tit1&fbclid=IwAR0Lcn8E89VosOWln-amBDx5N8rW1WiOsKjcBFv_7TjD7YsbJhWz0UtqUHk) come esempio per estrarre, in un elenco, gli articoli e la loro definizione. Se guardiamo l'immagine della pagina sopra l'idea è quella di avere come risultato un'elenco di questo tipo:

| Articolo | Definizione |
| --- | --- |
|Art. 1|Elementi costitutivi della Regione|
|Art. 2|Obiettivi|
|...|...|

Per fare questo è utile una **shell** unix, disponibile in linux e Mac, ma che è possibile installare anche in ambiente Windows, uno dei modi più semplici è descritto in questa ricetta **(INSERIRE LINK)**.

Una volta disponibile la shell è necessario installare l'eseguibile **scrape** dispobibile a questo [indirizzo](https://github.com/aborruso/scrape-cli/releases), una volta scaricato l'eseguibile, ad esempio **scrape.exe** lo salviamo in una cartella del computer ed aggiungiamo il percorso di questa cartella alla variabile **PATH** utente in modo da poterlo lanciare senza dover specificare ogni volta il percorso. Per fare questo apriamo un promt dei comandi windows e digitiamo

```
setx path "%path%;C:\PERCORSO_DELLA_CARTELLA_CHE_SCONTIENE_SCRAPE\"
```
e chiudiamo il prompt.

Ora analizziamo la pagina web con Google Chrome ed utilizzaimo il tasto destro del mouse sull'elemento **articolo**

![ispeziona articolo](./ispeziona_articolo.png)

selezionando **Ispeziona** si aprirà l'interfaccia sviluppatore di Chrome 

![intefaccia ispeziona articolo](./ispeziona_articolo_interfaccia.png)

ci posizioniamo sopra l'elemento selezionato e con il tasto destro del mouse e scegliamo **Copy** => **Copy element**, l'elemento copiato è il seguente

```html
<div class="articolo">Art. 1</div>
```

facciamo la stessa cosa per la descrizione dell'articolo ed otteniamo

```html
<div class="articolo_rubrica">Elementi costitutivi della Regione</div>
```

Per estrarre gli elementi individuati sopra si possono scrivere due **query xpath** che utilizzaremo per estrarre gli elementi

```
//div[@class="articolo_rubrica"]/text():
//div[@class="articolo_rubrica"]/text():
```

Con gli elementi che abbiamo individuato siamo pronti per poter estrarre i dati, iniziamo con lo scaricare la pagina 

```
https://demetra.regione.emilia-romagna.it/al/articolo?urn=er%3Aassemblealegislativa%3Alegge%3A2005%3B13&dl_t=text%2Fxml&dl_a=y&dl_id=10&pr=idx%2C0%3Bartic%2C0%3Barticparziale%2C1&anc=tit1&fbclid=IwAR0Lcn8E89VosOWln-amBDx5N8rW1WiOsKjcBFv_7TjD7YsbJhWz0UtqUHk
```

utilizzando l'utility **curl** di regola disponibile nelle shell linux

```
curl "https://demetra.regione.emilia-romagna.it/al/articolo?urn=er%3Aassemblealegislativa%3Alegge%3A2005%3B13&dl_t=text%2Fxml&dl_a=y&dl_id=10&pr=idx%2C0%3Bartic%2C0%3Barticparziale%2C1&anc=tit1&fbclid=IwAR0Lcn8E89VosOWln-amBDx5N8rW1WiOsKjcBFv_7TjD7YsbJhWz0UtqUHk" >./pagina
```

verrà creato un file locale chiamato **pagina** che contiene il codice **html** della pagine web, partendo da questo file locale inziamo ad estrarre gli elementi utilizzando il programma **scrape**

```
# estrai i titoli e sostituisci il tab di output con a capo
<./pagina scrape -e '//div[@class="articolo_rubrica"]/text()' | tr "\t" "\n" >./numero_articoli
# estrai numero articoli e sostituisci il tab di output con a capo
<./pagina scrape -e '//div[@class="articolo"]/text()' | tr "\t" "\n" >./articoli
# metti insieme articoli e titoli
paste articoli titoli >./output
```


Di base comunque un modo tipico è fare una query XPATH.

I titoli degli articoli hanno questra struttura HTML

<div class="articolo_rubrica">Elementi costitutivi della Regione</div>
La query XPATH è quindi //div[@class="articolo_rubrica"]/text():

//div > un div ovunque nella pagina
[@class="articolo_rubrica"] > a cui sia associata la classe articolo_rubrica
text() > ti estrae il testo contenuto nel div definito sopra
Gli articoli li potresti numerare automaticamente, sono progressivi.
Via XPATH , ragionando come sopra, è //div[@class="articolo"]/text()

A quel punto il tool che io trovo comodo è la shell e l'utility scrape (vedi sotto):

# scarichi la pagina
curl "https://demetra.regione.emilia-romagna.it/al/articolo?urn=er%3Aassemblealegislativa%3Alegge%3A2005%3B13&dl_t=text%2Fxml&dl_a=y&dl_id=10&pr=idx%2C0%3Bartic%2C0%3Barticparziale%2C1&anc=tit1&fbclid=IwAR0Lcn8E89VosOWln-amBDx5N8rW1WiOsKjcBFv_7TjD7YsbJhWz0UtqUHk" >./pagina
# estrai i titoli e sostituisci il tab di output con a capo
<./pagina scrape -e '//div[@class="articolo_rubrica"]/text()' | tr "\t" "\n" >./titoli
# estrai numero articoli e sostituisci il tab di output con a capo
<./pagina scrape -e '//div[@class="articolo"]/text()' | tr "\t" "\n" >./articoli
# metti insieme articoli e titoli
paste articoli titoli >./output

In output hai

Art. 1  Elementi costitutivi della Regione
Art. 2  Obiettivi
Art. 3  Politiche ambientali
Art. 4  Politiche del lavoro
Art. 5  Politiche economiche
Art. 6  Politiche sociali
Art. 7  Promozione dell'associazionismo
Art. 8  Le Autonomie locali
Art. 9  Le formazioni sociali
Art. 10 Sviluppo dei territori
Art. 11 Ordinamento europeo e internazionale
Art. 12 Partecipazione della Regione alla formazione e all'attuazione  del diritto comunitario
Art. 13 Attività di rilievo internazionale della Regione
come installare scrape
Al momento non ho creato l'installer. Quindi puoi fare così

# lo scarichi
wget https://github.com/aborruso/scrape-cli/releases/download/v1.0/scrape
# gli dai permessi di esecuzione
chmod +x ./scrape
# lo sposti in una cartella presente nel PATH
sudo mv ./scrape /usr/bin