# Come scrivere una ricetta -- in costruzione

- issue correlata: [#120](https://github.com/opendatasicilia/tansignari/issues/120)
- autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_; fornitore della ricetta: *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*;
- ingredienti: [Visual Studio Code](https://code.visualstudio.com/)
  
---

<!-- TOC -->

- [Come scrivere una ricetta -- in costruzione](#come-scrivere-una-ricetta----in-costruzione)
  - [Introduzione](#introduzione)
  - [Corpo ricetta](#corpo-ricetta)
    - [le fasi da rispettare sono:](#le-fasi-da-rispettare-sono)
    - [file `index.md`](#file-indexmd)
    - [file `_index.md`](#file-indexmd-1)

<!-- /TOC -->

---

## Introduzione

In questa nuova piattaforma la redazione e pubblicazione di una ricetta viene fatta usando solo il linguaggio Markdown e quindi risulta particolarmente semplice e veloce.

## Corpo ricetta

Le nuove ricette vanno aggiunte in `content/it/ricette` che contiene tante cartelle quante sono le categorie di ricette (`Mappe`, `Bash`, `Utilities`, ecc..);

### le fasi da rispettare sono:

- se la categoria esistesse allora:
  - se nella ricetta fossero previste immagini è obbligatorio creare una **_cartella_**  (`content/it/ricette/nuova-cartella`) con nome simile al titolo della ricetta, all'interno mettere tutte le immagini e il file `index.md` che rappresenta la vera ricetta scritta in `markdown`;
  - l'indice interno della ricetta è creata in automatico dal sistema qualora si utilizzassero i livelli con i #;
  - se la ricetta non prevedesse immagini non occorre creare cartelle, basta il solo file `nome-ricetta.md` scritto sempre in `markdown`;
- se la categoria non esistesse allora:
  - va creata una **_cartella_** per ogni nuova categoria di ricette (`Mappe`, `Bash`, `Utilities`, ecc..), all'interno va creato in file `_index.md`;

### file `index.md`

Ogni cartella rappresenta una nuova ricetta, all'interno troveremo le immagini e un file `index.md` che contiene la descrizione della ricetta. Ogni nuovo file `index.md` deve iniziare con:

```
---
title: "nome descrittivo ricetta - lungo"
linkTitle: "nome descrittivo ricetta - breve"
date: 2019-01-05
description: >
  Descrizione della ricetta.
---
```

subito sotto il corpo della ricetta.

### file `_index.md`

Ogni cartella che rappresenta una categoria deve contenere, oltre tutte le altre cartelle/ricette, il file `_index.md`, questo file inizia con:

```
---
title: "Nome cartella categoria"
linkTitle: "Nome cartella categoria"
weight: 11
description: >
  Una descrizione della categoria. [Fonte](https://it.wikipedia.org/wiki/xxxx)
---
```

Elenco Ricette

