# come fare leggere un file in formato .MD a ReadtheDocs

* autore: _[Ciro Spataro](https://twitter.com/cirospat)_
* issue: [#106](https://github.com/opendatasicilia/tansignari/issues/106) fornitore ricetta _[Andrea Borruso](https://twitter.com/aborruso?lang=it)_

---

## Problema

Se voglio far leggere un file .MD, oltre ai file .RTS, a ReadtheDocs quali impostazioni devo settare e dove li devo settare?

## Soluzione

Bisogna guardare questi due file:

- requirements con i requisiti di moduli da installare, vedi ad esempio: https://github.com/opendatasicilia/tansignari/blob/master/requirements.txt

- `conf.py`, il file di configurazione, in cui in queste linee si imposta la configurazione che abilita il markdown:
