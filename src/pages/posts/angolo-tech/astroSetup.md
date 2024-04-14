---
public: true
title: Astro Framework Setup Tutorial
tags:
  - Angolo Tech
layout: ../../../layouts/MarkdownPostLayout.astro
slug: astro-setup
pubDate: 2022-10-06
---

Come installare il framework Astro all'interno del tuo sito web<br /><br />

Piccola guida sul come preparare il setup per realizzare il tuo sito web con il framework <a href="https://astro.build/">Astro</a>.<br /><br />

**Premessa** <br /><br />
Per utilizzare questo Framework, sarà necessario installare <a href="https://nodejs.org/en/">Node.js</a>. Cliccando su <a href="https://nodejs.org/en/">questo link</a> sarai renderizzato al sito ufficiali di Node.Js dove, cliccando sul pulsante con la versione LTS, scaricherai l'eseguibile per installarlo.<br />
Dopo aver cliccato sull'eseguibile scaricato e aver completato l'installazione di Node.JS, ti appariranno questi programmi:<br /><br />

<img src="https://raw.githubusercontent.com/mattiaudisio/piacerematthew/main/public/images/posts/node1.png">

Quello che è stato installato è Node.JS e, insiseme, è stato installato _Node.Js command prompt_, quello che ci servirà in questo tutorial.
Aprilo e appena ti appare il prompt, digita <u>node-v</u> e, il numero che ti apparirà, rappresenta la versione che hai appena installato di Node.JS.


## Parte 1: Crea il progetto

Bene, ora che Node è installato, possiamo partire con il set up di Astro.<br />
Come prima cosa, tenendo aprto il prompt, creiamo la cartella dove verrà creato il nostro sito web. Per comodità, ti consiglio di possizionare questa cartella nella direcotry Documents (in particolare creiamo una cartella dentro Documents dove tenere tutti i nostri lavori) quindi, tramite prompt di Node, andiamo a crearla.<br />
Come prima cosa digita il comdando <u>cd Documenti/</u> (o Documents se hai l'OS in inglese), poi tramite il comando <u>mkdir developer</u> creiamo una cartella chiamata developer, entriamoci dentro tramite il comando <u>cd developer/</u>.<br /><br />

**P.S.**<br />
mi raccomando nei nomi delle directory, dette anche cartelle, e dei file non dovrebbero andare gli spazi, al posto di quelli usa o un - o un _).
Ora, se andari dentro _Documenti_, troverai tutte le cartelle che hai creato:<br /><br />

<img src="https://raw.githubusercontent.com/mattiaudisio/piacerematthew/main/public/images/posts/node2.png">

<br /><br />
Ora, come ultimissima cosa prima di cominciare seriamente, ti faccio scaricare un Package Manager che può tornarti utile durante il lavoro, <a href="https://yarnpkg.com/">Yarn</a>. Quindi, sempre dal tuo prompt di Node, digita <u>npm i -g corepack</u> e aspetta che venga installato.<br />
Ora possiamo veramente cominciare

## Parte 2: Installa Astro

Ora che abbiamo la base su cui cominciare, è ora di far entrare in scena il protagonista di questa guida, Astro. Come si può vedere dal sito ufficiale di Astro per installare Astro avremo bisogno di nuovo del prompt di Node. A questo punto digita <u>npm create astro@latest</u>.<br />
A questo punto sarai dentro il “processo di installazione di Astro” (facciamo che chiamarlo così). La prima cosa che ti uscirà è mettere il nome del sito<br /><br />

```

 Welcome to Astro! (create-astro v1.1.0)
 Lets walk through setting up your new Astro project.
 ? Where would you like to create your new project? >> nomeDelSito

```
<br /><br />
Dopo il nome, ti verrà chiesto che template vorresti usare (se vuoi creare qualcosa da zero basterà cliccare su <u>Empty Project</u>). Per questo esempio useremo un template _Portfolio_, quindi va su e giù con le frecciete e premi invio per scegliere. Dopo aver copiato il Template nel progetto, Astro ti chiederà se vuoi utilizzare i pacchetti di npm; Non mi metterò qua a spiegarti <a href="https://it.wikipedia.org/wiki/Npm_(software)">cosa sono</a>, a te basta digitare Y. La stessa cosa la fai per Git. Infine ti chiederà che vuoi settare TypeScript, io ti consiglio Strict.<br />
Bene, a questo punto hai installato Astro dentro il tuo sito, veloce no come procedimento 😀<br />
Se sei ancora incerto che abbia installato qualcosa, vai dentro la cartella developer e guarda se ti ha creato una cartella con il nome che hai inserito; Altrimenti digita <u>cd nomeDelSito</u> e digita <u>yarn start</u>, ti è uscito una cosa del genere?<br /><br />

```

 yarn run v1.22.19
 $ astro dev
    astro  v1.4.2 started in 49ms
   ┃ Local    http://127.0.0.1:3000/
   ┃ Network  use --host to expose

```

<br /><br />
Se non ti è uscito... controlla cosa ti è uscito, perché di solito ti dice cosa c'è che non va (poi al massimo copia su Google l'errore che ti esce).
Se ti è uscito, bene! Ora apri il tuo browser e digita http://127.0.0.1:3000/ e Tac, ecco il tuo sito con il template di default.

**BUON DIVERTIMENTO!**
