# Guida: Come costruire un orto idroponico NFT sul terrazzo con Arduino

*Integra i tuoi dati con MyZubster per monitoraggio in tempo reale*

---

## 1. Introduzione

L'idroponica NFT (Nutrient Film Technique) è un metodo di coltivazione senza terra dove le radici delle piante sono sospese in un flusso sottile di soluzione nutritiva. Costruire un sistema NFT sul terrazzo ti permette di:

- Coltivare verdure fresche tutto l'anno in spazi ridotti
- Risparmiare fino al 90% d'acqua rispetto all'agricoltura tradizionale
- Monitorare parametri critici (pH, EC, temperatura) in tempo reale

**Integrazione con MyZubster**: Collegando il tuo Arduino alla piattaforma MyZubster, i dati dei sensori vengono inviati automaticamente al tuo giardino virtuale, permettendoti di:
- Visualizzare grafici storici su web/app
- Ricevere alert se i parametri escono dai range ottimali
- Condividere i dati con la community per consigli

---

## 2. Lista Materiali

### Elettronica
| Componente | Quantità | Note |
|------------|----------|------|
| Arduino Uno / Nano / ESP32 | 1 | ESP32 consigliato per WiFi integrato |
| Sensore pH analogico (es. Gravity pH Meter v2) | 1 | Range 0-14, calibrazione 2 punti |
| Sensore EC analogico (es. Gravity EC Meter) | 1 | Range 0-20 mS/cm |
| Sensore Temperatura/Umidità DHT22 (AM2302) | 1 | Più preciso del DHT11 |
| Modulo WiFi ESP8266 (se usi Arduino Uno/Nano) | 1 | Non necessario con ESP32 |
| Breadboard + cavi jumper | Assortito | |
| Alimentatore 12V 2A (per pompa + Arduino) | 1 | |
| Relè 5V (per controllare pompa) | 1 | Opzionale, per automazione |

### Idraulica NFT
| Componente | Quantità | Note |
|------------|----------|------|
| Tubi PVC 50-75mm (canali di crescita) | 2-4 metri | Inclinazione 1-2% |
| Tubi flessibili 12mm (irrigazione) | 3-5 metri | |
| Pompa sommersa 12V 300-500 L/h | 1 | Flusso continuo sottile |
| Serbatoio 20-50L (contenitore opaco) | 1 | Per soluzione nutritiva |
| Vaschette retinate / net pots 50mm | 10-20 | Per piantine |
| Argilla espansa / lana di roccia | 5-10L | Substrato inerte |
| Gomiti PVC 90° + T | Assortito | Per circuito chiuso |

### Strumenti
- Trapano + fresa per fori net pots (50mm)
- Sega per PVC
- Metro, livello a bolla
- Cacciaviti, pinze
- Multimetro (per test sensori)

---

## 3. Schema Elettrico

```
                    ARDUINO / ESP32
                  ┌─────────────────┐
    ┌────────────│ A0 (pH Sensor)   │
    │            │ A1 (EC Sensor)  │
    │            │ D2  (DHT22)     │
    │            │ D3  (Relè Pompa)│
    │            │ 3.3V/5V         │
    │            │ GND             │
    │            └────────┬────────┘
    │                     │
    │    ┌────────────────┼────────────────┐
    │    │                │                │
    ▼    ▼                ▼                ▼
┌─────────┐         ┌─────────┐      ┌─────────┐
│ Sensore │         │ Sensore │      │  DHT22  │
│   pH    │         │   EC    │      │         │
│  A0     │         │  A1     │      │   D2    │
└────┬────┘         └────┬────┘      └────┬────┘
     │                   │                 │
     │        5V/GND     │        3.3V/GND │
     └────────┬──────────┴────────┬───────┘
              │                  │
         ┌────┴────┐        ┌────┴────┐
         │ Alimentazione     │ Alimentazione
         │  Condivisa        │  Condivisa
         └─────────┘        └─────────┘

         ┌─────────────────────────────────┐
         │         RELÈ 5V (D3)            │
         │  ┌─────┐        12V ──────────┐ │
         │  │ COM │──────────────────────►│ │
         │  │ NO  │──────► POMPA 12V      │ │
         │  └─────┘        GND ──────────┘ │
         └─────────────────────────────────┘
```

### Collegamenti Dettagliati

**Sensore pH (Gravity v2):**
- VCC → 5V (Arduino)
- GND → GND
- Signal → A0

**Sensore EC (Gravity):**
- VCC → 5V
- GND → GND
- Signal → A1

