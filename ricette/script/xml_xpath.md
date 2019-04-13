# Estrarre dati da un file XML con Google sheet (XPATH)

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue: [#50](https://github.com/opendatasicilia/tansignari/issues/50) fornitore ricetta _[Andrea Borruso](https://twitter.com/aborruso?lang=it)_


---

**Caso d'uso:** il file di tematizzazione di un layer (in [QGIS](https://qgis.org/it/site/)) è un file [XML](https://it.wikipedia.org/wiki/XML), alcune volte è necessario reperire i codici colore (in [rgba](https://it.wikipedia.org/wiki/RGBA)) direttamente dal file di tematizzazione: questa ricetta estrae i codici colori utilizzati e crea una tabella, in [CSV](https://it.wikipedia.org/wiki/Comma-separated_values), pronta per essere utilizzata in QGIS e messa in join con il layer in esame. (dalla [ricetta](https://tansignari.readthedocs.io/it/latest/ricette/script/Estrarre_dati_da_file_XML.html#utility-xmlstarlet-con-linguaggio-xpath) di [@Totò Fiandaca](https://twitter.com/totofiandaca?lang=it))

Per chi ha poca familiarità con *bash* e tutti gli ottimi applicativi *Linux*, usati nelle [ricetta](http://tansignari.opendatasicilia.it/it/latest/ricette/script/Estrarre_dati_da_file_XML.html) di _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_ una valida alternativa/soluzione potrebbe essere l'utilizzo di **Google sheet** e **XPath**.

Il file [sheet](https://docs.google.com/spreadsheets/d/1tjXYrhP2nggPxML3Vay2Ycab7ikACQ95scRHLjo_GYc/edit#gid=0) iniziale per l'importazione del file [tema.xml](https://gist.githubusercontent.com/aborruso/5452bbecbacfce8ac61b5cc8165ac0d4/raw/0b0243ac25361726fd1a112e8bdea7920d1d487b/tema.xml) e le relative query XPATH è scritto da [Andrea Borruso](https://twitter.com/aborruso?lang=it)

In questo caso il file xml deve essere prima caricato in un server remoto e poi richiamato con la funzione [IMPORTXML](https://support.google.com/docs/answer/3093342?hl=it). <br>
N. B.: Il server remoto può essere un semplice **[server ftp](https://it.wikipedia.org/wiki/Server_FTP)** o anche un **[repository Github](https://it.wikipedia.org/wiki/GitHub)**

Ricordiamoci prima i caricare i dati, di settare le **[impostazioni del foglio di lavoro](https://support.google.com/docs/answer/58515?co=GENIE.Platform%3DDesktop&hl=it)**, dal menu **File**, nella scheda *Generale* selezionare **Regno Unito** per le Impostazioni internazionali e spuntare **Usa sempre nomi di funzioni inglesi**, nella scheda *Calcolo* selezionare **A ogni modifica** nelle impostazioni del Ricalcolo.

**N.B.** La sintassi della funzione [IMPORTXML](https://support.google.com/docs/answer/3093342?hl=it) dipende dalle impostazioni del **[impostazioni del foglio di lavoro](https://support.google.com/docs/answer/58515?co=GENIE.Platform%3DDesktop&hl=it)** 

**Esempio**: 
* in italiano il separatore degli argomenti della formula è il **;** (punto e virgola) 
* in inglese è la **,** (virgola)

Sintassi per foglio di lavoro in **Italiano**

```
=IMPORTXML(url; query_xpath)
```
Sintassi per foglio di lavoro in **Inglese**

```
=IMPORTXML(url, query_xpath)
```
Dove: <br>
* **url** - L'URL della pagina da esaminare, incluso il protocollo (ad esempio http://).
  * Il valore di url deve essere racchiuso tra virgolette o essere un riferimento a una cella che contiene il testo appropriato.

* **query_xpath** - La query XPath da eseguire sui dati strutturati.
  * Per ulteriori informazioni su XPath, consulta la pagina [w3schools.com/xml/xpath](http://www.w3schools.com/xml/xpath_intro.asp)


**Esempio di utilizzo**

```
=IMPORTXML("http://gbvitrano.it/clip/umap/tema.xml","//category/@symbol")
```
---

File xml da cui estrarre i dati [tema.xml](http://gbvitrano.it/clip/umap/tema.xml) (server ftp)

![](/img/xpath/xml_00.jpg)

Studiando la struttura del file xml si capisce quali espressioni [XPath](https://www.html.it/pag/31760/xpath/) occorrono per estrarre i dati di nostro interesse.
Nel caso specifico dobbiamo estrarre i **Nomi delle Regioni** il **colore** utilizzato per la tematizzazione e i realativi **id**

![](/img/xpath/xml_01.jpg)

Formula per estrarre la colonna *name* (id colore) del gruppo **symbol**

![](/img/xpath/sheet_01.jpg)

```
=IMPORTXML("http://gbvitrano.it/clip/umap/tema.xml","//symbols/symbol/@name")
```

![](/img/xpath/sheet_02.jpg)

Formula per estrarre la colonna *colore* del gruppo **symbol**

![](/img/xpath/xml_02.jpg)

```
=IMPORTXML("http://gbvitrano.it/clip/umap/tema.xml","//symbols/symbol/layer/prop[@k='color']/@v")
```

![](/img/xpath/sheet_03.jpg)

Formula per estrarre la colonna *label* (nome regione) del gruppo **category**

![](/img/xpath/xml_03.jpg)
```
=IMPORTXML("http://gbvitrano.it/clip/umap/tema.xml","//category/@value")
```
Formula per estrarre la colonna *name* (id regione) del gruppo **category**

```
=IMPORTXML("http://gbvitrano.it/clip/umap/tema.xml","//category/@symbol")
```
![](/img/xpath/sheet_04.jpg)

alla fine si fa il JOIN con **[VLOOKUP](https://support.google.com/docs/answer/3093318?hl=it&authuser=1)** (cit. [Andrea Borruso](https://twitter.com/aborruso?lang=it)) per ottenere il colore utilizzato in ogni Regione.

```
=VLOOKUP(D2,A:B,2,FALSE)
```

---

## Soluzione usando Libreoffice Calc, Excel
Utilizzando la funzione **[FILTRO.XML](https://help.libreoffice.org/Calc/WEBSERVICE/it)**, che applica un'espressione XPath a un documento XML, si possono estrarre i dati ad file xml in **remoto** anche con LibreOffice Calc ed Excel.

```
FILTRO.XML(SERVIZIO.WEB(URI); espressione XPath)
```
Dove:
1. **SERVIZIO.WEB(URI)** ottiene del contenuto web da un URI.<br>
2. **URI**: il testo URI del servizio web, ottiene del contenuto web da un URI.<br>
3. **Espressione XPath** (richiesta): stringa contenente un'espressione XPath valida.<br>

descrizioni tratte dalla guida di [libreoffice](https://help.libreoffice.org/Calc/WEBSERVICE/it)

**Esempio** 

```
FILTRO.XML(SERVIZIO.WEB("http://gbvitrano.it/clip/umap/tema.xml"); "//category/@symbol")
```
Restituisce informazioni del valore *name* (id regione) del gruppo **category**

---

## Utility yq
Studiando il comando utilizzato da _[Andrea Borruso](https://twitter.com/aborruso?lang=it)_ per estrarre i dati con l'utility **[yq](https://stedolan.github.io/jq/)**, ci rendiamo conto che anche se scritta ovviamente in modo diverso, la query è sempre la stessa, il file *tema.xml* si trova il locale e la finstra *bash* è aperta direttamente nella cartella del file *tema.xml*

```
<tema.xml xq -r '.qgis["renderer-v2"].symbols.symbol[]|[.["@name"],.layer.prop[1]["@v"]]|@csv' >./idColori.csv
```
```
<tema.xml xq -r '.qgis["renderer-v2"].categories.category[]|[.["@symbol"],.["@value"]]|@csv' >./idRegioni.csv
```

---

## Soluzione usando [QGIS, yq, xmlstarlet, XPATH, Miller](https://tansignari.readthedocs.io/it/latest/ricette/script/Estrarre_dati_da_file_XML.html#utility-xmlstarlet-con-linguaggio-xpath)

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* issue: [#50](https://github.com/opendatasicilia/tansignari/issues/50) fornitore ricetta _[Andrea Borruso](https://twitter.com/aborruso?lang=it)
* ingredienti: [QGIS](https://qgis.org/it/site/), [yq](https://github.com/kislyuk/yq), [xmlstarlet](http://xmlstar.sourceforge.net/doc/UG/xmlstarlet-ug.html), [XPATH](https://www.w3schools.com/xml/xpath_intro.asp), [Miller](https://github.com/johnkerl/miller)
* ricetta è raggiungibile [qui](http://tansignari.opendatasicilia.it/it/latest/ricette/script/Estrarre_dati_da_file_XML.html)


