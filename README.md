# Forensische Analyse eines USB-Sticks – Fallstudie mit Autopsy

## 🕵️ Projektübersicht

Dieses Projekt simuliert eine realistische forensische Untersuchung eines USB-Sticks im Kontext eines möglichen Datenmissbrauchs im beruflichen Umfeld. Ziel war es, gelöschte, bearbeitete oder verdächtig benannte Dateien zu rekonstruieren und anhand digitaler Artefakte eine plausible Nutzungshistorie nachzuvollziehen. Die Ergebnisse wurden in einem strukturierten forensischen Bericht dokumentiert.

---

## 📁 Fallbeschreibung

Am 06.05.2025 wurde ein USB-Stick aufgefunden, dessen Inhalt Hinweise auf die Speicherung vertraulicher oder unerlaubter Dateien liefert. Mehrere Dateien schienen gelöscht oder manipuliert worden zu sein. Die Analyse erfolgte mit dem Ziel, gelöschte Inhalte wiederherzustellen, Zeitstempel zu interpretieren und die Nutzung systematisch zu dokumentieren.

---

## 🎯 Zielsetzung

- Erstellung eines forensischen Images im RAW-Format mit FTK Imager
- Integritätsnachweis über MD5-/SHA1-Hashwerte
- Analyse gelöschter, modifizierter und auffälliger Dateien
- Rekonstruktion von Nutzungsmustern anhand von MACB-Zeitstempeln und Artefakten
- Erstellung eines professionellen forensischen Untersuchungsberichts

---

## 🔧 Methodik

### 1. Vorbereitung

Ein USB-Stick wurde mit Testdaten präpariert:
- Office-Dateien, Bildmaterial, eine verdächtige `.exe`, ZIP-Archiv
- Strukturierung in Ordnern wie `/Privat`, `/Zugänge`, `/Gelöscht`
- Teilweise Bearbeitung und Löschung der Inhalte

### 2. Imaging

- Erstellung eines 1:1-Abbilds mit **FTK Imager** (`.dd`)
- Aktivierung von „Verify After Creation“
- Berechnung und Dokumentation der Hashwerte (MD5 & SHA1)

### 3. Analyse mit Autopsy

- Import des forensischen Images
- Aktivierte Module:
  - Datei-Analyse & Dateitypen
  - Gelöschte Dateien
  - Zeitstempel (MACB)
- Dokumentation per Screenshots und CSV-Exports

---

## 📊 Ergebnisse (Auszug)

| Fund | Bewertung |
|------|-----------|
| `vpn_zugangsdaten.txt` (gelöscht) | Inhalt rekonstruierbar, enthält Login-Daten |
| `gehaltsliste_2022.xlsx` (gelöscht) | Interne Personalinformation, wiederherstellbar |
| `nudes.jpg` | Provokanter Name, unbedenklicher Inhalt, wurde geöffnet |
| Temporärdateien (`~WRD`, `~WRL`) | Weisen auf aktive Office-Bearbeitung hin |
| Zeitfenster: 18:45–19:04 Uhr | Kompakte Nutzungsphase mit gezielten Dateiaktionen |

---

## 🧾 Bericht

Der vollständige Untersuchungsbericht befindet sich im Repository unter:

📄 [`/bericht/forensischer_untersuchungsbericht.md`](./bericht/forensischer_untersuchungsbericht.md)

Er enthält:
- Tabellen zu auffälligen Dateien
- MACB-Zeitstempelanalyse
- Artefakte & Screenshots
- Bewertung & Schlussfolgerung

---

## 📷 Screenshots

Eine Auswahl relevanter Screenshots zur Analyse (z. B. FTK Imager, Autopsy File Tree, Zeitstempel) befindet sich im Ordner `/screenshots/`.

---

## ⚖️ Rechtlicher Hinweis

Alle in diesem Projekt verwendeten Dateien, Dateinamen und Inhalte wurden ausschließlich zu **Ausbildungszwecken** künstlich erzeugt. Es wurden keinerlei reale personenbezogene oder sicherheitskritische Daten verwendet.

---

## 👤 Über mich

Ich studiere **Cyber Security (B.Sc.)** im berufsbegleitenden Format mit besonderem Interesse an **digitaler Forensik und sicherheitsrelevanter IT im öffentlichen Dienst**. Dieses Projekt entstand zur eigenständigen Vertiefung praktischer Kompetenzen in der IT-Forensik.

---

## 📄 Lizenz

Dieses Repository steht unter der **MIT-Lizenz**.  
Das forensische Image selbst ist aus Speicher- und Datenschutzgründen **nicht im Repository enthalten**.

