# 🚗🚌🚲 Jobb pendling – iOS Snarvei

[![Add to Shortcuts](https://img.shields.io/badge/Add%20to-Shortcuts-blue?logo=apple&logoColor=white)](https://www.icloud.com/shortcuts/3ccad90c297e43a38471e101177ccf80)
[![View on GitHub](https://img.shields.io/badge/View-GitHub-black?logo=github)](https://github.com/FriedCurmudgeon/ios-shortcuts/blob/main/shortcuts/Jobb%20pendling.shortcut)

En intelligent iOS-snarvei som samler **pendling, fokus-modus, varsling, navigasjon og underholdning** i én sømløs flyt.

Snarveien er laget for daglig bruk, med innebygde sjekker som hindrer:
- feil fokus
- overlappende kontekst
- unødvendige avbrytelser

Dette er ikke bare én snarvei, men et lite system bestående av:
- én manuell snarvei (start på reisen)
- automatisering ved ankomst jobb
- automatisering ved hjemkomst

---

## 🧭 Hva snarveien tar hensyn til

- Hvordan du reiser (bil, buss, sykkel, hjemmekontor)
- Hvilket fokus som allerede er aktivt
- Om noen skal varsles
- Automatisk navigasjon
- Valg av musikk eller podcast

---

## 📊 Flyt (oversikt)

> Merk: Diagrammet rendres kun i GitHub som støtter Mermaid.

```mermaid
flowchart TD
    A([Start snarvei]) --> B{Transportvalg}

    B -->|Bil| BilStart
    B -->|Buss| BussStart
    B -->|Sykkel| SykkelStart
    B -->|Hjemmekontor| HKStart
    B -->|Hjemme| HjemmeStart

    BilStart --> BilFokus[Sett fokus: Kjører] --> BilNav[Åpne Google Maps (driving)] --> MediaValg{Musikk eller Podcast?}
    BussStart --> BussFokus[Sett fokus: Busser] --> BussApp[Åpne Kolumbus] --> MediaValg
    SykkelStart --> SykkelFokus[Sett fokus: Sykler] --> SykkelNav[Åpne Google Maps (bicycling)] --> MediaValg

    MediaValg -->|Musikk| Spotify[Åpne Spotify]
    MediaValg -->|Podcast| Podcaster[Åpne Podcaster]

    HKStart --> HKFokus[Sett fokus: Hjemmekontor] --> HKVarsel[Vis påminnelse: Oppdater kalender]
    HjemmeStart --> HjemmeFokus[Sett fokus: Hjemme]
```

## ✨ Funksjoner i snarveien

### 🚦 Transportvalg
Ved start blir du spurt:

**Hvordan reiser du i dag?**

Tilgjengelige valg:
- 🚗 Bil
- 🚌 Buss
- 🚲 Sykkel
- 🏠 Hjemmekontor
- ❌ Hjemme

Hvert valg har egen logikk for fokus, varsler og navigasjon.

---

### 🔔 Varsling
Snarveien kan sende SMS/iMessage til en forhåndsvalgt mottaker.

Eksempler:
- Kjører hjem 😊
- Går til bussen 😅
- Sykler hjem nå 🚴‍♂️

Meldingen genereres dynamisk basert på valgt transport.

---

### 🧠 Fokus-modus (automatisk)
Snarveien bruker **Hent gjeldende fokus** for å unngå konflikter.

Fokus som benyttes:
- Kjører
- Busser
- Sykler
- Jobb
- Hjemmekontor
- Hjemme

Regler:
- Riktig fokus allerede aktiv → kun varsling
- Feil fokus aktiv → snarveien stoppes
- Fokus aktiveres kun når ingen konflikter finnes

Dette hindrer overlappende eller feilaktige fokus-endringer.

---

### 🗺️ Navigasjon
Navigasjon åpnes automatisk i **Google Maps**.

- Bil: `driving`
- Sykkel: `bicycling`

Destinasjon settes dynamisk basert på:
- hjemadresse
- jobbadresse

---

### 🎧 Musikk eller podcast
Etter at navigasjon er startet, blir du spurt:

**Vil du høre på musikk eller podcast?**

Valg:
- 🎵 Musikk → åpner Spotify
- 🎙 Podcast → åpner Apple Podcaster

Dette steget er felles for alle transportgrener.

---

### 🏠 Hjemmekontor / Hjemme
Spesiallogikk:
- Hjemmekontor kan kun aktiveres når ingen transport-fokus er aktive
- Ved konflikt vises tydelig varsel
- Brukeren minnes på å oppdatere kalender ved hjemmekontor

---

## 🧩 Variabler brukt

- `mottaker` – kontakt som mottar melding  
- `adresseHjem` – hjemadresse  
- `adresseJobb` – jobbadresse  
- `meldingTekst` – dynamisk generert meldingstekst  

---

## 🤖 Tilhørende automatiseringer

### 📍 Når jeg ankommer jobb

**Trigger**
- Ankomst jobbadresse
- Tidsrom: 05:00–14:00

**Logikk**
- Kjører kun hvis gjeldende fokus er Bilkjøring, Busser eller Sykler
- Utføres kun på hverdager
- Valgfri melding sendes ved sykkel
- Transport-fokus avsluttes
- Jobb-fokus aktiveres

**Resultat**
- Sømløs overgang fra pendling til arbeid
- Tydelig varsel
- Ingen manuell interaksjon

---

### 🏠 Når jeg kommer hjem

**Trigger**
- Ankomst hjemmeadresse
- Tidsrom: 10:00–18:00

**Logikk**
- Stopper umiddelbart hvis fokus allerede er:
  - Hjemme
  - Hjemmekontor
  - Soving
  - Ferie
- Avslutter kun transport-fokus
- Aktiverer ingen nytt fokus

**Resultat**
- Ryddig avslutning av arbeidsdagen
- Ingen jobb-kontekst henger igjen
- Myk overgang til fritid

---

## 🛡️ Designvalg og robusthet

- Alle fokus-endringer er beskyttet av sjekker
- Automatiseringer stopper seg selv ved konflikt
- Ingen duplisert logikk på tvers av grener
- Modulært oppsett: snarvei + automatiseringer

Dette gjør løsningen:
- trygg i daglig bruk
- lett å vedlikeholde
- enkel å forstå for andre

---

## ⬇️ Installere snarveien

### 📲 Anbefalt (iPhone / iPad)
Åpne lenken under på iPhone eller iPad for å legge snarveien direkte til i **Snarveier-appen**:

👉 https://www.icloud.com/shortcuts/3ccad90c297e43a38471e101177ccf80

Første gang må du kanskje tillate **Ubetrodde snarveier**  
(Innstillinger → Snarveier).

---

### 💾 Manuell nedlasting
Hvis du vil laste ned filen manuelt:

👉 https://github.com/FriedCurmudgeon/ios-shortcuts/blob/main/shortcuts/Jobb%20pendling.shortcut

Manuell nedlasting gir ikke automatisk «Legg til i Snarveier»-dialog.

---

## 🚀 Videre idéer

- Automatisk valg av transport basert på sted
- Enkel logg over pendling
- Kalender-integrasjon
- Automatisering for «Når jeg forlater jobb»

---