**DHT22:**
- VCC → 3.3V (o 5V)
- GND → GND
- Data → D2 (con resistenza pull-up 4.7kΩ tra Data e VCC)

**Relè Pompa:**
- VCC → 5V
- GND → GND
- IN → D3
- COM → 12V+ (alimentatore)
- NO → Pompa+
- Pompa- → 12V- (alimentatore)

---

## 4. Codice Arduino

### Librerie Necessarie
```bash
# Arduino IDE → Sketch → Include Library → Manage Libraries
# Installa:
# - "DHT sensor library" by Adafruit
# - "Adafruit Unified Sensor"
# - "ArduinoJson" (per JSON payload)
# - "WiFi" / "WiFiClientSecure" (built-in ESP32)
# - "HTTPClient" (built-in ESP32)
```

### Sketch Completo

```cpp
/*
 * MyZubster Hydroponic Monitor
 * Legge pH, EC, Temperatura, Umidità e invia a MyZubster Gateway
 * 
 * Hardware: ESP32 (consigliato) o Arduino + ESP8266
 * Sensori: Gravity pH, Gravity EC, DHT22
 */

#include <ArduinoJson.h>
#include <DHT.h>
#include <WiFi.h>
#include <HTTPClient.h>

// ================= CONFIGURAZIONE =================
// WiFi
const char* WIFI_SSID = "TUA_RETE_WIFI";
const char* WIFI_PASSWORD = "TUA_PASSWORD";

// MyZubster Gateway
const char* GATEWAY_URL = "https://api.myzubster.example.com";  // Cambia con URL reale
const char* GARDEN_ID = "garden_001";  // Il tuo garden ID da MyZubster
const char* API_TOKEN = "TUO_JWT_TOKEN";  // Token JWT da MyZubster

// Sensori
#define PH_PIN        A0
#define EC_PIN        A1
#define DHT_PIN       2
#define RELAY_PIN     3

#define DHT_TYPE      DHT22

// Calibrazione pH (calibrare con soluzioni pH 4.0, 7.0, 10.0)
const float PH_CALIBRATION_SLOPE = -5.70;  // Da calibrare
const float PH_CALIBRATION_OFFSET = 21.34; // Da calibrare

// Calibrazione EC
const float EC_CALIBRATION_K = 1.0;  // Costante di cella, da calibrare

// Timing
const unsigned long SEND_INTERVAL = 60000;  // Invia ogni 60 secondi
const unsigned long READ_INTERVAL = 5000;   // Leggi sensori ogni 5 secondi

// ================= VARIABILI GLOBALI =================
DHT dht(DHT_PIN, DHT_TYPE);

float phValue = 0.0;
float ecValue = 0.0;
float temperature = 0.0;
float humidity = 0.0;

unsigned long lastSendTime = 0;
unsigned long lastReadTime = 0;

bool wifiConnected = false;

// ================= SETUP =================
void setup() {
  Serial.begin(115200);
  delay(1000);
  
  Serial.println(F("\n=== MyZubster Hydroponic Monitor ==="));
  Serial.println(F("Inizializzazione..."));
  
  // Pin
  pinMode(RELAY_PIN, OUTPUT);
  digitalWrite(RELAY_PIN, LOW);  // Pompa spenta di default
  
  // Sensori
  dht.begin();
  
  // WiFi
  connectWiFi();
  
  Serial.println(F("Setup completato!"));
  Serial.println(F("====================================\n"));
}

// ================= LOOP PRINCIPALE =================
void loop() {
  unsigned long now = millis();
  
  // Lettura sensori
  if (now - lastReadTime >= READ_INTERVAL) {
    readSensors();
    lastReadTime = now;
  }
  
  // Invio dati a MyZubster
  if (now - lastSendTime >= SEND_INTERVAL) {
    if (wifiConnected) {
      sendDataToMyZubster();
    } else {
      connectWiFi();  // Tentativo riconnessione
    }
    lastSendTime = now;
  }
  
  // Controllo pompa (esempio: accendi 1 min ogni 10 min)
  static unsigned long pumpLastToggle = 0;
  static bool pumpState = false;
  if (now - pumpLastToggle >= (pumpState ? 60000 : 600000)) {
    pumpState = !pumpState;
    digitalWrite(RELAY_PIN, pumpState ? HIGH : LOW);
    Serial.print(F("Pompa: "));
    Serial.println(pumpState ? F("ACCESA") : F("SPENTA"));
    pumpLastToggle = now;
  }
  
  delay(100);
}

// ================= FUNZIONI SENSORI =================
void readSensors() {
  // --- pH ---
  int phRaw = analogRead(PH_PIN);
  float phVoltage = phRaw * (3.3 / 4095.0);  // ESP32: 12-bit ADC, 3.3V
  phValue = PH_CALIBRATION_SLOPE * phVoltage + PH_CALIBRATION_OFFSET;
  
  // --- EC ---
  int ecRaw = analogRead(EC_PIN);
  float ecVoltage = ecRaw * (3.3 / 4095.0);
  ecValue = ecVoltage * EC_CALIBRATION_K;  // Semplificato
  
  // --- DHT22 ---
  float newTemp = dht.readTemperature();
  float newHum = dht.readHumidity();
  
  if (!isnan(newTemp) && !isnan(newHum)) {
    temperature = newTemp;
    humidity = newHum;
  } else {
    Serial.println(F("Errore lettura DHT22"));
  }
  
  // Debug output
  Serial.print(F("pH: ")); Serial.print(phValue, 2);
  Serial.print(F(" | EC: ")); Serial.print(ecValue, 2); Serial.print(F(" mS/cm"));
  Serial.print(F(" | T: ")); Serial.print(temperature, 1); Serial.print(F("°C"));
  Serial.print(F(" | H: ")); Serial.print(humidity, 1); Serial.println(F("%"));
}

// ================= WIFI =================
void connectWiFi() {
  if (WiFi.status() == WL_CONNECTED) {
    wifiConnected = true;
    return;
  }
  
  Serial.print(F("Connessione WiFi..."));
  WiFi.mode(WIFI_STA);
  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  
  int attempts = 0;
  while (WiFi.status() != WL_CONNECTED && attempts < 20) {
    delay(500);
    Serial.print(F("."));
    attempts++;
  }
  
  if (WiFi.status() == WL_CONNECTED) {
    wifiConnected = true;
    Serial.println(F("\nConnesso! IP: "));
    Serial.println(WiFi.localIP());
  } else {
    wifiConnected = false;
    Serial.println(F("\nFallito! Riproverò tra 60s"));
  }
}

// ================= INVIO DATI A MYZUBSTER =================
void sendDataToMyZubster() {
  if (!wifiConnected) return;
  
  HTTPClient http;
  String url = String(GATEWAY_URL) + "/api/garden/data";
  
  http.begin(url);
  http.addHeader("Content-Type", "application/json");
  http.addHeader("Authorization", String("Bearer ") + API_TOKEN);
  
  // Costruisci JSON payload
  DynamicJsonDocument doc(512);
  doc["gardenId"] = GARDEN_ID;
  doc["ph"] = round(phValue * 100) / 100.0;
  doc["ec"] = round(ecValue * 100) / 100.0;
  doc["temperature"] = round(temperature * 10) / 10.0;
  doc["humidity"] = round(humidity * 10) / 10.0;
  
  String jsonString;
  serializeJson(doc, jsonString);
  
  Serial.print(F("Invio: "));
  Serial.println(jsonString);
  
  int httpResponseCode = http.POST(jsonString);
  
  if (httpResponseCode > 0) {
    String response = http.getString();
    Serial.print(F("Risposta ["));
    Serial.print(httpResponseCode);
    Serial.print(F("]: "));
    Serial.println(response);
    
    if (httpResponseCode == 200 || httpResponseCode == 201) {
      Serial.println(F("✓ Dati inviati con successo!"));
    }
  } else {
    Serial.print(F("✗ Errore HTTP: "));
    Serial.println(http.errorToString(httpResponseCode));
  }
  
  http.end();
}

// ================= CALIBRAZIONE (esegui su Serial Monitor) =================
/*
 * Per calibrare pH:
 * 1. Immergi sensore in soluzione pH 7.0, nota phVoltage
 * 2. Immergi in soluzione pH 4.0, nota phVoltage
 * 3. slope = (7.0 - 4.0) / (v7 - v4)
 * 4. offset = 7.0 - slope * v7
 * 
 * Aggiorna PH_CALIBRATION_SLOPE e PH_CALIBRATION_OFFSET
 */

// ================= FINE CODICE =================

---

## 5. Costruzione Sistema NFT

### 5.1 Progettazione Canali
```
Dimensioni tipiche per terrazzo:
- Lunghezza canale: 1.5 - 2.5 metri
- Larghezza tubo PVC: 50mm (piccole piante) / 75mm (grandi)
- Inclinazione: 1-2% (1-2 cm per metro)
- Distanza fori net pots: 20-25 cm
- Numero piante per canale: 8-12
```

### 5.2 Passi Costruzione

1. **Taglia i canali PVC** alla lunghezza desiderata
2. **Pratica i fori** per net pots (fresa 50mm, distanza 22-25cm)
3. **Assembla il circuito**:
   - Serbatoio → Pompa → Canale 1 → Canale 2 → ... → Ritorno al serbatoio
   - Usa gomiti 90° e T per collegamenti
   - Assicurati pendenza costante con livello a bolla
4. **Installa la pompa** nel serbatoio, collega al relè
5. **Test idraulico**: riempi d'acqua, verifica flusso uniforme, nessuna perdita

### 5.3 Preparazione Soluzione Nutritiva
| Fase | EC Target | pH Target | Note |
|------|-----------|-----------|------|
| Semina/Clone | 0.8-1.0 mS/cm | 5.8-6.0 | Soluzione debole |
| Crescita vegetativa | 1.2-1.8 mS/cm | 5.8-6.2 | Aumenta gradualmente |
| Fioritura/Frutto | 1.8-2.4 mS/cm | 6.0-6.3 | Più potassio/fosforo |

**Ricetta base (per 10L):**
- 10L acqua (lasciare riposare 24h se clorata)
- 20ml Nutrienti A (NPK + micro)
- 20ml Nutrienti B (Ca + Mg)
- Regola pH con pH Down/Up

---

## 6. Calibrazione Sensori (Fondamentale!)

### 6.1 Calibrazione pH (2 punti)
1. Accendi Arduino, apri Serial Monitor (115200 baud)
2. Immergi sensore in **soluzione pH 7.0** (buffer)
3. Aspetta 60 secondi, nota il valore `phVoltage` (es. 2.51V)
4. Immergi in **soluzione pH 4.0**
5. Aspetta 60 secondi, nota `phVoltage` (es. 3.05V)
6. Calcola:
   ```cpp
   slope = (7.0 - 4.0) / (2.51 - 3.05) = 3.0 / -0.54 = -5.56
   offset = 7.0 - (-5.56 * 2.51) = 7.0 + 13.95 = 20.95
   ```
7. Aggiorna costanti nello sketch, ricarica

### 6.2 Calibrazione EC (1 punto)
1. Prepara soluzione nota (es. 1413 µS/cm = 1.413 mS/cm)
2. Immergi sensore, aspetta stabilizzazione
3. Nota `ecVoltage` (es. 1.23V)
4. `EC_CALIBRATION_K = 1.413 / 1.23 = 1.15`

### 6.3 Verifica DHT22
- Confronta con termometro/igrometro di riferimento
- Se offset costante, aggiungi correzione software

---

## 7. Integrazione con MyZubster

### 7.1 Ottenere Credenziali
1. Registrati su **MyZubster Web** o app
2. Crea un nuovo **Giardino (Garden)**
3. Vai in Impostazioni → API → Genera Token
4. Copia `GARDEN_ID` e `API_TOKEN`

### 7.2 Configurazione Gateway URL
- Sviluppo locale: `http://192.168.1.XXX:3000` (IP del tuo server Gateway)
- Produzione: `https://api.myzubster.example.com`

