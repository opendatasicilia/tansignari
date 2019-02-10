# Ottenere i dati geografici di latitudine e longitudine dall'indirizzo.

Se si ha un file tabellare con in un colonna l'indirizzo è possibile ottenere i dati di latitudine e longitudine sfruttando un API di Openstreetmap denominata **Nominatim**

=JOIN(",", ImportXML(CONCATENATE("http://nominatim.openstreetmap.org/search/?format=xml&q=",A2), "//place[1]/@lat | //place[1]/@lon"))
