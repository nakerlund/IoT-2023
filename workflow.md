---
marp: true
---

# Arbetssätt

---

## Företagstyper

- **Startups**: Små, snabbväxande företag med innovativa idéer; dynamisk miljö med breda yrkesroller.
- **Storföretag**: Etablerade företag med strukturerade processer; tydliga roller och karriärvägar.
- **Enskilda konsulter**: Självständiga specialister som erbjuder tjänster direkt till kunder; hög flexibilitet och självständighet.
- **Tech-hus**: Specialiserade företag som utvecklar produkter åt andra företag; snabba och varierande projekt.
- **Konsultföretag**: Anställer konsulter för kunduppdrag; variation i projekt och branscher, kräver anpassningsförmåga.

---

## Produktlivcykel

- **PoC**: Proof of Concept, som ofta byggs med utvecklingskit och slutar i ett mycket begränsat demo.
- **Utveckling**: Utveckling av hårdvara och mjukvara uppdelat i workpackages.
- **Prototyper**: "Board bring up" är en process där hårdvaruprototyperna startas för första gången, vilket kräver nära samarbete mellan hårdvaru- och mjukvaruteam.
- **Certifiering**: Med en fungerande prototyp kan precompliance tester för CE-märklning påbörjas. Sedan följer slutgiltiga certifieringen.
- **Industrialisering**: Skapande av produktionslinjen inklusive produktionstester och provisionering av enheterna.
- **Underhåll**: Mjukvara måste underhållas och uppdateras under produktens livslängd enligt CRA (Cyber reciliance act)

---

## Dokumentation och kravinsamling

Dokumentation är avgörande för att skapa en tydlig bild av systemets krav och specifikationer.

- **Systemspecifikation**: En övergripande beskrivning av systemet, dess syfte, funktioner och arkitektur.
- **Hårdvaruspecifikation (HW Specifikation)**: Detaljer om hårdvarukomponenter, inklusive processorer, sensorer och andra fysiska enheter som används i systemet.
- **Mjukvaruspecifikation (SW Specifikation)**: Beskrivning av mjukvarans funktionalitet, operativsystem, och gränssnitt mellan olika moduler.
- **Testspecifikation**: Detaljerade tester för att verifiera att både hårdvara och mjukvara fungerar enligt specifikationerna, inklusive testfall och testscenarier.

---

## Agila metoder – Scrum och Kanban

Scrum med sprintar för iterativ utveckling, där teamet arbetar i korta, tidsbestämda cykler. Viktiga roller inkluderar **Scrum Master**, som ansvarar för att underlätta processen, och **Produktägare**, som prioriterar backloggen med uppgifter. **Backloggen** innehåller alla uppgifter som ska utföras och är ett centralt verktyg för planering. **Kanban** används för kontinuerligt arbetsflöde, med fokus på att visualisera arbetet och begränsa mängden arbete som pågår samtidigt.

<https://agilemanifesto.org>
<https://www.atlassian.com/agile/manifesto>

---

## Git och Jira - Verktyg för samarbete

Git används för versionshantering, och Jira för ärendehantering och projektspårning. Jira kopplas ofta till Scrum och Kanban-processerna för att hantera backloggen och planera sprintar, vilket underlättar spårning av uppgifter och ansvarsområden. När utvecklingsuppgifter tilldelas kan de resultera i nya **branches** i Git, där varje branch representerar en specifik funktion eller fix. **Commits** görs för att spara framstegen och synkronisera arbetet, vilket gör det möjligt att följa ändringar och säkerställa kvalitet genom kodgranskning och kontinuerlig integration.

[git](git.md)

<https://ifuckinghatejira.com>
