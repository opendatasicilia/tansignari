# Modificare un file XML

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* issue: [#58](https://github.com/opendatasicilia/tansignari/issues/58) fornitore ricetta *[Giovanni Pirrotta](https://twitter.com/gpirrotta?lang=it)* e *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*
* ingredienti: [QGIS](https://qgis.org/it/site/),[Python](https://www.python.org/), [xmlstarlet](http://xmlstar.sourceforge.net/doc/UG/xmlstarlet-ug.html), [XPATH](https://www.w3schools.com/xml/xpath_intro.asp), [Miller](https://github.com/johnkerl/miller)

---

**Caso d'uso:** Partendo da un file XML la cui struttura è quella di un file **QML** (proveniente dalla tematizzazione - metodo categorizzato - di un layer vettoriale in QGIS) sostituire/modificare alcuni valori presenti nel file.

## script

### Python

```python
import csv

myDict = {}

with open('dict.txt', 'r') as dictfile:
    csvreader = csv.reader(dictfile, delimiter=',')
    for row in csvreader:
        myDict[row[0]] = row[1]

from bs4 import BeautifulSoup

infile = open('tema.xml','r')
contents = infile.read()
soup = BeautifulSoup(contents,'xml')
symbols = soup.select('symbol')
for symbol in symbols:
    if symbol['name'] in myDict:
        prop = symbol.find('prop', {'k' : 'color'})
        prop['v'] = myDict[symbol['name']]

xml = soup.prettify('utf-8')
with open('tema_u.xml', 'wb') as file:
    file.write(xml)
```

dove `dict.txt` rappresenta un file CSV cosi strutturato:
```
"0","232,193,76,255"
"1","48,218,227,255"
"10","231,108,155,255"
"11","237,177,124,255"
"12","63,175,231,255"
"13","210,214,92,255"
"14","234,16,38,255"
"15","239,110,81,255"
"16","50,235,192,255"
"17","160,107,220,255"
"18","98,66,238,255"
"19","34,233,131,255"
"2","224,59,169,255"
"3","163,225,124,255"
"4","162,15,210,255"
"5","68,239,48,255"
"6","179,235,59,255"
"7","219,21,209,255"
"8","18,39,233,255"
"9","120,204,137,255"
```

- `tema.xml` è il file xml da modificare
- `tema_u.xml` è il file xml modificato

Il file `tema.xml` è la tematizzazione (metodo [categorizzato](https://docs.qgis.org/3.4/it/docs/user_manual/working_with_vector/vector_properties.html#categorized-renderer)) dello shapefile regioni ISTAT.

### utility xmlstarlet con linguaggio XPATH

```bash
#!/bin/bash
set -x

while IFS=$'\t' read -r col1 col2
do
    xmlstarlet ed --inplace -u '//symbols/symbol[@name='"$col1"']/layer/prop[@k="color"]/@v' -v "$col2" tema.xml
done < input.tsv
```

il file `input.tsv` è cosi strutturato

```
0	232,193,76,255
1	48,218,227,255
10	231,108,155,255
11	237,177,124,255
12	63,175,231,255
13	210,214,92,255
14	234,16,38,255
15	239,110,81,255
16	50,235,192,255
17	160,107,220,255
18	98,66,238,255
19	34,233,131,255
2	224,59,169,255
3	163,225,124,255
4	162,15,210,255
5	68,239,48,255
6	179,235,59,255
7	219,21,209,255
8	18,39,233,255
9	120,204,137,255
```


## Osservazioni

La ricetta è stata realizzata per un caso concreto utile nel mondo dei `gissari` ma il principio che ci sta dietro è generale.

Per ottenere il file `tema.xml` da QGIS: tasto destro del mouse sul layer tematizzato *| Stili | Copia lo stile | Simbologia*; questo permette di copiare lo stile in memoria, quindi aprire un editor di testo ed incollare, salvare il file come tema.xml.

il file `tema.xml` è scaricabile da [qui](https://github.com/opendatasicilia/tansignari/files/3055033/tema.zip)

---

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- [QGIS (RI)CREARE LA LEGENDA A PARTIRE DAL COLORE RGBA PRESENTE NELLA TABELLA ATTRIBUTI](https://pigrecoinfinito.wordpress.com/2019/04/16/qgis-ricreare-la-legenda-a-partire-dal-colore-rgba-presente-nella-tabella-attributi/), di Salvatore Fiandaca;