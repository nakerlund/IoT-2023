---
marp: true
---

# IP-, MAC-adresser

---

## IP-kommunikation och adressering

IP-kommunikation är en grundläggande komponent för IoT-enheter, där IPv4 och IPv6 är de huvudsakliga protokollen för adressering. Varje IoT-enhet behöver en unik adress för att kommunicera med andra enheter i nätverket, både lokalt och globalt. Det är också viktigt att förstå routrar, switchar, NAT, DHCP, DNS och VPN-lösningar för att effektivt hantera IoT-nätverk.

---

## IPv4 vs. IPv6

- **IPv4**: Fortfarande det mest använda protokollet för adressering i dagens nätverk. IPv4 stöder cirka 4,3 miljarder adresser, vilket skapar en adressbrist med den ökande mängden IoT-enheter. Detta leder ofta till användning av **NAT (Network Address Translation)** för att låta flera enheter dela en offentlig IP-adress, där privata IP-adresser används internt (som 192.168.x.x eller 10.x.x.x).
  
- **IPv6**: Har utvecklats för att lösa adressbristen genom ett mycket större adressutrymme (2^128 adresser), vilket gör det möjligt att tilldela unika adresser till alla IoT-enheter. IPv6 eliminerar behovet av NAT och gör det möjligt för enheter att kommunicera direkt över internet med globala adresser. **IPv6 är dock inte fullt etablerat ännu**, särskilt i mindre nätverk, vilket innebär att IPv4 fortfarande dominerar.

---

## Routrar och switchar

**Routrar** styr hur datapaket skickas mellan olika nätverk (t.ex. LAN och WAN) och hanterar **IP-adresser**, både för IPv4 och IPv6. De kan också hantera **NAT**, vilket översätter privata IP-adresser till en offentlig IP-adress för att möjliggöra internetåtkomst för flera enheter. Routrar kan dessutom fungera som **DHCP-servrar**, som dynamiskt tilldelar IP-adresser till IoT-enheter när de ansluter till nätverket. Alternativt kan vissa enheter konfigureras med **statiska IP-adresser**, vilket innebär att samma IP-adress alltid används, vilket kan vara användbart för enheter som kräver konstant åtkomst, som gateways eller servrar.

En **switch** kopplar samman enheter i samma lokala nätverk och skickar data till rätt destination baserat på enheternas **MAC-adresser** (fysiska adresser). Till skillnad från routrar hanterar switchar inte IP-adresser utan fungerar främst som ett verktyg för att dirigera trafik inom ett internt nätverk. De är särskilt viktiga i nätverk med många enheter, där de hjälper till att hantera nätverkets trafik och minska flaskhalsar.

---

## MAC-adresser och deras struktur

MAC-adress (Media Access Control-adress) är en unik identifierare som tilldelas varje nätverksgränssnitt. En MAC adress måste tilldelas om det inte är en privat eller mindre produktion. En MAC-adress består av 48 bitar (t.ex. `00:1A:2B:3C:4D:5E`) och består av två delar:

1. **OUI (Organizationally Unique Identifier)**: De första 24 bitarna* (`00:1A:2B`) utgör OUI, vilket är unikt för varje företag och tilldelas av **IEEE (Institute of Electrical and Electronics Engineers)**.

2. **Enhetsspecifik del**: De sista 24 bitarna (`3C:4D:5E`) gör MAC-addressen unik per nätverksgränssnitt.

\* Om första bytets näst lägsta bit är 1 så är det en slumpad MAC-adress.

---

### Typer av NICs (Network Interface Controllers) som använder MAC-adresser

MAC-adresser används i alla typer av nätverksgränssnitt som kommunicerar på ett lokalt nätverk men är ibland förprogrammerade.

- **WiFi NICs**: Används i trådlösa nätverk och kopplar upp enheter via WiFi. Alla WiFi-moduler har en MAC-adress för att identifiera sig i nätverket.
  
- **Ethernet NICs**: Används i trådbundna nätverk via Ethernet-kablar (t.ex. RJ45). Varje Ethernet-kontroller har en unik MAC-adress.
  
- **Bluetooth NICs**: Bluetooth-enheter, särskilt inom IoT, använder också MAC-adresser för att identifiera sig i nätverk och parkopplingar.
