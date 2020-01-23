# Come fare leggere un file in formato .MD a ReadtheDocs (in un progetto su Github) 


* autore: [Ciro Spataro](https://twitter.com/cirospat)
* issue: [#106](https://github.com/opendatasicilia/tansignari/issues/106) fornitore ricetta [mastro Andrea Borruso](https://twitter.com/aborruso?lang=it)

---

## Problema

Se voglio far leggere un file .MD a ReadtheDocs, oltre ai file .RTS, quali impostazioni devo settare e dove li devo settare su Github?

## Soluzione

Bisogna guardare questi due file `requirements.txt` e `conf.py` sul progetto ospitato da **Github**.

**`requirements.txt`**

`requirements.txt` è il file che contiene i requisiti dei moduli da installare. Vedi ad esempio: https://github.com/opendatasicilia/tansignari/blob/master/requirements.txt. Bisogna inserire nel file:
```bash
sphinx-rtd-theme 
sphinx 
recommonmark 
markdown  
sphinx-markdown-tables
```
--

**`conf.py`**

`conf.py`, è il file di configurazione in linguaggio python. In queste linee si imposta la configurazione che abilita il markdown

```bash
import recommonmark
from recommonmark.transform import AutoStructify

from recommonmark.parser import CommonMarkParser

source_parsers = {
    '.md': 'recommonmark.parser.CommonMarkParser',
}

source_suffix = ['.rst', '.md']

extensions = ['sphinx.ext.ifconfig','sphinx_markdown_tables']
```
Bisogna inserire queste righe di codice nel file `conf.py`.

---

### Se il progetto su Read the Docs non dovesse compilare 
In questo periodo (gennaio 2020) c'è un bug, seguire la procedura illustrata di seguito per permettere a Read the Docs di compilare il progetto ospitato su Github.

A questo link https://docs.readthedocs.io/en/stable/guides/wipe-environment.html viene spiegato come agire in maniera semplice.

Wiping a Build Environment
Sometimes it happen that your Builds start failing because the build environment where the documentation is created is stale or broken. This could happen for a couple of different reasons like pip not upgrading a package properly or a corrupted cached Python package.

In any of these cases (and many others), the solution could be just wiping out the existing build environment files and allow Read the Docs to create a new fresh one.

**Follow these steps to wipe the build environment**:
- Go to `Versions`
- Click on the **Edit** button of the version you want to wipe on the right side of the page
- Go to the bottom of the page and click the **wipe link**, next to the **“Save”** button

**NOTE**: By wiping the documentation build environment, all the `rst`, `md`, and `code` files associated with it will be removed but not the documentation already built (`HTML` and `PDF` files). Your documentation will still be online after wiping the build environment.

Now you can re-build the version with a fresh build environment!
