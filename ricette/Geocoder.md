# Ottenere i dati geografici di latitudine e longitudine dall'indirizzo.

Se si ha un file tabellare con in un colonna l'indirizzo è possibile ottenere i dati di latitudine e longitudine sfruttando un API di Openstreetmap denominata: **Nominatim**.

Di seguito la sintassi che deve essere editata su una cella, in cui A2 è la cella in cui si trova l'indirizzo:

```
=JOIN(",", ImportXML(CONCATENATE("http://nominatim.openstreetmap.org/search/?format=xml&q=",A2), "//place[1]/@lat | //place[1]/@lon"))
```

L'API di Openstreetmap permette di utilizzare i dati di latitudine e longitudine così trovati per qualsiasi riuso.

---


## Sfruttare componenti aggiuntivi dei fogli Google spreadsheet per ottenere dati geografici da indirizzi.

Se si usa un foglio Google spreadsheet è possibile installare un componente aggiuntivo denominato "**Geocode by Awesome Table**".
Tale componente aggiuntivo, una volta avviato sul foglio Google in uso, creerà in colonne accanto a quella dell'indirizzo, in automatico i dati di latitudine e longitudine.
E' importante sapere che i dati geografici così ottenuti, per le policy di Google, possono essere utilizzati solo nelle mappe di Google e non, ad esempio in uMap.
