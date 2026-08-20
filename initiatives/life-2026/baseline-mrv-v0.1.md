# MyZubster LIFE 2026 — Baseline & MRV v0.1

> **Status: WORKING DRAFT.** This document is incomplete, contains candidate roles and planning assumptions, and does not constitute a partnership, commitment, approved budget, funding decision, or final LIFE application.

> Imported from the MyZubster LIFE 2026 working folder on 19 August 2026. Personal contact details are redacted.

Documento operativo preliminare | Stato: pre-candidatura

Valori non ancora supportati da dati reali: TBD — da misurare/validare.

## 1. SCOPO

Definire il sistema di baseline, monitoraggio, reporting e verifica (MRV) del pilot MyZubster LIFE 2026. Il documento deve consentire di confrontare in modo trasparente la situazione iniziale con i risultati ottenuti dopo gli interventi, mantenendo tracciabilità di fonti, assunzioni e prove.

Catena di evidenza:

BASELINE → INTERVENTO → MONITORAGGIO → CALCOLO KPI → VERIFICA → RISULTATO → REPLICAZIONE.

## 2. PRINCIPI MRV

- Nessun valore ambientale viene assunto senza una fonte identificabile.

- I dati mancanti restano TBD fino a misurazione o validazione.

- Ogni KPI deve avere unità, formula, fonte, frequenza, responsabile e prova associata.

- I confronti prima/dopo devono essere normalizzati quando meteo, superficie, durata o intensità operativa rendono non comparabili i periodi.

- Dati manuali e dati IoT devono essere distinguibili.

- Correzioni, esclusioni e anomalie devono restare nell'audit trail.

- La metodologia finale deve essere validata con il partner scientifico/ambientale.

## 3. UNITÀ DI ANALISI DEL PILOT

Sito pilota: TBD

Titolare/gestore sito: TBD

Partner operativo: TBD

Superficie interessata (m²/ha): TBD

Tipologia di verde/attività: TBD

Periodo baseline: TBD

Periodo dimostrativo: TBD

Tecnologie/sensori installati: TBD

Metodo di confronto: prima/dopo e, se possibile, area/intervento di controllo.

## 4. BASELINE — ACQUA

Dati da acquisire:

- volume totale d'acqua utilizzato (m³);

- volume per singolo intervento (L o m³);

- superficie servita (m²/ha);

- fonte dell'acqua;

- data, ora e durata irrigazione/intervento;

- precipitazioni e condizioni meteo pertinenti;

- umidità del suolo, se disponibile;

- tipologia vegetazione e fabbisogno operativo;

- perdite/anomalie note;

- modalità attuale di decisione dell'intervento.

KPI candidati:

KPI-A1 = m³ acqua / ha / periodo.

KPI-A2 = litri acqua / intervento.

KPI-A3 = % risparmio idrico normalizzato rispetto alla baseline.

KPI-A4 = numero interventi evitati o ottimizzati senza deterioramento dell'esito operativo.

Baseline A1-A4: TBD.

Target: TBD — definire solo dopo baseline e validazione tecnica.

## 5. BASELINE — OPERAZIONI

Dati:

- numero interventi per periodo;

- ore-persona;

- ore-mezzo/macchina;

- km percorsi quando pertinenti;

- durata media intervento;

- chiamate/interventi straordinari;

- guasti o anomalie;

- attività di manutenzione preventiva/correttiva.

KPI candidati:

KPI-O1 = interventi / ha / periodo.

KPI-O2 = ore operative / ha.

KPI-O3 = % riduzione interventi non necessari.

KPI-O4 = % riduzione anomalie o interventi straordinari, se causalmente attribuibile al pilot.

Baseline e target: TBD.

## 6. BASELINE — MATERIALI E CIRCOLARITÀ

Dati:

- componenti/materiali sostituiti;

- massa o quantità per tipologia;

- motivo della sostituzione;

- componenti riparati;

- componenti riutilizzati;

- durata utile stimata/osservata;

- rifiuti generati e destinazione, quando documentabile;