### 7.3 Endpoint API Utilizzati

| Endpoint | Metodo | Descrizione |
|----------|--------|-------------|
| `/api/garden/data` | POST | Invia letture sensori |
| `/api/garden/{id}/stats` | GET | Statistiche storiche |
| `/api/gardens/search` | GET | Cerca giardini vicini |

### 7.4 Formato Payload
```json
{
  "gardenId": "garden_001",
  "ph": 6.2,
  "ec": 1.45,
  "temperature": 23.5,
  "humidity": 58.0
}
```

### 7.5 Risposta Successo (201)
```json
{
  "success": true,
  "dataId": "reading_abc123",
  "timestamp": "2026-07-31T15:30:00Z"
}
```

---

## 8. Risoluzione Problemi Comuni

| Sintomo | Causa Probabile | Soluzione |
|---------|-----------------|-----------|
| pH sempre 7.0 / non cambia | Sensore non calibrato / rotto | Ricalibrare, verificare cavi |
| EC = 0 / valori assurdi | Cavo scollegato / sensore asciutto | Verifica collegamenti, immergi bene |
| DHT22 NaN / Error | Cavo lungo / manca pull-up | Resistenza 4.7kΩ tra Data e VCC, cavi <1m |
| WiFi non connette | SSID/PWD errati / 5GHz | Usa 2.4GHz, verifica credenziali |
| HTTP 401 Unauthorized | Token scaduto / errato | Rigenera token su MyZubster |
| HTTP 404 Not Found | URL Gateway sbagliato | Verifica GATEWAY_URL + /api/garden/data |
| Pompa non parte | Relè non scatta / 12V mancante | Test relè con multimetro, verifica alimentatore |
| Flusso irregolare | Bolle d'aria / pompa debole | Spurgare aria, pompa più potente |
| Alghe nel serbatoio | Luce diretta | Copri serbatoio con telo nero |

