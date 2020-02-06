# Come creare una versione Portable di QGIS 3.x

- issue correlata: [#112](https://github.com/opendatasicilia/tansignari/issues/112)
- autore:  _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_ fornitore ricetta [Andrea Borruso](https://twitter.com/aborruso)
- ingredienti: [QGIS](https://qgis.org/it/site/), [bash](https://it.wikipedia.org/wiki/Bash), [sed](https://it.wikipedia.org/wiki/Sed_(Unix)), [7z](https://manpages.debian.org/jessie/p7zip-full/7za.1.en.html), [curl](https://curl.haxx.se/)
  
---

<!-- TOC -->

- [Come creare una versione Portable di QGIS 3.x](#come-creare-una-versione-portable-di-qgis-3x)
  - [Che cosa è una versione Portable](#che-cosa-%c3%a8-una-versione-portable)
  - [Step by step usando script Bash](#step-by-step-usando-script-bash)
  - [Script bash](#script-bash)
  - [Riferimento](#riferimento)
  - [Download Portable](#download-portable)
  - [Chi ha cucinato questa ricetta o ne ha tratto ispirazione](#chi-ha-cucinato-questa-ricetta-o-ne-ha-tratto-ispirazione)

<!-- /TOC -->

---

## Che cosa è una versione Portable

Per applicazione portabile (o applicazione portatile; in inglese portable application) si intende un software applicativo che non necessita di installazione all’interno del sistema operativo su cui viene eseguito. Programmi di questo genere possono essere memorizzati su supporto rimovibile come cd-rom o memorie flash. Un’applicazione portabile può indistintamente essere eseguita su qualsiasi computer in cui si dispone di un sistema operativo compatibile con l’applicazione stessa. Il vantaggio per l’utente è quindi quello di poter utilizzare la medesima applicazione su macchine diverse mantenendo le impostazioni personalizzate nell’uso dell’applicazione. Un secondo vantaggio delle applicazioni portabili deriva dal fatto che non richiedendo installazione possono spesso essere eseguite anche in ambienti in cui non si dispone dei diritti di amministrazione sul sistema operativo. [Wikipedia](https://it.wikipedia.org/wiki/Applicazione_portabile).
Per chiudere una issue è possibile seguire due vie:

## Step by step usando script Bash

1. creare una cartella sul desktop (es:**OSGeo4W64**);
2. scaricare il file [script.sh](https://github.com/pigreco/QGIS_portable_3x/blob/master/script.sh) all'interno della cartella appena creata al punto 1;
3. avviare Bash e digitare `chmod +x ./script.sh` per i permessi e poi `./script.sh`;
4. unzippare la cartella `OSGeo4W-xxxx.7z` e avviare il file `qgis-ltr.bat` presente in `/OSGeo4W/bin`.
   
   **PS:** nello script scarico la `QGIS-OSGeo4W-3.4.15-1-Setup-x86_64.exe` e i file `msvcp100.dll` e `msvcr100.dll` versione a 64 bit!!!

## Script bash

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

## Riferimento

- **Repository** : https://github.com/pigreco/QGIS_portable_3x

## Download Portable

* [**QGIS 3.10.2-2 A Coruña Portable**](https://mega.nz/#!hFpGgSqY!ortl0wgzflbQ_-HxrhK4uwu-T7tX5iu1FuwiXp0UQEM) (da unzippare in una pen drive F:\OSGeo4W e eseguire punto 5)
* [**QGIS 3.4.10 LTR Madeira Portable**](https://mega.nz/#!IN5VWaJY!nMUkHxy1krLLm9h1LdISTEVAcTRHyQumpPMDF927CpU) (da unzippare in una pen drive F:\OSGeo4W e eseguire punto 5)
* [**QGIS 3.8.0 Zanzibar Portable**](https://mega.nz/#!xNoUDSKZ!j3yRI0DOGI6AtP_NdqLLsIDSXYX0dbXcaLsoIOcHHFQ) (da unzippare in una pen drive F:\OSGeo4W e eseguire punto 5)
* [**QGIS 2.18.28-3 LTR Las Palmas Portable**](https://mega.nz/#!dFRCAAwC!x3hx-EazfFCHsWXNrUE4zQbzDp8FIXEQzRcoxMIOz7g) (da unzippare in una pen drive F:\OSGeo4W e eseguire punto 5)

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- **Blog Pigrecoinfinito** : https://pigrecoinfinito.com/2019/02/26/creare-una-versione-portable-di-qgis-2-18-ltr/
