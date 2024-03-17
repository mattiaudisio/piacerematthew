---
public: true
title: Come fare un Website Blocker con Python
tags:
  - Angolo Tech
layout: ../../layouts/MarkdownPostLayout.astro
slug: website-blocker
pubDate: 2022-08-16
---

Come creare un Website Blocker (un'applicazione che può essere usata per bloccare l'apertura di certi siti web) con Python e dargli anche una veste grafica grazie a tkinter. Questo è un programma molto utile per gli studenti che vogliono concentrarsi sugli studi e non vogliono altre distrazioni come i social media.<br /><br />

_Premessa_<br />
Prima di partire col progetto, bisogna abilitare i permessi di scrittura del file host, per questo, andare nel percorso _“C:\Windows\System32\drivers”_ e cambiare i permessi al file hosts.


## Parte 1: creiamo la grafica

Come prima cosa, creiamo il layout grafico del nostro progetto, così per avere una base da cui partire. Importiamo le librerie Python <a href="https://docs.python.org/3/library/tkinter.html">Tkinter</a> (per creare layout grafici) e <a href="https://pillow.readthedocs.io/en/stable/">PIL</a> (che aggiunge il supporto per l'apertura, la manipolazione e il salvataggio di diversi formati di file immagine), poi salviamoci dentro 2 variabili  la posizione del file hosts (_C:\Windows\System32\drivers\etc\hosts_) dando il permesso di scrittura e l'indirizzo Ip locale (127.0.0.1).<br /><br />

```

 from tkinter import *
 from PIL import Image, ImageTk

 hosts_path = r"C:\Windows\System32\drivers\etc\hosts"
 redirect_IP = "127.0.0.1"  # localhost's IP Address

```

Ora, sovente sono abituato a utilizzare classi e oggetti dell'OOP (programmazione ad oggetti) quando realizzo progetti con tkinter, e anche in questo caso ho scritto il codice seguendo questa mia abitudine, ma è opzionale come cosa.<br />
Creiamo la Classe Blocker, inizializzando gli attributi per creare tramite tkinter il “rettangolo” del programma, l'array in cui verranno inseriti i link da bloccare e i vari bottoni a lato con cui bloccare/sbloccare i siti.<br /><br />

```

 class Blocker:

     def __init__(self):
        # Create Window
        self.root = Tk()
        self.root.title('Python Website Blocker')
        self.root.geometry("500x350")
        self.root.configure(background='white')
        self.root.resizable(False, False)
        self.root.wm_iconphoto(False, ImageTk.PhotoImage(Image.open('img/favicon.png')))
        self.larghezza = self.root.winfo_screenwidth()
        self.site_to_block = []

        # Create Frame and Button
        self.frame1 = Frame(self.root, width=250, height=self.root.winfo_screenheight(), background='white')
        self.frame2 = Frame(self.root, width=250, height=self.root.winfo_screenheight(), background='white')
        self.frame1.grid(row=0, column=0, rowspan=2)
        self.frame2.grid(row=1, column=1, rowspan=2)

        # Create Image Column
        self.image = ImageTk.PhotoImage(file="img/img.png")
        self.label1 = Label(self.frame1, image=self.image, width=250, height=300, padx=5, background='white', pady=20)
        self.label1.grid(row=1, column=1)

        # Create Button
        self.button1 = Button(self.frame2, text="Blocca Social", width=30, height=5, command=self.blockSocial)
        self.button1.grid(row=0, column=0, padx=15, pady=15)
        self.button3 = Button(self.frame2, text="Blocca Tutto", width=30, height=5, command=self.blockAll)
        self.button3.grid(row=2, column=0, padx=15, pady=15)

```
<br />
Ora creiamo una funzione start, in modo che all'esecuzione del programma venga creata la finestra con i parametri settati in precedenza<br /><br />

```

 def start(self):
         self.root.mainloop()

```


## Parte 2: creiamo la funzioni

Come avrai notato, i tre bottoni permettono di bloccare tre tipi di siti: social networrk, siti porno, le due opzioni precedenti. Quindi ora la nostra attenzione deve concentrarsi su 3 importanti funzioni: blocca social, blocca porno, blocca tutto. Le 2 funzioni blocca social e blocca porno hanno al loro interno un array che contiene dei link (i siti da bloccare) e un controllo che modifica la scritta dei due bottoni da blocca * a sblocca * e, a seconda se il titolo del bottone a un testo o l'altro, vengono chiamate le funzioni per bloccare e sbloccare i siti. la funzione blocca tutto richiama le due funzioni citate prima<br /><br />

```

 def blockSocial(self):
    site = ['www.instagram.com', 'instagram.com', 'tiktok.com', 'www.tiktok.com', 'twitter.com']
    self.site_to_block.extend(site)
    if self.button1['text'] == "Blocca Social":
        self.button1.configure(text="Sblocca Social")
        self.block_websites()
    else:
        self.button1.configure(text="Blocca Social")
        self.unblock_website()


 def blockAll(self):
    if self.button3['text'] == "Blocca Tutto":
        self.blockSocial()
        self.button1.configure(text="Sblocca Social")
        self.button3.configure(text="Sblocca Tutto")
        self.block_websites()
    else:
        self.blockSocial()
        self.blockPorn()
        self.button1.configure(text="Blocca Social")
        self.button3.configure(text="Blocca Tutto")
        self.unblock_website()
        
```
<br />
Per finire, creiamo le due funzioni che creano il cuore di questo programma, le funzioni blockwebsites e unblockwebsites.<br />
La funzione blockwebsites, tramite l'array con i siti e dei for, scrive sul file host l'url del sito, mentre unblockwebsite li toglie.<br /><br />

```

 self.unblock_website()

 def block_websites(self):
 result = []
 for i in self.site_to_block:
   if i not in result:
    result.append(i)
 with open(hosts_path, 'r+') as hostfile:
 hosts_content = hostfile.read()
 for site in self.site_to_block:  # for site in  sites_to_block:
    if site not in hosts_content:
        hostfile.write(redirect_IP + ' ' + site + '\n')

 def unblock_website(self):
 with open(hosts_path, 'r+') as hostfile:
 lines = hostfile.readlines()
 hostfile.seek(0)
 for line in lines:
    if not any(site in line for site in self.site_to_block):
        hostfile.write(line)
    hostfile.truncate()

```
<br />
Per terminare, creiamo un oggetto Blocker e chiamiamo la funzione start.<br /><br />

```

 app = Blocker()
 app.start()

```

## Codice Completo

<br />

```

 from tkinter import *
 from PIL import Image, ImageTk

 hosts_path = r"C:\Windows\System32\drivers\etc\hosts"
 redirect_IP = "127.0.0.1"  # localhost's IP Address


 class Blocker:

    def __init__(self):
        # Create Window
        self.root = Tk()
        self.root.title('Python Website Blocker')
        self.root.geometry("500x350")
        self.root.configure(background='white')
        self.root.resizable(False, False)
        self.root.wm_iconphoto(False, ImageTk.PhotoImage(Image.open('img/favicon.png')))
        self.larghezza = self.root.winfo_screenwidth()
        self.site_to_block = []

        # Create Frame and Button
        self.frame1 = Frame(self.root, width=250, height=self.root.winfo_screenheight(), background='white')
        self.frame2 = Frame(self.root, width=250, height=self.root.winfo_screenheight(), background='white')
        self.frame1.grid(row=0, column=0, rowspan=2)
        self.frame2.grid(row=1, column=1, rowspan=2)

        # Create Image Column
        self.image = ImageTk.PhotoImage(file="img/img.png")
        self.label1 = Label(self.frame1, image=self.image, width=250, height=300, padx=5, background='white', pady=20)
        self.label1.grid(row=1, column=1)

        # Create Button
        self.button1 = Button(self.frame2, text="Blocca Social", width=30, height=5, command=self.blockSocial)
        self.button1.grid(row=0, column=0, padx=15, pady=15)
        self.button3 = Button(self.frame2, text="Blocca Tutto", width=30, height=5, command=self.blockAll)
        self.button3.grid(row=2, column=0, padx=15, pady=15)

    def start(self):
        self.root.mainloop()

    def blockSocial(self):
        site = ['www.instagram.com', 'instagram.com', 'tiktok.com', 'www.tiktok.com', 'twitter.com']
        self.site_to_block.extend(site)
        if self.button1['text'] == "Blocca Social":
            self.button1.configure(text="Sblocca Social")
            self.block_websites()
        else:
            self.button1.configure(text="Blocca Social")
            self.unblock_website()

    def blockAll(self):
        if self.button3['text'] == "Blocca Tutto":
            self.blockSocial()
            self.blockPorn()
            self.button1.configure(text="Sblocca Social")
            self.button3.configure(text="Sblocca Tutto")
            self.block_websites()
        else:
            self.blockSocial()
            self.blockPorn()
            self.button1.configure(text="Blocca Social")
            self.button3.configure(text="Blocca Tutto")
            self.unblock_website()

    def block_websites(self):
        result = []
        for i in self.site_to_block:
            if i not in result:
                result.append(i)
        with open(hosts_path, 'r+') as hostfile:
            hosts_content = hostfile.read()
            for site in self.site_to_block:  # for site in  sites_to_block:
                if site not in hosts_content:
                    hostfile.write(redirect_IP + ' ' + site + '\n')

    def unblock_website(self):
        with open(hosts_path, 'r+') as hostfile:
            lines = hostfile.readlines()
            hostfile.seek(0)
            for line in lines:
                if not any(site in line for site in self.site_to_block):
                    hostfile.write(line)
            hostfile.truncate()


 app = Blocker()
 app.start()

```

<br />
E questo è tutto. Ora hai il tuo website blocker personale!