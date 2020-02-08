# Pubblicare mappe a tasselli su github

- issue correlata: [#117](https://github.com/opendatasicilia/tansignari/issues/117)
- autore: [Totò Fiandaca](https://twitter.com/totofiandaca); fornitore della ricetta: [Andrea Borruso](https://github.com/aborruso);
- ingredienti: [GDAL](https://gdal.org/), [Tiles XYZ](https://en.wikipedia.org/wiki/Tiled_web_map), [GitHub](https://github.com/)

---

<!-- TOC -->

- [Pubblicare mappe a tasselli su github](#pubblicare-mappe-a-tasselli-su-github)
  - [Introduzione](#introduzione)
  - [Generazione dei tasselli](#generazione-dei-tasselli)
  - [URL dei tasselli](#url-dei-tasselli)
  - [Come utilizzarlo](#come-utilizzarlo)
    - [Esempio su QGIS](#esempio-su-qgis)
  - [Chi ha cucinato questa ricetta o ne ha tratto ispirazione](#chi-ha-cucinato-questa-ricetta-o-ne-ha-tratto-ispirazione)

<!-- /TOC -->

---

## Introduzione

Per chi lavora con i raster, alcune volte, nasce l'esigenza di condividere proprie elaborazioni (per esempio georeferenziazioni di mappe storiche) con il mondo; un modo molto veloce e pratico è attraverso la realizzazione di [Tiles XYZ](https://en.wikipedia.org/wiki/Tiled_web_map) e pubblicarli su GitHub. La procedura base è questa: si creano i tasselli, si pubblicano su un repo github e si abilitano le _github pages_ sul repository.

---

## Generazione dei tasselli

Si possono generare con [gdal2tiles](https://gdal.org/programs/gdal2tiles.html).

```
gdal2tiles.py index50kP2.tif
```

dove **index50kP2.tif** è un raster [geotiff](https://it.wikipedia.org/wiki/GeoTIFF)

In output verrà creata la cartella **index50kP2** che contiene i tasselli.


## URL dei tasselli

Una volta pubblicata la cartella che contiene i tasselli su un _repository github_, attivare le _github pages_: dal settings del repository

![](https://pigrecoinfinito.files.wordpress.com/2020/02/image-14.png?w=933)

L'URL del repository è evidenziato nella striscia verde. In questo caso la cartella dei tasselli è https://pigreco.github.io/gdal2tiles_su_github/index50kP2/

## Come utilizzarlo

Per utilizzare questa sorgente in [QGIS](https://qgis.org/it/site/), bisogna creare un **layer XYZ** con questo **URL**

https://pigreco.github.io/gdal2tiles_su_github/index50kP2/{z}/{x}/{-y}.png

### Esempio su QGIS

![](https://pigrecoinfinito.files.wordpress.com/2020/02/image-20.png?w=1024)

---

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- **Blog Pigrecoinfinito** : <https://pigrecoinfinito.com/2020/02/08/pubblicare-mappe-a-tiles-xyz-su-github/>