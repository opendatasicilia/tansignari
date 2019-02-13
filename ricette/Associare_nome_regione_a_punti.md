<!-- TOC -->

- [Associare il nome delle regioni ISTAT a dei punti demanio](#associare-il-nome-delle-regioni-istat-a-dei-punti-demanio)
  - [Dataset](#dataset)
  - [Procedimento](#procedimento)
  - [Query spaziale](#query-spaziale)
  - [Mapshaper](#mapshaper)
    - [Installare mapshaper](#installare-mapshaper)
  - [Cosa fa questa ricetta](#cosa-fa-questa-ricetta)

<!-- /TOC -->
# Associare il nome delle regioni ISTAT a dei punti demanio

- autore: _Totò Fiandaca_

---

## Dataset

* [01_demanio.csv](https://gist.github.com/aborruso/503df6c6477c341431e23bc51bc37149/raw/7aac29415b99512758acffd05fa463081f011484/01_demanio.csv)
* [regioni.shp](https://www4.istat.it/it/archivio/209722)

## Procedimento

Dopo aver scaricato i due dataset occorre convertirli in shapefile oppure importarli in un database sqlite (con estensione spaziale), verificare che I DUE STRATI abbiano stesso EPSG (sistema di riferimento delle coordinate)

## Query spaziale

```SQL
CREATE TABLE opendemanio_3857_reg AS
SELECT a.*, r.DEN_REG
FROM opendemanio_3857 a, regioni_3857 r
WHERE ST_Intersects(a.geometry,r.geometry)
AND a.rowid IN (SELECT rowid 
			FROM SpatialIndex 
			WHERE f_table_name = 'opendemanio_3857' AND search_frame = r.geometry);
```

## Mapshaper

```
mapshaper opendemanio_3857.shp -join regioni_3857.shp fields=COD_REG,DEN_REG -o opendemanio_v01.csv
```

### Installare mapshaper

```
## per installarlo

sudo npm install -g mapshapersudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
sudo npm install -g mapshaper

## per aggiornarlo:

sudo npm update -g mapshaper
```

## Cosa fa questa ricetta

Associa il nome delle regioni italiane ISTAT ai punti (demanio) che vi ricadono dentro; la query spaziale si puo' usare sia in [`spatialite_gui`](http://www.gaia-gis.it/gaia-sins/windows-bin-NEXTGEN-amd64/) che nella riga di comando, mentre la ricetta di [`mapshaper`](https://github.com/mbloch/mapshaper/wiki/Command-Reference) solo da riga di comando.

