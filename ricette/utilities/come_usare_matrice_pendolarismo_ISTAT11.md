# Come usare la matrice del pendolarismo ISTAT 2011

- issue correlata: [#105](https://github.com/opendatasicilia/tansignari/issues/105)
- autore:  _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_ fornitore ricetta [Andrea Borruso](https://twitter.com/aborruso)
- ingredienti: [bash](https://it.wikipedia.org/wiki/Bash), [SpatiaLite](https://www.gaia-gis.it/fossil/libspatialite/index), [VisiData](https://www.visidata.org/), [grep](https://it.wikipedia.org/wiki/Grep)
  
---

<!-- TOC -->

- [Come usare la matrice del pendolarismo ISTAT 2011](#come-usare-la-matrice-del-pendolarismo-istat-2011)
  - [Introduzione](#introduzione)
  - [Matrice OD](#matrice-od)
  - [Come leggere la matrice del Pendolarismo](#come-leggere-la-matrice-del-pendolarismo)
  - [Come usare il database SpatiaLite](#come-usare-il-database-spatialite)
  - [Chi ha cucinato questa ricetta o ne ha tratto ispirazione](#chi-ha-cucinato-questa-ricetta-o-ne-ha-tratto-ispirazione)
  - [Riferimenti utili](#riferimenti-utili)

<!-- /TOC -->

---

## Introduzione

La matrice del pendolarismo, per vari motivi, ha questa forma:

```
L 1 001 001  1 1 1 001 001 000 04 2 1 0000005.00         ND  
L 1 001 001  1 1 1 001 001 000 05 1 3 0000001.00         ND  
L 1 001 001  1 1 1 001 001 000 05 2 2 0000001.00         ND  
L 1 001 001  1 1 1 001 001 000 06 2 1 0000009.00         ND  
L 1 001 001  1 1 1 001 001 000 06 2 2 0000002.00         ND  
L 1 001 001  1 1 1 001 001 000 07 1 1 0000002.00         ND  
L 1 001 001  1 1 1 001 001 000 08 1 1 0000001.00         ND  
L 1 001 001  1 1 1 001 001 000 08 2 1 0000052.00         ND  
....
....
```

Alla matrice è allegato un documento metodologico che, oltre a descrivere la struttura dei dati, fornisce indicazioni utili per l’utilizzo della matrice, con particolare riferimento alle variabili rilevate con metodo campionario (mezzo di trasporto utilizzato, fascia oraria di partenza e durata del tragitto). Sono anche allegati alcuni documenti utili alla comprensione al corretto utilizzo dei dati (questionari e classificazioni).

Il [file ](http://www.istat.it/storage/cartografia/matrici_pendolarismo/matrici_pendolarismo_2011.zip) contiene i dati sul **numero di persone** che si **spostano tra comuni** – o all’interno dello stesso comune – classificate, oltre che per il **motivo dello spostamento**, per il sesso, il mezzo di trasporto utilizzato, la fascia oraria di partenza e la durata del tragitto.

## Matrice OD

Sarebbe interessante poter estrarre rapidamente una **matrice OD** (Origine Destinazione) cosi fatta:

origine|destinazione|valore
-------|------------|-----
037032|068028|3
037054|068028|1
041028|068028|1
.....|.......|...
042045|068028|3
043031|068028|1
044066|068028|22

dove:

* `origine` sono i codici istat dei comuni;
* `destinazione` codice istat del comune (es: Palermo `PRO_COM = 82053`)
* `valore` numero di persone (es: studenti)

la `matrice OD` è utile per creare mappette come questa:

![image](https://user-images.githubusercontent.com/7631137/72556528-1b779a00-389f-11ea-9269-5af5bbeac7bc.png)

## Come leggere la matrice del Pendolarismo

Il file con i dati è una tabella con i campi **fixed**. Nel documento descrittivo c'è 1) la lunghezza in caratteri di ogni campo, e 2) da quale carattere inizia ogni campo.

![image](https://user-images.githubusercontent.com/30607/72565191-a1044580-38b1-11ea-81e4-8fda777f2348.png)

Nei fogli elettronici si importa come sotto, fissando a mano i separatori di campo.

![image](https://user-images.githubusercontent.com/30607/72565302-dad54c00-38b1-11ea-8df1-114e82010606.png)

Il file del Pendolarismo ha _oltre 4 milioni di righe_, quindi non è importabile in un foglio elettronico. Una soluzione potrebbe essere quella di filtrare tutto ciò che riguarda Palermo (`pro_com_t=082053`), con 

```
<matrix_pendo2011_10112014.txt grep -E '082.+053' >palermo.txt
```

Le righe diventano circa 11.000 e quindi gestibile da LibreOffice Calc.

Oppure aprilo per intero con **VisiData** con `vd -f fixed matrix_pendo2011_10112014.txt`, buttando un occhio in basso a destra aspettando che finisca il load.

Oppure usare **Miller** e **Visidata** per i dati di Palermo:

```
mlr --p2c --implicit-csv-header filter -S '$8=="082" && $9=="053"' then put -S '$source=$3.$4;$destination=$8.$9;if ($1=="S") {$valore=gsub($15,"^0+","")} else {$valore=gsub($14,"^0+","")}' then cut -f source,destination,valore matrix_pendo2011_10112014.txt | vd -f csv
```

Oppure importare l'intera matrice del pendolarismo in una database **SpatiaLite**:

1. `mlr --p2c --implicit-csv-header cat matrix_pendo2011_10112014.txt >out_matrix.csv` , che aggiunge l'intestazione (1,2,3,4,5,6,7,8,9,10,11,12,13,14,15);
2. poi, aprilre il file con Notepad** e modificare l'intestazione a piacere;
3. importare il file `out_matrix.csv` utilizzando la gui di spatialite_gui e la fuznione `Load CSV/TXT`

##  Come usare il database SpatiaLite

Nel database sono presenti:

1. `Com2011_g_WGS84` - geotabella MUTLIPOLYGON;
2. `ElencoUnitaAmmin2011` - tabella;
3. `Localita_11_WGS84` - geotabella MUTLIPOLYGON
4. `Reg2011_g_WGS84` - geotabella MUTLIPOLYGON
5. `legenda_comuni` - tabella;
6. `matrice_OD_all` - VIEW nessun filtro
7. `matrice_OD_lr` - VIEW filtro lungo raggio
8. `matrice_OD_studenti` - VIEW filtro studenti
9. `out_matrix` - tabella matrice pendolariemo.

Query che genera gli archi del pendolarismo (città di Palermo come destinazione, solo studenti)

```SQL
WITH toto AS
(
SELECT q.*,e."X_WGS84_32N", e."Y_WGS84_32N"
FROM "ElencoUnitaAmmin2011" e,
(
SELECT m.*,c.comune
FROM "Com2011_g_WGS84" c,
(
SELECT t.source AS source, count(*) AS nro, sum (valore) AS valore_tot
FROM
(
SELECT "prov_stud_lav"||"com_stud_lav" AS destination,"prov_resid"||"com_resid" AS source, 
CASE WHEN "tipo_record" = 'S' THEN cast ("nro_indiv" AS real)
     ELSE cast ("stima_nro_indiv" AS real)
     END valore
FROM "out_matrix"
WHERE "prov_stud_lav"||"com_stud_lav" ='082053' -- Palermo città
) t
GROUP BY 1
) m
WHERE m.source = c."pro_com_t"
ORDER BY m.nro desc
) q
WHERE q.source = e."pro_com_t"
)

SELECT *,
makeline(
	 makepoint("X_WGS84_32N", "Y_WGS84_32N"),
	 makepoint((SELECT "X_WGS84_32N" FROM toto ORDER BY nro desc limit 1), 
		     (SELECT "Y_WGS84_32N" FROM toto ORDER BY nro desc limit 1)) 
         )	as geom
FROM toto;
```

ottengo la geotabella:

![image](https://user-images.githubusercontent.com/7631137/72679835-623ddd80-3ab3-11ea-9a93-2f56689348d6.png)

che in [QGIS ](https://qgis.org/it/site/)è cosi:

![image](https://user-images.githubusercontent.com/7631137/72679866-d5475400-3ab3-11ea-8c15-ad4f08f74e25.png)

Download [database spatialite](5kYjTDB39fGKX5RwRx7hTkBQ2ZyPkHdLsygoFUfZYRE)

## Chi ha cucinato questa ricetta o ne ha tratto ispirazione

- [Blog post](https://pigrecoinfinito.com/2020/01/15/pendolarismo-come-creare-un-hub-line-con-qgis/) su Pigrecoinfinito by  _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_

## Riferimenti utili

- Link ISTAT: <https://www.istat.it/it/archivio/139381>