- acquisti di ricambio pertinenti.

KPI candidati:

KPI-C1 = kg o unità di componenti/materiali evitati come rifiuto.

KPI-C2 = % componenti riparati/riutilizzati sul totale pertinente.

KPI-C3 = aumento documentato della vita utile.

KPI-C4 = riduzione delle sostituzioni rispetto alla baseline normalizzata.

Baseline e target: TBD.

## 7. BASELINE — ENERGIA ED EFFETTI INDIRETTI

Misurare l'energia aggiuntiva richiesta da sensori, gateway, comunicazioni, elaborazione o eventuale automazione, evitando di presentare un beneficio ambientale senza contabilizzarne gli oneri pertinenti.

Dati:

- consumo sensori/gateway (kWh);

- energia di eventuali attuatori/robotica (kWh);

- sostituzioni batterie;

- eventuale energia/combustibile evitato nelle operazioni, se dimostrabile.

KPI-E1 = kWh aggiuntivi del sistema / periodo.

KPI-E2 = energia netta evitata o aggiunta, se calcolabile con metodologia validata.

Baseline e target: TBD.

## 8. QUALITÀ DEL DATO

Per ogni flusso registrare:

- data source ID;

- proprietario/responsabile del dato;

- metodo di acquisizione: sensore/API/manuale/documentale;

- frequenza;

- unità;

- timestamp;

- completezza;

- validazione;

- anomalie/outlier;

- versione/calibrazione sensore quando applicabile;

- autorizzazioni e restrizioni d'uso.

KPI-D1 = % record completi.

KPI-D2 = % record validati.

KPI-D3 = % periodo coperto da dati utilizzabili.

KPI-D4 = numero di correzioni/anomalie documentate.

## 9. EVIDENZE

Evidenze ammissibili nel dossier MRV, in funzione del dato:

- letture contatore;

- export sensori/API;

- log MyZubster;

- registri intervento;

- ordini/manutenzioni/documenti tecnici;

- fotografie georeferenziate o datate quando appropriate;

- dataset meteo da fonte identificata;

- report del partner operativo;

- verbali di validazione scientifica/tecnica;

- metodologia e fogli di calcolo versionati.

## 10. NORMALIZZAZIONE

Prima di dichiarare un miglioramento valutare almeno:

- superficie;

- numero/giorni di attività;

- precipitazioni e temperatura;

- stagionalità;

- tipologia di vegetazione/processo;

- variazioni infrastrutturali indipendenti dal progetto;

- guasti o eventi eccezionali.

Formula generale del miglioramento:

Miglioramento % = ((Baseline normalizzata − Valore pilot normalizzato) / Baseline normalizzata) × 100.

La formula specifica di ogni KPI deve essere congelata prima della valutazione finale del pilot.

## 11. GOVERNANCE E RESPONSABILITÀ PROPOSTE

MyZubster: ingestion dati, data model, dashboard, audit trail, export e documentazione tecnica.

Partner operativo/pilot host: accesso al sito, registri operativi, verifica eventi e contestualizzazione dati.

Partner acqua/territorio: dati idrici e competenza tecnica dove pertinente.

Partner scientifico/universitario: protocollo baseline, normalizzazione, verifica formule e interpretazione risultati.

Partner ambientale/istituzionale: eventuale revisione metodologica e allineamento agli indicatori pertinenti.

Coordinator: controllo complessivo, reporting e coerenza con Grant Agreement/LPI.

Tutti i ruoli sono da confermare formalmente.

## 12. DATA REQUEST — FUTURA / PILOT OPERATIVO

Richiedere, se autorizzato:

- identificazione di 1–2 siti candidati;

- superficie e tipologia attività;

- calendario/frequenza irrigazione;

- consumi acqua storici disponibili;

- registri intervento e manutenzione;

- attrezzature e componenti pertinenti;

- criticità operative ricorrenti;

- disponibilità di almeno un referente tecnico.

## 13. DATA REQUEST — HERA/HERAMBIENTE

