# Capoluoghi di provincia italiani

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_
* issue: [#64](https://github.com/opendatasicilia/tansignari/issues/64) fornitore ricetta *[Andrea Borruso](https://twitter.com/aborruso?lang=it)* e *[Davide Taibi](https://twitter.com/dataibi?lang=it)*
* ingredienti: [geonames](http://www.geonames.org/), [wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page),[SPARQL](https://it.wikipedia.org/wiki/SPARQL), [Miller](https://github.com/johnkerl/miller)

---

<!-- TOC -->

- [Capoluoghi di provincia italiani](#capoluoghi-di-provincia-italiani)
  - [geonames](#geonames)
  - [wikidata](#wikidata)
  - [Chi ha cucinato questa ricetta o ne ha tratto ispirazione](#chi-ha-cucinato-questa-ricetta-o-ne-ha-tratto-ispirazione)

<!-- /TOC -->

---

**Caso d'uso:** Creare un dataset che rappresenti i Capoluoghi di provincia italiani in forma puntuale

## geonames

**geonames** fornisce molti dati in forma tabellare (senza intestazione e ciò rende più difficile la lettura), una possibile soluzione è filtrare la tabella usando feature code `PPLA2`, `PPA` e `PPLC` (per maggiori dettagli leggere issue #64) e usare questo script Miller (110 record):

```
mlr --n2c --ifs "\t"  filter -S '$8=="PPLA2"||$8=="PPLA"||$8=="PPLC"' IT.txt  >provinceIT2.csv
```

dove **IT.txt** è scaricabile da [qui](http://download.geonames.org/export/dump/)

## wikidata

Le suddivisioni amministrative in Italia sono complesse: qui una [query](https://bit.ly/2Dzqza6) SPARQL (106 record):

```SQL
SELECT ?UA ?UALabel ?tipoLabel ?istatIDUA ?capoluogo ?capoluogoLabel ?istatIDCapoluogo ?coordinate ?GeoNamesIDCapoluogo WHERE {
  {
# le "suddivisioni amministrative generiche". In wikidata c'è la provincia del Sud Sardegne
    ?UA wdt:P31 wd:Q56061.
    ?UA wdt:P17 wd:Q38.
    ?UA wdt:P635 ?istatIDUA.
    ?UA p:P31 ?statement.
    ?UA wdt:P31 ?tipo.
    OPTIONAL { ?UA wdt:P36 ?capoluogo.}
    OPTIONAL { ?capoluogo p:P625 ?pc .}
    OPTIONAL { ?pc ps:P625 ?coordinate .}
    OPTIONAL { ?capoluogo p:P1566 ?pg.}
    OPTIONAL { ?pg ps:P1566 ?GeoNamesIDCapoluogo.}
    OPTIONAL { ?capoluogo p:P635 ?pi.}
    OPTIONAL { ?pi ps:P635 ?istatIDCapoluogo.}
    FILTER(REGEX(STR(?istatIDUA), "^[0-9]{3}$"))
        SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],it". }
  } UNION {
# le "province di Italia"
    ?UA wdt:P31 wd:Q15089.
    ?UA wdt:P635 ?istatIDUA.
    ?UA p:P31 ?statement.
    ?UA wdt:P31 ?tipo.
    OPTIONAL { ?UA wdt:P36 ?capoluogo.}
    OPTIONAL { ?capoluogo p:P625 ?pc .}
    OPTIONAL { ?pc ps:P625 ?coordinate .}
    OPTIONAL { ?capoluogo p:P1566 ?pg.}
    OPTIONAL { ?pg ps:P1566 ?GeoNamesIDCapoluogo.}
    OPTIONAL { ?capoluogo p:P635 ?pi.}
    OPTIONAL { ?pi ps:P635 ?istatIDCapoluogo.}
    FILTER(REGEX(STR(?istatIDUA), "^[0-9]{3}$"))
    SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],it". }
  }
  UNION {
# le "città metropolitane"
    ?UA wdt:P31 wd:Q15110.
    ?UA p:P31 ?statement.
    ?UA wdt:P31 ?tipo.
    ?UA p:P635 ?p.
    ?p ps:P635 ?istatIDUA .
    OPTIONAL { ?UA wdt:P36 ?capoluogo.}
    OPTIONAL { ?capoluogo p:P625 ?pc .}
    OPTIONAL { ?pc ps:P625 ?coordinate .}
    OPTIONAL { ?capoluogo p:P1566 ?pg.}
    OPTIONAL { ?pg ps:P1566 ?GeoNamesIDCapoluogo.}
    OPTIONAL { ?capoluogo p:P635 ?pi.}
    OPTIONAL { ?pi ps:P635 ?istatIDCapoluogo.}
    SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],it". }
  }
  FILTER NOT EXISTS { ?statement pq:P582 ?x }
}

order by ?istatIDUA
```
---

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- "[CAPOLUOGHI DI PROVINCIA ITALIANI ISTAT](https://pigrecoinfinito.wordpress.com/2019/04/25/capoluoghi-di-provincia-italiani-istat/)", di Salvatore Fiandaca;