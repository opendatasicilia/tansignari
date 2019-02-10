# Ottenere i dati geografici di latitudine e longitudine dall'indirizzo.

Se si ha un file tabellare con in un colonna l'indirizzo è possibile ottenere i dati di latitudine e longitudine sfruttando un API di Openstreetmap denominata: **Nominatim**.

Di seguito la sintassi che deve essere editata su una cella, in cui A2 è la cella in cui si trova l'indirizzo:

```=JOIN(",", ImportXML(CONCATENATE("http://nominatim.openstreetmap.org/search/?format=xml&q=",A2), "//place[1]/@lat | //place[1]/@lon"))```

