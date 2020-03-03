# Come scrivere una ricetta

- issue correlata: [#120](https://github.com/opendatasicilia/tansignari/issues/120)
- autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_; fornitore della ricetta: *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*;
- ingredienti: [Visual Studio Code](https://code.visualstudio.com/)
  
---

<!-- TOC -->

- [Come scrivere una ricetta](#come-scrivere-una-ricetta)
  - [Introduzione](#introduzione)
  - [Corpo ricetta](#corpo-ricetta)
    - [le fasi da rispettare sono:](#le-fasi-da-rispettare-sono)
    - [file `index.md`](#file-indexmd)
      - [elementi del front matter del file index.md](#elementi-del-front-matter-del-file-indexmd)
    - [file `_index.md`](#file-indexmd-1)
      - [elementi del front matter file _index.md](#elementi-del-front-matter-file-indexmd)

<!-- /TOC -->

---

## Introduzione

In questa nuova piattaforma `Docsy` la redazione e pubblicazione di una ricetta viene fatta usando solo il linguaggio `Markdown` semplificando notevolemente i vari processi.

## Corpo ricetta

Le nuove ricette vanno aggiunte in `content/it/ricette` che contiene tante cartelle quante sono le categorie di ricette (`Mappe`, `Bash`, `Utilities`, ecc..);

### le fasi da rispettare sono:

- in presenza di categoria:
  - se nella ricetta fossero previste immagini è obbligatorio creare una **_cartella_**  (`content/it/ricette/nuova-cartella`) con nome simile al titolo della ricetta, all'interno mettere tutte le immagini e il file `index.md` che rappresenta la vera ricetta scritta in `markdown`;
  - l'indice interno della ricetta è creata in automatico dal sistema qualora si utilizzassero i livelli (`#` primo livello; `##` secondo livello, ecc...);
  - se la ricetta non prevedesse immagini non occorre creare cartelle, basta il solo file `nome-ricetta.md` scritto sempre in `markdown`;
- in assenza di categoria:
  - va creata una **_cartella_** per ogni nuova categoria di ricette (`Mappe`, `Bash`, `Utilities`, ecc..), all'interno va creato in file `_index.md`;

### file `index.md`

Ogni cartella rappresenta una nuova ricetta, all'interno troveremo le immagini e un file `index.md` che contiene la descrizione della ricetta. Ogni nuovo file `index.md` deve iniziare con il `front matter`:

```
---
title: "Come usare la matrice del pendolarismo ISTAT 2011"
linkTitle: "Come usare la matrice del pendolarismo ISTAT 2011"
date: 2020-03-03
description: >
  Come usare la matrice del pendolarismo ISTAT 2011.
tags:
  - csv
  - tsv
  - csv-tsv
  - miller
  - visidata
  - sqlite
issue: [105]
autori: ["Totò Fiandaca"]
chefs: ["Andrea Borruso"]
---
riga vuota
---
riga vuota
```

subito sotto, il corpo della ricetta (vedi template).

#### elementi del front matter del file index.md

- `title:` il titolo della ricetta tra doppi apici "";
- `linkTitle:` quello che compare nel menu a destra del `Docsy`, quindi puo' essere uguale al titolo, meglio se più corto.
- `date:` data nel formato `YYYY-mm-dd` della ricetta;
- `description: >` descrizione della ricetta, utile per semplificare il titolo della stessa;
- `tags:` parolo chiavi utilizzate nella ricetta, una sotto l'altra;
- `issue:` numero della issue di riferimento, scritte dentro parentesi quadre e separate da virgola [1,2];
- `autori:` autore della ricetta, scritte dentro parentesi quadre e separate da virgola ["a","b"];
- `chefs:` fornitore della ricetta, scritte dentro parentesi quadre e separate da virgola ["c","d"]

### file `_index.md`

Ogni cartella che rappresenta una categoria deve contenere, oltre tutte le altre cartelle/ricette, il file `_index.md`, questo file inizia con il `front matter`:

```
---
title: "Nome cartella categoria"
linkTitle: "Nome cartella categoria"
weight: 11
description: >
  Una descrizione della categoria. [Fonte](https://it.wikipedia.org/wiki/xxxx)
---
riga vuota
```

Elenco Ricette

(verranno aggiunte automaticamente le ricette della categoria)

#### elementi del front matter file _index.md

- `title:` il titolo della categoria "";
- `linkTitle:` quello che compare nel menu a destra del `Docsy`, quindi puo' essere uguale al titolo, meglio se più corto.
- `weight:` è un numero che rappesenta il peso della categoria, più è altro è piì si trova in basso nell'elenco complessivo;
- `description: >` descrizione della categoria, utile per semplificare il titolo della categoria;