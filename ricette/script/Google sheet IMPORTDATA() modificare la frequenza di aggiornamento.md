# Google sheet IMPORTDATA() modificare la frequenza di aggiornamento

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue: [#25](https://github.com/opendatasicilia/tansignari/issues/25) ricetta [Andrea Borruso](https://twitter.com/aborruso?lang=it)

---
La funzione [IMPORTDATA()](https://support.google.com/docs/answer/3093335?hl=en) di Google sheet by default aggiorna i dati ogni ora, ma se avete l’esigenza di avere i dati in tempo reale o quasi, per qualsiasi motivo, esiste una opzione per forzare l’aggiornamento della funzione anche ad ogni minuto.

Supponiamo di voler importare i dati di un file .csv da remoto, https://api.ona.io/api/v1/data/388501.csv, ci posizioniamo nella  cella **A1** del nostro foglio di lavoro scriviamo la seguente funzione:<br>
```=IMPORTDATA("https://api.ona.io/api/v1/data/388501.csv")``` <br>
in un attimo i dati saranno caricati.

![](/img/google/google_sheet2.png)

Per forzare l'aggiornamento della funzione basta usare un semplice script

![](/img/google/google_sheet3.png)

Dal menù **strumenti** (1) cliccare su **Editor di script** (2)

![](/img/google/google_sheet7.png)

Script tipo da copiare ed incollare nell'editor di script <br>
**Attezione** modificate il nome del foglio di lavoro **dati_ona** con il nome del vostro foglio di lavoro

```
{
// ATTENZIONE dati_ona è il nome del foglio di lavoro dove verrano caricati i dati

var csvUrl = “https://api.ona.io/api/v1/data/388501.csv”;
var csvContent = UrlFetchApp.fetch(csvUrl).getContentText();
var csvData = Utilities.parseCsv(csvContent);

var sheet = SpreadsheetApp.getActive().getSheetByName(‘dati_ona’)
sheet.getRange(1, 1, csvData.length, csvData[0].length).setValues(csvData);
}
``` 
## Come attivare lo script…? 
Si attiva semplicemente cliccando su **esegui**(icona play), la prima volta che lo eseguite vi chiederà l’autorizzazione, verrà visualizzato il messaggio che l’applicazione non è autenticata, non è sicura etc etc… per bypassare tutto questo, cliccare su applicazione avanzate e confermare i permessi per poter lavorare…

![](/img/google/google_sheet13.png)

Come si può notare nelle script non c’è nessun riferimento al tempo. L’intervallo di tempo di lancio dello script si imposta da **Trigger**

![](/img/google/google_sheet5.png)

Per personalizzare i valori del **Trigger**, bisogna cliccare su **I miei attivatori** e selezionare quello dedicato allo script appena creato importData() e modificarne i valori. In questa modo lo script attiverà una verifica di nuovi dati (dalla fonte CSV pre impostata nel trigger) con una frequenza temporale del singolo minuto.

![](/img/google/google_sheet8.png)



