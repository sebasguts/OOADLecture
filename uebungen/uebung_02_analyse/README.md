# Übungsblatt 2: Objektorientierte Analyse & Übergang zum Design
**Modul 2: Anforderungsanalyse, Akteure, Use Cases, 9-Punkte-Szenarien, Aktivitätsdiagramme, Defensive UI (Poka-Yoke), BDD & Abbott-Methode**

---

## Kontext & Problemstellung: „GreenOffice“ – Das B2B-Pflanzenabo bei Ada

*Ada's Botanical Innovations* erweitert das Geschäftsmodell um ein neues Standbein: **„GreenOffice“**, ein Rundum-Sorglos-Pflanzenabonnement für Unternehmen, Arztpraxen und Kanzleien. Geschäftskunden kaufen keine einzelnen Pflanzen mehr, sondern mieten vorkonfigurierte Begrünungspakete für ihre Büro- und Konferenzräume inklusive regelmäßiger Pflege vor Ort durch professionelle Servicegärtner (Gießen, Düngen, Schädlingskontrolle und kostenloser Austausch kranker Pflanzen).

Um das neue Angebot online zu skalieren, soll der Prozess rund um die **Konfiguration und den verbindlichen Abschluss eines Büro-Pflanzenabonnements** softwareseitig analysiert und in ein erstes fachliches Klassenmodell überführt werden.

Ihre Aufgabe ist es, für diesen neuen Geschäftsbereich eine strukturierte **Objektorientierte Analyse (OOA)** bis hin zum **ersten Python-Klassenentwurf (OOD)** durchzuführen.

---

## Aufgabe 1: Lastenheft vs. Pflichtenheft & Rollenanalyse

1. **Lastenheft vs. Pflichtenheft:**  
   Erklären Sie präzise den Unterschied zwischen **Lastenheft** (*Auftraggeber-Perspektive: WAS & WARUM*) und **Pflichtenheft** (*Auftragnehmer-Perspektive: WIE & WOMIT, prüfbar und messbar*). Formulieren Sie für das *GreenOffice*-Pflanzenabo jeweils zwei konkrete, fachlich korrespondierende Anforderungen im direkten Vergleich.
2. **Akteursidentifikation & Rollenbegriff:**  
   - Wer ist der **primäre Akteur** des Buchungsprozesses?
   - Welche **sekundären / unterstützenden Akteure** (z. B. externe Auskunfteien, Bank-Gateways oder interne Servicerollen) sind beteiligt?
   - Erläutern Sie anhand eines konkreten Beispiels (z. B. Kanzleipartnerin Frau Dr. Weber), warum in der OOA strikt zwischen einer konkreten **Person** und einer **Rolle (Actor)** unterschieden werden muss.

---

## Aufgabe 2: UML-Use-Case-Modellierung mit `<<include>>` und `<<extend>>`

Modellieren Sie das Teilsystem rund um den zentralen Anwendungsfall **„Büro-Pflanzenabo abschließen“**:
1. **Beziehungen identifizieren & begründen:**  
   - Bestimmen Sie mindestens zwei zwingend notwendige Teil-Use-Cases (`<<include>>`, z. B. Bonitätsprüfung, SEPA-Zahlungsplan) sowie mindestens zwei optionale bzw. bedingte Erweiterungen (`<<extend>>`, z. B. Vor-Ort-Lichtanalyse, IoT-Sensor-Monitoring). Begründen Sie Ihre Zuordnung fachlich.
   - Begründen Sie, warum ein einzelner Bedienschritt wie *„Postleitzahl-Eingabefeld auf 5 Ziffern prüfen“* **kein** eigenständiger Use Case im Diagramm sein darf (Gefahr der funktionalen Zerlegung).
2. **Diagrammerstellung:**  
   - Erstellen Sie das vollständige UML-Use-Case-Diagramm in valider Mermaid-Syntax (`flowchart LR`).
   - Achten Sie exakt auf die **Pfeilrichtungen** für `<<include>>` (`Basis -.->|include| Teilfall`) und `<<extend>>` (`Erweiterung -.->|extend| Basis`) sowie auf ungerichtete Linien (`---`) zwischen Akteuren und Use Cases.

---

## Aufgabe 3: Vollständige 9-Punkte-Szenariotabelle nach Cockburn

Spezifizieren Sie den Use Case **„UC-05: Büro-Pflanzenabo abschließen“** vollständig mit allen 9 Feldern aus der Vorlesung:
- **1. Name & ID** | **2. Kurzbeschreibung** | **3. Beteiligte Akteure & Kürzel**
- **4. Vorbedingungen** (mindestens 2 bereits gesicherte Zustände)
- **5. Nachbedingungen** (Erfolgsgarantien + **Minimalgarantie** bei Abbruch/Fehler)
- **6. Auslöser (Trigger)**
- **7. Standardszenario (Happy Path):** Nummerierte Schritte `1.` bis `n.` ohne `if/else`-Verzweigungen
- **8. Alternative Pfade (Extensions):** Mindestens 2 erfolgreiche Verzweigungen (z. B. `1a.`, `1b.`)
- **9. Fehlersituationen / Ausnahmen:** Mindestens 3 konkrete Fehlerpfade (z. B. Adresse außerhalb des Gärtner-Betreuungsgebiets, Bonität abgelehnt, kein freier Gärtner-Slot) inklusive sauberer Kompensation/Aufräumarbeit des Systems.

---

## Aufgabe 4: UML-Aktivitätsdiagramm (Kontrollfluss & Parallelität)

