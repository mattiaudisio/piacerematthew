---
public: true
title: Usare Thunderbird come backup per le mail di Gmail
tags:
  - Angolo Tech
layout: ../../../layouts/MarkdownPostLayout.astro
slug: thunderbird-backup
pubDate: 2024-01-24
---

In questi anni ho notato una tendenza che trovo particolare. Nel mondo del lavoro, molte persone, in particolare nelle piccole imprese, tendono ad usare utilizzare la propria mail personale.<br />
Ora, lasciando da parte il dibattuto se questa scelta sia un ottima scelta _(non è un ottima scelta)_ oppure no _(cof. cof. **è una scelta di merda** cof. cof.)_, parliamo di un avvenimento capitato vicino a me ma che può essere d'aiuto a qualcuno... **il tuo account gmail ti segna 15GB su 15 GB utilizzati** (sì lo so può sembrare strano a qualcuno ma vi giuro che ho visto quella scritta con i miei occhi).<br />
In questi casi però il caro e vecchio “cancella tutte le mail” non può venirci in aiuto, dato che la suddetta mail viene usata per un lavoro in cui servono documenti e queste mail sono piene di documenti che servono. La soluzione che ti consiglio: fare un backup in locale.<br />

## Gmail

Cominciamo dalla parte più facile, Gmail. Mettiamo l'esempio che ti vuoi scaricare le mail di un determinato anno (ad esempio tutte le mail del 2022), come fare?<br />
Semplice. Selezioni tutte le mail ricevute nel 2022, clicchi su **“etichette”** _(Il simbolo che sembra una casa rovesciata in orizzontale)_, vai su **Crea Nuova**, la chiami 2022 e clicchi **Crea**.<br />
Ora, per scaricarla, basta andare sulla pagina di <a href="https://takeout.google.com/settings/takeout">Google Takeout</a>, Deselezionare tutto, andare alla voce **Posta**, cliccare su _“Tutti i dati della posta inclusi”_, togliere il flag a “Includi tutti i messaggi nella Posta” e deselezionare tutto. Successivamente basta solo flaggare la voce 2022, premere ok, andare il fondo alla pagina dove c'è il button “Passaggio successivo”, selezionare la grandezza dello zip e aspettare che Google mandi la mail con il link per scaricare questo zip.<br />

## Thunderbird

Come dice il <a href="https://www.thunderbird.net/it/">sito</a>, _Thunderbird è un'applicazione libera e gratuita per la gestione della posta elettronica_, ma molto probabilmente se sei qua a leggere questa pagina sai già cos'è.... allora andiamo subito al punto.<br />
Per aggiungere i file mbox a Thunderbird ci servirà un estensione, ImportExportTools NG, e per scaricarla ci basterà andare su Impostazioni _(La trovi in basso a sinistra)_, Componenti aggiuntivi _(Lo trovi in basso a sinistra)_, cercare <a href="https://addons.thunderbird.net/it/thunderbird/addon/importexporttools-ng/">ImportExportTools NG</a> e aggiungerlo a Thunderbird.<br />
Dopo averlo scaricato, basterà cliccare su **Cartelle locali** (Che trovi sotto le mail), anda re su ImportExportTools NG e, all'interno del menù a tendina che si apre, selezionare **importa file mbox**, dove potrete selezionare il vostro file MBOX.
<br /><br />
Fatto questo bisognerà aspettare Thunderbird che scarichi e sincronizzi il tutto (ci vorranno un paio di minuti) e voilà, ecco un bel backup in locale di tutte le vostre mail!