---

## 9. Automazioni Avanzate (Idee Future)

### 9.1 Controllo pH Automatico
- Aggiungi pompa dosatrice peristaltica (pH Down)
- Logica: se pH > 6.3 → dosa 1ml → attendi 5 min → rileggi

### 9.2 Controllo EC Automatico
- Dosatore nutrienti concentrati A+B
- Se EC < target → dosa nutrienti

### 9.3 Data Logging Locale (SD Card)
```cpp
#include <SD.h>
File dataFile = SD.open("hydro_log.csv", FILE_WRITE);
dataFile.printf("%lu,%.2f,%.2f,%.1f,%.1f\n", 
  millis(), phValue, ecValue, temperature, humidity);
dataFile.close();
```

### 9.4 Dashboard Web Locale
- ESP32 come web server (AsyncWebServer)
- Grafici Chart.js in tempo reale
- Accessibile da `http://esp32.local`

### 9.5 Alert Telegram/Email
```cpp
// Se pH < 5.5 o > 6.5 → invia alert
if (phValue < 5.5 || phValue > 6.5) {
  sendTelegramAlert("⚠️ pH fuori range: " + String(phValue));
}
```

---

## 10. Sicurezza e Manutenzione

### Checklist Settimanale
- [ ] Verifica pH e EC (confronta con tester manuale)
- [ ] Controlla livello soluzione nel serbatoio (rabbocca acqua)
- [ ] Pulisci filtri pompa
- [ ] Ispeziona radici (sane = bianche, marce = marroni/molle)
- [ ] Cambia soluzione nutritiva ogni 2-3 settimane

