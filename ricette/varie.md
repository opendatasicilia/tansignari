<!-- TOC -->

- [Varie](#varie)
    - [Creare un feed RSS a partire da una pagina web](#creare-un-feed-rss-a-partire-da-una-pagina-web)

<!-- /TOC -->

# Varie

## Creare un feed RSS a partire da una pagina web

- issue correlata: [#5](https://github.com/opendatasicilia/tansignari/issues/5)
- autore: [Ciro Spataro](https://github.com/cirospat)

---

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/Feed-icon.svg/40px-Feed-icon.svg.png)
Per **creare un Feed RSS di una pagina web** ci sono diversi modi.

Uno, il più semplice è usare **Feedburner** https://feedburner.google.com/fb/a/myfeeds.
Ma a volte per alcune pagine web può non funzionare. Si rende necessario usare altri strumenti online.
Uno molto efficace è https://feed43.com/.

Prendiamo ad esempio questa pagina dalla quale vogliamo creare un feed RSS: https://www.lafeltrinelli.it/fcom/it/home/pages/puntivendita/negozi/trova/sicilia/RicordiMediaStores-Palermo.html

Per creare un feed RSS con **Feed43**, devi partire dall'analizzare il codice HTML della pagina web sorgente, e cercare l’elemento che si ripete. Tasto destro sulla parte di pagina con un elemento da trasformare in feed e poi ispeziona il codice.
Devi cercare l’intero blocco di codice che si ripete per ogni elemento. Qui ad esempio è

```html
<div class="event clearfix"><img width="60" src="https://www.lafeltrinelli.it/mediaObject/eventi/2019/01/Spyrosil-Marinaio-Italiano-27624/resolutions/res-l60x10000/Spyrosil-Marinaio-Italiano-27624.jpg"/><div class="text"><h4 class="date">Martedì 5 Febbraio 2019 dalle ore 18:00</h4><h3><a href="https://www.lafeltrinelli.it/fcom/it/home/pages/puntivendita/eventi/Palermo/2019/Febbraio/Spyrosil-Marinaio-Italiano-27624.html">Spyros Il marinaio italiano</a></h3><div class="button-link button-detail clearfix"><a href="https://www.lafeltrinelli.it/fcom/it/home/pages/puntivendita/eventi/Palermo/2019/Febbraio/Spyrosil-Marinaio-Italiano-27624.html">SCOPRI</a></div></div></div>
```

Nella pagina originale non è indentato, così è più leggibile

```html
<div class="event clearfix">
   <img width="60" src="https://www.lafeltrinelli.it/mediaObject/eventi/2019/01/Spyrosil-Marinaio-Italiano-27624/resolutions/res-l60x10000/Spyrosil-Marinaio-Italiano-27624.jpg"/>
   <div class="text">
      <h4 class="date">Martedì 5 Febbraio 2019 dalle ore 18:00</h4>
      <h3><a href="https://www.lafeltrinelli.it/fcom/it/home/pages/puntivendita/eventi/Palermo/2019/Febbraio/Spyrosil-Marinaio-Italiano-27624.html">Spyros Il marinaio italiano</a></h3>
      <div class="button-link button-detail clearfix"><a href="https://www.lafeltrinelli.it/fcom/it/home/pages/puntivendita/eventi/Palermo/2019/Febbraio/Spyrosil-Marinaio-Italiano-27624.html">SCOPRI</a></div>
   </div>
</div>
```

Nel codice HTML devi cercare le parti variabili e sostituirle con `{%}`. Quindi prendendo il codice originale (quello non indentato) avrai

```html
<div class="event clearfix"><img width="60" src="{%}"/><div class="text"><h4 class="date">{%}</h4><h3><a href="{%}">{%}</a></h3><div class="button-link button-detail clearfix"><a href="{%}">SCOPRI</a></div></div></div>
```
![image](https://user-images.githubusercontent.com/30607/52532163-7401f700-2d20-11e9-9ba2-8ecca90450b2.png)

A quel punto potrai estrarre i vari item con feed43

E infine dirgli che `{%4}` è il titolo `{%3}` il link, ecc..

E alla fine avrai un RSS https://feed43.com/7445176480120553.xml
