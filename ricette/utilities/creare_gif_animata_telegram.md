# Come creare una GIF animata per Telegram

- issue correlata: `[#107](https://github.com/opendatasicilia/tansignari/issues/107)`
- autore: `[Andrea Borruso](https://twitter.com/aborruso)`;
- ingredienti: [ffmpeg](https://www.ffmpeg.org/)
  
---

Questa ricetta nasce perché se si fa l'**upload** diretto di una GIF animata su Telegram, questa perde in qualità e diventa poco leggibile; sopratutto dopo lo zoom.

Per fare in modo che mantenga la leggibilità, basta convertirla in formato `MP4` e poi fare l'upload di questo file, che verrà trasformato di nuovo in GIF animata dal client Telegram.

Per fare la convertsione da GIF animata in `MP4` si può usare l'**utility open source** ffmpeg, disponibile per tutti i sistemi operativi.<br>
Si esegue dal terminale (la shell, il prompt, ecc.).

Questo il comando:

```bash
ffmpeg -f gif -i input.gif -filter_complex "loop=1:32767:0,scale=trunc(iw/2)*2:trunc(ih/2)*2" -preset slow -pix_fmt yuv420p output.mp4
```

