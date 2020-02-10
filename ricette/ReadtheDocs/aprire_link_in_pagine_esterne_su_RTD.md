# Dove è (e qual è) l'istruzione da dare su Github per fare aprire su RTD i link in una pagina esterna?

* autore: [Ciro Spataro](https://twitter.com/cirospat)
* issue: [#116](https://github.com/opendatasicilia/tansignari/issues/116) fornitore ricetta [Giovan Battista Vitrano](https://twitter.com/gbvitrano?lang=it)

---

## Obiettivo

Sui progetti di documentazione esposti su Read the Docs ad un determinato link voglio far aprire la pagina correlata in una pagina diversa da quella che sto leggendo.

## Soluzione

Bisogna dare un istruzione sul file **``conf.py``** per fare aprire su RTD i link in una pagina esterna. L'istruzione è la seguente:

```bash
html_theme_options = {
    'style_external_links': True
}
```

Se si vogliono forzare tutte le pagine ad aprirsi in una nuova finestra, uno script su stackoverflow.com soddisfa l'esigenza. Basta aggiungere questo script nel file **``layout.html``**, prima della chiusara del blocco finale:

```bash
<!-- Adds target=_blank to external links -->
<script type="text/javascript">
   $(document).ready(function () { 
      $('a[href^="http://"], a[href^="https://"]').not('a[class*=internal]').attr('target', '_blank'); }); 
</script>
```
