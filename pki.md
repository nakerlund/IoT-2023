---
marp: true
---

# mTLS och PKI

---

## TLS 1.3 Handshake och symmetrisk kryptering

- Klienten skickar ett ClientHello med sitt certifkat och vilken kryptering som stöds, vilket inleder handshaken.
- Servern svarar med ett ServerHello, vilket inkluderar den valda krypteringen och server certifikatet.
- Nyckelutbyte sker genom att använda en publik/privat nyckelbaserad metod (ECDH), och både klienten och servern härleder en gemensam pre-master secret.
- Symmetrisk kryptering etableras genom att generera en session key baserat på pre-master secret och slumptal från båda parterna.

All efterföljande kommunikation krypteras med denna symmetriska nyckel, vilket säkerställer att trafiken är snabb och säker.

---

## Självsignerad/privat CA

Det första steget är att skapa en självsignerad CA. Detta certifikat kommer att användas för att signera enheters certifikat och etablera din egen betrodda certifikatkedja. Använd gärna Git Bash på Windows som har med sig OpenSSL.

---

### 1. Skapa en privat nyckel för din CA

```bash
openssl genrsa -out ca.key 2048
```

Detta skapar en privat nyckel (`ca.key`) för din CA av typen RSA med 2048 bitar.

---

### 2. Skapa ett självsignerat certifikat för din CA

```bash
openssl req -x509 -new -nodes -key ca.key -sha256 -days 3650 -out ca.crt
```

Du kommer att bli ombedd att fylla i information om din CA (Common Name, etc.). Certifikatet (`ca.crt`) kommer att vara giltigt i 10 år (3650 dagar).
Använd "localhost" som Common Name om det är till egna datorn. Välj annars domänen som används.

---

## Provisionera en Enhet

Nästa steg är att generera en privat nyckel och en **CSR (Certificate Signing Request)** på enheten. Den privata nyckeln lämnar aldrig enheten – endast CSR:n skickas till CA:n för signering.

### 1. Generera en privat nyckel på enheten

På IoT-enheten eller vilken enhet som ska provisioneras, generera en privat nyckel:

```bash
openssl genrsa -out device.key 2048
```

---

### 2. Skapa en CSR (Certificate Signing Request)

CSR:n är en förfrågan om att få ett certifikat signerat och innehåller den publika nyckeln (men inte den privata) och annan information om enheten.

```bash
openssl req -new -key device.key -out device.csr
```

När du kör detta kommando kommer du att bli ombedd att fylla i information som Common Name (namnet på enheten, t.ex. `device1.example.com`) och andra uppgifter som behövs för att identifiera enheten.

---

### 3. Överför CSR till CA

När **device.csr** har skapats på enheten kan du överföra den till din CA, exempelvis via en säker metod som SSH eller ett annat säkert överföringsprotokoll. Den privata nyckeln (`device.key`) stannar kvar på enheten och lämnar aldrig den.

Nu när du har mottagit CSR:n på din CA-server kan du signera den med din self-signed CA.

---

### 4. Signera enhetens certifikat med din CA

Använd CA:ns privata nyckel och certifikat för att signera enhetens CSR och skapa ett certifikat för enheten:

```bash
openssl x509 -req -in device.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out device.crt -days 365 -sha256
```

---

### 5. Installera certifikatet på enheten

Nu när certifikatet är signerat kan du överföra det tillbaka till enheten. Den privata nyckeln stannar på enheten, och certifikatet används för att etablera säkra anslutningar.

Ofta fortsätter provisioneringen genom att bränna in serienummer och nycklar för att möjligöra Secure Boot och flashning av firmware.
