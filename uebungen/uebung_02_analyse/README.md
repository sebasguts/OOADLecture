# Übungsblatt 2: Objektorientierte Analyse (OOA)
**Modul 2: Anforderungsanalyse, Akteure, Use Cases, Cockburn-Szenarien, User Stories & BDD, Aktivitätsdiagramme & Abbott-Methode**

---

## Kontext & Problemstellung: "GreenOffice" – Das B2B-Pflanzenabo bei Ada

*Ada's Botanical Innovations* erweitert das Geschäftsmodell um ein neues Standbein: **"GreenOffice"**, ein Rundum-Sorglos-Pflanzenabonnement für Unternehmen und Kanzleien. Geschäftskunden kaufen keine einzelnen Pflanzen mehr, sondern mieten vorkonfigurierte Begrünungspakete für ihre Büro- und Konferenzräume inklusive regelmäßiger Pflege vor Ort durch professionelle Servicegärtner (z. B. Gießen, Düngen, Schädlingskontrolle und kostenloser Austausch eingehender Pflanzen).

Um das neue Angebot online zu skalieren, soll der Prozess rund um die **Konfiguration und den verbindlichen Abschluss eines Büro-Pflanzenabonnements** softwareseitig analysiert und entworfen werden. 

Ihre Aufgabe ist es, für diesen neuen Geschäftsbereich eine strukturierte **Objektorientierte Analyse (OOA)** durchzuführen.

---

## Aufgabe 1: Lastenheft vs. Pflichtenheft & Akteursanalyse

1. **Lastenheft vs. Pflichtenheft:**  
   Erklären Sie den Unterschied zwischen Lastenheft (*Was will der Auftraggeber?*) und Pflichtenheft (*Wie und womit setzt der Auftragnehmer dies verbindlich um?*). Formulieren Sie für das B2B-Pflanzenabo jeweils zwei konkrete, fachlich differenzierte Anforderungen.
2. **Akteursidentifikation:**  
   - Wer ist der **primäre Akteur** des Buchungsprozesses?
   - Welche **unterstützenden / sekundären Akteure** (z. B. Fremdsysteme, Dienstleister oder interne Servicerollen) sind beteiligt?
   - Erläutern Sie anhand eines konkreten Beispiels aus dem Bürokontext, warum in der objektorientierten Analyse strikt zwischen **Person** und **Akteur / Rolle** unterschieden werden muss.

---

## Aufgabe 2: UML-Use-Case-Modellierung mit `<<include>>` und `<<extend>>`

Modellieren Sie das Teilsystem rund um den zentralen Anwendungsfall **"Büro-Pflanzenabo abschließen"**:
1. **Beziehungen identifizieren & begründen:**  
   - Bestimmen Sie mindestens einen zwingend notwendigen Teilschritt (`<<include>>`) sowie mindestens eine optionale oder bedingte Erweiterung (`<<extend>>`). Begründen Sie Ihre Einordnung fachlich.
2. **Diagrammerstellung:**  
   - Erstellen Sie das vollständige UML-Use-Case-Diagramm in valider Mermaid-Syntax (`flowchart LR`).
   - Achten Sie exakt auf die Standard-Pfeilrichtungen nach OMG UML 2.5 für Include- und Extend-Beziehungen sowie auf die korrekte Verbindungsart zwischen Akteuren und Anwendungsfällen.

---

## Aufgabe 3: Vollständige 9-Punkte-Cockburn-Szenariotabelle

Spezifizieren Sie den Use Case **"Büro-Pflanzenabo abschließen"** tabellarisch nach der 9-Punkte-Vorlage von Alistair Cockburn:
1. **Name & ID**
2. **Beteiligte Akteure** (differenziert nach Primär, Sekundär und System)
3. **Vorbedingungen** (mindestens 2 überprüfbare Vorbedingungen)
4. **Nachbedingungen** (Erfolgsgarantien sowie Minimalgarantie im Fehlerfall)
5. **Auslöser (Trigger)**
6. **Standardablauf (Happy Path)** (nummerierte Schritte von der Auslösung bis zum erfolgreichen Abschluss)
7. **Alternative Pfade** (mindestens 2 fachlich plausible Verzweigungen)
8. **Fehlerfälle (Exceptions)** (mindestens 2 Ausnahmebehandlungen inkl. Systemreaktion)
9. **Offene Punkte / Fachfragen** (mindestens 1 regulatorische oder operative Fragestellung)

