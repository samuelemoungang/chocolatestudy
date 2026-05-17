# The Chocolate Study — Landing Page

Sito vetrina per il progetto di Data Science (Module 376, HES-SO Valais 2026).

**Gruppo:** Samuele, Lydia, Noah
**Progetto 5:** Comparaison de barres chocolatées

---

## 📁 Struttura

```
chocolate-site/
├── public/
│   ├── index.html       ← landing page
│   ├── style.css        ← stile (estetica editoriale-luxe)
│   ├── notebook.html    ← placeholder, da sostituire col notebook esportato
│   ├── chocolate.mp4    ← (TU lo aggiungi) video di cioccolato in loop
│   └── poster.jpg       ← (opzionale) frame statico se il video non carica
├── vercel.json          ← config per deploy su Vercel
└── README.md            ← questo file
```

---

## 🎬 1. Aggiungere il video di cioccolato

Il file `chocolate.mp4` **non è incluso**. Devi scaricarlo tu (è meglio così, scegli quello che ti piace di più).

**Dove trovarlo gratis e senza copyright:**
- [Pexels — melting chocolate](https://www.pexels.com/search/videos/melting%20chocolate/)
- [Pixabay — chocolate](https://pixabay.com/videos/search/chocolate/)
- [Coverr](https://coverr.co/) — cerca "chocolate"

**Specifiche consigliate:**
- formato: `.mp4` (H.264)
- risoluzione: 1920×1080 o 1280×720
- durata: 10-20 secondi (va in loop)
- peso: **sotto i 5 MB** se possibile (Vercel ha limiti sul free tier — sotto i 100MB per file ma per performance tienilo leggero)
- consiglio: passalo da [HandBrake](https://handbrake.fr/) o ffmpeg per comprimerlo:
  ```bash
  ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -preset slow -an chocolate.mp4
  ```
  (`-an` toglie l'audio, che non serve)

Una volta scaricato, rinominalo `chocolate.mp4` e mettilo in `public/`.

**Poster (opzionale ma raccomandato):** un frame del video salvato come `poster.jpg`, sempre in `public/`. Si mostra mentre il video carica.

---

## 📓 2. Sostituire il notebook

Quando il notebook `.ipynb` è pronto, esportalo in HTML:

```bash
# nella cartella dove c'è il vostro .ipynb
jupyter nbconvert --to html chocolate_study.ipynb --output notebook.html

# poi copia notebook.html dentro public/ (sovrascrivendo il placeholder)
cp notebook.html /percorso/al/chocolate-site/public/notebook.html
```

**Tip:** se volete uno stile più carino dell'export di default, usate:
```bash
jupyter nbconvert --to html --template lab chocolate_study.ipynb --output notebook.html
```

Il `.ipynb` originale rimane vostro per modifiche — l'HTML è solo la "fotografia" pubblicata. Ogni volta che aggiornate il notebook, rigenerate l'HTML e fate un nuovo deploy.

---

## 🚀 3. Deploy su Vercel

**Opzione 1 — via GitHub (consigliata):**
1. Crea un repo su GitHub e fai push di questa cartella.
2. Vai su [vercel.com](https://vercel.com), accedi con GitHub.
3. "Add New Project" → seleziona il repo → Deploy.
4. Vercel rileva automaticamente che è un sito statico e serve la cartella `public/`.
5. Ogni volta che fate `git push`, Vercel ridepoya automaticamente.

**Opzione 2 — via CLI:**
```bash
npm i -g vercel
cd chocolate-site
vercel        # primo deploy (preview)
vercel --prod # deploy in produzione
```

**Dominio:** Vercel ti dà gratis un sottodominio tipo `chocolate-study.vercel.app`. Se vuoi un dominio custom, si compra a parte.

---

## 🎨 Personalizzazione veloce

**Cambiare il numero "1 795":** in `index.html` cerca `<span class="num">1&#8202;795</span>` e cambialo col numero reale di righe del dataset.

**Cambiare i nomi del gruppo:** in `index.html` cerca `<div class="signatures">`.

**Cambiare i colori:** in `style.css`, in cima trovi le CSS variables (`--cocoa-deep`, `--gold`, ecc). Modificate lì.

**Aggiungere sezioni:** la struttura è semplice (`<section>` con classe). Copiate la sezione `.about` come modello.

---

## 🧪 Test locale

Per vedere il sito prima di deployare:

```bash
cd chocolate-site/public
python3 -m http.server 8000
# poi apri http://localhost:8000 nel browser
```

Oppure con Node:
```bash
npx serve public
```

---

## ⚠️ Note importanti

- **Non c'è autenticazione.** Come ti ho spiegato, il sistema di login `@hes-so.ch` che descrivevi inizialmente è complicato da fare bene e fuori scope per un progetto di corso. Il notebook è pubblico in sola lettura — chiunque con il link può vederlo, ma nessuno può modificarlo (è HTML statico).
- **Il notebook online è statico.** Non è eseguibile. Se volete un notebook eseguibile dal browser, valutate [Google Colab](https://colab.research.google.com/) o [JupyterLite](https://jupyter.org/try-jupyter/lab/) — ma sono opzioni separate, non integrate qui.
- **Browser support:** il sito è testato su Chrome/Firefox/Safari moderni. Su Internet Explorer non funziona (ma nessuno lo usa più).

---

## 📝 Licenza

Codice del sito: libero per uso del gruppo. Dataset: rispettate la licenza originale del dataset Flavors of Cacao (vedi notebook per dettagli).
