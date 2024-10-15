---
marp: true
---

# IoT-produktkategorier och teknologier

---

## Typer av IoT-enheter

IoT-enheter kan variera från enkla uppkopplade enheter till avancerade sensor-noder och gateways som sammanbinder flera enheter. Några exempel:

- **Smarta belysning**: Ibland med protocol som DALI. Även i smarta städer med t.ex. SMART.
- **Sensor-noder**: Enheter som samlar in data från omgivningen, såsom temperatur, luftfuktighet eller ljusnivå, och vidarebefordrar den till en central enhet.
- **Bärbara enheter (Wearables)**: Exempelvis smartklockor eller aktivitetsarmband som samlar in data om användarens hälsa och fysisk aktivitet. Ofta BLE.
- **Säkerhetskameror**: Uppkopplade enheter som övervakar och skickar video till användare eller säkerhetssystem.
- **Smarta lås**: Lås som kan styras på distans och ger ökad säkerhet och kontroll över tillträde till fastigheter.

---

## Hårdvarukomponenter i IoT

IoT-enheter innehåller flera viktiga hårdvarukomponenter som behövs för att hantera data och utföra beräkningar.

- **Processorer**: Mikroprocessorer eller mikrokontrollersystem (MCU) som ansvarar för att bearbeta data och styra enhetens funktioner. Exempel inkluderar ARM Cortex-M och ESP32. Ibland även SOC (System on a chip)
- **Kommunikationsmoduler**: Modem-, Wi-Fi-, Bluetooth-, eller Zigbee-moduler som möjliggör trådlös anslutning.
- **Strömförsörjning**: Batterier eller strömadaptrar som driver enheten, ibland kombinerat med energihanteringskretsar för att maximera effektivitet och förlänga batteritid.

---

## Bussar och GPIO-pinnar

- **GPIO (General Purpose Input/Output)**: Används för att interagera med externa komponenter, såsom sensorer, knappar och lysdioder. GPIO kan programmeras för att fungera som både ingång eller utgång beroende på applikationen. Ibland även med PWM, ADC eller DAC.
- **UART (Universal Asynchronous Receiver/Transmitter)**: Ett seriellt kommunikationsgränssnitt som används för asynkron överföring av data mellan en mikrocontroller och andra enheter, som datorer eller externa moduler.
- **SPI (Serial Peripheral Interface)**: Ett synkront seriellt kommunikationsprotokoll som ofta används för hög hastighet mellan en mikrocontroller och externa enheter, såsom sensorer, minnen eller skärmar. SPI är master-slav-baserat och kan kommunicera med flera slav-enheter samtidigt.
- **I2C (Inter-Integrated Circuit)**: Ett populärt seriellt kommunikationsprotokoll som tillåter flera enheter att anslutas till samma tvåtrådsbuss genom att använda en unik adress för varje enhet.

---

## Antenner och trådlös kommunikation

Valet av antenn beror på flera faktorer, såsom våglängd, frekvens, och krav på räckvidd. Frekvensen påverkar hur långt signalen kan färdas och hur väl den tränger igenom hinder, vilket gör det viktigt att välja rätt antenntyp för optimal trådlös prestanda i IoT-system.

- Det finns olika typer av antenner som används beroende på applikationens behov och kommunikationsprotokoll:
- **Chipantenner**: En typ av antenn som ofta används i små, kompakta IoT-enheter där utrymme är begränsat.
- **PCB-antenner**: Dessa antenner är integrerade direkt på kretskortet och används ofta för enheter som kräver en kompakt design, såsom smarta glödlampor eller wearables. De är kostnadseffektiva och fungerar bra för kortare räckvidder.
- **Kvartsvågsantenner**: Vanliga i applikationer där längre räckvidd behövs, exempelvis gateways eller LoRa-enheter. Dessa antenner erbjuder högre prestanda än PCB-antenner och är effektiva för att hantera signaler på längre avstånd.

---

## Operativsystem för IoT

Olika IoT-enheter kräver olika operativsystem beroende på användningsområde och resurstillgånglighet.

- **Zephyr OS**: Ett lättvikts realtidsoperativsystem (RTOS) som är idealiskt för resurssvaga enheter med begränsat minne och strömförbrukning. Det används främst i sensor-noder och andra små IoT-enheter som kräver snabb respons och låg strömförbrukning. Ersätter FreeRTOS och liknande.
- **Linux och Yocto**: Linux-baserade system, används ofta i kraftfullare IoT-enheter som gateways, där mer datorkraft och minne behövs. Dessa operativsystem erbjuder flexibilitet och möjligheten att köra mer komplexa applikationer. Yocto är särskilt användbart för att skapa anpassade Linux-distributioner för specifika inbyggda system.
- **Android**: Används i mer användarcentrerade lösningar, exempelvis smarta skärmar och wearables, där ett användarvänligt gränssnitt är viktigt. Android erbjuder ett välkänt ekosystem med stöd för appar och avancerade användarfunktioner.