---

## Aufgabe 4: Agile Spezifikation: User Story & BDD-Akzeptanzkriterien

Überführen Sie die Anforderungen aus Aufgabe 3 in eine agile Spezifikation:
1. **User Story:**  
   Formulieren Sie das Kernziel des B2B-Kunden als User Story im Standard-Template:  
   `Als <Rolle> möchte ich <Ziel / Funktionalität>, um <fachlicher Nutzen>.`
2. **BDD-Akzeptanzkriterien:**  
   Formulieren Sie für diese Story zwei ausführbare Testszenarien in deutscher Gherkin-Syntax (`# language: de`):
   - **Szenario 1 (Happy Path):** Erfolgreicher Abschluss des Abonnements inklusive Bonitätsprüfung, Zahlungsplan und Disposition des Pflegeteams.
   - **Szenario 2 (Defensive Validierung):** Ein Fehlerfall (z. B. Adresse liegt außerhalb des Betreuungsgebiets für Vor-Ort-Pflege oder Bonitätsprüfung schlägt fehl). Das System muss defensiv reagieren, den Vertrag blockieren und eine fachlich verständliche Alternative oder Begründung ausgeben.

---

## Aufgabe 5: Ablaufmodellierung mit UML-Aktivitätsdiagramm

Modellieren Sie den dynamischen Kontrollfluss für den Abschluss des Büro-Pflanzenabos als **Aktivitätsdiagramm** in Mermaid-Syntax (`flowchart TD`):
- Startknoten und initialer Einstieg.
- Mindestens ein **Entscheidungsknoten (Decision)** zur Prüfung einer Geschäftsregel mit zwei klar abgegrenzten Ausgängen (Guards).
- Eine **parallele Verzweigung (Fork / Join)** für mindestens zwei Aufgaben, die fachlich unabhängig voneinander abgearbeitet werden können, bevor der Prozess synchronisiert weiterläuft.
- Erfolgreicher und fehlerhafter Endknoten.

---

## Aufgabe 6: OOA-zu-OOD-Übergang mit der Abbott-Methode & Bounded Contexts

Gegeben ist folgende Beschreibung der Fachanforderung:
> *"Ein verifizierter Geschäftskunde konfiguriert für seine Büroflächen ein monatliches Pflanzenabonnement mit gewünschtem Raumpaket und Startdatum. Das System prüft die Postleitzahl der Firmenadresse gegen das Betreuungsgebiet für Vor-Ort-Pflege und holt über einen externen Auskunftsdienst eine Bonitätsauskunft ein. Ist die Bonität ausreichend, richtet das System ein SEPA-Firmenlastschriftmandat ein und ermittelt den monatlichen Abonnementpreis unter Berücksichtigung gewählter Zusatzoptionen. Parallel reserviert das System die Anfangsausstattung an Büropflanzen im Bestand und weist dem Servicegärtner einen Erstausstattungstermin im Tourenplan zu. Nach erfolgreicher Bestätigung wird das Abonnement aktiviert und die Vertragsbestätigung an den Kunden versendet."*

1. **Abbott-Analyse (Substantiv-Verb-Analyse):**
   - **Substantive:** Ordnen Sie die extrahierten Begriffe begründet den Kategorien **Entity** (eindeutige Identität & Lebenszyklus) und **Value Object** (unveränderlicher Wert, Gleichheit über Attribute) zu.
   - **Verben:** Leiten Sie Methoden ab und weisen Sie diese nach dem GRASP-Muster *Information Expert* den passenden Klassen zu.
   - **Adjektive / Zustände:** Leiten Sie relevante Status-Enums ab.
2. **Bounded Contexts (Domain-Driven Design):**  
   Grenzen Sie mindestens drei Bounded Contexts für die Gesamtlösung voneinander ab. Diskutieren Sie anhand der Begriffe **"Kunde"** und **"Status"**, warum ein globales, einheitliches Datenmodell problematisch wäre und welche unterschiedlichen Verantwortungen diese Begriffe in den jeweiligen Kontexten tragen.
