# Reverse Geocoding usando la riga di comando

- issue correlata: [#38](https://github.com/opendatasicilia/tansignari/issues/38) [#39](https://github.com/opendatasicilia/tansignari/issues/39) [#42](https://github.com/opendatasicilia/tansignari/issues/42)
- autore: [Totò Fiandaca](https://twitter.com/totofiandaca?lang=it) e script di [Andrea Borruso](https://twitter.com/aborruso?lang=it)

---

![logo](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Openstreetmap_logo.svg/150px-Openstreetmap_logo.svg.png) Usando [Nominatim](https://wiki.openstreetmap.org/wiki/Nominatim), ricavare **l'indirizzo** partendo da coppie di coordinate **lat lon** e usando la riga di comando (CLI).

File CSV coordinate cosi strutturato, `lat` prima colonna, `lon` seconda colonna e senza intestazione:

```csv
38.11744375,13.3627383
38.11941245,13.3618317
38.12941165,13.3621113
...
```

Lanciare questo script BASH dalla stessa cartella dove è presente il file CSV

```bash
#!/bin/bash
sed -i -r 's/^(.*),(.*)$/lat=\1\&lon=\2/g' lat_lon_coordinates.csv
for i in $(cat lat_lon_coordinates.csv); do
curl -L "http://nominatim.openstreetmap.org/reverse.php?format=json&"$i"&addressdetails=1"| jq -r '.|[.lat,.lon,.display_name]|@csv' >> reverse_geo.csv
done
```

Il risultato sarà un nuovo file CSV (_reverse_geo.csv_) cosi strutturato:

```csv
"38.11744375","13.3627383","Teatro Biondo, 258, Via Roma, La Loggia, I Circoscrizione, Palermo, PA, SIC, 90133, Italia"
"38.11941245","13.3618317","Palazzo Credito Italiano, 314, Via Roma, La Loggia, I Circoscrizione, Palermo, PA, SIC, 90133, Italia"
"38.12941165","13.3621113","EXPOfficina, Via del Mare, La Loggia, Arenella, Palermo, PA, SIC, 90100, Italia"
```

con tre colonne: latitudine, longitudine e indirizzo.