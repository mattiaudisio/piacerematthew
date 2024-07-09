+++
title = 'Creare un intero podcast artificialmente'
date = 2023-12-20T21:07:49+02:00
tags = ['👨‍💻 Echo 404']
+++

Ieri, mentre cazzeggiavo nella timeline locale, mi sono imbattuto in  [questo post](https://livellosegreto.it/@cesco/111606253044821035) di [cesco](https://livellosegreto.it/@cesco) che, per una persona a cui piace sperimentare scrivendo righe di codice, non dirà niente di nuovo... a me invece sta cosa ha fatto scoreggiare il cervello.

Ok, lo so che può suonare strano agli smanettoni dell'IA, ma guardiamo un attimo cosa c'è:

```
 Riciclando del vecchio codice che avevo scritto e aggiungendo qualcosa di  nuovo, in 5 min e 
 38 righe di codice ho messo in piedi uno script in python che:
 – Scarica un articolo da una famosa testata giornalistica
 – Lo riassume in breve
 – Fa il TTS trasformandolo in un articolo letto da una voce sintetizzata. Che sulla carta non è pensata per 
 la lingua italiana, ma che comunque fa già un lavoro sorprendentemente buono.
```
_Chiedo venia per il brusco copia incolla_

<br />

Ho letto tutto questo mentre stavo ascoltando l'audio che c'è in allegato a questo toot e piano piano, nella mia testa, è cominciato un coro, all'inizio non coordinato e abbastanza stonato, che piano piano ha cominciato ad unirsi in un unica e potente frase: “Questo è un podcast”.

Perchè sì, togliendo l'effetto della voce, che ci fa capire che è fatta con un IA, tutto quello che ho sentito poteva essere tranquillamente un intermezzo di un podcast che mi ascolto al mattino mentre vado a lavorare, sì senza musiche ed effetti sonori di sottofondo, però l'essenza è quella.

Ed è lì che mi viene illuminazione...

passare le ultime 4 ore della mia vita a verificare (lo so che è già stato verificato tutto quasi un milione di volte, ma ho l'ossessione di reinventare la ruota) questo mio pensiero e, dato che si parlava di AI, sfruttare l'AI di Bing.

## 1. Bing AI mi darà una mano?

Devo essere sincero, fino a qualche giorno fa, non avevo mai provato l'AI di Bing, e non perchè avevo della diffidenza a rigurardo (cof. cof. Microsft cof. cof.), ma semplicemente perché non avendo Edge installato, dato che uso Fedora come OS principale, non mi era mai capitato di provarlo.

Ma negli ultimi giorni, causa un regalo da fare ad un amico, ho voluto prendere un portatile che ho qua a casa, usato dalla mia famiglia, e provare a creare qualcosa con Bing Image Creator... inutile dire che tempo 5 minuti sono finito col passare le mie ore a creare cagate su cagate per vedere quanto assurdi possono essere i comandi che puoi dare.

Ma tolto sta parentesi, non avevo provato ad usarlo per scrivere del codice quindi, dato che il chiodo fisso del giorno è fare questo cosa, mi sono messo lì, con due portatili accanto, a creare sto script con Bing AI.

Sincero, mi ha aiutato molto. Sì, alcune cose alla fine sono andato a cercarmele [qua](https://platform.openai.com/), ma per il resto mi ha dato un enorme mano in alcuni punti.

_Da persona che si è sempre ostinata nel fare da se senza bisogno di AI, vorrei prendermi a sberle visto che ho capito solo ora che queste cose mi sarebbero stati utili quando programmavo più assiduamente, in modo da non fare delle supercazzole di 100 righe che si potevano riassumere in 25..._

ma tolto questo...

## 2. Si crea lo scirpt

Partiamo da una cosa, che non ho mai preso seriamente in considerazione ma perchè python tolto l'uso scolastico non l'ho usato più di tanto _(lo so, sono una brutta persona)_, ovvero il file requirments.txt.

Perchè non lo prendo in considerazione.... perchè sono solito usare il comando pip... vabbè

**requirments.txt**
```
 beautifulsoup4==4.10.0
 openai==0.27.0
```

e per installare questi pacchetti utilizzare il comando  pip install -r requirments.txt.

Tolto sta parentesi imbarazzante, lo script si divide in 4 passaggi:

1. Scaricare il contenuto dell'articolo
2. Estrarre il testo dall'inzio
3. Generare l'audio TSS
4. Salvare l'audio in un file MP3 

e, all'interno dello script, ho utilizzato due pacchetti in particolare, quelli installati prima, beautifulsoup (un pacchetto per il web scraping) e openAI (che penso non abbia bisogno di presentazioni).

il loro ruolo si può riassumere sostanzialmente nel scaricare da internet l'articolo interessato grazie a beautifulsoup e con openai convertirlo in audio.
Tolto il fatto che ho dovuto creare un account openai per sto esperimento e so che me ne pentirò fortemente (del tipo che finisco questo articolo e lo cancello), il problema si è rivelato nel ricavare l'articolo.

Il primo articolo che ho utilizzato, non aveva una struttura adatta a questo tipo di esperimento e, cercando nella mia lista di link interessanti, non riuscivo a trovare niente che andasse bene, dato che ogni sito ha una struttura diversa dall'altro. Per fortuna ho scoperto che Rollign Stone si presta benissimo a quello che devo fare, quindi sono riuscito a salvarmi così.

Senza troppi giri di parole, dato che non mi so spiegare, ecco qua lo script finito:

**script.py**

```
 import openai
 from bs4 import BeautifulSoup
 import requests

 # Url dell'articolo
 url_articolo = "https://www.rollingstone.it/cultura/gaming/un-programmatore-misterioso-ha-fatto-mario-64-per-pc/515650/"

 # Scarica il contenuto dell'articolo
 response = requests.get(url_articolo)
 soup = BeautifulSoup(response.content, 'html.parser')
 article_content = soup.find("div",class_="l-article-content")

 # Estrai il testo dall'inzio
 article_text = article_content.get_text()

 # Genera laudio TSS
 response = openai.OpenAI(api_key="ciuppaNonLascioIlMio").audio.speech.create(
     model="tts-1",
     voice="alloy",
     input=article_text   
 )

 # Salva l'audio in un file MP3
 response.stream_to_file("articolo_mario64.mp3") 

 print("Contenuto scaricato con successo!")
```

Qua c'è il risultato finale

{{<center>}}
<iframe width="760" height="415" src="https://www.youtube.com/embed/tvQzAGsA41k?si=Qb_3G2yZz_s2apTV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
{{</center>}}

## 3. pensieri mei

Dopo tutta sta pappardella totalmente inutile, ma che ho fatto con il solo intento di provare a riscrivere codice in python e di usare Bing AI, arriviamo a quello che la mia mente a processato.

Ascoltando l'audio che mi è uscito  a fine esperimento non riesco a non pensare che questo non possa essere una bozza audio che un qualsiasi editor di un podcast che tratta notizie riceve in fase di montaggio... le pause, la parlantina, tutto... si capisce che sì, è fatto con un IA, ma nell'effettivo non è neanche fastidiosa come quella di gTTS (comunemente chiamata la voce di Trenitalia), ma anzi si ascolta anche volentieri.

Tempo fa mi ricordo che girava la voce “Eh facile fare podcast, ti metti davanti ad un microfono e spari cazate finchè non ti stufi”... beh qua siamo andati oltre.

Prendiamo ad esempio Rolling Stone. Vuole fare un podcast dove vengono raccontati gli articoli scritti del giorno, come fa? Sì può investire in doppiatori e speaker di qualità che raccontano le notizie... oppure può usare un mini script come questo, cambiare la voce ad ogni notizia ed il gioco e fatto.

Con queste 30 righe di codice, copiando gli articoli online, potrei o potresti creare un podcast giornalieri, anche di un ora, dove vengono raccontate le notizie di attualità. Non devi più sbatterti a parlare ed incepparti al microfono, basta che scrivi quello che vuoi dire e openAi fa il resto per te, poi un pò di tagli e di musica e tac, ecco una puntata pronta per essere pubblicata.

Il podcast, almeno per me, è sempre stato una prova. Per quanto leggevo articoli online, io ho iniziato il mio primissimo podcast con l'obbiettivo di parlare più lentamente e di riuscire a leggere ad alta voce senza impappinarmi.

Non erano pensieri e testi miei ok lo ammetto, ma lo dicevo all'inzio di ogni puntata che questo era un esercizio per me, ero io che mi mettevo alla prova nel parlare, nel leggere, nel sentire e nel registrare la mia voce.

Facendo così togliamo tutto questo. Togliamo il senso di sincerità che i podcaster, almeno quelli più piccoli, mettono all'interno di ogni episodio che registrano; togliamo il senso mettersi alla prova nel lavorare un audio e nel farlo uscire come vuoi te; togliamo l'anima e la voce umana dai podcast e li facciamo diventare (almeno per me) come i telegiornali, freddi e senza anima, il rumore di fondo che alla lunga ti infastidisce e che un giorno o l'altro lo spegnerai per sempre.