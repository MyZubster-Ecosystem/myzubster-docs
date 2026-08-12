# Contributing to MyZubster Ecosystem

👽 **Grazie per il tuo interesse nel contribuire a MyZubster!**

Questo documento fornisce le linee guida per contribuire a qualsiasi repository dell'ecosistema MyZubster.

## 📋 Indice

1. [Codice di Condotta](#codice-di-condotta)
2. [Come Contribuire](#come-contribuire)
3. [Segnalare Bug](#segnalare-bug)
4. [Suggerire Miglioramenti](#suggerire-miglioramenti)
5. [Pull Request](#pull-request)
6. [Bounty System](#bounty-system)
7. [Automazione e AI](#automazione-e-ai)
8. [Linee Guida per il Codice](#linee-guida-per-il-codice)
9. [Documentazione](#documentazione)
10. [Licenza](#licenza)

---

## 📜 Codice di Condotta

Tutti i contributori devono rispettare il nostro [Codice di Condotta](CODE_OF_CONDUCT.md). Siamo impegnati a creare un ambiente inclusivo e rispettoso per tutti.

## 🤝 Come Contribuire

### 1. Trova un'issue

- Cerca issue con label `good-first-issue` per iniziare
- Cerca issue con label `help-wanted` per contributi urgenti
- Cerca issue con label `bounty` per contributi pagati in XMR/MYZ

### 2. Assegna l'issue

- Lascia un commento con `/claim` per richiedere l'assegnazione
- L'issue ti verrà assegnata automaticamente (se il bot è attivo)

### 3. Sviluppa

- Crea un branch con un nome descrittivo: `feature/nome-feature` o `fix/nome-bug`
- Segui le linee guida per il codice
- Aggiungi test se necessario

### 4. Invia una Pull Request

- Apri una Pull Request (PR) contro il branch `main`
- Descrivi cosa hai fatto e perché
- Collega l'issue risolta: `Closes #NUMERO_ISSUE`

## 🐛 Segnalare Bug

Usa il template di issue per segnalare bug:

**Titolo**: `[BUG] Breve descrizione`

**Corpo**:Descrizione

Descrizione chiara e concisa del bug.
Passi per riprodurre

    Vai su '...'

    Clicca su '....'

    Vedi l'errore

Comportamento atteso

Cosa dovrebbe succedere.
Screenshot

Se applicabile, aggiungi screenshot.
Ambiente

    OS: [es. Ubuntu 24.04]

    Browser: [es. Chrome 120]

    Versione: [es. v1.0.0]

text


## 💡 Suggerire Miglioramenti

**Titolo**: `[FEATURE] Breve descrizione`

**Corpo**:

Descrizione

Descrizione chiara e concisa della funzionalità.
Motivazione

Perché questa funzionalità è importante?
Soluzione proposta

Come potrebbe essere implementata?
Alternative considerate

Quali alternative sono state considerate?
text


## 📥 Pull Request

### Checklist PR

Prima di inviare una PR, assicurati che:

- [ ] Il codice segue le linee guida di stile
- [ ] Hai aggiunto test per le nuove funzionalità
- [ ] Tutti i test passano
- [ ] La documentazione è aggiornata
- [ ] Hai collegato l'issue risolta (`Closes #NUMERO`)

### Processo di Review

1. Un maintainer esaminerà la PR
2. Potrebbero essere richieste modifiche
3. Dopo l'approvazione, la PR verrà mergiata

## 🪙 Bounty System

MyZubster utilizza un sistema di bounty per incentivare i contributi.

### Tipi di Bounty

| Tipo | Ricompensa | Label |
|------|------------|-------|
| Bug Fix | 5-50 MYZ | `bounty-bug` |
| Feature | 10-100 MYZ | `bounty-feature` |
| Documentazione | 5-30 MYZ | `bounty-docs` |
| Testing | 5-20 MYZ | `bounty-test` |
| High Impact | 100+ MYZ | `bounty-high` |

### Come richiedere un bounty

1. Trova un'issue con label `bounty`
2. Lascia un commento con `/claim`
3. Descrivi il tuo approccio
4. Completa il lavoro
5. Invia la PR

### Pagamento

- I bounty vengono pagati in **MYZ** (token MyZubster)
- Il pagamento avviene dopo il merge della PR
- La fee di piattaforma è del 2%

## 🤖 Automazione e AI

Questo progetto utilizza automazione per gestire alcune attività.

### Bot Automatizzati

| Bot | Funzione |
|-----|----------|
| **Claim Bot** | Assegna automaticamente le issue claimate |
| **Bounty Bot** | Traccia e paga i bounty |
| **PR Bot** | Controlla automaticamente le PR |

### Come identificare i bot

- I bot lasciano commenti con un'icona 🤖
- I bot hanno account con nome `*-bot`
- I bot non richiedono risposta (sono automatizzati)

## 📝 Linee Guida per il Codice

### JavaScript/Node.js

- Usa `const` e `let`, evita `var`
- Usa template literals per le stringhe
- Aggiungi commenti per il codice complesso
- Segui le convenzioni di naming: `camelCase` per variabili e funzioni

### Python

- Segui PEP 8
- Usa type hints
- Aggiungi docstring

### Generale

- Scrivi codice leggibile e mantenibile
- Aggiungi test per le nuove funzionalità
- Aggiorna la documentazione

## 📚 Documentazione

La documentazione è fondamentale per MyZubster.

### Come contribuire alla documentazione

1. Cerca issue con label `documentation`
2. Aggiorna i file `README.md`
3. Aggiungi guide nella cartella `docs/`
4. Aggiorna la wiki di GitHub

### Struttura della documentazione

docs/
├── api/ # Documentazione API
├── guides/ # Guide per utenti
├── development/ # Guida per sviluppatori
└── legal/ # Documenti legali
text


## 📄 Licenza

Contribuendo a MyZubster, accetti che il tuo contributo sia rilasciato sotto la licenza MIT.

---

## 📞 Contatti

- **GitHub**: [MyZubster-Ecosystem](https://github.com/MyZubster-Ecosystem)
- **Email**: daniel@myzubster.io
- **Telegram**: @MyZubsterBot

---

*👽 Pytho dice: 'Grazie per il tuo contributo! Insieme rendiamo MyZubster più forte!'* 🚀🌿
