# [uMap](http://umap.openstreetmap.fr/it/) - Tematizzare i poligoni

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue:
 
[uMap](http://umap.openstreetmap.fr/it/) è un software potentissimo per la creazione di mappe online, da inserire nel proprio sito, che fanno uso di [OpenStreetMap](http://osm.org/) come sfondo.
Il software è creato dall’italo-francese [Yohan Boniface](http://yohanboniface.me/), rilasciato in open source con la licenza “[do what the fuck you want to public license](https://github.com/yohanboniface/uMap)“, scritto in [django](https://www.djangoproject.com/) e [leaflet](http://leafletjs.com/), e reso disponibile sugli spazi di [OpenStreetMap France](http://www.openstreetmap.fr/) – http://umap.openstreetmap.fr. (cit. [da de.straba.us](http://de.straba.us/2015/05/22/tutorial-creare-una-mappa-online-con-fotografie-in-umap-aggiornabile-con-ethercalc/))

In questo breve tutorial non voglio spigare cosa è uMap e come funziona, questo è stato fatto benissimo da [@napo](https://twitter.com/napo) nel suo [blog de.straba.us](http://de.straba.us/2015/05/22/tutorial-creare-una-mappa-online-con-fotografie-in-umap-aggiornabile-con-ethercalc/), da [@piersoft](https://twitter.com/Piersoft) nel suo [blog](http://www.piersoft.it/da-un-csv-o-geojson-ad-una-mappa/) [(tutti gli articoli su uMap)](http://www.piersoft.it/?s=umap) e da [@cirospat](https://twitter.com/cirospat) nel suo [Tutorial per creare mappe online su UMAP aggiornabili con file CSV da GOOGLEDRIVE](https://coseerobe.gbvitrano.it/Tutorial%20per%20creare%20mappe%20online%20su%20UMAP%20aggiornabili%20con%20file%20CSV%20da%20GOOGLEDRIVE), ma  proverò a spiegare come tematizzare velocemente i poligoni che vengono importati in uMap da altri software GIS.

La cosa più semplice da fare è quella di esportare i poligoni tematizzati del nostro file in oggetto in  più file, ovvero, suddividiamo i poligoni del file originale in **n** file, tanti quanto sono i temi.

![](/img/uMap/qgis1.jpg)

Il file/layer Grado di Vulnerabilità sismica è tematizzato secondo una scala di vulnerabilità in 5 categorie (1) per riproporre velocemente la stessa tematizzazione in [uMap](http://umap.openstreetmap.fr/it/) basta salvare/esportare i poligoni di ogni categoria in un nuovo file.

![](/img/uMap/umap_02.jpg)

I file ottenuti dall’esportazione dei poligoni di ogni singola categoria, importati in [uMap](http://umap.openstreetmap.fr/it/)  (1)

![](/img/uMap/umap_03.jpg)

Dal pannello Shape propertis configuriamo le proprietà dei poligoni di tutto il layer, colore del riempimento, trasparenza, linea di contorno, etc

![](/img/uMap/umap_04.jpg)

Risultato finale, il file/layer originale, è stato suddivido in 5 nuovi file, ognuno dei quali può essere attivato o disattivato al bisogno.

**Ma se non voglio o non posso suddividere il file di base in tanti file…?**
**o se non voglio avere una colonna infinita di layer nel pannello delle informazioni di uMap…?**
*devo tematizzare singolarmente ogni poligono...?*

## Come tematizzare velocemente i poligoni
Studiando la struttura di [uMap](http://umap.openstreetmap.fr/it/) mi sono reso conto che [uMap](http://umap.openstreetmap.fr/it/) aggiunge una o più colonne al file viene importato, nello specifico per tematizzare i poligoni viene aggiunta la colonna _umap_options, (nella vecchia versione la colonna si chiamava _storage_options).

In questa colonna vengono scritte tutte le info che riguardano le proprietà del poligono, colore, trasparenza, spessore delle linee, ect… che tradotto in codice si scrive così:

```
{ "fillColor": "#b2b2b2", "color": "Black", "weight": "1", "opacity": "1", "fillOpacity": "0.75", "dashArray": "4" }
```

I **valori** sono a titolo di esempio e vanno adattati alle proprie esigenze.

- **fillColor** = colore di riempimento
- **color** = colore bordo
- **weight** = spessore bordo
- **opacity** = opacità bordo
- **fillOpacity** = opacità riempimento
- **dashArray** = tratteggio linea bordo, per ottenere la linea continua, basta omettere il comando

![](/img/uMap/qgis2.jpg)

Per aggiungere la nuova colonna ho utilizzato [QGIS](https://www.qgis.org/it/site/) , colonna _umap_options (1) per la nuova versione sel server uMap o la colonna _storage_options  (2) per la vecchia versione di uMap. Dopo aver aggiunto la nuova colonna non ci resta che importare il file su uMap ed i poligoni verranno tematizzati automaticamente secondo le nostre istruzioni.

Qui un esempio di mappa  [Vulnerabilità sismica degli edifici residenziali di Palermo](http://u.osmfr.org/m/129487/)

<a href="http://u.osmfr.org/m/129487/"><img  title="uMap - Tematizzare velocemente i poligoni - Vulnerabilità sismica degli edifici residenziali di Palermo " src="https://raw.githubusercontent.com/opendatasicilia/tansignari/master/img/uMap/umap.jpg" alt="uMap - Tematizzare velocemente i poligoni - Vulnerabilità sismica degli edifici residenziali di Palermo " width="auto" /></a>



