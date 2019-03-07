# OpenRefine Geocoding con Nominatim

Una semplice ricetta per estrarre Latitudine e longitudine dai tuoi dati utilizzando il servizio di Nominatim (evitando GoogleMaps). Tale ricetta non è farina del mio sacco, ma frutto della mente geniale di Andrea Borruso.

- Apri OpenRefine e carica i tuoi dati tabellari
- Rinomina la colonna contenente le informazioni geografiche (indirizzo, luogo, etc.) come '2geocode'
- Clicca su Undo/Redo
- quindi Clicca Apply

Incolla questo codice nella finestra che si è aperta

```json
[
{
"op": "core/column-addition-by-fetching-urls",
"description": "Create column geocode_results at index 2 by fetching URLs based on column 2geocode using expression grel:\"https://nominatim.openstreetmap.org/search?format=json&email=tuoindirizzo@gmail.com&app=google-refine&addressdetails=1&q=\" + escape(value, 'url')",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "geocode_results",
"columnInsertIndex": 2,
"baseColumnName": "2geocode",
"urlExpression": "grel:\"https://nominatim.openstreetmap.org/search?format=json&email=tuoindirizzo@gmail.com&app=google-refine&addressdetails=1&q=\" + escape(value, 'url')",
"onError": "set-to-blank",
"delay": 1000
},
{
"op": "core/column-addition",
"description": "Create column latitude at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"lat\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "latitude",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"lat\"]",
"onError": "set-to-blank"
},
{
"op": "core/column-addition",
"description": "Create column longitude at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"lon\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "longitude",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"lon\"]",
"onError": "set-to-blank"
},
{
"op": "core/column-addition",
"description": "Create column osm_type at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"osm_type\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "osm_type",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"osm_type\"]",
"onError": "set-to-blank"
},
{
"op": "core/column-addition",
"description": "Create column importance at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"importance\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "importance",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"importance\"]",
"onError": "set-to-blank"
},
{
"op": "core/column-addition",
"description": "Create column class at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"class\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "class",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"class\"]",
"onError": "set-to-blank"
},
{
"op": "core/column-addition",
"description": "Create column type at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"type\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "type",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"type\"]",
"onError": "set-to-blank"
},
{
"op": "core/column-addition",
"description": "Create column display_name at index 3 based on column geocode_results using expression grel:value.parseJson()[0][\"display_name\"]",
"engineConfig": {
"facets": [],
"mode": "row-based"
},
"newColumnName": "display_name",
"columnInsertIndex": 3,
"baseColumnName": "geocode_results",
"expression": "grel:value.parseJson()[0][\"display_name\"]",
"onError": "set-to-blank"
}
]
```

- lancia 'perform operations'

Fine
