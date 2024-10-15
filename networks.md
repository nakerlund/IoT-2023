---
marp: true
---

# Nätverk

---

## Nätverkstyper

IoT-enheter använder olika trådlösa tekniker beroende på krav på räckvidd, energiförbrukning och datamängd. Dessa kan delas upp i tre katogeries:

- **IP-baserade**: Direktkommunikation över IP-nätverk.
- **Cellulära**: Använder mobilnätverk för direktuppkoppling till internet utan behov av en gateway, till exempel 4G, 5G, LTE-M och NB-IoT.
- **Övriga**: Använder andra kommunikationsprotokoll som kräver en gateway för att kopplas till internet, till exempel Bluetooth Low Energy (BLE), Zigbee och LoRa.

---

### Nätverk - IP Baserade

[IP och MAC](ip.md)

- **WiFi**: Direktkommunikation över IP-nätverk och anslutning till internet via WiFi-router/gateway. Snabbt, men kräver mer ström.
- **Thread**: Ett IP-baserat nätverk med mesh-topologi. Kräver minst en border router (gateway) för internetuppkoppling.

---

### Nätverk - Cellulära

Kräver SIM-kort eller eSIM.

- **4G**: Hög hastighet och pålitlig täckning. Används för applikationer som videostreaming, telemetri och smarta städer.
- **5G**: Mycket snabb, låg latens och stöd för många enheter. Perfekt för autonoma fordon, industriell automation och smarta städer.
- **LTE-M**: Optimerat för batteridrivna enheter som behöver röra sig mellan celler. Vanligt i wearables och logistik.
- **NB-IoT**: Låg energi, små datamängder. Perfekt för sensorer i smarta städer, jordbruk och vattenmätare.

---

### Nätverk - Övriga

Endast ett urval.

- **LoRa**: Lång räckvidd och låg energiförbrukning, behöver en gateway för internetanslutning. Används i smarta städer och jordbruk.
- **Zigbee**: Lågenergi mesh-nätverk, kräver en gateway för att ansluta till internet. Vanligt i smarta hem, belysning och säkerhetssystem.
- **Bluetooth Low Energy (BLE)**: Kortdistanskommunikation, men även BLE Mesh och Long Range används. Kräver ofta en gateway för internet, men kan användas i mesh-lösningar för större nätverk som belysning och industriell automation.

---

## Trådbundna anslutningar och bussar

Trådbundna anslutningar är viktiga för IoT-applikationer som kräver hög tillförlitlighet och låg latens. Kan kombineras med strömförsörjning och använda olika sorters kablar.

**Ethernet**: Pålitlig och snabb anslutning, vanlig i industriella miljöer. Fiber används för längre avstånd och högre hastigheter.

**Modbus**: Industriellt protokoll för kommunikation mellan sensorer och styrsystem, används ofta över RS-485 eller TCP/IP.

**CAN-bus**: Robust bussprotokoll för fordon och industri. Tillåter flera enheter att kommunicera i realtid över samma tvåtrådsbuss.

**USB**: Enklast att komma igång med till Linux baserade IoT enheter.

---

## VPN och säkerhet

VPN används för att skapa säkra, krypterade tunnlar mellan enheter och nätverk eller molntjänster, vilket skyddar trafiken från avlyssning eller attacker.

- **WireGuard**: WireGuard är ett populärt VPN-protokoll i IoT-miljöer eftersom det är snabbt, enkelt att implementera och mer resurseffektivt än traditionella VPN-lösningar som IPSec. VPN gör det möjligt att säkert ansluta IoT-enheter till ett centralt nätverk, även över osäkra internetförbindelser. **NetBird** är ett bra verktyg för att enekelt använda WireGuard.

- **ZeroTrust**: ZeroTrust är en säkerhetsmodell som förutsätter att ingen del av nätverket är pålitligt, inte ens interna enheter. I IoT-sammanhang innebär detta att varje enhet och varje kommunikationstillfälle måste verifieras, och att åtkomsten är strikt kontrollerad. Det minimerar risken för att en komprometterad enhet kan påverka hela nätverket.

- **

---

## OSI Modellen: Kan användas för att jämföra anslutningstyper

