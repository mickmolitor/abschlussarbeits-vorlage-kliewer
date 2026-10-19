# LaTeX-Formatvorlage für Abschluss- und Seminararbeiten

Vorlage der Professur für Wirtschaftsinformatik der Freien Universität Berlin. Sie läuft direkt auf [Overleaf](https://www.overleaf.com), auch mit einem kostenlosen Account.

## Ordner und Dateien

| Pfad | Inhalt |
|---|---|
| `main.tex` | Wurzeldokument, aus dem das PDF erstellt wird |
| `Bilder/` | alle Bilder und Grafiken der Arbeit |
| `Kapitel/` | je Kapitel eine `.tex`-Datei |
| `Literatur/quellen.bib` | alle Literaturangaben (BibTeX-Format) |
| `Titel/titel.tex` | Deckblatt (Titel, Name, Betreuung usw.) |

## Wurzeldokument `main.tex`

Ob die Arbeit als Online- oder als Druckversion erzeugt wird, legt die `\documentclass`-Zeile fest: `twoside=off` für die Onlineversion, `twoside=on` für die Druckversion.

Die Datei ist in zwei Teile gegliedert:

1. **Packages:** In der Regel sind hier keine Änderungen nötig. Alle Formatierungen (Schrift, Seitenränder, Zeilenabstand, Seitenzahlen, Überschriften, Verzeichnisse) sind hier zentral eingestellt. Auf Overleaf sind alle Pakete bereits installiert; lokal empfiehlt sich eine vollständige TeX-Live- bzw. MiKTeX-Installation.
2. **Document:** Hier werden die Bestandteile der Arbeit eingebunden, z. B. Titelblatt, Abstract, Verzeichnisse, Kapitel und Literaturverzeichnis.
   - Der **Sperrvermerk** (`Kapitel/X_sperrvermerk.tex`) ist standardmäßig auskommentiert. Er wird nur bei Arbeiten mit vertraulichen Unternehmensdaten benötigt; dann die entsprechenden Zeilen in `main.tex` einkommentieren.
   - Das **Abkürzungsverzeichnis** wird in `Kapitel/0_abkuerzungen.tex` gepflegt.

Zeilen, die mit `%` beginnen, sind Kommentare und werden beim Übersetzen ignoriert.

## Übersetzen (Kompilieren)

Die Vorlage nutzt BibTeX mit dem Paket `apacite` (Zitierstil APA) und den Zitierbefehlen aus `natbib`.

```
pdflatex -> bibtex -> pdflatex -> pdflatex
```

Overleaf und `latexmk` führen diese Schritte automatisch aus.

> **Warum nicht biblatex/biber?** biber ist deutlich langsamer als bibtex. Der erste Komplettbuild dauert damit etwa doppelt so lange und überschreitet das Compile-Zeitlimit von Overleaf im kostenlosen Account (10 Sekunden). `biblatex` daher nicht zusätzlich laden – es ist mit `natbib` und `apacite` inkompatibel und erzeugt Fehler.

### Hinweise zu Overleaf (kostenloser Account)

Der allererste Durchlauf ist der teuerste, weil alle Hilfsdateien neu erzeugt werden müssen. Danach nutzt Overleaf die zwischengespeicherten Hilfsdateien, und jede weitere Kompilierung braucht meist nur noch einen Lauf.

- „Recompile from scratch“ (löscht den Cache) nur gezielt nutzen.
- Während des Schreibens den Modus „Fast [draft]“ (Pfeil neben „Recompile“) wählen.
- Große Bilder (hochauflösende Fotos oder Screenshots) vorab verkleinern.

## Zitieren (natbib + apacite)

Die wichtigsten Zitierbefehle, wie sie auch in Tabelle 2.1 der Vorlage gezeigt werden (Ausgabe im APA-Stil):

| LaTeX-Quellcode | Ergebnis im PDF |
|---|---|
| `\citep{kliewer2006time}` | (Kliewer, Mellouli & Suhl, 2006) |
| `\citet{kliewer2006time}` | Kliewer et al. (2006) zeigen … |
| `\citep[S.~1620]{kliewer2006time}` | (Kliewer et al., 2006, S. 1620) |
| `\citep[vgl.][]{kliewer2006time}` | (vgl. Kliewer et al., 2006) |
| `\citeauthor{kliewer2006time}` | Kliewer et al. |
| `\citeyear{kliewer2006time}` | 2006 |
| `\citep{kliewer2006time,gopen1990science}` | (Gopen & Swan, 1990; Kliewer et al., 2006) |

**Faustregel:** `\citep` setzt den gesamten Verweis in Klammern und eignet sich, wenn die zitierten Personen nicht Teil des Satzes sind. `\citet` macht die zitierten Personen zum Satzsubjekt. Über die optionalen Argumente in eckigen Klammern lassen sich Seitenangaben oder Zusätze wie „vgl.“ ergänzen.

Bei der ersten Nennung einer Quelle mit drei bis fünf Namen schreibt APA alle Namen aus, danach „et al.“ – das erledigt `apacite` automatisch (siehe erste Zeile der Tabelle). Mehrere Quellen in einem Befehl werden alphabetisch sortiert.

Das Literaturverzeichnis wird am Ende von `main.tex` mit `\bibliography{Literatur/quellen}` ausgegeben und enthält automatisch alle zitierten Quellen. Hinweise zum Format der Einträge stehen als Kommentar am Anfang von `Literatur/quellen.bib`.

## Erklärungen am Ende der Arbeit

### Eigenständigkeitserklärung

Die Eigenständigkeitserklärung (`Kapitel/6_1_eigenstaedigkeitserklaerung.tex`) ist bereits in der Vorlage enthalten und muss unverändert übernommen werden. Damit versichern Sie, dass Sie die Arbeit selbstständig verfasst, alle verwendeten Quellen korrekt angegeben und keine unzulässigen Hilfsmittel verwendet haben.

### Verantwortungsvoller Umgang mit generativer KI

Grundsätzlich sind wir als Wirtschaftsinformatik-Lehrstuhl offen für neue Technologien und sehen in generativer KI großes Potenzial. In einigen Arbeiten ist ihr Einsatz sogar explizit Gegenstand der Untersuchung. Gleichzeitig erwarten wir für Abschlussarbeiten einen verantwortungsvollen Umgang im Sinne der KI-Richtlinien der FU Berlin: KI in der Lehre

Konkrete Anforderungen:

- Fügen Sie Ihrer Arbeit die KI-Erklärung nach Gimpel et al. (2023) bei. Das Formular (`Kapitel/6_2_kognition.tex`) ist bereits in der Vorlage enthalten.
- Beachten Sie, dass die Nutzung generativer KI auch bei vollständiger Offenlegung und dokumentierter Herkunft (Provenance) eine Grenzüberschreitung im wissenschaftlichen Sinne darstellen kann.

Grenzüberschreitungen liegen insbesondere vor, wenn

- Referenzen falsch oder vollständig fabriziert sind (sogenannte „Halluzinationen“ der KI),
- kontextspezifisches Wissen vorgetäuscht wird (z. B. Erfahrungen, Daten oder Aktivitäten, die nicht tatsächlich vorliegen),
- theoretische Konzepte unsauber oder oberflächlich verwendet werden,
- Verantwortung für Zitationen, Argumentation, Interpretation oder Beiträge an die KI delegiert wird.

> **Wichtig:** Nicht jede dieser Grenzüberschreitungen führt automatisch zum Nichtbestehen. Entscheidend ist jedoch, dass Sie die Verantwortung für Ihre Arbeit übernehmen und die Standards wissenschaftlichen Arbeitens einhalten.

## Software

- **[Overleaf](https://www.overleaf.com)** – kollaborativer Online-Editor, keine Installation nötig
- **TeXworks / TeXstudio** – lokale Bearbeitung und Erstellung der PDF-Dokumente
- **MiKTeX / TeX Live** – lokale LaTeX-Distribution (optional)
- **JabRef, Zotero, Citavi** – Literaturverwaltung und Export als `.bib`-Datei (optional)
