# FxV v7 — consegna per revisione

Rapporto del 19 ottobre 2026. Versione preparata per revisione, non autorizzata alla pubblicazione.

## Base e rami esaminati

- Repository di lavoro: `https://github.com/pingsil-boom/FxV.git`.
- `origin/main`: `6f2671bf67a120eceade594b9024649f4fe45f13`. La home precedente aveva il documento cookie chiamato `Cookies` e mancava `privacy.html`.
- `origin/modulo-contatti-formspree`: `4de75a36b5f1918d58c6cd07db569667458b9917`. Contiene form Formspree, informative effettive, navigazione e modali accessibili. È la base scelta per la v7.
- Repository originale consultato solo in lettura: `FxVlapotenzadelmovimento/FxV`, unico ramo remoto `main`, `17a9f47a826f33fb1da177bb02d074c113711636`. Nessuna modifica eseguita su quel repository.
- Nuovo ramo locale: `release/v7-pubblicazione`, creato dalla base Formspree. Nessun merge e nessuna pubblicazione.

## Modifiche

| File | Intervento |
| --- | --- |
| `index.html` | Integrazione del prototipo allegato v7: grafica, sfondo, fotografie, testi, disposizione, navigazione, modali e barra mobile. Nelle card solo Federico e Valerio; nelle presentazioni nomi completi. Biografie identiche al v7. Favicon ricavata dal logo esistente per eliminare un 404. |
| `assets/v7/fonts.css` | Definizioni tipografiche estratte dal prototipo senza modificarne pesi, intervalli Unicode e ordine. |
| `assets/v7/font-*.woff2` (12 file) | Font Inter e Montserrat già incorporati nel prototipo, conservati senza modifiche binarie e senza richieste esterne per i caratteri. |
| `assets/v7/photo-170351de7c38.jpg` | Fotografia introduttiva estratta dal prototipo, senza ricompressione. |
| `assets/v7/INTER-OFL.txt`, `assets/v7/MONTSERRAT-OFL.txt` | Licenze ufficiali per la distribuzione locale dei font. |
| `VERIFICA-V7.md` | Questo rapporto. |

`privacy.html`, `cookie.html`, `fxv-social-preview.jpg` e le fotografie preesistenti sono ereditati dalla base Formspree e non modificati. Rispetto a `main`, la base porta anche la rinomina `Cookies` → `cookie.html` e l'aggiunta dell'informativa privacy e dell'immagine social.

Le informative incorporate nel prototipo coincidono con quelle del ramo Formspree. Nella versione del sito i collegamenti aprono i veri file HTML, senza il meccanismo Blob usato dal prototipo autonomo. Nessun framework, pacchetto di produzione o processo di build aggiunto.

## Funzionamento preservato

- Endpoint: `https://formspree.io/f/xqpeyzzz`, metodo `POST`, corpo `FormData`, intestazione `Accept: application/json`.
- Campi: `nome`, `email`, `macroarea`, `messaggio`, `presa_visione_privacy`; valori tecnici `performance`, `salute`, `info` e `si` invariati. Requisiti di compilazione invariati.
- Gestore JavaScript dell'invio identico al ramo Formspree, inclusi validazione, disabilitazione del pulsante, messaggi di esito, reset e gestione degli errori.
- Barra Chiama/Scrivici fino a 740 px, spazio inferiore riservato, safe area e occultamento durante il focus nel modulo come nel v7. Modali sopra la barra.
- URL canonical e immagine social mantenuti sull'indirizzo originale previsto dal prototipo. Confermare l'URL definitivo prima della pubblicazione.

## Test realmente eseguiti

Suite locale con Chromium 154, Playwright già disponibile nell'ambiente e axe-core 4.10.3 usato esclusivamente per i test. Servizio HTTP locale su percorso `/FxV/`, poi arrestato.

