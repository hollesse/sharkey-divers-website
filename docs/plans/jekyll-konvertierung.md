# Plan: Jekyll-Konvertierung der Sharkey Divers Website

## Übersicht
Konvertierung des statischen HTML-Prototyps in eine flexible Jekyll-Website mit konfigurierbaren Inhalten.

## 1. Konfigurierbare Elemente

### 1.1 Site-weite Konfiguration (`_config.yml`)
**Anpassbare Inhalte:**
- Vereinsinformationen
  - `club_name`: "Sharkey Divers Weilburg e.V."
  - `club_emoji`: "🦈"
  - `founding_year`: 1996
  - `tagline`: "Taucht mit uns ein in die faszinierende Welt unter Wasser"

- Kontaktinformationen
  - Vorstand (Name, Adresse)
  - Telefon, E-Mail

- Mitgliedschaften & Verbände
  - VDST, HTSV, LSB Hessen, CMAS

- SEO & Meta
  - title, description, keywords
  - Google Analytics (optional)

### 1.2 Daten-Dateien (`_data/`)

#### `vorteile.yml`
Liste aller Vereinsvorteile mit:
- emoji
- titel
- beschreibung

**Vorteil:** Neue Vorteile können einfach hinzugefügt werden ohne HTML zu ändern.

#### `ausbildung.yml`
Ausbildungsstufen strukturiert:
```yaml
stufen:
  - id: grundtauchschein
    emoji: "🎯"
    name: "Grundtauchschein"
    beschreibung: "..."
    ort: "Schwimmbad"
    im_beitrag: true
  - id: bronze
    emoji: "🥉"
    ...

sonderbrevets:
  - emoji: "🧭"
    name: "Orientierung"
  ...
```

#### `schnuppertauchen.yml`
Features des Schnuppertauchens:
- icon/emoji
- titel
- beschreibung

#### `hero.yml`
Hero-Section Inhalte:
- haupttitel
- untertitel
- cta_buttons (Text, Link, Farbe)

#### `about.yml`
"Über uns" Texte:
- absätze (als Array)
- badges (Seit 1996, CMAS, etc.)

#### `navigation.yml`
Navigationspunkte:
```yaml
main:
  - name: "Startseite"
    url: "#home"
  - name: "Schnuppertauchen"
    url: "#schnuppern"
  ...
```

### 1.3 Theme-Konfiguration

#### Tailwind Config
- Ocean-Farbpalette als CSS Custom Properties
- In `assets/css/main.css` oder separater Config-Datei
- Ermöglicht einfache Farbanpassungen

## 2. Jekyll-Struktur

### 2.1 Layouts (`_layouts/`)
- `default.html` - Basis-Layout mit HTML-Grundstruktur
- `home.html` - Spezifisches Layout für die Startseite

### 2.2 Includes (`_includes/`)
Wiederverwendbare Komponenten:
- `head.html` - Meta-Tags, CSS, Scripts
- `navigation.html` - Header & Navigation
- `footer.html` - Footer
- `hero.html` - Hero-Section
- `vorteile.html` - Vereinsvorteile-Section
- `about.html` - Über uns Section
- `schnuppertauchen.html` - Schnuppertauchen-Section
- `ausbildung.html` - Ausbildungs-Section
- `kontakt.html` - Kontaktformular-Section

**Vorteil:** Modularer Aufbau, einfache Wartung, Wiederverwendbarkeit

### 2.3 Assets (`assets/`)
```
assets/
├── css/
│   └── main.css (Tailwind + Custom CSS)
├── js/
│   └── main.js (Mobile Menu, Smooth Scroll)
└── images/
    └── (zukünftige Bilder)
```

### 2.4 Pages
- `index.md` - Hauptseite (nutzt home.html Layout)
- `impressum.md` - Impressum
- `datenschutz.md` - Datenschutzerklärung
- `satzung.md` - Vereinssatzung

## 3. Vorteile der Jekyll-Struktur

### 3.1 Inhaltspflege
- Nicht-technische Nutzer können YAML-Dateien bearbeiten
- Keine HTML-Kenntnisse erforderlich
- Strukturierte, übersichtliche Daten

