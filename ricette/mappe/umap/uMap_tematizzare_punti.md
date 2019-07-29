# uMap - Tematizzare i punti

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue:

Abbiamo già visto come tematizzare [velocemente i poligoni](http://tansignari.opendatasicilia.it/it/latest/ricette/mappe/umap/uMap.html), ma possiamo fare la stessa cosa con una mappa puntuale?

Prendendo spunto dalla domanda posta da [Piersoft](https://twitter.com/Piersoft) su [facebook](https://www.facebook.com/piersoft/posts/10214546139942792)

![](/img/uMap/piersoft_facebook.png)

ho fatto un qualche prova veloce, utilizzando sempre il famoso campo  **_umap_options**

## Tematizzare un punto 
Usando il campo  **_umap_options** possiamo usare il seguente codice:

```
{ "color": "Blue", "iconClass": "Default", "iconUrl": "http:\/\/gbvitrano.it\/clip\/umap\/accessible_beach_white.png" }
```
I **valori** sono a titolo di esempio e vanno adattati alle proprie esigenze.

- **color** = colore di riempimento
- **iconClass** = forma dell'icona
- **iconUrl** = indirizzo dell'immagine da mostrare nell'icona

- **iconClass": "Default"**  per l'icona classica quadrata
- **"iconClass": "Drop"** per l'icona a goccia

Ma [Piersoft](https://twitter.com/Piersoft) cerca come prima opzione di usare il testo di un campo del suo db, in questo caso basta sostituire **iconUrl** invece di far caricare un'immagine interna o esterna ad [Umap](http://umap.openstreetmap.fr/it/) facciamo caricare un campo del db

```
{ "color": "Blue", "iconClass": "Drop", "iconUrl": "{id}" }
```
dove il campo **{id}** delnostro db sostituisce **url**

