# Estrarre dei punti di interesse da OpenStreetMap con Overpass turbo

- PR correlata: [#35](https://github.com/opendatasicilia/tansignari/pull/35) 
- autore: [Gabriele Francescotto](https://github.com/gabrielefrancescotto)

**[Overpass turbo](https://overpass-turbo.eu/)** è uno strumento web-based per l'estrazione di dati OpenStreetMap.

Utilizzando overpass turbo puoi eseguire query per Overpass API e analizzare dati [OpenStreetMap](https://www.openstreetmap.org/) su mappa in maniera interattiva. È disponibile la procedura guidata che rende estremamente semplice creare una richiesta.

Qui sotto trovi un esempio pratico di utilizzo.

## Esempio: come estrarre i punti di interesse presenti nel Comune di Palermo

**Tip**: come è fatto un punto di interesse?
la definizione in RDF è presente su **OntoPiA**: [Punti di interesse - POI](https://github.com/italia/daf-ontologie-vocabolari-controllati/tree/master/Ontologie/POI)
La classificazione dei punti di interesse di OntoPiA coincide con quella di OpenStreetMap

### Estrarre i POI da OSM

* Apri: https://overpass-turbo.eu/
* Incolla il codice sottostante nell'area di input
* Premi il pulsante "Esegui"


CODICE

```
// specificare il formato di output (CSV o JSON), quindi formulare la query

[out:csv(::id,::lat,::lon, "name",aerialway,aeroway,amnity,barrier,building,geological,highway,historic,leisure,man_made,natural,office,public_transport,railway,sport,tourism,"addr:housenumber","addr:street","addr:postcode","addr:city","contact:email","contact:fax","contact:phone","website","wikipedia","wikidata";true)];

// specifica l'area in cui effettuare la ricerca
{{geocodeArea:Palermo}}->.searchArea;

// specifica le tipologie di luogo

(

        way[aerialway][name](area.searchArea);
        way[aeroway][name](area.searchArea);
        way[amnity][name](area.searchArea);
        way[barrier][name](area.searchArea);
        way[building][name](area.searchArea);
        way[geological][name](area.searchArea);
        //way[highway][name](area.searchArea);
        way[historic][name](area.searchArea);
        way[leisure][name](area.searchArea);
        way[man_made][name](area.searchArea);
        way[natural][name](area.searchArea);
        way[office][name](area.searchArea);
        way[public_transport][name](area.searchArea);
        //way[railway][name](area.searchArea);
        way[sport][name](area.searchArea);
        way[tourism][name](area.searchArea);

);

// stampa i risultati
out body center;
>;
out skel qt;

```


## Esempio: come estrarre i punti geografici delle caserme di Palermo

Da una domanda [di Ciro Spataro](https://github.com/opendatasicilia/tansignari/issues/178).

La prima domanda è: come si etichetta (tagga) una <caserma>?

Sul web openstreetmap cercando il tag <caserma> militare, ottieni tra le pagine questa: [https://wiki.openstreetmap.org/wiki/Template:IT:Map_Features:military](https://wiki.openstreetmap.org/wiki/Template:IT:Map_Features:military).

In OverPass un tag di riferimento è <barracks>.

![](https://user-images.githubusercontent.com/30607/112823165-39d34b00-9089-11eb-82b4-55302a5fcf69.png)


**La prima modalità, per iniziare è questa**:

- apri [https://overpass-turbo.eu/](https://overpass-turbo.eu/)
- zoommi su Palermo
- fai click su Wizard, nel pop-up inserisci barracks e poi lanci la query

![](https://user-images.githubusercontent.com/30607/112823515-ae0dee80-9089-11eb-8f2c-03a4a9bd59bf.png)

in mappa avrai qualcosa come:

![](https://user-images.githubusercontent.com/30607/112823571-c0882800-9089-11eb-9579-f65395cd73a7.png)

e potrai esportare in vari formati:

![](https://user-images.githubusercontent.com/30607/112823667-ddbcf680-9089-11eb-8e3b-f1d6139c44ef.png)

Questo è solo per iniziare.

<Ricetta fornita da Andrea Borruso>





