# Come ottimizzare uno script bash

- issue correlata: [#112](https://github.com/opendatasicilia/tansignari/issues/112) - [#111](https://github.com/opendatasicilia/tansignari/issues/111) - [#110](https://github.com/opendatasicilia/tansignari/issues/110)
- autore:  _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_ fornitore ricetta [Andrea Borruso](https://twitter.com/aborruso)
- ingredienti: [bash](https://it.wikipedia.org/wiki/Bash), [sed](https://it.wikipedia.org/wiki/Sed_(Unix)), [7z](https://manpages.debian.org/jessie/p7zip-full/7za.1.en.html), [curl](https://curl.haxx.se/)
  
---

<!-- TOC -->

- [Come ottimizzare uno script bash](#come-ottimizzare-uno-script-bash)
  - [Introduzione](#introduzione)
    - [script iniziale](#script-iniziale)
    - [script ottimizzato](#script-ottimizzato)
  - [Riferimenti](#riferimenti)
  - [Chi ha cucinato questa ricetta o ne ha tratto ispirazione](#chi-ha-cucinato-questa-ricetta-o-ne-ha-tratto-ispirazione)

<!-- /TOC -->

---

## Introduzione

Per realizzare le versioni Portable di QGIS è stato usato il seguente [script bash](https://github.com/pigreco/QGIS_portable_3x/blob/master/script.sh)

### script iniziale

```bash
#!/bin/bash

set -x

curl http://download.osgeo.org/qgis/win64/QGIS-OSGeo4W-3.4.10-1-Setup-x86_64.exe >QGIS-OSGeo4W-3.4.10-1-Setup-x86_64.exe
7z x QGIS-OSGeo4W-3.4.10-1-Setup-x86_64.exe
mv '$_25_' OSGeo4W
mv '$PLUGINSDIR' OSGeo4W
cd OSGeo4W/bin
mv qgis-ltr.bat.tmpl qgis-ltr.bat
cd ../apps/qgis-ltr/bin
curl -L "https://github.com/pigreco/QGIS_portable_3x/raw/master/file/win64/win64.zip" >win64.zip
7z x win64.zip
rm win64.zip
cd ../../../../
7z a OSGeo4W_3410.7z OSGeo4W
```

- dove occorre scrivere **tre** volte il nome del file da scaricare (`QGIS-OSGeo4W-3.4.10-1-Setup-x86_64.exe`) con potenziali errori di scrittura;
- nell'ultima riga dello script: occorre formulare il nome (`OSGeo4W_3410.7z`) della cartella finale da zippare;

con le **ottimizzazioni**:
- scrivo **una** sola volta il nome del file da scaricare assegnandola alla variabile (`versione`);
- il nome della cartella finale viene estratto automaticamente facendo uso di [`sed`](https://it.wikipedia.org/wiki/Sed_(Unix)) che lo associa alla variabile `nome`;

script **ottimizzato**:

### script ottimizzato

```bash
#!/bin/bash

set -x

versione="QGIS-OSGeo4W-3.4.15-1-Setup-x86_64.exe"
nome=$(sed -r 's/(QGIS-)(.+)(-Setup-x86_64.exe)/\2/g' <<<"$versione")
echo "$nome"

curl http://download.osgeo.org/qgis/win64/"$versione" >"$versione"
7z x "$versione"
mv '$_25_' OSGeo4W
mv '$PLUGINSDIR' OSGeo4W
cd OSGeo4W/bin
mv qgis-ltr.bat.tmpl qgis-ltr.bat
cd ../apps/qgis-ltr/bin
curl -L "https://github.com/pigreco/QGIS_portable_3x/raw/master/file/win64/win64.zip" >win64.zip
7z x win64.zip
rm win64.zip
cd ../../../../
7z a "$nome".7z OSGeo4W
```

## Riferimenti
- [**Index of /qgis/win64/**](http://download.osgeo.org/qgis/win64/)
- [**repository**](https://github.com/pigreco/QGIS_portable_3x)
- [**Impara X in Y minuti**](https://learnxinyminutes.com/docs/it-it/bash-it/)
- [**QGIS**](https://qgis.org/it/site/)

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- [**Come creare una versione Portable di QGIS 3.x**](http://tansignari.opendatasicilia.it/it/latest/ricette/utilities/come_creare_portable_QGIS.html)
