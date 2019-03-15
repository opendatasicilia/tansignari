# Reverse Geocoding con Two-way Geocoding

- issue correlata: [#36](https://github.com/opendatasicilia/tansignari/issues/36)
- autore: [Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)

Usare i fogli di Google Drive e installare il componente aggiuntivo **Two-way Geocoding**.

Questo componente permette di fare un geocoding in entrambi i sensi: da indirizzo a coordinate, da coordinate a indirizzo che è il nostro caso.

dopo aver installato il componente:
![image](https://user-images.githubusercontent.com/7631137/54376996-90c57d80-4684-11e9-83b8-4c289efda745.png)
occorre settare, per il foglio, le impostazioni internazionali del Regno Unito (File –> impostazioni).

Crea un nuovo foglio:
![image](https://user-images.githubusercontent.com/7631137/54377229-09c4d500-4685-11e9-8a09-838056f80b8a.png)
in modo da ottenere questa impostazione dello sheet, usando il menu componenti aggiuntivi → Two-way Geocoding → Create new sheet

a questo punto non ti resta che popolare i campi delle coordinate (LATITUDE e LONGITUDE), potresti anche popolare gli altri campi NAME e DESCRIPTION.

Successivamente, ritorna nel menu `Componenti Aggiuntivi` e seleziona `Geocode → Coordinates`
![image](https://user-images.githubusercontent.com/7631137/54380403-9ffbf980-468b-11e9-8d5e-de4cde60fb9f.png).

Dopo qualche secondo verrà popolato il campo `ADDRESS` in questo formato:

ADDRESS|LATITUDE|LONGITUDE
----|-------|-----
Piazza del Parlamento, 1, 90129 Palermo PA, Italy|38.112213|13.352615
Foro Umberto I, 11, 90133 Palermo PA, Italy|38.119753|13.371337
Via Dell' Arsenale, 148, 90142 Palermo PA, Italy|38.135400|13.369116

**OSSERVAZIONI**
Con i dati cosi ottenuti puoi farci poco, leggi qui: https://goo.gl/6hYJh7
in particolare:
`
You can display Geocoding API results on a Google Map, or without a map. If you want to display Geocoding API results on a map, then these results must be displayed on a Google Map. It is prohibited to use Geocoding API data on a map that is not a Google map.
`

Blog post su [Pigrecoinfinito](https://pigrecoinfinito.wordpress.com/2019/03/14/two-way-geocoding-con-gdrive-spreadsheet/)