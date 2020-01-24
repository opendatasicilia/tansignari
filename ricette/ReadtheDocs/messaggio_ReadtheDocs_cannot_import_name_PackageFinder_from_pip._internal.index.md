# Messaggio Read the Docs di “build fails”: [cannot import name “PackageFinder” from “pip._internal.index”]

* autore: [Ciro Spataro](https://twitter.com/cirospat)
* issue: [#106](https://github.com/opendatasicilia/tansignari/issues/106#issuecomment-577152591) - aiuto nell'individuazione della  soluzione: [Andrea Borruso](https://twitter.com/aborruso?lang=it)

---

Può capitare che durante la procedura di compilazione del progetto su **Read the Docs** appaia un messaggio: *“cannot import name “PackageFinder” from “pip._internal.index”*. Ciò comporta la **non compilazione del progetto** su Read the Docs, quindi gli aggiornamenti apportati sulle pagine di Github non vengono renderizzati sulle pagine `HTML` di Read the Docs.


## La causa
[Dall'issue del 20 gennaio 2020](https://github.com/readthedocs/readthedocs.org/issues/6554)

*Currently all builds are failing because the automatic upgrade [(since #4823)](https://github.com/readthedocs/readthedocs.org/issues/4823) to pip 20.0 was buggy [(see pypa/pip#7620)](https://github.com/pypa/pip/issues/7620). There’s now a 20.0.1 release which seems to have fixed the problem for others … but how can I force my readthedocs to also upgrade to the .1 version?*



## La soluzione 
[Da Read the Docs / Wiping a Build Environment](https://docs.readthedocs.io/en/stable/guides/wipe-environment.html)

A volte capita che le tue build inizino a fallire perché l'ambiente di build in cui viene creata la documentazione è obsoleto o danneggiato.

In uno di questi casi (e molti altri), la soluzione potrebbe essere semplicemente cancellare i file dell'ambiente di build esistente e consentire a Leggi i documenti di crearne uno nuovo.

Seguire questi passaggi per cancellare l'ambiente di compilazione: 
- Vai alle **“Versioni”** 
- Fare clic sul pulsante **“Modifica”** della versione che si desidera cancellare sul lato destro della pagina 
- Vai in fondo alla pagina e fai clic sul collegamento di **Wype** (cancellazione), accanto al pulsante **"Salva"**.

**Nota**: Pulendo l'ambiente di creazione della documentazione (attraverso il "Wype"), verranno rimossi tutti i file ``rst``, ``md`` e ``code`` associati ma non la documentazione già creata (file ``HTML`` e ``PDF``). La documentazione sarà ancora online dopo aver cancellato l'ambiente di compilazione.

Ora è possibile ricostruire la versione con un nuovo ambiente di compilazione! Nella pagina "**compilazioni**" del progetto Read the Docs cliccare su "**Versione di Compilazione**" e una uova compilazione sarà avviata.
