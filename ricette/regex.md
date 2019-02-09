# Introduzione

Qui le ricette a tema Espressioni Regolari, che verranno fuori dalle issue di progetto

## selezionare righe con spazio iniziale

* `^( )(.+)` - solo uno spazio iniziale; [test](https://regex101.com/r/Qn4BTb/1)
* `^( +)(.+)` - uno o più spazi iniziali; [test](https://regex101.com/r/Qn4BTb/2)

### sostituzione

* `$2` - sostituisce l'intera riga senza spazi iniziali

## selezionare righe con spazio finale

* `(.+)( )$` - solo uno spazio finali; [test](https://regex101.com/r/Qn4BTb/3)
* `(.+?)( +)$` - uno o più spazi finali; [test](https://regex101.com/r/Qn4BTb/4)

### sostituzione

* `$1` - sostituisce l'intera riga senza spazi finali