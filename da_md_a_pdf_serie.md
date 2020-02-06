# Convertire molti file markdown in PDF -- in costruzione

- issue correlata: [#93](https://github.com/opendatasicilia/tansignari/issues/93)
- autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_; fornitore della ricetta: *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*;
- ingredienti: [Visual Studio Code](https://code.visualstudio.com/), [Pandoc](https://pandoc.org/)
  
---
<!-- TOC -->

- [Convertire molti file markdown in PDF -- in costruzione](#convertire-molti-file-markdown-in-pdf----in-costruzione)
  - [Usando Pandoc](#usando-pandoc)
    - [installazione](#installazione)
  - [Usando VS Code e estensioni](#usando-vs-code-e-estensioni)

<!-- /TOC -->

---

Cartella con molti file markdown da convertirli in PDF.

## Usando Pandoc

[Pandoc](https://pandoc.org/) è convertitore universale di documenti, un tool da riga di comando.

### installazione

1. creare una cartella temporanea sul desktop;
2. avvia Bash dalla cartella;
3. lanciare questo comando `wget https://github.com/jgm/pandoc/releases/download/2.7.3/pandoc-2.7.3-1-amd64.deb`;
4. scaricherà il file `pandoc-2.7.3-1-amd64.deb`;
5. poi, lanciare il comando: `sudo dpkg -i pandoc-2.7.3-1-amd64.deb` che installerà Pandoc;
6. controllo versione, lanciare il comando `pandoc --version`
7. lanciare il comando `sudo apt-get install texlive-xetex` per installare `--pdf-engine`


---

## Usando VS Code e estensioni

corpo ricetta 

per le immagini creare una cartella all'interno della cartella `img`
