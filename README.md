# Dashboard Preselezioni Attive – Regione Lazio

Versione strumento **1.1**

Creatore: **Gabriele Ferri** — Service Designer  
Contatto: **gaferri@regione.lazio.it**

Applicazione web per consultare e analizzare le preselezioni attive pubblicate dalla Regione Lazio. La dashboard acquisisce i dati da un foglio Google Sheets pubblico, li elabora nel browser e offre filtri, indicatori, grafici, mappa ed elenco di dettaglio.

## Funzionalità

- Selettore rapido tra preselezioni Standard, Art. 22 o entrambe.
- Ricerca libera su identificativo, qualifica, mansioni, sede, azienda, CPI, tipologia e retribuzione.
- Filtri per:
  - provincia e comune della sede di lavoro;
  - Centro per l'Impiego (CPI);
  - collocamento mirato ai sensi della L. 68/99;
  - qualifica;
  - tipo di contratto e orario;
  - tipologia di preselezione, ricavata da `ModoEvasioneRichiesta`;
  - stato di pubblicazione;
  - scadenza delle candidature.
- Indicatori sintetici per preselezioni attive, lavoratori richiesti, preselezioni riservate e modalità di evasione della richiesta.
- Tooltip esplicativo per le preselezioni riservate a disabili art. 1 o categorie protette art. 18 della L. 68/99.
- Mappa interattiva dei comuni e delle province del Lazio.
- Grafici interattivi per provincia, qualifiche più richieste e tipologia di contratto offerto. Il grafico provinciale mostra le cinque province del Lazio e aggrega tutte le altre sedi in “Extra-Regione”.
- Elenco di dettaglio con contratto, retribuzione e relative note, scadenza, posti, azienda e tipologia di preselezione.
- Layout responsive con filtri disposti orizzontalmente sui monitor ampi; su schermi piccoli la tabella diventa un elenco di schede leggibili senza scorrimento orizzontale.
- Pannelli comprimibili e filtri applicabili anche tramite grafici e mappa.

## Dati utilizzati

La fonte principale è un CSV esportato dinamicamente da Google Sheets. I principali campi elaborati sono:

- `ID_Richiesta`, `TipoPreselezione`, `CPI`;
- `Qualifica`, `Mansioni`, `NumeroLavoratoriRichiesti`;
- `ProvinciaSedeLavoro`, `ComuneSedeLavoro`;
- `TipoContratto`, `TipoOrario`;
- `ModoEvasioneRichiesta`;
- `Retribuzione`, `Retribuzione_Note`;
- `CategoriaRiserva`;
- `DataInserimento`, `DataScadenza`, `StatoPubblicazione`;
- `Azienda`, `LinkPubblicazioneOfferta`.

I valori mancanti vengono normalizzati in fase di caricamento. Le URL delle offerte sono accettate solo se usano HTTPS.

## Indicatori e criteri

- **Preselezioni attive:** numero di righe risultanti dai filtri correnti.
- **Lavoratori richiesti:** somma di `NumeroLavoratoriRichiesti` sui risultati filtrati.
- **Preselezioni riservate:** annunci riconosciuti come riservati tramite `CategoriaRiserva`.
- **Tipologia di preselezione:** confronto fra modalità esplicitamente “con preselezione” e “senza preselezione” presenti in `ModoEvasioneRichiesta`.

Tutti gli indicatori e i grafici reagiscono ai filtri attivi.

## Tecnologia

Il progetto è una single-page application senza framework composta da:

- HTML, CSS e JavaScript;
- SheetJS per la lettura del CSV;
- Plotly.js per i grafici;
- Leaflet per la mappa;
- file GeoJSON locali con sorgente remota di riserva.

## Avvio locale

Servire la cartella tramite un web server locale, ad esempio:

```powershell
python -m http.server 8000
```

Aprire quindi `http://localhost:8000`. L'apertura diretta del file HTML può impedire il caricamento di alcune risorse a causa delle regole di sicurezza del browser.

## Privacy

I dati personali devono essere trattati esclusivamente per finalità istituzionali e nel rispetto della normativa vigente in materia di protezione dei dati personali.

## Novità della versione 1.1

- Sostituito il KPI delle scadenze ravvicinate con quello delle preselezioni riservate.
- Aggiunto il KPI “Tipologia di preselezione”.
- Aggiunti filtro e colonna basati su `ModoEvasioneRichiesta`.
- Aggiunte retribuzione e note retributive nell'elenco.
- Sostituito il grafico delle scadenze con il grafico dei contratti offerti.
- Imposti valori interi sull'asse quantitativo del grafico delle qualifiche.
- Migliorata la resa su smartphone.
- Inserito il footer istituzionale con versione dello strumento.
