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
- `sphinx-rtd-theme` 
- `sphinx` 
- `recommonmark` 
- `markdown`  
- `sphinx-markdown-tables` 

-

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
