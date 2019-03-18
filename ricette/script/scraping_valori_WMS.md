# Scraping valori da un servizio WMS

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* issue: [#44](https://github.com/opendatasicilia/tansignari/issues/44) fornitore ricetta _[Andrea Borruso](https://twitter.com/aborruso?lang=it)_

---

Dato un servizio [WMS](http://www.pcn.minambiente.it/mattm/servizio-wms/) (DTM 20 m) e una serie di punti (x,y), come realizzare il _draping_ dei punti sul DTM, cioè come ottenere la quota dei punti (x,y,elev) sul DTM.

## script bash

```bash
#!/bin/bash
gdallocationinfo "http://wms.pcn.minambiente.it/ogc?map=/ms_ogc/WMS_v1.3/raster/DTM_20M.map&SERVICE=WMS&VERSION=1.1.1&REQUEST=GetMap&LAYERS=EL.DTM.20M&SRS=EPSG:4326&BBOX=6.5,35.3,18.6,47.1" -xml -geoloc 13 38  -b 1  | scrape -e '//value_0/text()'
```

questo script `gratta` la quota del punto di coordinate (13 38) → 181

per ottenere le elevazioni su una serie di punti occorre realizzare un loop:

```bash
IFS=$'\n';
for LINE in $(cat point.tsv); do
    VARA=$(echo ${LINE} | awk '{ print $1}')
    VARB=$(echo ${LINE} | awk '{ print $2 }')
gdallocationinfo "http://wms.pcn.minambiente.it/ogc?map=/ms_ogc/WMS_v1.3/raster/DTM_20M.map&SERVICE=WMS&VERSION=1.1.1&REQUEST=GetMap&LAYERS=EL.DTM.20M&SRS=EPSG:4326&BBOX=6.5,35.3,18.6,47.1" -xml -geoloc ${VARA} ${VARB}  -b 1  | scrape -e '//value_0/text()' >> output.csv
done
paste point.tsv toto.csv > punti_quotati.tsv
rm ./output.csv
```

**NB:** il file dei punti (point.tsv) non deve avere intestazione e deve contenere solo le coordinate x e y con separatore `tab`; alla fine dello script otterremo un file (punti_quotati.tsv) con `x` `y` `elev` ma senza intestazione.

lon|lat|elev
--|--|--
14.77560|37.819703|713
15.04366|37.772526|1957
14.58021|37.608423|269
14.52765|37.876929|1265
14.47786|37.830808|1005
