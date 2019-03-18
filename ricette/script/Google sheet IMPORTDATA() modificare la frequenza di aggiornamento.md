# Google sheet IMPORTDATA() modificare la frequenza di aggiornamento

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue: [#25](https://github.com/opendatasicilia/tansignari/issues/25) ricetta [Andrea Borruso](https://twitter.com/aborruso?lang=it)

---
La funzione [IMPORTDATA()](https://support.google.com/docs/answer/3093335?hl=en) di Google sheet by default aggiorna i dati ogni ora, ma se avete l’esigenza di avere i dati in tempo reale o quasi, per qualsiasi motivo, esiste una opzione per forzare l’aggiornamento della funzione anche ad ogni minuto.

Supponiamo di voler importare i dati di un file .csv da remoto, https://api.ona.io/api/v1/data/388501.csv, ci posizioniamo nella  cella **A1** del nostro foglio di lavoro scriviamo la seguente funzione ```=IMPORTDATA("https://api.ona.io/api/v1/data/388501.csv")```
in un attimo i dati saranno caricati.

![](/img/google/google_sheet2.png)