| OSI Layer                     | Bluetooth/GATT                                                | LoRaWAN                                                                               | ZigBee                                                                            | LwM2M/CoAP over UDP                                                        | HTTP                                                                             | MQTT                                                                                     | Modbus over RS485                                             | CAN                                                                     | Thread                                                                | Matter                                                                             |
| ----------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Lager 1 - Fysiskt lager       | Bluetooth-radiovågor, modulation                              | LoRa-radio, modulation (chirp spread spectrum)                                        | ZigBee-radio, baserat på IEEE 802.15.4                                            | Använd fysisk länk som stöder IP-nätverk                                   | Ethernet, Wi-Fi, eller liknande fysisk länk                                      | Ethernet, Wi-Fi eller liknande fysisk länk                                               | RS485 fysisk länk (tvåtråds eller fyrtråds system)            | CAN-buss (Controller Area Network) fysisk överföring                    | IEEE 802.15.4-bas för trådlös kommunikation                           | Baserat på Thread (IEEE 802.15.4) eller Wi-Fi                                      |
| Lager 2 - Länklager           | Baseband, LMP (Link Manager Protocol)                         | LoRaWAN MAC layer                                                                     | ZigBee MAC layer (IEEE 802.15.4)                                                  | LoWPAN eller liknande, beroende på nätverksteknologi                       | Data link (t.ex. Ethernet eller Wi-Fi protokoll)                                 | Data link (Ethernet eller Wi-Fi)                                                         | RS485 elektrisk specifikation för länkkommunikation           | CAN-protokoll för dataöverföring och felhantering                       | IEEE 802.15.4 MAC layer                                               | MAC layer beroende på underliggande teknik (t.ex. 802.15.4 eller Wi-Fi)            |
| Lager 3 - Nätverkslagret      | Ej tillämpbart direkt (men kan stödja IP via andra protokoll) | LoRaWAN använder IPv6, men nätverkslaget hanteras av Gateways och Network Servers     | ZigBee Network Layer (stödjer mesh routing)                                       | IPv6 routing (används med 6LoWPAN)                                         | IP (Internet Protocol)                                                           | IP (Internet Protocol)                                                                   | Modbus RTU-adressering och routing                            | CAN-används ej för klassiskt nätverkslager, ingen routing               | IPv6-baserad nätverkskommunikation med mesh-routing                   | IPv6-baserad kommunikation                                                         |
| Lager 4 - Transportlagret     | L2CAP (Logical Link Control and Adaptation Protocol)          | UDP över IP (används i gateway/server-lösningar)                                      | ZigBee Transport layer (utbyte av paket mellan noder)                             | UDP som transportlager                                                     | TCP som transportlager                                                           | TCP som transportlager (MQTT kräver en stabil anslutning)                                | Modbus överför dataramar (framing) på transportlagret         | CAN-ramar (frames) hanteras direkt på transportlagret                   | UDP som transportlager (baserat på IP-kommunikation)                  | UDP eller TCP beroende på applikationen                                            |
| Lager 5 - Sessionslagret      | ATT (Attribute Protocol)                                      | Sessionshantering med krypterade nycklar (för både nätverk och applikation)           | Sessionslagret hanteras av ZigBee Application Support Sub-layer                   | CoAP hanterar sessionslagret med enkla metodik som GET, POST, PUT, DELETE  | HTTP hanterar sessionslagret med tillståndslösa förfrågningar (request/response) | MQTT hanterar sessionslagret genom att upprätthålla anslutningar och övervaka abonnemang | Sessionslagret är implicit genom adressering och sekvensering | Sessionslagret är inte specificerat, data skickas kontinuerligt         | Sessionshantering via standard IPv6-metoder (t.ex. CoAP eller TCP)    | Sessionshantering för enhetsstyrning och applikationsutbyte                        |
| Lager 6 - Presentationslagret | Data format, GATT services och characteristics                | Ej specifikt presentationslager, men dataformat är definierat i applikationen         | Presentationslagret är applikationsspecifikt, kan variera                         | Presentationslagret kan definiera dataformat med LwM2M-resurser och objekt | Presentationslagret använder format som JSON, HTML, XML för att presentera data  | Presentationslagret använder specifika payload-format som kan variera                    | Enkelt presentationslager för dataregister                    | Ej specifikt presentationslager, men meddelandestrukturen är definierad | Presentationslagret är applikationsspecifikt, definieras av användare | Presentationslagret definierar interoperabilitet och dataformat för smarta enheter |
| Lager 7 - Applikationslagret  | GATT (Generic Attribute Profile)                              | Applikationslagret hanteras av specifika applikationsservrar, kryptering för payloads | ZigBee Application Framework (specifik för olika profiler, t.ex. Home Automation) | LwM2M-applikationsprotokoll som styr enheter och sensorer                  | HTTP-protokollet fungerar på applikationslagret för webbtjänster                 | MQTT fungerar på applikationslagret för publicering/abonnemang av meddelanden            | Modbus applikationsprotokoll för att läsa/skriva register     | Applikationsspecifika CAN-protokoll, t.ex. CANopen eller J1939          | Thread-protokoll stöder IP-baserade applikationer, såsom Matter       | Matter applikationsprotokoll för smarta hem-enheter                                |

