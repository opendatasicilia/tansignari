# Da coppie di coordinate a linee

* autore: _[gbvitrano](https://twitter.com/gbvitano?lang=it)_
* issue: [#46](https://github.com/opendatasicilia/tansignari/issues/46) fornitore ricetta *[Andrea Borruso](https://twitter.com/aborruso?lang=it)* e _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* ingredienti: [SQLite](https://www.sqlite.org/index.html), [GDAL/OGR](https://www.gdal.org/ogr2ogr.html)

---

<!-- TOC -->

- [Da coppie di coordinate a linee](#da-coppie-di-coordinate-a-linee)
  - [script bash](#script-bash)
  - [Dati](#dati)
  - [Chi ha cucinato questa ricetta o ne ha tratto ispirazione](#chi-ha-cucinato-questa-ricetta-o-ne-ha-tratto-ispirazione)

<!-- /TOC -->

---

**Caso d'uso:** scrivere il caso -------

## script bash

```
ogr2ogr -f geojson -dialect sqlite -sql  \
"SELECT t.lineID, 
MakeLine(MakePoint(CAST(t.longitude AS float),CAST(t.latitude AS float),4326)) AS geom 
FROM (SELECT * FROM lineegb ORDER BY CAST(lineID AS integer), 
CAST(point AS integer)) t GROUP BY 1" lineCTgb_asc.geojson lineegb.csv
```

## Dati

il file CSV `lineegb.csv` è scaricabile da [qui](https://github.com/opendatasicilia/tansignari/files/3098483/lineegb.zip)


---

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- [DA COPPIE DI PUNTI A LINEE USANDO GDAL/OGR](https://pigrecoinfinito.wordpress.com/2019/04/20/da-coppie-di-punti-a-linee-usando-gdal-ogr/)
