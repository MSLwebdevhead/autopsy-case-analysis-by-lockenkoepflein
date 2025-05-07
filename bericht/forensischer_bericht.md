# Forensischer Untersuchungsbericht – USB-Stick-Analyse

## 1. Allgemeine Informationen

**Untersuchungsgegenstand:**  
USB-Stick (FAT16), Kapazität: 1,99 GB

**Datum der Sicherstellung:**  
06.05.2025

**Datum der Analyse:**  
07.05.2025

**Analystin:**  
[R. Metz]

**Verwendete Tools:**  
- Autopsy (Version 4.22.1)
- FTK Imager (Version 4.7.3.81, zur Image-Erstellung)
- Windows 10 (Analyse-Umgebung)
- Hash-Funktion: MD5 / SHA1

---

## 2. Fallbeschreibung

Am 06.05.2025 wurde ein USB-Stick aufgefunden, dessen Inhalt Hinweise auf die Speicherung vertraulicher oder unerlaubter Dateien gibt. Mehrere Dateien scheinen gelöscht oder umbenannt worden zu sein. Ziel der Analyse ist die Wiederherstellung dieser Daten sowie die Nachvollziehbarkeit der Nutzung durch Zeitstempel und Artefakte.

---

## 3. Vorgehensweise

### 3.1 Imaging

- Der USB-Stick wurde mit **FTK Imager** im RAW-Format (`.dd`) gesichert.
- Es wurden **keine Veränderungen** am Originalmedium vorgenommen (Read-Only-Zugriff).
- Die Integrität wurde durch folgende Hashwerte dokumentiert:

MD5: fbed49a7180efb3c371a3ea85a5e2608,
SHA1: bf0621d955e244938e6b5bfac00fcede0a63d33f

### 3.2 Import & Analyse

- Das Image wurde in Autopsy importiert.
- Folgende Module wurden aktiviert:
  - Datei-Analyse
  - Gelöschte Dateien
  - Zeitachsen-Darstellung (MACB)
  - Hash-Sets (Default)

---

## 4. Ergebnisse

### 4.1 Verzeichnisse & Dateien

Im Rahmen der Analyse wurden die auf dem USB-Stick gespeicherten Dateien systematisch untersucht. Die folgende Tabelle fasst die besonders relevanten oder auffälligen Dateien zusammen. Eine vollständige Dateiliste inklusive Metadaten befindet sich im Anhang als CSV-Datei.

[Dateiübersicht als CSV anzeigen](../dokumentation/usb_image.001.csv)

## Übersicht: Auffällige Dateien auf dem USB-Stick

| Ordner         | Dateiname                | Status     | Typ           | Auffälligkeit / Kommentar                           |
|----------------|--------------------------|------------|----------------|-----------------------------------------------------|
| /Zugänge       | vpn_zugangsdaten.txt     | gelöscht   | Textdatei      | Zugangsdaten zu einem VPN-Server, Inhalt rekonstruierbar |
| /Zugänge       | admin_passwoerter.xlsx   | vorhanden  | Excel-Datei    | Plausible Liste mit Admin-Zugangsdaten              |
| /Privat        | nudes.jpg                | gelöscht   | Bild           | Provokanter Dateiname, Inhalt unbedenklich          |
| /Downloads     | spotify_crack.zip        | vorhanden  | ZIP-Archiv     | Verdacht auf illegale Software, enthält leere Datei |
| /Tools         | putty.exe                | vorhanden  | .exe-Datei     | Typische Remote-Access-Software                     |
| /Gelöscht      | gehaltsliste_2022.xlsx   | gelöscht   | Excel-Datei    | Interne Gehaltsdaten, rekonstruierbar               |
| /Gelöscht      | kündigung.docx           | gelöscht   | Word-Dokument  | Enthält Kündigungsschreiben                         |
| /Privat        | urlaub2023.jpg           | vorhanden  | Bild           | Privatbild, unauffällig                             |

### 4.2 Zeitstempelanalyse (MACB)

Die Analyse der Dateiattribute zeigt bei mehreren Dateien Unterschiede zwischen Erstellungs- und Änderungszeit. Dies spricht für eine gezielte Nutzung und nachträgliche Bearbeitung.

Beispiele:

- **Firmenintern.docx**  
  - Erstellt: 06.05.2025, 18:48 Uhr  
  - Zuletzt geändert: 06.05.2025, 18:51 Uhr  
  - Bearbeitet mit: Microsoft Office Word  
  → Die Datei wurde innerhalb weniger Minuten nach Erstellung bearbeitet, was auf eine bewusste Anpassung vor dem Speichern oder Weitergeben hindeuten kann.

- **Temporäre Word-Dateien (_WRD0000.tmp, _WRD0002.tmp, _WRL0001.tmp)**  
  - Alle erstellt und modifiziert zwischen 18:48 Uhr und 18:51 Uhr  
  - Gehören zu einer Word-Sitzung, die Dateiänderungen speichert  
  → Diese Dateien bestätigen die Bearbeitung von `Firmenintern.docx` und geben Hinweise auf den Zeitpunkt und Umfang der Nutzung.