---

## Dataöverföringshastigheter, räckvidder och topologier

| Teknik                 | Maximal Hastighet  | Maximal Räckvidd     | Topologi                  | Användningsområde                                     |
| ---------------------- | ------------------ | -------------------- | ------------------------- | ----------------------------------------------------- |
| **Ethernet**           | Upp till 100 Gbps  | 100 meter            | Punkt-till-punkt          | Industriella gateways, pålitliga anslutningar         |
| **Fiber**              | Upp till 1 Tbps    | Flera mil            | Punkt-till-punkt          | Hög hastighet i industriella miljöer, lång räckvidd   |
| **Wi-Fi 7**            | Upp till 46 Gbps   | 50-100 meter inomhus | Stjärn-/punkt-till-punkt  | Högpresterande smarta hem, industriella applikationer |
| **Wi-Fi 6**            | Upp till 9,6 Gbps  | 50-100 meter inomhus | Stjärn-/punkt-till-punkt  | Smarta hem, kameror, gateways med hög bandbredd       |
| **Thread**             | Upp till 250 kbps  | Upp till 100 meter   | Mesh                      | Smarta hem, industriella IoT-nätverk med låg energi   |
| **Bluetooth 5**        | Upp till 2 Mbps    | Upp till 200 meter   | Punkt-till-punkt          | Wearables, trådlösa sensorer                          |
| **BLE Long Range**     | Upp till 125 kbps  | Upp till 1 kilometer | Punkt-till-punkt          | Långdistanssensorer, lågenergienheter                 |
| **BLE Mesh**           | Upp till 1 Mbps    | Flera hundra meter   | Mesh                      | Nätverk i smarta hem, belysningssystem                |
| **LoRaWAN**            | Upp till 50 kbps   | Flera kilometer      | Stjärn-/punkt-till-punkt  | Miljöövervakning, jordbruk                            |
| **Zigbee**             | Upp till 250 kbps  | Upp till 100 meter   | Mesh                      | Smarta hem, belysnings- och säkerhetssystem           |
| **NB-IoT**             | Upp till 250 kbps  | Flera kilometer      | Stjärn-/punkt-till-punkt  | Smarta vattenmätare, miljösensorer                    |
| **Cat-M1**             | Upp till 1 Mbps    | Flera kilometer      | Stjärn-/punkt-till-punkt  | Transport, fordon, mobila tillämpningar               |
| **USB 2.0**            | Upp till 480 Mbps  | 5 meter              | Punkt-till-punkt          | Dataöverföring för externa enheter                    |
| **USB 3.0/3.1**        | Upp till 5-10 Gbps | 3 meter              | Punkt-till-punkt          | Snabbare anslutning för hårddiskar, kameror, etc.     |
| **USB 4.0**            | Upp till 40 Gbps   | 1 meter              | Punkt-till-punkt          | Högpresterande anslutningar, stöd för video och data  |

Här är en utökad version som förklarar de olika kommunikationsprotokollen du nämnde:

---

## Kommunikationsprotokoll 

| Protokoll | Användningsområde | Fördelar | Nackdelar |
| --------- | ----------------- | -------- | --------- |
| **HTTP**  | Webbtjänster, molnkommunikation | Välkänt, robust för större datamängder | Resurskrävande, ineffektivt för små data |
| **MQTT**  | Sensorer, smarta hem, fjärrövervakning | Effektivt över låg bandbredd, QoS-stöd | Kräver en broker, centraliserat |
| **LwM2M** | Fjärrövervakning, enhetshantering | Optimerat för resursbegränsade enheter, baserat på CoAP | Kräver LwM2M-stöd, begränsad datakomplexitet |
| **WebRTC**| Realtidskommunikation, video/ljudströmning | Låg latens, peer-to-peer-kommunikation | Resurskrävande, bäst för stabila nätverk |
