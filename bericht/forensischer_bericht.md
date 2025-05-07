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

![Hashwerte Screenshot](../screenshots/Screenshot_Hash_Values.png)

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

Alle analysierten Zeitstempel (Erstellung, Änderung und Zugriff) befinden sich innerhalb eines kompakten Zeitraums von etwa [z. B. 18:45 Uhr bis 19:05 Uhr] am 06.05.2025. Dies spricht für eine konzentrierte Nutzung des USB-Sticks in einer kurzen Sitzung, vermutlich im Zusammenhang mit gezielten Dateioperationen wie dem Erstellen, Bearbeiten und anschließenden Löschen sensibler Inhalte.

[Dateiübersicht der analysierten Zeitstempel](../dokumentation/Metadata_MACB.csv)

### 4.3 Artefakte

Bei der Analyse konnten mehrere typische Nutzungsartefakte identifiziert werden:

- **Temporärdateien**: Im Wurzelverzeichnis des USB-Sticks fanden sich temporäre Dateien mit den Präfixen `~WRD` und `~WRL` (z. B. `_WRD0000.tmp`, `_WRL0001.tmp`). Diese werden von Microsoft Word beim Bearbeiten von Dokumenten automatisch erzeugt. Ihr Vorhandensein deutet darauf hin, dass mindestens ein Word-Dokument (z. B. `firmenintern.docx`) aktiv geöffnet und bearbeitet wurde. Da diese Dateien nicht gelöscht wurden, ist davon auszugehen, dass die Bearbeitung nicht ordnungsgemäß abgeschlossen oder dass gezielt manipuliert wurde.

- **Verdächtige Ordnerstruktur**: Die existierenden Verzeichnisse `/Zugänge`, `/Privat` und `/Gelöscht` legen eine thematische Sortierung sensibler Inhalte nahe. Im Ordner `/Gelöscht` fanden sich rekonstruierbare Dateien mit potenziell vertraulichem Inhalt (z. B. `gehaltsliste_2022.xlsx`, `vpn_zugangsdaten.txt`).

- **Gelöschte Dateien**: Die exportierte Liste gelöschter Dateien zeigt, dass mehrere dieser sensiblen Dateien nach ihrer Erstellung oder Bearbeitung gezielt gelöscht wurden. Sie konnten jedoch vollständig wiederhergestellt und analysiert werden.

- **$Recycle.Bin**: Überreste im Papierkorb-Ordner belegen, dass mehrere Dateien nicht endgültig gelöscht, sondern zunächst in den Papierkorb verschoben wurden – ein typisches Verhalten bei Löschung über die Benutzeroberfläche.

Eine vollständige Übersicht der gelöschten Dateien befindet sich hier: 


---

## 5. Bewertung & Schlussfolgerung

Die forensische Analyse hat gezeigt, dass der USB-Stick **gezielt genutzt wurde**, um sensible oder auffällig benannte Dateien zu speichern und anschließend teilweise zu löschen. Die wiederhergestellten Daten lassen auf eine **intentionale Nutzung im Kontext dienstlicher Informationen** schließen.

---

## 6. Screenshots & Belege

Siehe Ordner `/screenshots/` im Repository.

---

## 7. Hinweise & Limitierungen

- Das Image wurde auf einem Testsystem ohne Write-Blocker erstellt (kein Produktiveinsatz)
- Alle verwendeten Inhalte wurden ausschließlich zu Ausbildungszwecken erzeugt
- Eine weitergehende Hash-Analyse mit bekannten Malware-Signaturen wurde nicht durchgeführt

---

## 8. Anhang (optional)

- Image-Metadaten
- Zeitachsenübersicht
- Dateiübersicht (CSV)

---

*Ende des Berichts – Erstellt am [TT.MM.JJJJ]*

