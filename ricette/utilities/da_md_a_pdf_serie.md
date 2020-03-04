# Convertire molti file markdown in PDF

- issue correlata: [#93](https://github.com/opendatasicilia/tansignari/issues/93)
- autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_; fornitore della ricetta: *[Andrea Borruso](https://twitter.com/aborruso?lang=it)*;
- ingredienti: [Visual Studio Code](https://code.visualstudio.com/), [Pandoc](https://pandoc.org/)
  
---
<!-- TOC -->

- [Convertire molti file markdown in PDF](#convertire-molti-file-markdown-in-pdf)
  - [Introduzione](#introduzione)
  - [Usando Pandoc](#usando-pandoc)
    - [Opzione 1](#opzione-1)
    - [Opzione 2](#opzione-2)
    - [Installare Pandoc](#installare-pandoc)
  - [Usando VS Code e estensioni](#usando-vs-code-e-estensioni)
  - [Riferimenti utili](#riferimenti-utili)

<!-- /TOC -->

---
## Introduzione

Utilizzando molto [GitHub](https://github.com/) è altrettanto frequente l'utilizzo del linguaggio [`markdowm`](https://it.wikipedia.org/wiki/Markdown) (`md`), un linguaggio semplice da usare che permette la formattazione del testo in brevissimo tempo. Alcune volte nasce l'esigenza di convertire molti file `*.md` in `PDF`: esistono varie estensioni (sono stati testati alcuni in [VS code](https://code.visualstudio.com/) oppure facendo uso della riga di comando in _bash_ (usando `Pandoc`) con passaggio intermedio, cioè creazione di file `odt` ([Libre Office Writer](https://it.wikipedia.org/wiki/LibreOffice_Writer)).

## Usando Pandoc

[Pandoc](https://pandoc.org/) è convertitore universale di documenti, un tool da riga di comando.

### Opzione 1

Il tool da utilizzare è **pandoc** (nel caso è da installare). È a riga di comando, open source e disponibile per tutti i sistemi operativi.

Il comando è:

```
pandoc -o output.odt --reference-doc=myPandocTemplate.odt input.md
```

A partire da un file `Markdown` di input, e da un file `odt` che viene usato come modello per lo stile, viene generato un file di output (sempre `odt`) che tiene conto degli stili del modello (intestazioni, corpo testo, larghezza pagina, header, ecc.).

Il file template è un file `odt` a cui assegnare/modificare gli stili che si vogliono utilizzare: se ne crea uno nuovo, con `F11` si apre il pannello degli stili, si modificano/aggiungono e si salva il file.

**Nota bene 1**: se si vuole che le immagini presenti del file `Markdown` si adattino alla larghezza della pagina del file `odt`, bisogna impostarla al 100% (ad esempio `![](./imgs/4116_1.png){ width=100% }`).

**Nota bene 2**: è sempre bene avere installato una versione recente di `pandoc`.

### Opzione 2

Nella modalità soprastante, è necessario "sporcare" un po' il file `Markdown`, aggiungendo il parametro sulla larghezza. Inoltre c'è da ricordarsi di farlo per ogni immagine.

`pandoc` consente la [manipolazione](https://pandoc.org/lua-filters.html) dei documenti tramite il linguaggio [`Lua`](https://www.lua.org/about.html); una delle cose che consente di fare, è quella di applicare un filtro, che assegna a tutte le immagini di un documento sorgente un determinato valore di un attributo (come la larghezza).

Basta creare un file `imgWidth.lua` con all'interno

```lua
function Image(img)
  img.attributes.width="100%"
  return img
end
```

e lanciare il comando

```
pandoc -o output.odt --lua-filter=imgWidth.lua --reference-doc=myPandocTemplate.odt input.md
```

Verrà prodotto un file `odt`, con tutte le immagini che riempiono in larghezza il `100%` dello spazio disponibile (esclusi eventuali margini). L'altezza si modificherà in proporzione.

### Installare Pandoc

1. creare una _cartella_ temporanea sul desktop;
2. avvia `Bash` dalla _cartella_;
3. lanciare questo comando `wget https://github.com/jgm/pandoc/releases/download/2.7.3/pandoc-2.7.3-1-amd64.deb` che scaricherà il file `pandoc-2.7.3-1-amd64.deb`;
4. poi, lanciare il comando: `sudo dpkg -i pandoc-2.7.3-1-amd64.deb` che installerà Pandoc;
5. controllo versione, lanciare il comando `pandoc --version`
6. lanciare il comando `sudo apt-get install texlive-xetex` per installare `--pdf-engine`

## Usando VS Code e estensioni

Una estensione molto potente è [**Markdown Converter**](https://marketplace.visualstudio.com/items?itemName=manuth.markdown-converter) un'estensione del codice di Visual Studio che consente di esportare il file Markdown come file PDF, HTML o immagine.
Offre molte funzionalità, come la formattazione di DateTime, la configurazione dei propri stili CSS, l'impostazione di intestazioni e piè di pagina, FrontMatter e molto altro.

![](./mdTOpdf/img_01.png)

dopo l'installazione, premendo `F1` (Tasto funzione) e digitando **Markdown**:

![](./mdTOpdf/img_02.png)

menu a tendina con le varie possibilità per convertire: export (pdf, export (html), export (all:pdf, html, png, jpg)

Il plugin automaticamente converte tutti i file `.md` che si trovano nella cartella radice e sottocartelle varie.

---

## Riferimenti utili

1. [Pandoc](https://pandoc.org/)
2. [lua](https://pandoc.org/lua-filters.html)
3. [VS code](https://code.visualstudio.com/)
4. [Markdown Converter](https://marketplace.visualstudio.com/items?itemName=manuth.markdown-converter)
5. [GitHub](https://github.com/)
6. [markdowm](https://it.wikipedia.org/wiki/Markdown)
7. [Libre Office Writer](https://it.wikipedia.org/wiki/LibreOffice_Writer)