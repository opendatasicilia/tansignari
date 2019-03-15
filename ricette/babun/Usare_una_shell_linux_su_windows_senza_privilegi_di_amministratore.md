## Usare una shell linux su Windows senza i privilegi di amministratore

- issue correlata: [#29](https://github.com/opendatasicilia/tansignari/issues/29)
- autore: [Lorenzo Perone](https://github.com/lorenzoperone); fornitore della ricetta: [Andrea Borruso](https://github.com/aborruso); 
---

![image](https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_vim.png)

Per **utilizzare una shell linux su windows** ci sono diversi modi, in questa ricetta vediamo un approccio adatto a chi sul proprio computer, con sistema operativo Windows 10, non dispone dei privilegi di amministratore.

Utilizzeremo **[Babun](http://babun.github.io/)** un progetto che purtroppo da pochi giorni ha annunciato la sospensione delle attività per mancanza di *mantariner*.

1. Scarichiamo **Babun** da [questo](http://projects.reficio.org/babun/download) link.
2. Decomprimiamo il file **zip**
2. Eseguiamo il file ** install.bat** che installerà **babun** nella directory di default **C:\Users\%USERPROFILE%\\.babun**
3. Lanciamo il collegamento **babun** creato sul Desktop oppure cerchiamo nella cartella **C:\Users\%USERPROFILE%\\.babun** lo script **babun.bat**
   -  nella cartella degli script é presente anche lo
 script **update.bat* utile per l'aggiornamento dei pacchetti installati.

Babun scrive, in fase di installazione, nella variabile $PATH dell'utente il proprio percorso di installazione, quindi è possibile lanciarlo anche da un promt dei comandi (shell) digitando 

```
babun
```

Per installare dei **pacchetti** non presenti nel sistema è possibile usare il suo comodo installer, ad esempio per installare le librerie ed eseguibili **gdal** digito 

```
pact install gdal
```
 e **Babun** scaricherà ed installera i pacchetti richiesti.