### Checklist Mensile
- [ ] Calibra sensori pH/EC
- [ ] Pulisci canali (spazzola + acqua)
- [ ] Controlla tenuta giunti PVC
- [ ] Backup dati SD card

### Sicurezza Elettrica
- Usa **GFCI/RCD** (salvavita differenziale) per presa esterna
- Alimentatori 12V certificati CE
- Cavi esterni: guaina UV-resistente
- Nessuna giunzione elettrica esposta all'umidità

---

## 11. Risorse Utili

### Librerie Arduino
- [DHT sensor library](https://github.com/adafruit/DHT-sensor-library)
- [ArduinoJson](https://arduinojson.org/)
- [WiFiManager](https://github.com/tzapu/WiFiManager) (config WiFi via captive portal)

### Guide Idroponica
- [Hydroponics Basics - University of Arizona](https://cals.arizona.edu/hydroponics/)
- [NFT System Design Guide](https://www.growertoday.com/nft-hydroponics/)

### MyZubster
- Repository Gateway: `github.com/MyZubster-Ecosystem/MyZubsterGateway`
- Repository Marketplace: `github.com/MyZubster-Ecosystem/MyZubster-Marketplace`
- Web App: `github.com/MyZubster-Ecosystem/myzubster`

### Fornitori Componenti (Italia/EU)
- **Elettronica**: RS Components, Mouser, DigiKey, Amazon
- **Idraulica**: BricoCenter, Leroy Merlin, IdroponicaShop.it
- **Nutrienti**: Advanced Nutrients, Canna, GHE, Plagron

---

## 12. Licenza e Contributi

Questa guida è rilasciata sotto licenza **MIT**. 
Sentiti libero di:
- Usarla per progetti personali/commerciali
- Modificare e condividere
- Aprire PR con miglioramenti su GitHub

**Contribuisci a MyZubster!** 
Ci sono bounty aperte per:
- Integrazione sensori aggiuntivi (CO2, PAR, flusso)
- App mobile React Native
- Algoritmi predittivi per nutrienti

---

*Ultimo aggiornamento: Luglio 2026*
*Versione: 1.0*
*Autore: CloudPaw-Master per MyZubster Community*