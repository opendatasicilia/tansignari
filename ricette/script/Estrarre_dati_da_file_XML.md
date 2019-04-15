# Estrarre dati da un file XML

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* issue: [#50](https://github.com/opendatasicilia/tansignari/issues/50) fornitore ricetta *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*
* ingredienti: [QGIS](https://qgis.org/it/site/), [yq](https://github.com/kislyuk/yq), [xmlstarlet](http://xmlstar.sourceforge.net/doc/UG/xmlstarlet-ug.html), [XPATH](https://www.w3schools.com/xml/xpath_intro.asp), [Miller](https://github.com/johnkerl/miller)

---

**Caso d'uso:** il file di tematizzazione di un layer (in [QGIS](https://qgis.org/it/site/)) è un file [XML](https://it.wikipedia.org/wiki/XML), alcune volte è necessario reperire i codici colore (in [rgba](https://it.wikipedia.org/wiki/RGBA)) direttamente dal file di tematizzazione: questa ricetta estrae i codici colori utilizzati e crea una tabella, in [CSV](https://it.wikipedia.org/wiki/Comma-separated_values), pronta per essere utilizzata in QGIS e messa in join con il layer in esame.

## script bash

### utility yq

```bash
#!/bin/bash
set -x

<tema.xml xq -r '.qgis["renderer-v2"].symbols.symbol[]|[.["@name"],.layer.prop[1]["@v"]]|@csv' >./idColori.csv
<tema.xml xq -r '.qgis["renderer-v2"].categories.category[]|[.["@symbol"],.["@value"]]|@csv' >./idRegioni.csv
mlr --csv --implicit-csv-header --headerless-csv-output  join  -j 1 --lp colori --rp regioni -f idColori.csv idRegioni.csv >./out_regioni_yq.csv

rm idColori.csv
rm idRegioni.csv
```

### utility xmlstarlet con linguaggio XPATH

```bash
#!/bin/bash
set -x

<tema.xml xmlstarlet fo -D | xmlstarlet sel -T -t -m "//symbols/symbol" -v $'concat(@name,"\t",layer/prop[@k="color"]/@v)' -n >./idColori.tsv
<tema.xml xmlstarlet fo -D | xmlstarlet sel -T -t -m "//category" -v $'concat(@symbol,"\t",@value)' -n >./idRegioni.tsv
mlr --tsv --implicit-csv-header --headerless-csv-output  join  -j 1 --lp colori --rp regioni -f idColori.tsv idRegioni.tsv >./out_regioni_xpath.tsv


rm idColori.tsv
rm idRegioni.tsv
```

Il file `tema.xml` è la tematizzazione (metodo [categorizzato](https://docs.qgis.org/3.4/it/docs/user_manual/working_with_vector/vector_properties.html#categorized-renderer)) dello shapefile regioni ISTAT, entrambi gli script creano un file CSV/TSV come mostrato sotto:


id|rgba|regione
--|----|-----
0|232,193,76,255|Abruzzo
1|48,218,227,255|Basilicata
2|224,59,169,255|Calabria
3|163,225,124,255|Campania
4|162,15,210,255|Emilia-Romagna
5|68,239,48,255|Friuli Venezia Giulia
6|179,235,59,255|Lazio
7|219,21,209,255|Liguria
8|18,39,233,255|Lombardia
9|120,204,137,255|Marche
10|231,108,155,255|Molise
11|237,177,124,255|Piemonte
12|63,175,231,255|Puglia
13|210,214,92,255|Sardegna
14|234,16,38,255|Sicilia
15|239,110,81,255|Toscana
16|50,235,192,255|Trentino-Alto Adige
17|160,107,220,255|Umbria
18|98,66,238,255|Valle d'Aosta
19|34,233,131,255|Veneto

**In QGIS:** tramite un semplice JOIN è possibile unire questa tabella con il layer regioni (campo unione `regioni`)


## Osservazioni

La ricetta è stata realizzata per un caso concreto utile nel mondo dei `gissari` ma il principio che ci sta dietro è generale.

Per ottenere il file `tema.xml` da QGIS: tasto destro del mouse sul layer tematizzato *| Stili | Copia lo stile | Simbologia*; questo permette di copiare lo stile in memoria, quindi aprire un editor di testo ed incollare, salvare il file come tema.xml.

il file `tema.xml` è scaricabile da [qui](https://github.com/opendatasicilia/tansignari/files/3055033/tema.zip)

## Soluzione usando Google Sheet

* autore: *[gbvitrano](https://twitter.com/gbvitrano)*
* issue: [#50](https://github.com/opendatasicilia/tansignari/issues/50) fornitore ricetta *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*
* ingredienti: [QGIS](https://qgis.org/it/site/), Google Sheet, [XPATH](https://www.w3schools.com/xml/xpath_intro.asp)
* ricetta è raggiungibile [qui](http://tansignari.opendatasicilia.it/it/latest/ricette/script/xml_xpath.html)

---

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- "[QGIS popolare un campo della tabella attributi con i colori dello stile categorizzato usato](https://pigrecoinfinito.wordpress.com/2019/04/11/qgis-popolare-un-campo-della-tabella-attributi-con-i-colori-dello-stile-categorizzato-usato/?fbclid=IwAR3vwe7zlO3BGcIQvBkg8cMUqwImyKMhNz6GOcdU1yRD7j4WjNS_dssuuGA)", di Salvatore Fiandaca;
- "[Estrarre dati da un file XML con Google sheet e XPath](https://medium.com/coseerobe/estrarre-dati-da-un-file-xml-con-google-sheet-e-xpath-b9e56be403)", di Gian Battista Vitrano;
- "[QGIS — Creare una Legenda categorizzata a partire da un campo della tabella attributi con codice colore](https://medium.com/@ivano.giuliano/qgis-creare-una-legenda-categorizzata-a-partire-da-un-campo-della-tabella-attributi-con-codice-10e4c4ca8b21)", di Ivano Giuliano.