Solche Zeitstempel-Muster lassen sich als Hinweis auf gezielte inhaltliche Bearbeitungen interpretieren – insbesondere, wenn sie in engem zeitlichen Zusammenhang mit Löschvorgängen oder Zugriffen stehen.

Alle analysierten Zeitstempel (Erstellung, Änderung und Zugriff) befinden sich innerhalb eines kompakten Zeitraums von etwa [18:45 Uhr bis 19:04 Uhr] am 06.05.2025. Dies spricht für eine konzentrierte Nutzung des USB-Sticks in einer kurzen Sitzung, vermutlich im Zusammenhang mit gezielten Dateioperationen wie dem Erstellen, Bearbeiten und anschließenden Löschen sensibler Inhalte.

[Dateiübersicht der analysierten Zeitstempel](../dokumentation/Metadata_MACB.csv)

### 4.3 Artefakte

Bei der Analyse konnten mehrere typische Nutzungsartefakte identifiziert werden:

- **Temporärdateien**: Im Wurzelverzeichnis des USB-Sticks fanden sich temporäre Dateien mit den Präfixen `~WRD` und `~WRL` (z. B. `_WRD0000.tmp`, `_WRL0001.tmp`). Diese werden von Microsoft Word beim Bearbeiten von Dokumenten automatisch erzeugt. Ihr Vorhandensein deutet darauf hin, dass mindestens ein Word-Dokument (z. B. `firmenintern.docx`) aktiv geöffnet und bearbeitet wurde. Da diese Dateien nicht gelöscht wurden, ist davon auszugehen, dass die Bearbeitung nicht ordnungsgemäß abgeschlossen oder dass gezielt manipuliert wurde.

- **Verdächtige Ordnerstruktur**: Die existierenden Verzeichnisse `/Zugänge`, `/Privat` und `/Gelöscht` legen eine thematische Sortierung sensibler Inhalte nahe. Im Ordner `/Gelöscht` fanden sich rekonstruierbare Dateien mit potenziell vertraulichem Inhalt (z. B. `gehaltsliste_2022.xlsx`, `vpn_zugangsdaten.txt`).

- **Gelöschte Dateien**: Die exportierte Liste gelöschter Dateien zeigt, dass mehrere dieser sensiblen Dateien nach ihrer Erstellung oder Bearbeitung gezielt gelöscht wurden. Sie konnten jedoch vollständig wiederhergestellt und analysiert werden.

- **$Recycle.Bin**: Überreste im Papierkorb-Ordner belegen, dass mehrere Dateien nicht endgültig gelöscht, sondern zunächst in den Papierkorb verschoben wurden – ein typisches Verhalten bei Löschung über die Benutzeroberfläche.

Eine vollständige Übersicht der gelöschten Dateien befindet sich hier: 

[Dateiübersicht der gelöschten Dateien](../dokumentation/deleted_files.csv)

## 5. Bewertung & Schlussfolgerung

Die forensische Untersuchung hat ergeben, dass der USB-Stick **gezielt und bewusst genutzt wurde**, um dienstlich relevante sowie potenziell sensible Dateien zu speichern, zu bearbeiten und anschließend teilweise zu löschen. Die analysierte Ordnerstruktur, Dateinamen und gelöschten Inhalte lassen auf eine strukturierte und thematisch gegliederte Ablage schließen.

Zeitstempelanalysen (MACB) sowie die identifizierten Artefakte deuten auf eine **kompakte Nutzungssitzung** am 06.05.2025 hin, bei der gezielte Dateioperationen vorgenommen wurden. Temporärdateien aus Microsoft Word sowie gelöschte, aber rekonstruierbare Dokumente belegen eine aktive Nutzung zur Bearbeitung interner Inhalte. Die Verwendung von Dateinamen wie `vpn_zugangsdaten.txt` oder `gehaltsliste_2022.xlsx` sowie der Versuch, diese zu löschen oder im Ordner `/Gelöscht` abzulegen, spricht für ein **bewusstes Vorgehen**, möglicherweise mit dem Ziel, Spuren zu verschleiern oder Dateien unauffällig zu entfernen.

Im Rahmen der Zielsetzung – nämlich die Wiederherstellung gelöschter Inhalte und die Nachvollziehbarkeit der Nutzung – konnten die gestellten Fragen vollständig beantwortet und der Ablauf der Nutzung plausibel rekonstruiert werden.

## 6. Screenshots & Belege

Siehe Ordner `/screenshots/` im Repository.

---

## 7. Hinweise & Limitierungen

- Das Image wurde auf einem Testsystem ohne Write-Blocker erstellt (kein Produktiveinsatz)
- Alle verwendeten Inhalte wurden ausschließlich zu Ausbildungszwecken erzeugt
- Eine weitergehende Hash-Analyse mit bekannten Malware-Signaturen wurde nicht durchgeführt

---

## 8. Anhang

- `usb_image.001.csv` – Vollständige Dateiliste
- `Metadata_MACB.csv` – Zeitstempelanalyse
- `deleted_files.csv` – Übersicht gelöschter Dateien
- `image_hashwerte.txt` – Hashverlauf und Image-Protokoll

---

*Ende des Berichts – Erstellt am [07.05.2025]*

