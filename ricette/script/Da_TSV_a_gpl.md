# Traformare un file TSV in gpl

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* issue: [#63](https://github.com/opendatasicilia/tansignari/issues/63) fornitore ricetta *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*
* ingredienti: [QGIS](https://qgis.org/it/site/), [xmlstarlet](http://xmlstar.sourceforge.net/doc/UG/xmlstarlet-ug.html), [XPATH](https://www.w3schools.com/xml/xpath_intro.asp), [Miller](https://github.com/johnkerl/miller)

---

<!-- TOC -->

- [Traformare un file TSV in gpl](#traformare-un-file-tsv-in-gpl)
  - [script bash](#script-bash)
  - [script passo passo](#script-passo-passo)
    - [file di input out_regioni_xpath.tsv](#file-di-input-outregionixpathtsv)
    - [creo un file gpl con testo costante](#creo-un-file-gpl-con-testo-costante)
    - [output](#output)
  - [estraggo in ordine i campi 2 e 3 e rinomino](#estraggo-in-ordine-i-campi-2-e-3-e-rinomino)
    - [output](#output-1)
  - [trasformare il campo rgba in 4 campi](#trasformare-il-campo-rgba-in-4-campi)
    - [output](#output-2)
  - [rimuovere il campo con il IV valore di colore](#rimuovere-il-campo-con-il-iv-valore-di-colore)
    - [output](#output-3)
  - [allinea a destra](#allinea-a-destra)
    - [output](#output-4)
  - [creare un solo campo](#creare-un-solo-campo)
    - [output](#output-5)
- [script unico](#script-unico)
    - [output](#output-6)
  - [Dati](#dati)

<!-- /TOC -->

---

**Caso d'uso:** A partire da un file `QML` (file di tematizzazione di QGIS) ottenere un file **QGIS Palette** in formato `gpl` da riutilizzare in QGIS per la tematizzazione feature e legenda.

## script bash

```
#!/bin/bash
set -x

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl

# riarrangio il file di input (out_regioni_xpath.tsv) per ottenere il file gpl
mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
then nest --explode --values --across-fields -f rgba --nested-fs "," \
then cut -x -f rgba_4 \
then put -S 'if ($rgba_1=~"^.{2}$") {$rgba_1=" ".$rgba_1};if ($rgba_2=~"^.{2}$") {$rgba_2=" ".$rgba_2};if ($rgba_3=~"^.{2}$") {$rgba_3=" ".$rgba_3}' \
then put -S '$rgb=$rgba_1." ".$rgba_2." ".$rgba_3' \
then cut -o -f rgb,regione   out_regioni_xpath.tsv >>./legenda.gpl
```

DOVE:

- `out_regioni_xpath.tsv`, file di input per lo script
- `legenda.gpl` file di output dello script
- `cut -o -f 2,3` , per estrarre in ordine il campo 2 e 3
- `then label rgba,regione` , per rinominarli 
- `then nest --explode --values --across-fields -f rgba --nested-fs ","` , per trasformare il campo rgba in 4 campi
- `then cut -x -f rgba_4` , per rimuovere il campo con il IV valore di colore
- `then put -S 'if ($rgba_1=~"^.{2}$") {$rgba_1=" ".$rgba_1};if ($rgba_2=~"^.{2}$") {$rgba_2=" ".$rgba_2};if ($rgba_3=~"^.{2}$") {$rgba_3=" ".$rgba_3}'` , per fare in modo che i valori numerici di due caratteri, siano trasformati in spazio seguito dai due caratteri
- `then put -S '$rgb=$rgba_1." ".$rgba_2." ".$rgba_3'` , per creare un solo campo che contiene i valori con gli spazi come sopra
- `then cut -o -f rgb,regione   input.txt`, per tenere soltanto il campo con regione e rgb nell'ordine scritto


## script passo passo

### file di input out_regioni_xpath.tsv

```
0	232,193,76,255	Abruzzo
1	48,218,227,255	Basilicata
2	224,59,169,255	Calabria
3	163,225,124,255	Campania
4	162,15,210,255	Emilia-Romagna
5	68,239,48,255	Friuli Venezia Giulia
6	179,235,59,255	Lazio
7	219,21,209,255	Liguria
8	18,39,233,255	Lombardia
9	120,204,137,255	Marche
10	231,108,155,255	Molise
11	237,177,124,255	Piemonte
12	63,175,231,255	Puglia
13	210,214,92,255	Sardegna
14	234,16,38,255	Sicilia
15	239,110,81,255	Toscana
16	50,235,192,255	Trentino-Alto Adige
17	160,107,220,255	Umbria
18	98,66,238,255	Valle d'Aosta
19	34,233,131,255	Veneto
```

### creo un file gpl con testo costante

```
#!/bin/bash
set -x

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl
```

### output

```
GIMP Palette
Name: QGIS Palette
Columns: 4
#
```

## estraggo in ordine i campi 2 e 3 e rinomino

```
#!/bin/bash
set -x

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl

mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
out_regioni_xpath.tsv >>./legenda.gpl
```

### output

```
rinomino campi:
+-----------------+-----------------------+
| rgba            | regione               |
+-----------------+-----------------------+
| 232,193,76,255  | Abruzzo               |
| 48,218,227,255  | Basilicata            |
| 224,59,169,255  | Calabria              |
+-----------------+-----------------------+
```

```
GIMP Palette
Name: QGIS Palette
Columns: 4
#
232,193,76,255	Abruzzo
48,218,227,255	Basilicata
224,59,169,255	Calabria
163,225,124,255	Campania
162,15,210,255	Emilia-Romagna
68,239,48,255	Friuli Venezia Giulia
179,235,59,255	Lazio
219,21,209,255	Liguria
18,39,233,255	Lombardia
120,204,137,255	Marche
231,108,155,255	Molise
237,177,124,255	Piemonte
63,175,231,255	Puglia
210,214,92,255	Sardegna
234,16,38,255	Sicilia
239,110,81,255	Toscana
50,235,192,255	Trentino-Alto Adige
160,107,220,255	Umbria
98,66,238,255	Valle d'Aosta
34,233,131,255	Veneto
```

## trasformare il campo rgba in 4 campi

```
#!/bin/bash
set -x

intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda1.gpl

mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
then nest --explode --values --across-fields -f rgba --nested-fs "," \
out_regioni_xpath.tsv >>./legenda1.gpl
```

### output

```
GIMP Palette
Name: QGIS Palette
Columns: 4
#
232	193	76	255	Abruzzo
48	218	227	255	Basilicata
224	59	169	255	Calabria
163	225	124	255	Campania
162	15	210	255	Emilia-Romagna
68	239	48	255	Friuli Venezia Giulia
179	235	59	255	Lazio
219	21	209	255	Liguria
18	39	233	255	Lombardia
120	204	137	255	Marche
231	108	155	255	Molise
237	177	124	255	Piemonte
63	175	231	255	Puglia
210	214	92	255	Sardegna
234	16	38	255	Sicilia
239	110	81	255	Toscana
50	235	192	255	Trentino-Alto Adige
160	107	220	255	Umbria
98	66	238	255	Valle d'Aosta
34	233	131	255	Veneto
```

## rimuovere il campo con il IV valore di colore

```
#!/bin/bash
set -x

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl

# riarrangio il file di input (out_regioni_xpath.tsv) per ottenere il file gpl
mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
then nest --explode --values --across-fields -f rgba --nested-fs "," \
then cut -x -f rgba_4 \
out_regioni_xpath.tsv >>./legenda.gpl
```

### output

```
GIMP Palette
Name: QGIS Palette
Columns: 4
#
232	193	76	Abruzzo
48	218	227	Basilicata
224	59	169	Calabria
163	225	124	Campania
162	15	210	Emilia-Romagna
68	239	48	Friuli Venezia Giulia
179	235	59	Lazio
219	21	209	Liguria
18	39	233	Lombardia
120	204	137	Marche
231	108	155	Molise
237	177	124	Piemonte
63	175	231	Puglia
210	214	92	Sardegna
234	16	38	Sicilia
239	110	81	Toscana
50	235	192	Trentino-Alto Adige
160	107	220	Umbria
98	66	238	Valle d'Aosta
34	233	131	Veneto
```

## allinea a destra

```
#!/bin/bash
set -x

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl

# riarrangio il file di input (out_regioni_xpath.tsv) per ottenere il file gpl
mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
then nest --explode --values --across-fields -f rgba --nested-fs "," \
then cut -x -f rgba_4 \
then put -S 'if ($rgba_1=~"^.{2}$") {$rgba_1=" ".$rgba_1};if ($rgba_2=~"^.{2}$") {$rgba_2=" ".$rgba_2};if ($rgba_3=~"^.{2}$") {$rgba_3=" ".$rgba_3}' \
out_regioni_xpath.tsv >>./legenda.gpl
```

### output

```
GIMP Palette
Name: QGIS Palette
Columns: 4
#
232	193	 76	Abruzzo
 48	218	227	Basilicata
224	 59	169	Calabria
163	225	124	Campania
162	 15	210	Emilia-Romagna
 68	239	 48	Friuli Venezia Giulia
179	235	 59	Lazio
219	 21	209	Liguria
 18	 39	233	Lombardia
120	204	137	Marche
231	108	155	Molise
237	177	124	Piemonte
 63	175	231	Puglia
210	214	 92	Sardegna
234	 16	 38	Sicilia
239	110	 81	Toscana
 50	235	192	Trentino-Alto Adige
160	107	220	Umbria
 98	 66	238	Valle d'Aosta
 34	233	131	Veneto
 ```

## creare un solo campo

```
#!/bin/bash
set -x

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl

# riarrangio il file di input (out_regioni_xpath.tsv) per ottenere il file gpl
mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
then nest --explode --values --across-fields -f rgba --nested-fs "," \
then cut -x -f rgba_4 \
then put -S 'if ($rgba_1=~"^.{2}$") {$rgba_1=" ".$rgba_1};if ($rgba_2=~"^.{2}$") {$rgba_2=" ".$rgba_2};if ($rgba_3=~"^.{2}$") {$rgba_3=" ".$rgba_3}' \
then put -S '$rgb=$rgba_1." ".$rgba_2." ".$rgba_3' \
out_regioni_xpath.tsv >>./legenda.gpl
```

### output

```
GIMP Palette
Name: QGIS Palette
Columns: 4
#
232	193	 76	Abruzzo	232 193  76
 48	218	227	Basilicata	 48 218 227
224	 59	169	Calabria	224  59 169
163	225	124	Campania	163 225 124
162	 15	210	Emilia-Romagna	162  15 210
 68	239	 48	Friuli Venezia Giulia	 68 239  48
179	235	 59	Lazio	179 235  59
219	 21	209	Liguria	219  21 209
 18	 39	233	Lombardia	 18  39 233
120	204	137	Marche	120 204 137
231	108	155	Molise	231 108 155
237	177	124	Piemonte	237 177 124
 63	175	231	Puglia	 63 175 231
210	214	 92	Sardegna	210 214  92
234	 16	 38	Sicilia	234  16  38
239	110	 81	Toscana	239 110  81
 50	235	192	Trentino-Alto Adige	 50 235 192
160	107	220	Umbria	160 107 220
 98	 66	238	Valle d'Aosta	 98  66 238
 34	233	131	Veneto	 34 233 131
 ```

# script unico

```
#!/bin/bash
set -x

# estraggo i dati dal file QML
<tema.qml xmlstarlet fo -D | xmlstarlet sel -T -t -m "//symbols/symbol" -v $'concat(@name,"\t",layer/prop[@k="color"]/@v)' -n >./idColori.tsv
<tema.qml xmlstarlet fo -D | xmlstarlet sel -T -t -m "//category" -v $'concat(@symbol,"\t",@value)' -n >./idRegioni.tsv
mlr --tsv --implicit-csv-header --headerless-csv-output  join  -j 1 --lp colori --rp regioni -f idColori.tsv idRegioni.tsv >./out_regioni_xpath.tsv

# creo file con testo fisso
intestazione="GIMP Palette
Name: QGIS Palette
Columns: 4
#"

echo "$intestazione" >./legenda.gpl

# riarrangio i dati per ottenere il file gpl
mlr --nidx --fs "\t" cut -o -f 2,3 \
then label rgba,regione \
then nest --explode --values --across-fields -f rgba --nested-fs "," \
then cut -x -f rgba_4 \
then put -S 'if ($rgba_1=~"^.{2}$") {$rgba_1=" ".$rgba_1};if ($rgba_2=~"^.{2}$") {$rgba_2=" ".$rgba_2};if ($rgba_3=~"^.{2}$") {$rgba_3=" ".$rgba_3}' \
then put -S '$rgb=$rgba_1." ".$rgba_2." ".$rgba_3' \
then cut -o -f rgb,regione   out_regioni_xpath.tsv >>./legenda.gpl

# cancello i file non piu' utili
rm idColori.tsv
rm idRegioni.tsv
rm out_regioni_xpath.tsv
```

### output

```
GIMP Palette 
Name: QGIS Palette 
Columns: 4 
#
232 193  76	Abruzzo
 48 218 227	Basilicata
224  59 169	Calabria
163 225 124	Campania
162  15 210	Emilia-Romagna
 68 239  48	Friuli Venezia Giulia
179 235  59	Lazio
219  21 209	Liguria
 18  39 233	Lombardia
120 204 137	Marche
231 108 155	Molise
237 177 124	Piemonte
 63 175 231	Puglia
210 214  92	Sardegna
234  16  38	Sicilia
239 110  81	Toscana
 50 235 192	Trentino-Alto Adige
160 107 220	Umbria
 98  66 238	Valle d'Aosta
 34 233 131	Veneto
 ```

## Dati

- il file QML `tema.qml` è scaricabile da [qui](https://github.com/opendatasicilia/tansignari/files/3055033/tema.zip)
- il file CSV `out_regioni_xpath.tsv` è scaricabile da [qui](https://github.com/opendatasicilia/tansignari/files/3084977/out_regioni_xpath.zip)