Übersetzen Sie Ihre Szenariotabelle aus Aufgabe 3 in ein **UML-Aktivitätsdiagramm** (`flowchart TD`):
1. Modellieren Sie die Prüfungen für Pflegegebiet und Bonität als Entscheidungsknoten (`{ }`) mit **Guards** in eckigen Klammern (`[PLZ im Pflegegebiet]`).
2. Nutzen Sie eine **parallele Verzweigung (`=== FORK ===` und `=== JOIN ===`)** für die gleichzeitige Reservierung der Pflanzen im Lager und die Terminbuchung im Tourenplaner des Servicegärtners.

---

## Aufgabe 5: Defensives UI-Design (Poka-Yoke) & Agile BDD-Spezifikation

1. **UI-Mockup & Poka-Yoke (Fehlerprävention):**  
   - Entwerfen Sie ein strukturiertes Mockup (als übersichtliche Text-/HTML-Skizze) für die Buchungsmaske von *GreenOffice* in zwei Zuständen: **Zustand A (Happy Path)** vs. **Zustand B (Defensiver Fehlerzustand bei PLZ außerhalb des Betreuungsgebiets)**.
   - Zeigen Sie konkret, wie das **Poka-Yoke-Prinzip** mindestens zwei Bedienfehler verhindert (Deaktivieren des Abo-Buttons mit verständlicher Inline-Begründung + direkter Alternativvorschlag *„Einmaliger Kauf per Spedition“*).
   - Erklären Sie, warum eine solche UI-Sperre im Browser allein niemals ausreicht und im Backend-Code erneut geprüft werden muss (`F12`-Problem).
2. **Agile User Story & Ausführbare BDD-Tests (Gherkin):**  
   - Formulieren Sie eine User Story nach dem Schema `Als [Rolle] möchte ich [Ziel], damit [fachlicher Nutzen]`.
   - Schreiben Sie drei präzise Gherkin-Szenarien (`# language: de` mit `Angenommen` / `Wenn` / `Dann`):
     1. *Happy Path* (Erfolgreicher Abschluss inkl. Bonität & Tourenplanung),
     2. *Fehlerpfad 2a* (Standort außerhalb des Pflegegebiets),
     3. *Fehlerpfad 5a* (Bonitätsprüfung abgelehnt → System blockiert SEPA-Lastschrift und bietet Jahres-Vorauskasse an).

---

## Aufgabe 6: Systematischer Übergang zum Design (Abbott-Methode, GRASP & Python-Code)

Gegeben ist folgender Auszug aus der Fachbeschreibung:
> *„Ein verifizierter Geschäftskunde konfiguriert für seine Büroflächen ein monatliches Pflanzenabonnement mit gewünschtem Raumpaket und Startdatum. Das System prüft die Postleitzahl gegen das Servicegebiet für Vor-Ort-Pflege. Ist die Bonität positiv, ermittelt das Abonnement den monatlichen Beitrag in Euro und Cent aus dem Basispreis des Raumpakets und einer optionalen Sensor-Pauschale (+15,00 €). Anschließend wird das Abonnement durch Hinterlegung einer SEPA-Mandatsreferenz aktiviert.“*

1. **Abbott-Analyse & Klassifikation (Entity vs. Value Object vs. Service):**  
   Ordnen Sie die Begriffe `Geschaeftskunde`, `PflanzenAbonnement`, `ServiceTermin`, `Geldbetrag`, `RaumPaket`, `ServiceGebiet` und `AboBuchungsService` begründet den drei Grundtypen **Entity**, **Value Object** und **Service** zu. Erklären Sie dabei, warum Geldbeträge niemals als `float` gespeichert werden dürfen.
2. **GRASP Information Expert & UML-Klassendiagramm:**  
   Begründen Sie nach dem *Information-Expert-Prinzip*, welche Klasse die Methode `bedient(plz: str) -> bool` und welche Klasse die Methode `berechne_monatsbeitrag() -> Geldbetrag` erhalten muss. Zeichnen Sie das resultierende **UML-Klassendiagramm** mit Multiplizitäten und Beziehungspfeilen (`*--`, `-->`, `..>`).
3. **Python-Implementierung mit Guard Clauses (`solution.py`):**  
   Implementieren Sie in Python 3.12+:
   - Das unveränderliche Value Object `@dataclass(frozen=True) class Geldbetrag(cent: int, waehrung: str = "EUR")` mit Methoden `addiere(anderer: Geldbetrag) -> Geldbetrag` und `formatiere() -> str`.
   - Das Value Object `@dataclass(frozen=True) class ServiceGebiet(name: str, erlaubte_plz_praefixe: tuple[str, ...])` mit der Methode `bedient(plz: str) -> bool`.
   - Das Value Object `@dataclass(frozen=True) class RaumPaket(name: str, flaeche_qm: int, anzahl_pflanzen: int, basis_preis: Geldbetrag)`.
   - Das Entity `PflanzenAbonnement` mit Status-Enum `AboStatus`, Methode `berechne_monatsbeitrag() -> Geldbetrag` (inkl. optionalem `sensor_monitoring: bool`) sowie der Methode `aktivieren(plz: str, gebiet: ServiceGebiet, bonitaet_ok: bool, sepa_mandat_ref: str) -> None`, die alle Vorbedingungen aus der Szenariotabelle über **Guard Clauses** prüft und bei Verstößen sprechende Exceptions (`ValueError` / `PermissionError`) wirft.
