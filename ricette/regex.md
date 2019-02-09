<!-- TOC -->

- [Introduzione](#introduzione)
- [Ricette](#ricette)
    - [Selezionare righe con spazio iniziale](#selezionare-righe-con-spazio-iniziale)
    - [Selezionare righe con spazio finale](#selezionare-righe-con-spazio-finale)
- [Siti utili](#siti-utili)

<!-- /TOC -->

# Introduzione

Qui le ricette a tema "**Espressioni Regolari**", che verranno fuori dalle issue di progetto

Tabella: significato dei caratteri speciali

CARATTERE|SIGNIFICATO|ESEMPIO
---------|-----------|------
`*` | corrisponde a **zero**, **uno** o **più** del carattere precedente | `Ah*` corrisponde a `Ahhhhh` o `A`
`?` | corrisponde a zero o uno del carattere precedente |	`Ah?` corrisponde a `A` o `Ah`
`+` | corrisponde a **uno** o **più** del carattere precedente  |	`Ah+` corrisponde a `Ah` o `Ahhh` ma non a  `A`
`\` | Usato per escludere un carattere speciale | `Hungry\?` corrisponde a `Hungry?`
`.` | Wildcard, carattere jolly, corrisponde a **qualsiasi** carattere |	`do.*` corrisponde a `dog`, `door`, `dot`, etc.
`( )` | **Gruppo** di caratteri	Vedi ad esempio `|`
`[ ]` | corrisponde ad un **range** di caratteri | `[cbf]ar` corrisponde a `car`, `bar`, o `far`; `[0-9]+` corrisponde a **qualsiasi** numero intero positivo tra 0 e 9 inclusi; `[a-zA-Z]` corrisponde a lettere ASCII `a-z` (maiuscole e minuscole); `[^0-9]` corrisponde a **qualsiasi** carattere non numerico
`|` | corrisponde al precedente OR successivo carattere/gruppo |	`(Mon)|(Tues)day` corrisponde a `Monday` o `Tuesday`
`{ }` | corrisponde aa un numero specificato di occorrenze del carattere precedente | `[0-9]{3}` corrisponde a `315` ma non a  `31`; `[0-9]{2,4}` corrisponde a `18`, `125` e  `1234`; `[0-9]{2,}` corrisponde a `1234567…`
`^` | Inizio di una stringa o all'interno di un intervallo di caratteri [] negazione.	| `^http` corrisponde stringhe che iniziano con `http`, ad esempio un URL. `[^0-9]` corrisponde a qualsiasi carattere diverso da `0-9`.
`$` | Fine stringa | `ta$` corrisponde a `cascata` e no a `tavola`

piccola guida alle [regex](https://www.evemilano.com/come-funzionano-le-espressioni-regolari-regex/)

# Ricette

## Selezionare righe con spazio iniziale

* `^( )(.+)` - solo uno spazio iniziale; [test](https://regex101.com/r/Qn4BTb/1)
* `^( +)(.+)` - uno o più spazi iniziali; [test](https://regex101.com/r/Qn4BTb/2)

Vedi issue [#1](https://github.com/opendatasicilia/tansignari/issues/1)

## Selezionare righe con spazio finale

* `(.+)( )$` - solo uno spazio finali; [test](https://regex101.com/r/Qn4BTb/3)
* `(.+?)( +)$` - uno o più spazi finali; [test](https://regex101.com/r/Qn4BTb/4)

Vedi issue [#2](https://github.com/opendatasicilia/tansignari/issues/2)

# Siti utili

- **regex101**, per testare espressioni regolari e imparare a usarle [https://regex101.com/](https://regex101.com/)