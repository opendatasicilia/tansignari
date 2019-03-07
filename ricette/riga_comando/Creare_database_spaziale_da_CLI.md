
# Creare database spaziale da riga di comando

- issue correlata: [#15](https://github.com/opendatasicilia/tansignari/issues/15)
- autore: [_Totò Fiandaca_](https://github.com/pigreco)
  

<!-- TOC -->

- [Creare database spaziale da riga di comando](#creare-database-spaziale-da-riga-di-comando)
  - [dataset](#dataset)
  - [procedimento](#procedimento)
  - [Script Bash](#script-bash)
  - [Cosa fa questo script](#cosa-fa-questo-script)

<!-- /TOC -->

  
---

## dataset

* [01_demanio.csv](https://gist.github.com/aborruso/503df6c6477c341431e23bc51bc37149/raw/7aac29415b99512758acffd05fa463081f011484/01_demanio.csv)

## procedimento

Salvare lo script bash con nome `geometry.sh` e poi, da riga di comando, dargli i permessi di esecuzione con `chmod +x geometry.sh` e poi lanciarlo con `./geometry.sh`

## Script Bash

```Bash
#!/bin/bash

sqlite3 nomeDb.sqlite <<EOF

.load /usr/local/lib/mod_spatialite.so
.mode csv 01_demanio
.import 01_demanio.csv opendemanio

SELECT InitSpatialMetaData(1);

SELECT  AddGeometryColumn ('opendemanio','geometry',3857,'POINT','XY');

UPDATE opendemanio SET geometry =
MakePoint(CAST(X AS float),CAST(Y AS float),3857);

EOF
```

## Cosa fa questo script

Crea un database spatialite con geotabella partendo da un file CSV con coordinate.
