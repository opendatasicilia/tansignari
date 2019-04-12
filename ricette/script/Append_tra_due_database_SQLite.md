# Append tra due database SQLite tramite script

* autore: _[Totò Fiandaca](https://twitter.com/totofiandaca?lang=it)_

---

<!-- TOC -->

- [Append tra due database SQLite tramite script](#append-tra-due-database-sqlite-tramite-script)
  - [script bash](#script-bash)
  - [script SQL](#script-sql)
  - [come e dove usare gli script](#come-e-dove-usare-gli-script)

<!-- /TOC -->

---

Appendere dati da una tabella a un'altra è una operazione ripetitiva che si risolve, brillantemente, attraverso lo scripting usando, per esempio, la libreria [GDAL/OGR](https://www.gdal.org/ogr2ogr.html) o script [SQL](https://it.wikipedia.org/wiki/Structured_Query_Language). Questa procedura facilita enormemente il lavoro di gruppo su uno stesso database SQLite (_db_main.sqlite_) distribuito a più persone (per esempio _db01.sqlite_): permettendo di appendere i dati nel db originario dopo una sessione di lavoro.

## script bash

```bash
#!/bin/bash

ogr2ogr -update -append -f SQLite db_main.sqlite -nln "nomeTabellaDestinazione" db01.sqlite "nomeTabellaOrigine"
```

## script SQL

```sql
--
-- the present SQL script is intended to be executed from SpatiaLite_gui
--
-- initializing the output db-file
--
SELECT InitSpatialMetadata(1);

--
-- attaching the input DB-file

ATTACH DATABASE 'percorso_al_db/db01.sqlite' AS input;
SELECT CloneTable('input', 'nomeTabellaOrigine', 'nomeTabellaDestinazione', 1, '::append::'); -- appendo seconda tabella

-- detaching the input db-file
--
DETACH DATABASE input;

--
-- vacuuming the output db-file
--
VACUUM;
```

## come e dove usare gli script

* lo `script bash` va lanciato da un terminale, a partire dalla cartella che contiene i db;
* lo `script SQL` va eseguito all'interno di spatialite_gui (Execute SQL script, dal menu).