### 3.2 Wartbarkeit
- Komponenten sind isoliert
- Änderungen an einem Include wirken sich global aus
- DRY-Prinzip (Don't Repeat Yourself)

### 3.3 Erweiterbarkeit
- Einfaches Hinzufügen neuer Sections
- Blog-Funktionalität kann später ergänzt werden
- Mehrsprachigkeit möglich (mit Plugins)

### 3.4 Deployment
- Statische HTML-Generierung
- Kann auf GitHub Pages, Netlify, etc. gehostet werden
- Schnelle Ladezeiten, keine Datenbank nötig

## 4. Besonderheiten & Überlegungen

### 4.1 Tailwind CSS
**Option A:** CDN-Version (wie im Prototyp)
- Einfach, keine Build-Pipeline nötig
- Größere Dateigröße

**Option B:** Tailwind CLI mit PostCSS
- Kleinere CSS-Datei (Purge unused styles)
- Erfordert Build-Step

**Empfehlung:** Start mit CDN, später Migration zu CLI wenn Performance wichtig wird.

### 4.2 Kontaktformular
Das HTML-Formular im Prototyp ist nicht funktional (kein Backend).

**Optionen:**
1. **Formspree / Netlify Forms** - Externe Services
2. **mailto:-Link** - Einfachste Lösung
3. **JavaScript + API** - Später implementierbar

**Empfehlung:** Netlify Forms nutzen wenn auf Netlify gehostet, sonst Formspree.

### 4.3 Bilder
Der Prototyp nutzt Placeholder (Emoji + Text).

**Plan:**
- Placeholder in `_data` konfigurierbar machen
- `image`-Feld für jede Section vorbereiten
- Falls Bild vorhanden: anzeigen, sonst Placeholder

### 4.4 Mobile Menu
JavaScript für Mobile-Navigation muss erhalten bleiben.
- In `assets/js/main.js` auslagern
- Im Layout einbinden

## 5. Umsetzungsschritte

### Phase 1: Grundstruktur
1. Jekyll-Basis bereinigen (Standard-Theme entfernen)
2. Layouts erstellen (default.html, home.html)
3. _config.yml konfigurieren

### Phase 2: Komponenten
4. Navigation-Include erstellen
5. Footer-Include erstellen
6. Head-Include mit Tailwind

### Phase 3: Sections
7. Hero-Section als Include
8. Vorteile-Section mit Daten
9. Über-uns-Section
10. Schnuppertauchen-Section
11. Ausbildung-Section
12. Kontakt-Section

### Phase 4: Assets & Interaktivität
13. CSS aufräumen und organisieren
14. JavaScript für Mobile Menu
15. Smooth Scrolling

### Phase 5: Content & SEO
16. _data-Dateien befüllen
17. Meta-Tags & SEO optimieren
18. Rechtliche Seiten (Impressum, Datenschutz)

### Phase 6: Testing & Deployment
19. Testen auf verschiedenen Geräten
20. Build optimieren
21. Deployment vorbereiten

## 6. Dateistruktur (Endresultat)

```
website/
├── _config.yml
├── _data/
│   ├── navigation.yml
│   ├── vorteile.yml
│   ├── ausbildung.yml
│   ├── schnuppertauchen.yml
│   ├── hero.yml
│   └── about.yml
├── _includes/
│   ├── head.html
│   ├── navigation.html
│   ├── footer.html
│   ├── hero.html
│   ├── vorteile.html
│   ├── about.html
│   ├── schnuppertauchen.html
│   ├── ausbildung.html
│   └── kontakt.html
├── _layouts/
│   ├── default.html
│   └── home.html
├── assets/
│   ├── css/
│   │   └── main.css
│   ├── js/
│   │   └── main.js
│   └── images/
├── index.md
├── impressum.md
├── datenschutz.md
└── satzung.md
```

## 7. Anpassbarkeit - Zusammenfassung

**Sehr einfach anpassbar (YAML-Editierung):**
- Vereinsinformationen
- Kontaktdaten
- Vereinsvorteile (hinzufügen/entfernen/ändern)
- Ausbildungsstufen & Sonderbrevets
- Hero-Texte & CTAs
- Über-uns-Texte
- Navigation

**Mit HTML/CSS-Kenntnissen:**
- Layout-Änderungen
- Neue Sections
- Styling-Anpassungen

**Entwickler-Level:**
- Tailwind-Build-Pipeline
- Neue Features
- JavaScript-Funktionalität

## 8. Nächste Schritte

1. Diesen Plan mit dem Benutzer abstimmen
2. Mit Phase 1 beginnen
3. Iterativ entwickeln und testen
4. Feedback einholen und anpassen
