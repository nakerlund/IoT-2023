# **Systemspecificering för IoT-baserad batteriövervakning för telemaster**

## 1. **Inledning**

Denna Proof of Concept (PoC) beskriver en IoT-lösning för att övervaka batteribackuper som används för telemaster och annan infrastruktur. Kunden har efterfrågat en enkel och pålitlig metod för att fjärrövervaka batterinivåer med lång batteritid och säker kommunikation. Lösningen bygger på NB-IoT-teknologi och använder LwM2M-protokollet för effektiv och skalbar kommunikation mellan enheterna och backend-systemet. Säkerhetsfunktioner såsom DTLS, secure boot, och FOTA (Firmware Over The Air) med rollback-möjlighet är implementerade för att säkerställa säker och kontinuerlig drift.

PoC:n är utformad för att visa hur systemet kommer att fungera i praktiken, med en laptop som simulerar batteriövervakningen via dess inbyggda batteri. Backend är byggt med Docker Compose och använder Leshan, InfluxDB och Grafana för datalagring och visualisering. LwM2M klienten som körs under PoC är skriven i Python.

## 2. **Systemarkitektur**

### **2.1 Enhetsarkitektur**

Enheten som används för övervakning består av:

- **NB-IoT-modul** med RS232-gränssnitt, som hanterar kommunikationen.
- **Batterisensor** kopplad via RS232 till NB-IoT-modulen, som övervakar backup-batteriets laddningsstatus.
- **Inbyggt batteri** som övervakas för att säkerställa att enheten klarar att driva sig själv under ett år.
- **Firmware** utvecklad med Zephyr OS för att optimera strömförbrukningen och möjliggöra trådlösa uppdateringar.

### **2.2 Backend**

Backend-systemet körs i en Docker Compose-miljö och innehåller:

- **Leshan LwM2M-server**: Används för att hantera kommunikationen med IoT-enheterna och möjliggöra FOTA och övervakning.
- **InfluxDB**: En time-series databas för att lagra batteridata som samlas in från enheterna.
- **Grafana**: Används för att visualisera batteridata i realtid och larm.
- **NodeRed**: För hantering och bearbetning av dataflöden mellan olika komponenter i systemet.

### **2.3 Kommunikationsprotokoll**

Systemet använder följande protokoll och standarder:

- **NB-IoT**: För trådlös uppkoppling.
- **LwM2M**: För hantering av enheterna och batteridata samt fjärruppdateringar.
- **DTLS**: För säker överföring av data mellan enheter och servern, implementerad med en privat CA.

### **2.4 Säkerhet**

Säkerhet är en kritisk komponent i systemet:

- **DTLS (Datagram Transport Layer Security)**: Används för att säkra kommunikationen mellan NB-IoT-enheterna och backend-systemet.
- **Secure Boot**: Varje enhet startar endast firmware som är signerad med en godkänd nyckel, för att förhindra körning av skadlig kod.
- **FOTA med rollback**: Systemet kan fjärruppdatera firmware på enheterna. Om en uppdatering misslyckas, rullas enheten tillbaka till en tidigare fungerande version.
- **Manuell firmwareuppdatering via serviceport**: Enligt kundkrav finns en serviceport som tillåter att firmware kan uppdateras manuellt på plats om trådlös uppdatering inte fungerar.

### **2.5 Drifttid och strömbudget**

För att möta kravet på ett års batteritid:

- Zephyr OS används för att optimera strömförbrukningen.
- NB-IoT-modulen är konfigurerad för låg energiförbrukning genom strömsparlägen och effektiv kommunikationshantering.
- Batterinivåer övervakas kontinuerligt och rapporteras regelbundet via NB-IoT till backend-systemet.

## 3. **Cyber Resilience Act (CRA) Överensstämmelse**

Systemet följer Cyber Resilience Act genom att inkludera:

- **Säker kommunikation** via DTLS för att skydda data från avlyssning och manipulation.
- **Secure Boot** för att förhindra att osignerad eller skadlig firmware körs på enheten.
- **FOTA med rollback** för att säkerställa att systemet kan fjärruppdateras säkert, samtidigt som risken för avbrott minimeras.
- **Firmwarehantering** med kontinuerlig övervakning av CVEs (Common Vulnerabilities and Exposures) för att snabbt kunna adressera nya säkerhetshot.

## 4. **Skalbarhet och framtida utveckling**

Lösningen är utformad för att vara skalbar:

- Genom att använda LwM2M och NB-IoT kan systemet enkelt skalas för att inkludera fler enheter i framtiden, utan att kompromissa med prestanda eller säkerhet.
- Systemet stödjer flera miljöer (utveckling, staging, produktion) som kan anpassas beroende på om de hostas i molnet eller lokalt.
- **Grafana** möjliggör flexibel och skalbar visualisering, och kan anpassas för fler mätpunkter eller längre tidsperioder.
  
## 5. **Hosting och Certifikat**

För att stödja en säker molnbaserad lösning:

- **Let's Encrypt** används för att automatiskt hantera HTTPS-certifikat för webbgränssnittet.
- Kunden behöver tillhandahålla ett domännamn för att möjliggöra en säker och publik tillgång till systemet.
- Val av molnplatfform eller drift i egen server.