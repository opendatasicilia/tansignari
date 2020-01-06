# QGIS e i grigliati NTv2 per la Sicilia

- issue correlata: [#100](https://github.com/opendatasicilia/tansignari/issues/100)
- autore: [Totò Fiandaca](https://twitter.com/totofiandaca); fornitore della ricetta: [Andrea Giudiceandrea](https://github.com/agiudiceandrea); 
- ingredienti: [QGIS](https://qgis.org/it/site/), [SQL](https://it.wikipedia.org/wiki/Structured_Query_Language), [SpatiaLite](https://www.gaia-gis.it/fossil/libspatialite/index), [NTv2](https://webapp.geod.nrcan.gc.ca/geod/tools-outils/ntv2.php)
  
---

Lo standard **NTv2** (_National Transformation versione 2_) è stato definito nel 1995 dal [servizio geodetico del governo canadese](http://webapp.geod.nrcan.gc.ca/geod/) per archiviare le traslazioni da apportare alle coordinate geografiche per il passaggio tra datum diversi (originariamente da NAD27 a NAD83). Questo standard si è ora diffuso in tutto il mondo ed è utilizzato da tutti i più diffusi software GIS, sia [proprietari](https://it.wikipedia.org/wiki/Software_proprietario) che [Open Source](https://it.wikipedia.org/wiki/Open_source).

Per gli scopi di numerosi progetti GIS, non è necessario raggiungere la precisione fornita dai grigliati calcolati da IGM, ma è comunque estremamente utile poter operare trasformazioni sull’intero territorio nazionale con precisione submetrica.

Grazie all’Ing. [`Ernesto Sferlazza`](http://osgeo-org.1560.x6.nabble.com/grigliato-NTV2-per-la-Sicilia-td4182271.html) ([Descrizione procedura per la generazione di griglie NTV2](http://www.provincia.agrigento.it/flex/cm/pages/ServeAttachment.php/L/IT/D/D.6360cf6e7857e4788f2f/P/BLOB%3AID%3D309)) per aver creato e condiviso una griglia di scostamenti (grid shift: dal sistema di coordinate geografiche ROMA40  al sistema WGS84 ) nel formato NTv2 per tutto il territorio siciliano, isole minori comprese

---

## Come integrarlo in QGIS

Scaricato l’archivio `*.gsb` e incollarlo nella sotto-cartella dell’installazione di **QGIS**, in particolare per chi usa:

- **OSGeo4W Network Installer (64 bit)**: `C:\OSGeo4W64\share\proj`
- **Standalone (64 bit)**: `C:\Program Files\QGIS 3.10\share\proj`

Successivamente occorre aggiungere una riga al database di QGIS che gestisce i CRS, in particolare al db che si trova qui: ‪`C:\OSGeo4W64\share\proj\proj.db` (per la standalone `C:\Program Files\QGIS 3.10\share\proj`)

quindi aprire il db con **SpatiaLite_gui** e usare:

```sql
INSERT INTO "grid_transformation"
VALUES ('PROJ','EPSG_4265_TO_EPSG_4258','Monte Mario (ROMA40) TO
ETRS89/ETRF89 (GN)',
'Per tutto il territorio siciliano, isole minori comprese - Ing.Sferlazza',
'LOCALE',
'EPSG','9615','NTv2',
'EPSG','4265','EPSG','4258',
'EPSG','1127', -- Area of use Tutta Italia
NULL,
'EPSG','8656','Latitude and longitude difference file',
'ItalyRome40ToWGS84_NTV2_GN.gsb',
NULL,NULL,NULL,NULL,NULL,NULL,NULL,0);
```
Il grigliato `ItalyRome40ToWGS84_NTV2_GN.gsb` viene utilizzato automaticamente in **QGIS 3.10.1** senza ulteriori necessità di impostare alcuna _Default Datum Trasformation_.

## RINGRAZIAMENTI

- [Andrea Giudiceandrea](https://github.com/agiudiceandrea)
- [Ing. Sferlazza](http://osgeo-org.1560.x6.nabble.com/grigliato-NTV2-per-la-Sicilia-td4182271.html)
- [Lista gvSIG Italian](http://osgeo-org.1560.x6.nabble.com/gvSIG-Italian-f4178756.html)
- [Lista QGIS-it](http://osgeo-org.1560.x6.nabble.com/Integrare-i-grigliati-NTv2-in-QGIS-3-10-futura-LTR-td5426354.html)


---

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- [Blog post su Pigrecoinfinito](https://pigrecoinfinito.com/2020/01/06/qgis-e-i-grigliati-ntv2-per-la-sicilia/)