- **99/99 controlli della suite browser superati**: navigazione desktop e mobile, CTA, apertura e chiusura menu, Escape, clic esterno, ridimensionamento, apertura delle due modali da tastiera e mouse, Tab/Shift+Tab, ritorno del focus, pulsanti di chiusura, collegamenti privacy/cookie e ritorno alla home.
- **Confronto visivo dell'intera pagina** a 320, 375, 390, 740, 741, 768, 1024 e 1440 px: immagini pixel per pixel identiche al v7 dopo aver abbreviato i nomi delle card nella sola copia di confronto. File allegato originale lasciato intatto; animazioni disabilitate per stabilizzare le schermate.
- Nessun overflow orizzontale alle otto larghezze. Immagini decodificate correttamente. Tutti i collegamenti interni a sezioni e documenti locali risolti.
- Form: campi vuoti, email invalida e privacy non selezionata bloccano l'invio. Richiesta multipart intercettata e verificata per endpoint, metodo, intestazione e campi. Successo 200, errori 422/500 e rete assente **simulati**: messaggi, reset al successo, conservazione dati all'errore e ripristino pulsante verificati.
- **Zero violazioni automatiche axe** su home mobile, home desktop, entrambe le modali, privacy e cookie. La home e le modali hanno verifiche incomplete di contrasto su sfondi complessi e di attributi ARIA che richiedono valutazione manuale: il risultato non equivale a una certificazione di accessibilità.
- Nessun errore JavaScript o HTTP inatteso. Gli errori di rete prodotti intenzionalmente dai test del form sono registrati separatamente.
- Controlli di integrità: CSS visivo e biografie identici al v7; 19 asset binari unici riprodotti byte per byte; informative, contratto tecnico dei campi e gestore invio invariati rispetto alla base Formspree. `git diff --check` senza errori.
- **18/18 controlli supplementari superati**, comprendenti le verifiche di integrità sopra, animazione normale e preferenza di riduzione movimento, entrambe le modali a 390 px con testo finale raggiungibile e livello superiore alla barra, e pulsante disabilitato durante l'attesa di un invio simulato.

Il rapporto JSON e gli script dei controlli sono inclusi negli allegati di consegna. I test usano risposte simulate e non trasmettono richieste al servizio Formspree reale.

## Questioni prima della pubblicazione e verifiche manuali

1. **ACSI: blocco editoriale esplicito.** Il diploma nominativo di Federico e la formulazione della dicitura ACSI devono ancora essere verificati. La frase è conservata fedelmente nella biografia e non va considerata definitivamente approvata. Il commento `BOZZA NON PUBBLICARE` resta nel codice. Verificare anche gli altri titoli dichiarati, incluso il Master di Valerio, sulla documentazione dei professionisti.
2. **Immagini e diritti.** Nessun asset mancante o alterato. Il repository e il prototipo non forniscono una documentazione completa delle licenze fotografiche, delle liberatorie dei soggetti e dei diritti sul logo. Confermare i diritti per tutte le fotografie, inclusa l'immagine di pallavolo e quella introduttiva estratta dal prototipo; la presenza di una foto nei file non ne prova l'autorizzazione. Le licenze OFL dei font sono allegate; la provenienza delle immagini resta da documentare.
3. **Contenuti legali.** Informative conservate, non validate legalmente. Confermare titolare Valerio Pignalosa Conti, accesso alla casella condivisa da entrambi i professionisti, conservazione fino a sei mesi e ruolo/trasferimenti dei fornitori, soprattutto Formspree. Le informative menzionano il caricamento tramite Google Fonts, mentre questa v7 usa i font locali già presenti nel prototipo: serve una revisione legale coerente con il sito effettivo. Nessuna modifica autonoma ai testi legali.
4. **Invio reale e recapiti.** Effettuare una prova concordata con dati non sensibili: accettazione dell'endpoint, ricezione nella casella corretta e risposta al mittente. Non eseguita qui. Verificare anche telefono e avvio del client email su dispositivo: i relativi URI sono stati controllati, ma non è stata effettuata una chiamata o spedita un'email.
5. **Dispositivi e accessibilità manuale.** Provare Safari/iPhone, Android reale e Firefox; tastiera virtuale, rotazione, notch/safe area, zoom elevato, lettore di schermo, contrasto sugli sfondi complessi e correttezza delle descrizioni delle immagini. I test desktop con viewport ridotte non sostituiscono dispositivi fisici o tecnologie assistive.
6. **Revisione finale del proprietario.** Verificare anteprima, testi, immagini e dominio previsto. La v7 è tecnicamente preparata per la revisione, ma resta sospesa dalla pubblicazione fino alla risoluzione delle questioni sopra e all'approvazione finale dell'utente.

## Anteprima e riproduzione

L'HTML autonomo allegato alla consegna contiene gli stessi asset della versione finale e una copia incorporata delle informative per consentirne la consultazione aprendo un singolo file. Il pacchetto ZIP contiene invece il sito con le vere pagine separate. Non è stato creato un URL pubblico o un hosting di anteprima.

Per eseguire il sito dal checkout o dalla cartella ZIP estratta: `python -m http.server 8000`, poi aprire `http://localhost:8000/`. Il sito non richiede compilazione. Prima di una prova effettiva dell'invio, concordare il test con chi riceve le richieste.
