# MyZubster — Roadmap delle app/integrations disponibili in ChatGPT

## Verifica

Questa lista riflette le integrazioni/app e plugin che risultano disponibili nel workflow ChatGPT corrente. Non equivale all'elenco completo delle app presenti nelle impostazioni personali dell'account: la disponibilità effettiva può dipendere da piano, workspace, ruolo, regione e autorizzazioni.

OpenAI indica che le app collegano ChatGPT a strumenti e dati esterni e che le autorizzazioni determinano quando ChatGPT può leggere o eseguire azioni. Dal 9 luglio 2026 la directory delle app è stata migrata nella directory dei plugin. 

## 01 — ChatGPT / Orchestrazione

**Ruolo:** centro operativo del progetto.

### Roadmap
1. Raccolta requisiti e contesto
2. Analisi e progettazione
3. Generazione documentazione e specifiche
4. Coordinamento delle integrazioni
5. QA e controllo coerenza
6. Preparazione di release e decisioni

**Output:** decisioni, brief, specifiche, analisi, prompt, QA.

## 02 — GitHub

**Ruolo:** source of truth per codice e documentazione.

### Roadmap
1. Struttura repository
2. Architecture & security docs
3. Roadmap e visual-production docs
4. Issues e PR per l'implementazione
5. CI/QA e release evidence
6. Versionamento degli asset/documenti

**Output:** repository, commit, issue, PR, documentazione versionata.

## 03 — Slack

**Ruolo:** comunicazione operativa e coordinamento.

### Roadmap
1. Individuazione dei canali rilevanti
2. Organizzazione di decisioni e discussioni
3. Thread per follow-up e review
4. Canvas per informazioni durevoli
5. Aggiornamenti di milestone/release
6. Collegamento Slack ↔ GitHub ↔ documentazione

**Output:** decisioni, aggiornamenti, thread, Canvas, coordinamento.

## 04 — Canva

**Ruolo:** produzione visuale.

### Roadmap
1. Visual foundation
2. Core product story
3. Technical architecture diagrams
4. Roadmap screens
5. Social adaptations
6. Visual QA e asset library

**Output:** design editabili, infografiche, social asset, diagrammi.

## 05 — Data Analytics

**Ruolo:** analisi quantitativa, KPI, dashboard e report.

### Roadmap
1. Data quality e definizioni metriche
2. KPI framework
3. Diagnostica dei movimenti
4. Dashboard/report
5. Validazione analitica
6. Monitoring continuo

**Output:** KPI, analisi, dashboard, report e notebook riproducibili.

## 06 — Public Equity Investing

**Ruolo:** workflow specializzato per ricerca e analisi di società quotate.

### Roadmap
1. Company research / tearsheet
2. Financial normalization
3. Earnings analysis
4. Comps / valuation
5. DCF e operating models
6. Thesis, catalysts, scenarios e risk management

**Output:** tearsheet, modelli, valuation, earnings notes, thesis e risk analysis.

## 07 — Sales

**Ruolo:** workflow commerciale e customer-facing.

### Roadmap
1. Account/company research
2. Meeting preparation
3. Deal strategy
4. Competitive/business case analysis
5. Follow-up e customer evidence
6. Forecast e leadership reporting

**Output:** meeting briefs, account plans, business cases, competitive briefs, follow-up, forecast.

## 08 — Plugin Management

**Ruolo:** gestione dell'ecosistema di integrazioni e autorizzazioni.

### Roadmap
1. Discovery delle integrazioni
2. Verifica dipendenze
3. Controllo permessi
4. Installazione/disconnessione quando richiesto
5. Governance delle autorizzazioni
6. Audit del workflow

**Output:** inventario, dipendenze, configurazione e controllo accessi.

## Operating model

```text
                         CHATGPT
                    orchestration / QA
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
       GITHUB            SLACK            CANVA
     source of truth   coordination      visual layer
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                 DATA / BUSINESS LAYERS
                 ┌─────────┴─────────┐
                 ▼                   ▼
          DATA ANALYTICS       SALES / EQUITY
```

## Regola di utilizzo

- ChatGPT coordina e ragiona.
- GitHub conserva la fonte versionata.
- Slack conserva il contesto operativo e le decisioni di team.
- Canva conserva la fonte visuale editabile.
- Data Analytics valida numeri e KPI.
- Sales gestisce workflow commerciali.
- Public Equity Investing gestisce workflow di ricerca finanziaria.
- Plugin Management governa integrazioni e autorizzazioni.

## Stato

**Disponibili nel workflow corrente:** ChatGPT, GitHub, Slack, Canva, Data Analytics, Public Equity Investing, Sales, Plugin Management.

**Nota:** una capacità disponibile nel workflow non significa necessariamente che ogni account/app sia connesso o che ogni azione abbia permessi di scrittura. Le autorizzazioni effettive vanno verificate nelle impostazioni dell'app/plugin.
