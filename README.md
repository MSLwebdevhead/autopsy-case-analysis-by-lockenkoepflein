# Forensische Analyse eines USB-Sticks – Fallstudie mit Autopsy

## Projektübersicht
Dieses Projekt simuliert eine reale forensische Untersuchung eines USB-Sticks. Ziel ist es, gelöschte, manipulierte oder verdächtige Dateien wiederherzustellen und die Benutzeraktivität nachvollziehbar zu dokumentieren. Das Image wurde auf einem präparierten USB-Stick selbst erstellt, analysiert und in einem strukturierten Gutachten ausgewertet.

Die Untersuchung wurde mit dem forensischen Tool **Autopsy** durchgeführt.

---

## Fallbeschreibung
Am Arbeitsplatz wird ein USB-Stick gefunden, dessen Inhalt auf eine mögliche missbräuchliche Nutzung hindeutet. Es besteht der Verdacht, dass vertrauliche Dokumente und Programme zur Umgehung von Sicherheitsrichtlinien darauf gespeichert wurden. Einige Dateien scheinen gelöscht oder manipuliert worden zu sein.

---

## Zielsetzung
- Erstellung eines forensischen Images des USB-Sticks im RAW-Format
- Rekonstruktion gelöschter Dateien
- Analyse von Dateinamen, Zeitstempeln und Ordnerstrukturen
- Beurteilung der Relevanz der aufgefundenen Daten

---

## Methodik

### Vorbereitung
1. Erstellung eines realitätsnahen Datei-Sets auf dem USB-Stick:
   - `vpn_zugangsdaten.txt`
   - `gehaltsliste_2022.xlsx`
   - `putty.exe` (Platzhalterdatei)
   - `nudes.jpg` (harmloses Testbild)
2. Teilweises Löschen und Bearbeiten der Dateien
3. Strukturierung in Ordnern wie `/Privat`, `/Zugänge`, `/Gelöscht`

### Imaging
- Erstellung eines forensischen 1:1-Abbilds (`.dd`) mit **FTK Imager**
- Berechnung von MD5- und SHA1-Hashwerten
- Sicherung des Images auf separatem Datenträger

### Analyse
- Import des Images in **Autopsy**
- Aktivierung der Module:
  - Gelöschte Dateien
  - Zeitstempel / MACB-Timeline
  - Dateisystemstruktur
  - Dateitypen-Übersicht
- Screenshots und Notizen zur Auswertung

---

## Ergebnisse (Beispiele)
- **Gelöschte Datei wiederhergestellt**: `vpn_zugangsdaten.txt` mit Referenzen auf interne Systeme
- **Manipulierter Zeitstempel** bei `gehaltsliste_2022.xlsx` – Diskrepanz zwischen „Last Access“ und „Modified“
- **Datei mit auffälligem Namen** (`nudes.jpg`) in `/Privat`, geöffnet vor Löschung
- Leerer ZIP-Container (`keylogger.zip`) gefunden, jedoch ohne Inhalt

---

## Fazit
Die Analyse ergab mehrere Hinweise auf die Nutzung des USB-Sticks für potenziell dienstwidrige Zwecke. Gelöschte Dateien konnten teilweise rekonstruiert werden. Die Zeitstempel legen nahe, dass einzelne Dateien gezielt gelöscht oder umbenannt wurden. Dieses Projekt zeigt, wie digitale Artefakte auch nach Löschung verwertbar bleiben.

---

## Screenshots
(Screenshots der Analyse-Oberfläche, Fundstellen, Zeitachsen können hier ergänzt werden)

---

## Rechtlicher Hinweis
Alle in diesem Projekt verwendeten Daten wurden vom Autor zu Ausbildungszwecken erstellt. Es wurden keine personenbezogenen oder sensiblen Daten Dritter verwendet.

---

## Über mich
Ich bin Studentin im Studiengang **Cyber Security (B.Sc.)** mit besonderem Interesse an **IT-Forensik** und digitaler Beweissicherung im öffentlichen Dienst. Dieses Projekt entstand im Eigenstudium zur Vertiefung forensischer Kompetenzen.

---

## Lizenz
Dieses Repository steht unter der MIT-Lizenz. Das erzeugte Image ist nicht enthalten und verbleibt aus Datenschutz- und Speichergründen lokal.