Solo in caso di interesse formale:

- casi d'uso coerenti con acqua/circolarità/risorse;

- dataset aggregabili e utilizzabili;

- metriche ambientali già adottate;

- processi di manutenzione/recupero/riuso pertinenti;

- sito o processo candidato alla replicazione;

- requisiti di data governance e sicurezza.

## 14. DATA REQUEST — CONSORZIO DI BONIFICA / ANBI

- disponibilità e origine dei dati idrici pertinenti;

- modalità di misura/contabilizzazione;

- stagionalità e vincoli di distribuzione;

- indicatori già utilizzati per efficienza idrica;

- possibili siti/casi di replicazione;

- variabili necessarie per una corretta normalizzazione.

## 15. DATA REQUEST — UNIVERSITÀ / ARPAE

Chiedere revisione di:

- disegno baseline;

- durata minima del periodo osservativo;

- selezione variabili confondenti;

- formule KPI;

- criteri di data quality;

- metodo di verifica statistica/tecnica;

- compatibilità con indicatori LIFE pertinenti.

16. REGISTRO KPI v0.1

A1 Acqua/ha — baseline TBD — target TBD — fonte TBD — owner TBD.

A2 Acqua/intervento — baseline TBD — target TBD — fonte TBD — owner TBD.

A3 Risparmio idrico normalizzato — baseline TBD — target TBD — fonte multipla — owner TBD.

O1 Interventi/ha — baseline TBD — target TBD.

O2 Ore operative/ha — baseline TBD — target TBD.

C1 Materiali/rifiuti evitati — baseline TBD — target TBD.

C2 Riparazione/riuso — baseline TBD — target TBD.

E1 Energia aggiuntiva sistema — baseline 0 per tecnologia non presente, da verificare — target TBD.

D1 Completezza dati — baseline TBD — target TBD.

D2 Validità dati — baseline TBD — target TBD.

## 17. GATE DI QUALITÀ PRIMA DEL PILOT

GO solo se:

- sito identificato e autorizzato;

- baseline disponibile o misurabile;

- almeno un KPI ambientale primario è quantificabile;

- fonte e ownership dei dati sono chiare;

- protocollo di misura è approvato;

- non esistono gap che impediscono il confronto prima/dopo.

HOLD se i dati sono parziali ma recuperabili entro tempi compatibili.

NO-GO per quel sito se non è possibile produrre una baseline credibile o attribuire il risultato all'intervento.

## 18. OUTPUT MRV PREVISTI

- Baseline Report v1.0;

- Data Dictionary;

- Measurement Protocol;

- KPI Register;

- Data Quality Log;

- Pilot Monitoring Dashboard;

- Verification Report;

- Replication Dataset/Toolkit, nei limiti di proprietà, privacy e sicurezza.

## 19. ALLINEAMENTO LIFE

Gli indicatori LIFE devono essere selezionati in funzione del sub-programma e dell'impatto effettivamente perseguito. Il progetto dovrà mantenere coerenza tra indicatori della proposta, Grant Agreement, dati raccolti e risultati dichiarati. Gli indicatori specifici MyZubster integrano, ma non sostituiscono, gli LPI obbligatori applicabili.

## 20. PROSSIME AZIONI P0

1. Identificare sito pilota e referente dati.

2. Ottenere almeno 6–12 mesi di dati storici se disponibili; in alternativa definire un periodo baseline prospettico tecnicamente sufficiente con il partner scientifico.

3. Validare KPI acqua e metodo di normalizzazione.

4. Definire Data Dictionary e schema sensori/API.

5. Confermare partner scientifico/ambientale.

6. Mappare i KPI MyZubster agli LPI applicabili della call definitiva.

7. Congelare Measurement Protocol prima dell'avvio del confronto sperimentale.

Nota metodologica: questo documento non costituisce una validazione scientifica né una dichiarazione di risultati ambientali già ottenuti. I target quantitativi saranno inseriti solo dopo disponibilità di dati e validazione del metodo.
