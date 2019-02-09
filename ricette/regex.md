# Introduzione

Qui le ricette a tema Espressioni Regolari, che verranno fuori dalle issue di progetto

piccola guida alle [regex](https://www.evemilano.com/come-funzionano-le-espressioni-regolari-regex/)

## selezionare righe con spazio iniziale issue [#1](https://github.com/opendatasicilia/tansignari/issues/1)

* `^( )(.+)` - solo uno spazio iniziale; [test](https://regex101.com/r/Qn4BTb/1)
* `^( +)(.+)` - uno o più spazi iniziali; [test](https://regex101.com/r/Qn4BTb/2)

### sostituzione

* `$2` - sostituisce l'intera riga senza spazi iniziali

## selezionare righe con spazio finale issue [#2](https://github.com/opendatasicilia/tansignari/issues/2)

* `(.+)( )$` - solo uno spazio finali; [test](https://regex101.com/r/Qn4BTb/3)
* `(.+?)( +)$` - uno o più spazi finali; [test](https://regex101.com/r/Qn4BTb/4)

### sostituzione

* `$1` - sostituisce l'intera riga senza spazi finali