# Come raccogliere dati geolocalizzati

* autore: [gbvitrano](https://twitter.com/gbvitrano)
* issue:

---

E’ possibile raccogliere dati geolocalizzati, ordinati secondo uno schema,  che ci consente di mappare (in tempo reale) tutto quello che ci circonda…? e che sia anche una soluzione a basso costo e semplice da usare in mobile/computer…?

## ODK
**Si… la risposta è SI…** Tutto questo ed anche di più è possibile realizzarlo con [Open Data Kit](https://opendatakit.org/) un progetto “open” che consente l’impostazione di sistemi client-server di raccolta e archiviazione di dati da parte di operatori sul campo tramite dispositivi mobili.

Cit. dal blog [TANTO – Raccolta dati per tutti: GeoODK e smartphones per sensori urbani (parte I)](http://blog.spaziogis.it/index.html_p=6786.html).

[Open Data Kit](https://opendatakit.org/) (ODK) consente di:
* costruire una form (o “questionario”) di raccolta dati;
* raccogliere dati su di un dispositivo mobile;
* aggregare i dati raccolti su di un server ed estrarli in formati utilizzabili.

Il sistema richiede diversi elementi da integrare.

Innanzitutto una *form*, ovvero il questionario da sviluppare.

Una **‘piattaforma’ per la raccolta dei dati**: qui ci viene in aiuto [enketo.org](https://enketo.org/) per la realizzazione di una **webform** compilabile da (virtualmente) qualsiasi dispositivo, oppure un’app da caricare su dispositivo mobile. Diverse app sono state sviluppate: [ODK Collect](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=2ahUKEwjh6PWy7ojhAhXqsaQKHRhLCCEQFjAAegQIBxAB&url=https%3A%2F%2Fplay.google.com%2Fstore%2Fapps%2Fdetails%3Fid%3Dorg.odk.collect.android%26hl%3Dit&usg=AOvVaw24t_x8wIkiQj7jI7z-8cvB) e [KoBo Collect](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=2ahUKEwidmqvC7ojhAhXFGuwKHZe4B68QFjAAegQIAxAB&url=https%3A%2F%2Fwww.kobotoolbox.org%2F&usg=AOvVaw0mpRrQ9A3VHIKgZRP547tB), solo per citarne un paio, soprattutto nell’ambito di progetti a contenuto umanitario o sviluppati apposta per scopi educativi.

Un server, ovvero un sistema centralizzato in cui salvare i dati immessi. Senza ricorrere a un nostro server si può fare riferimento alle piattaforme [ODK aggregate](https://docs.opendatakit.org/aggregate-intro/) e [Ona.io](https://ona.io/home/) (nel nostro caso).

Per capire meglio il funzionamento del sistema di raccolta dati di [Open Data Kit](https://opendatakit.org/) vi invito a leggere l’articolo su [TANTO – Raccolta dati per tutti: GeoODK e smartphones per sensori urbani (parte I)](http://blog.spaziogis.it/index.html_p=6786.html). In questo post mi limiterò a descrivere il procedimento che ci ha permesso di realizzare i diversi form per la raccolta dati, l’archiviazione e l’estrazione dei dati per la pubblicazione e l’interfaccia web per esporli già mappati. (ricerca e sviluppo di opendatasicilia.it)

# ona.io

## Registrazione

La prima cosa da fare è scegliere il server/piattaforma che ospiterà i dati da noi raccolti, noi abbiamo scelto **[Ona.io](https://ona.io/home/)**, la stessa cosa si può fare con [kobotoolbox.org](https://www.kobotoolbox.org/), [mapyourworld.org](http://mapyourworld.org/), [datawinners.com](https://www.datawinners.com/) e tante altre piattaforme, tutti servizi online free e basati sulle webform di [enketo.org](https://enketo.org/).

![](/img/odk_ona/ona_register.jpg)
[Registazione alla Piattaforma ona.io](https://ona.io/join)

Dopo la registrazione per prima, di iniziare un nuovo progetto,  sarebbe opportuno entrare nel Settings del proprio profilo e impostare Require Phone Authentication?, ovvero decidere se limitare o meno l’invio dei moduli solo ad utenti registrati.
![](/img/odk_ona/ona_settings.jpg)

## New Projects

to be continued...
