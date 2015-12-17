ENGLISH: This "project" is nothing more than a document I created to save a wealth of information regarding software architecture. It is entirely German, therefore the rest of this description will be German, too. If you feel like there's a need for an English edition - just fork!

# Eine (absolut subjektive) Zusammenstellung relevanter Aspekte der Software-Architektur

#### Erste Version vom 04.10.2012, letztes Update am 17.12.2015

In diesem Dokument sammle ich alle mir relevant erscheinenden Punkte zum Thema Software-Architektur. Es ist weder vollständig noch übermäßig gut sortiert aber inzwischen hat sich einiges gesammelt. 

Ich habe das Dokument im Zuge der Vorbereitung meiner Prüfung zum Certified Professional for Software Architecture erstellt.

Das Dokument besteht ausschließlich aus Stichpunkten die in bestimmten Themenkomplexen zusammengefaßt werden. Folgende Themen werden behandelt:

- Definition und Aufgaben von Software-Architekten
- Vorgehen im Entwurf von Software-Architekturen
- Qualitätsmerkmale
- Konstruktion (Schnittstellen, Bausteine/Komponenten)
- Domänenzentrierte Entwicklung
- Design Patterns
- Architektur-Patterns
- Dokumentation von Architekturen
- Bewertung von Architekturen
- Fehlerbehandlung in Architekturen
...sowie weitere Abschnitte zu spezifischeren Themen wie ATAM, Datenbanken, Sicherheit, Anforderungsanalyse, Web-Applikationen und weiteres.

Neben eigenen Praxiserfahrungen sind meine wesentlichen Quellen folgende:

- Design Patterns von Gamm/Helm/Johnson/Vlissides
- POSA 4 von Buschmann/Henney/Schmidt
- Patterns of Enterprise Application Architecture von Martin Fowler
- Basiswissen für Softwarearchitekten von Gharbi/Koschel/Rausch/Starke
- Effektive Softwarearchitekturen von Gernot Starke
- Effective Java von Joshua Bloch
- Quasar 3 von Engels/Kremer/Nötzold/Wolf/Prott/Hohwiller/Hofmann/Seidl/Schlegel/Nandico
- Software Estimation: Demystifying the black art von Steve McConnell
- Release It! von Michael T. Nygard

## Definition & Aufgaben von SW-Architekten

*   zerlegt großes Problem in kleine Teile und beschreibt eine (möglichst einfache) Lösung
*   Wurzeln liegen im Bauwesen – Gebäude sollen nützlich, fest und schön sein – das gilt auch für Software (Anforderungen, Stabilität, Struktur)
*   Architektur gilt sowohl als Bauplan als auch Ablaufplan (beschreibt eine Lösung bzw. den Lösungsweg)
*   **SW-Architektur** definiert grundlegende Prinzipien und Regeln für die Organisation eines Systems. Ein System wird in Bausteine, Schnittstellen und deren Beziehung sowie die Umgebung unterteilt. Sie legt Richtlinien für den gesamten Lebenszyklus (Analyse, Entwurf, Implementierung, Betrieb, Weiterentwicklung) sowie die Organisation von Entwicklung und Betrieb fest.
*   A. trifft übergreifende Entscheidungen, die nachträglich schwer zu ändern sind (stabiles Grundgerüst aus Bausteinen, die auch geänderte Anforderungen abbilden können)
*   Architekturziele sind meist langfristig, Projektziele oft kurzfristig
*   Kern-Aufgaben des Architekten:
	*   Anforderungen klären, A. entwerfen, Entscheidungen treffen, A. kommunizieren, Umsetzung überwachen, A. bewerten
	*   Effektiv (das Richtige tun) und effizient (Dinge richtig tun) arbeiten, dabei natürlich wirtschaftlich bleiben (optimale Nutzung der Ressourcen)
	*   fordert konkrete Qualitätsziele an
	*   Machbarkeit der Anforderungen und Qualitätsziele anhand der A. darstellen
	*   Bausteine des Systems sowie Schnittstellen und Interaktionen festlegen
	*   Lösungsansätze für übergreifende Aspekte entwerfen
	*   FAs und NFAs (Schwerpunkt!) zuordnen, reflektieren und priorisieren
	*   Architekt erklärt Wege zur Entscheidungsfindung, Vorund Nachteile, Anforderungen, Randbedingungen, Annahmen, Architekturziele (Lösungsweg)
	*   Abgrenzung von Nachbarsystemen
	*   Unterstützt bei Risikoanalyse und –vermeidung, Erarbeitung alternativer Lösungsansätze
	*   Programmierrichtlinien erarbeiten und schulen
	*   Prototypen und exemplarische Lösungen entwickeln (Vorgabe für EW, vgl. Grundriß beim Hausbau)
	*   Tester unterstützen (z.B. mit Rahmenbedingungen und Testfällen)
	*   Lebenszyklus der Software im Blick haben (einschließlich Rollout, Updates, Migration und Ablösung/Entfernen))
	*   Kommunikation aller Änderungen am System (einschließlich Version, Zeitpunkt, Umfang, sichtbarer Änderungen), definiert auch relevante KPIs für die Stakeholder (Prozess-Dauer, parallele Prozesse, Wartezeit, ...) die dann regelmäßig (durchaus täglich) kommuniziert werden sollten
	*   Kümmert sich auch um Change Requests (auch hier der gesamte Prozess mit Einreichung, Analyse, Beurteilung, Zuweisung, Priorisierung, Planung, Implementierung, Test und Verifikation)
	*   Zentraler Ansprechpartner für z.B. PL, Betrieb, EW, …
*   weitere denkbare Aufgaben von SW-Architekten: Projektplanung, Risikoanalyse, Design/Implementierung, QS
*   A. muß aber nicht nur Aufgaben generieren sondern auch Zusammenhänge darstellen (welche Aufgabe liefert/beeinflußt welches Arbeitsergebnis)
*   Typische Arbeitsergebnisse: Domänenmodell, Spezifikationen, Prozessdoku, kompakte Entscheidungsgrundlagen (für eine oder mehrere Zielgruppen)
*   Architekturrelevante Entscheidungen:
	*   betreffen Qualitätsmerkmale
	*   haben Kostenrelevanz (X Euro)
	*   haben Auswirkungen auf externe Schnittstellen
	*   haben Auswirkungen auf den Systembetrieb
	*   haben Risiken hinsichtlich Implementierung und Test
*   übergreifende Aspekte sind **Konzepte**, lassen sich in Bausteinen schlecht unterbringen:
	*   fachliche Strukturen und Modelle (Domänenmodell)
	*   Persistenz, Transaktionsund Sessionbehandlung
	*   Benutzungsoberfläche, Ergonomie (Performance, Verfügbarkeit, Robustheit)
	*   Geschäftsregeln, Validierung, Ablaufsteuerung
	*   Verteilung, Konfigurierbarkeit, Verfügbarkeit
	*   Caching, Skalierung
	*   Sicherheit, Fehlerbehandlung
	*   Build-Management, Codegenerierung, Testbarkeit
*   A. schaffen **softwareintensive Systeme**: Mehrere Bausteine erfüllen gemeinsam den Zweck des Systems, diese Bausteine bestehen ganz oder teilweise aus Software
*   Software bezeichnet dabei eine Menge von Programmen, Prozeduren und Daten sowie deren Dokumentation
*   die meisten Software-Projekte haben entweder einen Manufaktur-Ansatz (d.h. Individualsoftware, wird oft agil entwickelt) oder stützen sich auf Standard-Produkte (vor allem zur Unterstützung von Prozessen, inkrementeller Prozess)
*   oft ist schwer voraussehbar, wie lange die "Lebenszeit" eines Systems sein wird - für die Auswahl von Technologien ist dies aber relevant
*   Magisches Viereck erfolgreicher Softwareprojekte: Aufwand, Funktionalität, Zeit, Qualität
*   Drei wesentliche Systemarten (überlappen sich teilweise):
	*   **Informationssystem**: verwaltet und verarbeitet Informationen (große Datenmengen & Strukturen) z.B. Stammdaten, CAD, SAP, Simulationen / oft Schichtenarchitektur mit Transaktionen, kritisch sind meist Verfügbarkeit und Performance
	*   **Eingebettete Systeme**: kritische Anwendungen (z.B. Regelung, Steuerung, Kommunikation) unter eingeschränkten Ressourcen z.B. Waschmaschinen, Handys, Parkassistenten / Bus-Systeme mit Schwerpunkt auf Scheduling & Batches, lose gekoppelte Module, zeitkritisch, ereignisbasierte Steuerung
	*   **Mobile Systeme**: autonome S. mit hoher Interaktion mit lokalen/autonomen Funktionen (keine kontinuierliche Verbindung) z.B. Smartphone, Transportroboter, Sensoren / Shared Memory mit Schwerpunkt auf GUI und Hardware
*   alternative Unterteilung: Interaktive S., Entscheidungsunterstützung (Suche, BI), Hintergrund (Datenmanipulation), Embedded, Echtzeit
*   Bezogen auf das Web: CRUD-Anwendungen (z.B. Evernote), eCommerce (Amazon), Video/Streaming (Netflix), Desktop Application Port (Salesforce), mobile Anwendung, Multi-User-Anwendung (Scribblar), Prototyping
*   Systeme unterscheiden sich weiterhin u.a. noch hinsichtlich ihres Standardisierungs-Grades (Kosten), des Kopplungs-Grades (Zuverlässigkeit) sowie ihrer Komplexität (Pflege) - alles zusammen bildet die "Total Cost"
*   andere Architekturen, die SW-Architektur allenfalls berührt:
	*   Infrastruktur: Technische Infrastruktur wie Hardware, Netze, ...
	*   Enterprise: Struktur von Anwendungslandschaften, orientiert sich vor allem an den Geschäftszielen (Unterstützung der täglichen Geschäftspraxis, Kostenreduktion, ...)
	*   Business/Geschäftsprozeß: Struktur von Geschäftsprozessen
*   Erst reden, dann schreiben: Optionen mit Fachleuten durchdiskutieren (Whiteboard), erst dann dokumentieren
*   NFAs bilden Grundlagen und Abhängigkeiten/Beschränkungen der Anwendung
*   technische A. gewichtet die technischen Anforderungen und ermittelt den Scope des Systems, legt v.a. das Zusammenspiel der Komponenten des Domänenmodells fest
*   fachliche A. teilt System in Subsysteme, beschreibt Anwendungsfälle, erzeugt fachliches Datenmodell sowie Nachbarschnittstellen und beschreibt Dialoge (Layout/Aktionen)
*   Softwaredesign (Aufbau des Programms & Implementierung) ist Architektur untergeordnet
*   **Entwicklungsprozeß:** Wie arbeitet ein Team um Software zu erstellen, definiert Rollen, Ergebnisse und Schritte (letztlich eine Sammlung von best practices), zwei Arten:
	*   definiert: wiederholbar, Prozeß definiert das Produkt (Vergleich: Auto vom Fließband)
	*   empirisch: Ergebnis durch Erfahrungswerte & Ausprobieren (Vergleich: Idee / Konstruktion des Autos)
*   wird wichtiger, je größer das Team wird, sollte nicht von außen erzwungen werden (Team)
*   EW sollte keinen Zugriff auf die Produktivsysteme haben (müssen)
*   entweder hat jeder Entwickler Zugriff auf alles (vgl. facebook) oder anwendungsspezifische Rechte (sicherer, aber komplizierter)
*   Einheitlicher Programmierstil wichtig (Styleguide, klare Strukturierung), der Ablauf innerhalb des Programms muß nachvollziehbar und kommentiert sein
*   Generell immer eher domänenspezifische Datentypen einsetzen (z.B. Objekt "Password" statt String, obwohl es ein String ist)
*   Architekt kann oft auch gut einschätzen, welches Teammitglied sich für welche Aufgabe eignet
*   Generell so wenig Technologie wie möglich einsetzen
*   Alle sollten immer über die Aufgaben des Einzelnen Bescheid wissen ohne diesen zwangsläufig zu unterbreechen (vgl. Thiels One-thing-Management), umsetzbar z.B. über Chat-Status-Message mit Link zum JIRA-Ticket oder JIRA selbst
*   Zentrales Repository essenziell, dabei klare Richtlinien hinsichtlich Branching (z.B. für jedes Feature aber auch nicht zu viele) und Tagging (z.B. nach jedem Release) festlegen, Integration mit Issue Tracker und IDE beachten (z.B. Vorgaben für Kommentare, automatische Integration)
*   Es sollte ein Staging-Prozess für neu zu entwickelnde Features definiert sein, Systemumgebung muß dafür vollständig herstellbar sein (Services, Regeln, externe Komponenten), dabei auch die notwendigen Code-Reviews beachten
*   Architekt sollte auch Muster für Versionierung vorgeben (z.B. Major.Minor.Micro.Phase.Build.Date), wobei "Phase" z.B. für RC, RTM, GA, U, SP, SR steht
*   Klare Abgrenzung der Release-Typen wichtig: Micro (Bug fixes), Minor (einige neue Features) oder Major (viele neue Features, evtl. Inkompatibilität)
*   zum Ermitteln von NFAs beim Kunden ruhig etwas provozieren ("Wir müssen den Server jede Woche einmal runterfahren“ / "Wir designen alles selbst")
*   Typische Abfolge: Spezifikation NFAs, fachliche Architektur, Entwurf TI-Architektur, Querschnittskonzepte, Entwurf technische Architektur, Fertigstellung technische Architektur, Anwendungsarchitektur, IT-Konzept für jede Komponente
*   **Spezifikationsbausteine:** Fachliche Subsysteme/Komponenten, fachliches Datenmodell, Anwendungsfälle, Anwendungsfunktionen, Nachbarsystemschnittstellen
*   Wann bin ich fertig?
	*   technisch: Hardund Softwareprodukte klar, Umsetzung der Querschnittskonzepte, Beschreibung der Schnittstellen und der Schichtenarchitektur, Gestaltung der Entitätsund Datentypen, Umsetzung der Komponenten
	*   fachlich: Komponenten erstellt, Entitäten zugeordnet, wesentliche Anwendungsfälle durchgespielt, Datenmodell und Anwendungskomponentenmodell fertig (Umsetzung fachlicher Funktionen durch Komponenten, quasi UML-Komponentendiagramm)
*   Komplexität entsteht meist durch mehrere Threads, mehrere Plattformen, (Last)Verteilung, Performance-Anforderungen
*   Typische Geschäftsanwendungen mit speziellen Architekturen: Zahlungssysteme, Tracking, Analysesoftware, Warenketten, Abrechnungen
*   Keine Geschäftsanwendungen: Betriebssysteme, Aufzugssteuerung, Telefon-Switches, Compiler, Spiele
*   bei Großprojekten (mehr als 20 Entwickler) bzw. verteilten Systemen sollte nicht eine Person alle A.-Entscheidungen treffen (auch technologieabhängig), generell ist jedes Teammitglied natürlich auch für die A. zuständig
*   gute SW-Architekten arbeiten proaktiv, holen Feedback ein statt zu vermuten, arbeiten nicht im Elfenbeinturm und optimieren nur bei Notwendigkeit
*   Lösungen meist nur durch enge Abstimmung mit PL/Management, Zwischenlösungen (Features weglassen), Revision, Einkauf von Komponenten, Anforderungen überarbeiten
*   Interessanter Ansatz von Amazon: "Working from the customer backwards", d.h. mit Pressemitteilung beginnen und das einfachste mögliche Design entwickeln
*   Architekten lernen u.a. durch…
	*   Nachbarprojekte
	*   Architektur- und Entwurfsmuster
	*   Beispiel- und Referenzarchitekturen (Firma, Kollegen, Online)
	*   User Groups (gegenseitige Vorstellung und Diskussion)
*   Diskussionsmethode **Six Thinking Hats** (besonders gut für Brainstorming geeignet):
	*   alle Beteiligten geben sich eine Rolle = Hut
	*   jeder Hut hat eine Farbe:
		*   Weiß: Informationen und Fakten
		*   Rot: Emotional
		*   Schwarz: Vorsichtig, konservativ
		*   Gelb: Optimistisch, harmoniesuchend
		*   Grün: Provozierend, hinterfragend
		*   Blau: Meta-Ebene
	*   Steuerung erfolgt durch blauen Hut, der weiße Hut eröffnet meist die Diskussion, Gruppe entscheidet nach einem Thema stets, was als nächstes kommt
*   **Werkzeuge** für Software-Architekten:
	*   **Anforderungsmanagement (z.B. Enterprise Architect, in-Step)**: Erfassung, Analyse, Darstellung und Nachverfolgung (Anforderungen/Architektur/Code) der Anforderungen / mehrbenutzerfähig (schwierig bei UML), Versionierung, Datenaustausch mit EW-Prozeß, Übersichtlichkeit
	*   **Modellierung (z.B. ArgoUML, MagicDraw)**: Sollten alle gängigen Modellarten unterstützen (UML, SysML, Entity-Relationship, BPMN, …), zu Kommunikation, Doku, Design, Basis für Implementierung (Codegenerierung) / sollte mehrbenutzfähig sein, Generierung ermöglichen und Import/Exportfunktionen haben, ggf. Reverse-Engineering
	*   **Generierung (z.B. ANTLR, openArchitectureWare, Spring Roo)**: Erzeugt Rahmen/Gerüst der Implementierung, erzeugt Artefakte aus textuellen/grafischen Modellen (z.B. Java-Code oder auch DDLs/SQLs, XSDs) / muß konfigurierbar sein, Metamodelle und Schablonen sollten vorgegeben sein, plattformunabhängig, Trennung zwischen generiertem und manuellem Code muß machbar sein
	*   **Statische Codeanalyse (z.B. CAST, Sonar, JDepend)**: formale Prüfung zur Bewertung von Qualitätseigenschaften und Umsetzung (z.B. strukturelle Komplexität), Quellcode entspricht Architektur-Vorgaben / automatisierbar, Ergebnisse aufbereiten & visualisieren, flexible Kriterien & Metriken, mehrere Programmiersprachen
	*   **Dynamische Analyse (z.B. JProfiler, AppDynamics)**: Bewertung hinsichtlich Performance, Ressourcen und Last zur Laufzeit/ Tool darf Ergebnis nicht verfälschen, Ergebnisse aufbereiten & visualisieren, ggf. Beschränkung auf Systemteile, Messung in verteilten Umgebungen
	*   **Build (z.B. ANT, Ivy, Maven):** automatisieren Kompilierung (Übersetzung der Quelltexte), Generierung, Auflösung von Abhängigkeiten, Paketierung (z.B. EAR), Deployment, Ausführen der Tests (Unit- und Integration), Testreports, Kompatibilitäts-Checks, Analyse der Konfiguration (z.B. XML-Validierung), Einhaltung QS / anpaß- und erweiterbar, Unterstützung verschiedener Programmiersprachen, Staging, Anbindung an Continuous Integration (sollte nach Push/Commit eigenständig neuen Build erzeugen), Auswertung/Verteilung der Ergebnisse, Erzeugen von Doku und Release Notes
	*   **Konfigurations-/Versionsmanagement (z.B. SVN, Git, Perforce):** Versionierung aller Ergebnisse (Artefakte) von Architektur und EW, erstellt Versionen, Revisionen und Konfigurationen, ermöglichen Auswahl und Zuordnung von Elementen zu einer Konfiguration, Inventarisierung, Rekonstruktion / muß stabil, sicher und robust sein, Branches und Merges oft schwierig (Vorteil Git), gute Integration mit anderen Tools (Build, Bugtracker, Doku), plattformunabhängig
	*   **Code-Management (z.B. Eclipse, Visual Studio)**: Unterstützen beim Schreiben von Code, bieten syntaktische Hilfen, ermöglichen Refactoring und Debugging / Stabilität, mehrere Programmiersprachen, Integration von Tests sowie Build & Deployment
	*   **Tests (z.B. xUnit, FitNess, Cucumber)**: Feedback über Struktur und Zusammenarbeit mit Unitund Integrationstests / müssen verteilte Systeme unterstützen, Mocking, Verwaltung von Testfällen, UI-Tests
	*   **Dokumentation (z.B. Word, Wikis)**: Beschreibung/Kommunikation aller Aspekte und Entscheidungen zur Architektur / mehrbenutzerfähig (Gruppen), Versionierung, Generierung der Doku aus Modellen, Unterstützung von Metamodellen, modifizierbarer Detailgrad und Umfang je nach Zielgruppe (Export), verteilte Reviews
*   Auswahl der Werkzeuge anhand folgender Kriterien:
	*   Vorkenntnisse
	*   Einarbeitungs-/Schulungsaufwand
	*   Lizenzkosten und –bedingungen, Reputation des Herstellers
	*   Supportmöglichkeiten
	*   Öffentlich verfügbare Informationen (Bücher, Foren, …)
	*   Referenzprojekte

## Vorgehen im Entwurf von Software-Architekturen
*   W-Fragen:
	*   Warum: Ziele, Prinzipien, Erfolgskriterien, aktueller und zukünftiger Kontext
	*   Was: Anforderungen, Struktur, Ziele, Gesamt-Umfang mit einzelnen Teilproblemen ermitteln
	*   Wie: Kurz- und langfristige Lösungen, Struktur der Architektur, Organisation des Weges zur Zielerreichung
	*   Womit: Implementierung, Prozesse, Hardware/Software zur Erfüllung der gesetzten Ziele
*   Zu Beginn eines Entwurfs Informationen sammeln:
	*   Domänenspezifisches Wissen, technische Hintergründe
	*   Vorhandene Systeme ermitteln und auf Wiederverwendbarkeit prüfen
	*   Drittsysteme ermitteln die ähnliche Aufgaben bzw. Teile erfüllen
	*   Technische Literatur für Lösungsansätze/Vorgehensmuster sichten
*   **Entwurfsentscheidungen**: Entscheidungen mit lang anhaltender Wirkung, strategisch, riskant, qualitätsrelevant und evtl. mit Überraschungseffekt (z.B. für neue Entwickler)begründen:
	*   Was ist das Problem?
	*   Warum ist es relevant?
	*   Welche Auswirkungen hat es?
*   Entwurf der SW-Architektur am besten nur mit Schnittstellen zu anderen Systemen
*   i.d.R. vier (parallele) Tätigkeiten des Entwurfsprozesses:
	*   **Anforderungen und Randbedingungen analysieren**: Qualität und Stabilität der FAs und NFAs, Lücken finden, Verständnis für A. schaffen(Metapher), zentrale Entscheidungskriterien für Entwurf finden
	*   **Architektursichten und technische Konzepte entwerfen**: detaillierte Darstellung der Sichten, dabei FAs in technische und NFAs in querschnittliche Lösungsbausteine konzipieren
	*   **Architektur und Entwurfsentscheidungen bewerten**: QS über Reviews, Prototypen, Tests sowie analysierende und bewertende Verfahren (Voraussetzung: Szenarien wurden aus Anforderungen abgeleitet), Anforderungsszenarien durchspielen
	*   **Umsetzung begleiten und überprüfen**: zielgruppengerechte Kommunikation mit allen Stakeholdern (Produktmanagement, Projektleitung, EW, Tester, QS, Nutzer, Anforderungsmanagement, Führungsebene, Betrieb), ggf. selbst programmieren
*   Die Tätigkeiten werden in stetigem Wechsel der Abstraktionsstufen/Architekturebenen ausgeführt (wahlweise Bottom-Up bzw. Top-Down):
	*   Umgebung, Vorgaben und Randbedingungen (Input für Architekturentwurf, FA+NFA)
	*   Softwarearchitektur mit Abstraktionsstufen: Architekturstil (z.B. Schichtenarchitektur auf verteiltem System), technische Infrastruktur, fachliche und technische A. (Entwurf von Komponenten und deren Zusammenspiel)
	*   Programmdesign und Implementierung (Realisierung, möglichst iterativ)
*   drei denkbare Perspektiven der Architektur: Anwendung (Struktur der Software), Technik (Laufzeitumgebung), Infrastruktur (Hardware, Netze)
*   eine mögliche (serielle) Herangehensweise in fünf Schritten:
	*   Informationen sammeln, Geschäftsziele und Geschäftsmodell (Umfeld) verstehen
	*   Systemidee entwickeln (evtl. über Schritte Ideal-Ist-Soll)
	*   Einflüsse und Lösungen dafür ermitteln
	*   Sichten entwerfen
	*   Heuristiken anwenden
*   **Heuristiken**: Verfahren, die dabei helfen, Probleme ressourcensparend zu lösen
*   kann auf verschiedenen Wegen erreicht werden:
	*   **Top-Down**: zerlegt Problem in Teilprobleme und erstellt daraus das Gesamtprojekt (sehr allgemein, gut verständlich, saubere Schnittstellen, aber späte Integration, spätes Feedback, übersieht existierende Lösungen) – geht vom Projekt aus
	*   **Bottom-Up**: beginnt mit konkreter Implementierung (schnelle Ergebnisse, Erkennen von Risiken, gut wiederverwendbar, schrittweise, aber potenzielle Redundanzen/Wildwuchs, sehr technikorientiert) – geht von Tooling (z.B. Bibliotheken, Frameworks) aus
	*   **Aufteilung (hierarchische Dekomposition)**: „Teile und Herrsche“, Aufgaben zerlegen bis Teilaufgabe beherrschbar, am Ende entsteht eine Hierarchie (Lösung des Problems dann entweder durch Zusammenfügen der Teile, Auswahl eines Teils oder letzte Lösung = Gesamtlösung)
*   Weitere Ansätze: Analogien suchen (ähnliches Problem), Generalisieren / Spezialisieren, Problem variieren, Rückwärtige Suche (Was bringt mich zu dem gewünschten Ergebnis?), Reduktion (Wandle das Problem zu einem anderen für das es eine Lösung gibt), Trial and Error (Versuche alles, was geht)
*   Pragmatisches Vorgehen: Wesentliche fachliche und technische AFOs auf einer Seite/Folie zusammenfassen und gewichten. Daraus dann PoCs ableiten und an Mitglieder des Teams verteilen. Daraus entsteht dann ein erster Prototyp.
*   eine (eventuell entstehende) Spezifikation beschreibt dann genauer, was das System tun wird (die Problemstellungen werden sozusagen transformiert)
*   Spez enthält zumindest das logische Datenmodell, Use Cases und Dialogbeschreibungen
*   entsteht zunächst grob auf Basis der Fachdomänen und wird dann detaillierter und teilt die Lösung in Komponenten auf
*   ständiger Austausch mit allen Stakeholdern (jeder sollte zumindes das "Big Picture" verstanden und im Kopf haben), jeweilige Abstraktionsebene beachten
*   Basispatterns: Separation of Concerns, Information Hiding
*   Regelmäßiges Refactoring/Redesign: jede SW-Architektur degeneriert, teilweise Re-Implementierung sinnvoller, daher stetig Strukturen vereinfachen bzw. umstrukturieren
*   Hilfreich ist immer eine geskriptete Umgebung (Projektverzeichnis, CI, IDE, Tests), kann über Batch/Shell oder auch Puppet/Chef erfolgen (vgl. DevOps), zahlt sich besonders beim Onboarding aus
*   Degenerierte Systeme zeigen sich u.a. durch:
	*   Zerbrechlichkeit: 1 Änderung = 1000 neue Probleme
	*   Starrheit: Modifikationen sind generell schwierig (Faustregel: Abfolge Ausrollen / Messen / Lernen soll stets in kurzen Intervallen möglich sein, langwierige und komplexe Releases machen dies unmöglich)
	*   Schlechte Wiederverwendung: Komponenten haben hohe Abhängigkeiten
*   Regelmäßige schrittweise Anpassungen sind im Projekt eigentlich immer sinnvoll - in der Praxis findet sich oft folgendes Vorgehen:
    *   zunächst externe API definieren
    *   Methoden erstellen und mit Stubs / Mockups füllen
    *   Erste Tests schreiben und ausführen
    *   Funktionalitäten gemäß Prio implementieren
    *   Assertions, Fehlerprüfungen und Kommentare ergänzen
*   Dabei stets nur eine Sache zur selben Zeit ändern (Implikationen)
*   zu Beginn des Projektes stets fragen: Was ist das Problem? Was erwartet ihr? Wie arbeitet ihr?
*   die Aussagen des Kunden auch in eigenen Worten wiedergeben / auf Flipchart zeichnen
*   oft zieht man voreilige Schlüsse und kategorisiert ein Problem zu früh irgendwo ein, obwohl es viel komplizierter ist (zuhören = verstehen)
*   Wichtige Umgebungsbereiche der SW-Architektur:
	*   **Projektumfeld und Management**: viele andere Projekte & Anwendungen (Landschaft), kann z.B. Auswirkungen auf Schnittstellen haben
	*   **Produktmanagement und Requirements Engineering**: generiert FAs & NFAs, diese verändern sich
	*   **Ausführung und Betrieb**: Nutzung vorhandener Plattformen
	*   **Werkzeugumgebung und Entwicklung**: Bereitstellung von IDEs, Berücksichtigung etablierter Tools
*   Typische Einflußfaktoren: Politik, Organisation, Technik (Hardware, Software, Werkzeuge, Programmiersprachen, Frameworks, Datenstrukturen), Vorgehensmodell, Produkt, Zeit, Geld, Ausstattung, Personal, (Qualitäts-)Normen wie ISO-9000
*   Typische Projektrisiken: Zeitplan, Ressourcen (Geld, Personal, Wissen), neue Produkte, kritische Schnittstellen, technische Infrastruktur, schlechte Anforderungen
*   Systeme charakterisieren sich weiterhin durch Geschäfts- und Umgebungs-Charakteristiken:
    *   Ablösung eines bestehenden Systems vs. Neuentwicklung
    *   Dynamik der Anforderungen (häufige Änderungen / Ergänzungen)
    *   Anzahl der verschiedenen Services/Prozesse
    *   Problemstellungen dieser Services (CRUD vs. komplexe Berechnungen)
    *   Interaktion der Nutzer (komplex oder linear)
    *   Komplexität der benachbarten Systeme
    *   Abhängigkeiten zwischen Komponenten und Features
    *   Anforderungen hinsichtlich der Sicherheit
    *   Zu erwartende Beteiligung des Kunden am Projekt (Partizipation)
    *   Möglicher Outsourcing- / Offshore-Anteil (beachte aber: man lernt vor allem durch eigene Erfahrungen, mit Outsourcing geht dies verloren)
    *   Nutzung vorhandener (Standard-) Software und Open Source
    *   Priorität hinsichtlich Umfang oder Zeit, Bedeutung der verschiedenen NFAs
    *   Wichtigkeit der Nachvollziehbarkeit von Entscheidungen
    *   Änderungen im Team über die Zeit
    *   zentralisiertes vs. verteiltes Arbeiten
*   Gutes Gleichnis für die Charakterisierung eines Systems sind Verkehrsmittel:
    *   Motorroller: Schnelle Umsetzung (oft agil), moderne Technologien, vermutlich kurze Lebenszeit, häufig wechselnde Anforderungen, geringer Fokus auf Spezifikation und Doku
    *   Auto: Weniger flexibel, aber weiterhin nur geringer Fokus auf Methodik, längere Lebenszeit, wichtiger für das Geschäft
    *   Bus: Ähnlich wie ein Zug, aber dynamischer (häufigere Änderungen), Komplexität der Komponenten unterscheidet sich (Zug / Motorroller), Infrastruktur ist weniger wichtig, aber ähnliche Lebenszeit wie ein Zug
    *   Zug: Geschäftskritisch, lange Lebenszeit, Wartung und Pflege sind zentrale Punkte, saubere Methodik sowie ausführliche Dokumentation wichtig, tendenziell langer Umsetzungszeitraum (meist inkrementell), viele Anwender und Stakeholder
*   Verschiedene (sich ergänzende) Vorgehensweisen beim Entwurf:

*   Systemidee: Was ist die Kernaufgabe? Wie und von wem wird es genutzt? Welche GUI und welche Benutzerschnittstellen? Wie erfolgt die Datenverwaltung? Wie wird das System gesteuert?
*   Domain-Driven Design: Beginnt mit domänenspezifischen Abstraktionen (Entities und Services), Oberfläche und Infrastruktur werden ergänzt
*   Quality-driven Architecture: Qualitätsziele leiten Entwurfsentscheidungen ab
*   Test-driven Design: Prüfung aller Bausteine vor der Implementierung
*   die meisten Aufgabenstellungen sind nicht neu, darum sollte eine vorhandene Codebasis bewußt weiter verwendet werden (Design by Routine / systematisch abschreiben, Gegensatz: design-by-innovation)
*   Entwurf sollte Struktur der Anforderungsanalyse übernehmen und Informationen ergänzen, aber nicht die Struktur verändern
*   Entwurf trennt Interaktion & Anwendungslogik sowie Fachlichkeit & Technik (Infrastruktur)
*   Sichten zeigen wichtige Merkmale der A. aus bestimmtem Betrachtungswinkel, vier Arten:
*   **Kontext**:
	*   betont das System-Umfeld und das Zusammenspiel (Schwerpunkt: Schnittstellen)
	*   S. genau definieren (Was wird übertragen? Medium? Format?)
	*   kann fachlich oder technisch sein
	*   ist für praktisch alle Stakeholder interessant
	*   Wichtige Elemente: Nachbarsysteme, Benutzer, System, Schnittstellen, Protokolle, Übertragung (synchron/asynchron)
	*   Beschreibung durch Kontextdiagramme und Listen der Nachbarsysteme, in UML vor allem Komponentenund Kompositionsstrukturdiagramme, das zu entwickelnde System ist dann quasi eine Black Box in der Mitte
*   **Baustein**:
	*   Bildet die Struktur eines Software-Systems ab (letztlich Abstraktionen von Quellcode)
	*   zeigt funktionale und ggf. technische Softwarebausteine und ihre Beziehungen (z.B. Klassen, Prozeduren, Programme, Pakete, Subsysteme / vgl. Grundriß Hausbau)
	*   quasi eine hierarchische Sammlung von Black Box und White Box-Beschreibungen
	*   kann gut ausgehend von der Kontextsicht entworfen werden
	*   in UML meist Komponenten-, Paket- oder Klassendiagramme (bei Verfeinerung)
	*   oft die aufwändigste und wichtigste Sicht
	*   richtet sich vor allem an EW, QS, Test, PM
*   **Laufzeit**:
	*   Welche Bestandteile des Systems existieren zur Laufzeit und wie wirken sie zusammen (Prozesse, Jobs, Threads), Nachrichtenaustausch (Messaging)
	*   Elemente können frei angeordnet sein (nicht nur links > rechts)
	*   deckt auch betriebliche Aspekte ab (Start, Konfiguration, Administration)
	*   Fokus liegt oft auf Teilen des Systems (Überblick, Beispiele)
	*   in UML über Sequenz-, Aktivitäts- oder Kommunikationsdiagramme, zur Vertiefung können auch nummerierte Listen nützlich sein
*   **Verteilung**:
	*   technische Umgebung (Netzwerk, Server, DBs, Knoten, Protokolle) des Systems
	*   generell werden Artefakte (z.B. WAR-File, Skript) den Knoten (Server) zugeteilt
	*   neben physischen Gegebenheiten auch Leistungsmerkmale (z.B. Durchsatz/Störungsrisiken) festhalten
	*   wenn vorhanden dann auch auf Buildund Deployskripte verweisen
	*   in UML über Deployment-Diagramme
*   oft sind auch spezialisierte Sichten sinnvoll, Beispiel:
	*   Datensicht für DB-Strukturen (Entity-Relationship-Modell)
	*   Big Picture für High Level-Architekturüberblick (Management)
	*   Masken-/Ablaufsicht für Screens und Web-Abläufe
*   Änderungen in einer Sicht haben Konsequenzen auf andere Sichten (iterativ entwickeln)
*   Sichtenbeschreibung kann z.B. in folgende Abschnitte unterteilt werden:
	*   Kurzbeschreibung
	*   Diagramme
	*   Elementkatalog (alle Bausteine der Sicht und deren Beziehungen/Schnittstellen)
	*   Kontext (Zusammenhang, äußere Umgebung)
	*   Variabilität (hinsichtlich Anforderungen, Architektur, Infrastruktur, … / ist gut für Konfiguration sowie absehbare Änderungen und Erweiterungen)
	*   Hintergrundinformationen (Begründung konkreter Entscheidungen, Annahmen, Testergebnisse, …)
*   Jeder Entwurf sollte sich nach zwei wesentlichen Verantwortlichkeiten richten
	*   Wissen: Komponente mit Menge an Informationen
	*   Handeln: Aktivität der Komponente, Anwendungslogik
*   Ansatz: Baue Prototyp, der nur NFAs abdeckt und Anwendungslogik wegläßt (Simulation über sleep-Statements)
*   Datenverwaltung: Persistenz, Lizenzmodell, Datenvolumen, Performance, Erweiterbarkeit, Parallelität, Datenintegrität, Transaktionen, Abfragesprache, Ausfallsicherheit
*   Verschiedene Wege zur Steuerung eines Systems:
	*   Ereignisgetrieben: Controller
	*   Prozedural: meist ohne GUI
	*   Parallel: unabhängige Komponenten
	*   Deklarativ: Regelinterpreter, besonders im Bereich KI
*   zukünftige Änderungen an Software sind niemals vorhersehbar, alles muß austauschbar sein
*   jeder Entwurf muß so einfach wie möglich ausfallen (keep-it-simple), alle Entwürfe sollten immer auch Alternativen (Optionen) enthalten
*   ein entworfenes Modell immer zusammen mit dem Auftraggeber und anderen Projektbeteiligten verifizieren
*   Sicherstellen der Konsistenz z.B. durch Code Review, sinnvoller Ablauf des Review-Prozess:
    *   Aufgabe wird im eigenen Feature- bzw. Issue-Branch umgesetzt
    *   EW führt alle Tests und Checks aus
    *   Review wird (z.B. mit Architekt) durchgeführt
    *   Fehler beseitigen und Verbesserungen umsetzen
    *   Integration in den Hauptentwicklungszweig
*   Branches sollten generell eher "kurzlebig" sein, nicht zu viele Branches parallel laufen lassen (ggf. zwei unabhängige Features in einem Branch)
*   Falls Merging zu schwierig/komplex alternativer Ansatz mit Feature Toggles, d.h. alle EW arbeiten im Master Branch aber jedes Feature/jede User Story ist über eigenes Feature Toggle aktivierbar/konfigurierbar (sinnvoll v.a. für komplexere Features, die mehrere Tage/Wochen in Anspruch nehmen)
*   Trennung von Zuständigkeiten (**Separation of Concerns**): jeder Teil beschäftigt sich mit einer Aufgabe (z.B. verschiedene Server für unterschiedliche Aufgaben) bzw. einem Aspekt des Problems – Grundlage für ein modulares System
*   Dabei auch fachliche (Abstraktion) und technische (Implementierung) Teile trennen
*   Abhängigkeiten minimieren **(Loose Coupling)**: Softwareteile sollten nur lose gekoppelt sein, erfolgt über Schnittstellen und Patterns wie Adapter/Facade/Proxy/Strategy/Factory
*   gutes Beispiel: **Observer**-Pattern
*   Kopplung beeinflußt Wartbarkeit, Verständlichkeit, Fehlerraten, Wiederverwendbarkeit
*   Lose Kopplung führt aber oft zu hoher Kohäsion
*   K. läßt sich recht leicht ermitteln: zähle die Anzahl der Beziehungen zu anderen Bausteinen
*   Verschiedene Kopplungsarten:
	*   Aufruf: eine Klasse nutzt direkt eine Methode einer anderen Klasse
	*   Erzeugung: eine Instanz erzeugt eine neue Instanz einer anderen Klasse
	*   Daten: Klassen kommunizieren über globale Datenstruktur oder diese ist „fix“
	*   Ausführungsort: Klassen müssen auf der gleichen Maschine/ Umgebung laufen
	*   Zeit: zeitliche Abfolge der Bausteine ist wichtig
	*   Vererbung: Unterklasse erbt Eigenschaften
*   **Information Hiding** (Geheimnisprinzip)**:** internes Wissen (z.B. Datenstrukturen) des Softwareteils ist nicht von außen zugänglich, Zugriff nur via Schnittstelle
*   **Information Obscurity**: einheitliche Namensgebung (z.B. für Server) gut für Pflege, aber schlecht aus Sicherheitssicht (Schema ist leicht zu durchschauen, angreifbar)
*   **Cohesion:** ähnlich zu Kopplung, bezieht sich aber auf die Abhängigkeiten von Methoden in einem Modul (Kopplung bezieht sich auf Abhängigkeiten zwischen Modulen)
*   Klassen nicht unbedingt nach Typ (z.B. alle Validatoren) sondern nach Systemen/ Subsystemen/Paketen gruppieren
*   **Open/Closed-Principle:** Softwareteile sind offen für Erweiterungen, aber nicht modifizierbar
*   Softwareteile dürfen aber Erweiterungspunkte für neue Module anbieten
*   **Dependency Inversion**: erlaube nur Abhängigkeiten von Abstraktionen
*   Beispiel: API von Systemfunktionen nicht direkt sondern über OS-Abstraktion nutzen
*   **Zyklische Abhängigkeiten auflösen**: nicht immer möglich
*   Beispiel: Komponente A ruft B auf, die C aufruft, die wiederum A benötigt
*   Lösung: Nimm alle Teile aus A, die von C benötigt werden
*   **Liskov-Prinzip:** Bei Vererbung sollte jede Klasse durch ihre Unterklasse ersetzbar sein
*   **Don´t Repeat Yourself:** Kein beliebiges Copy & Paste von Code
*   **Keep it simple, stupid (KISS):** Wähle stets die einfachste mögliche Lösung
*   **Vorsicht vor Optimierungen:** Optimierung nur falls nötig, Verständlichkeit geht vor
*   **Composition over Inheritance:** Komposition verhindert Abhängigkeiten, daher im Zweifel eher auf Vererbung verzichten
*   **Homogenity** (Homogenität): vergleichbare Problemstellungen ähnlich lösen, dabei gleiche Größen und Einheiten verwenden
*   Redundanzfreiheit: technische und fachliche Funktionalität die in mehreren Programmteilen genutzt wird herauslösen und verallgemeinern
*   **Design by Contract** (vertragsbasierter Entwurf): Schnittstellenverträge für das System definieren und umsetzen (ermöglicht Austauschbarkeit von Komponenten)
*   **Data Sovereignty** (Datenhoheit): Ein Softwareteil ist für genau ein Element des Datenhaushalts zuständig, eine Komponente hat z.B. die Datenhoheit über die Entities in diesem Teil der Anwendung
*   **Reuse** (Wiederverwendung): Nutze Referenzlösungen (bereits existierende Implementierungen, Entwurfsmuster, Referenzarchitekturen)
*   **Abstraktion:** Allgemeiner Blick auf ein Problem, keine Details/Konfiguration für Funktion nötig (möglich durch Facade-/Factory-Pattern, Vererbung, DSLs, Separation of Concerns)
*   **Dependency Injection**: Konfiguration der Abhängigkeiten zwischen Objekten
*   automatische Auflösung der Abhängigkeiten, verbessert u.a. die Testbarkeit
*   hierfür eigenständiger Baustein: Assembler
*   Modul kapselt Verantwortlichkeit, bildet eine Blackbox für andere Module (getrennte Entwicklung, einfache Änderungen, Austauschbarkeit)
*   in OOP: Realisierung über Klassen (**Information Hiding** über public/private, abstrakte Klassen) und Komponenten (Funktionalität und Anforderungen über Interfaces definiert)
*   Gegenteil von Aufteilung: Kompression führt mehrere Funktionalitäten zusammen (Kompression sollte automatisch erfolgen, wird ansonsten meist nur angewandt, um die Performance zu verbessern (ansonsten besser lassen)
*   Beispiele: Makros, generische Programmierung (C++ Templates), ORM
*   **Polymorphismus:** mehrere Objekte mit ähnlicher Funktion implementieren ein Interface, Abhängigkeit nur von Abstraktion und nicht von der Implementierung
*   **Load Balancing** verteilt Last und schafft im besten Fall auch Ausfallsicherheit
*   komplexer als einfache Redundanz (Cold/Warm Standby)
*   Es lohnt sich oft, "defensiv" zu entwickeln, d.h. man sollte nachgiebig bei Eingaben sein (NPE immer vermeiden) und präzise bei Ausgaben sein
*   die Konfiguration des Systems sollte sich am "hier und jetzt" orientieren, d.h. nicht alles vorausschauend konfigurierbar machen
*   Kostenfrage: Failover mit identischen oder unterschiedlich leistungsfähigen Maschinen?
*   es macht wenig Sinn, ein leistungsfähiges System nur bei Ausfall des Primärsystems zu nutzen
*   Web- und Application-Server werden in großen Systemen aus Sicherheitsgründen eher getrennt (Webserver in DMZ, AS intern), Webserver sollte nur statische Daten ausliefern
*   Lastverteilung ist damit schichtenabhängig steuerbar, leichte Erweiterbarkeit wenn nötig, Nachteil sind aber viele RPC-Calls
*   Typisches Bild bei Web-Anwendungen ist die Drachenform:
	*   Web Server haben oft wenig Last (besonders bei statischen Inhalten)
	*   Application Server stehen ordentlich unter Dampf
	*   DB-Server werden meist nur gespiegelt
*   fast immer ist eine Zwischenschicht (API) zwischen DB und Anwendung sinnvoll, da dann alle Clients (Browser / App / externe API) darauf zugreifen können ohne die DB zu kennen
*   API entkoppelt, ermöglicht dediziertes Caching und Performanceoptimierung, erleichtert das Hinzufügen von Ressourcen und ermöglicht geteilte Funktionalität/Infrastruktur zwischen verschiedenen Projekten
*   **Datenreplikation:** auf verschiedenen Systemen müssen Daten synchron sein, sollte möglichst asynchron erfolgen (z.B. Master/Slave)
*   Für intensives Datamining empfiehlt sich eine eigene Offline-DB, da die Daten nicht 100%ig aktuell sein müssen (Offline Reporting)
*   oft wird Datenstruktur für Datamining angepaßt (Tabellen kombinieren, Felder weglassen)
*   **Stateless**: zwischen Requests wird kein Zustand gespeichert (Abfrage von statischen Informationen), nur begrenzt einsetzbar
*   Stateless ist generell besser, da dann Skalierbarkeit gewährleistet ist
*   Daher auch eher mehrere Dienste auf einem Server sammeln statt jedem Dienst einen eigenen Server zu geben (Virtualisierung entkoppelt ggf.)
*   Schwierigkeit: nach Abschluß der Session müssen alle Ressourcen wieder freigegeben werden
*   Stateful ist ein System bereits wenn Nutzerdaten in Session gespeichert werden sollen
*   Alternative: Ein Thread pro Request, dann aber Datenintegrität nicht gewährleistet
*   **Aspektorientierung**: Aufgaben treten oft an mehreren Stellen im Code auf, AOP kapselt sozusagen Querschnittsaufgaben (z.B. Logging, Validierung, Session, Fehler)
*   **MDA**: generiert Teile oder ganze Anwendungen aus Modellen (UML)
*   **MDSD**: transformiert SW-Komponenten aus Modellen, betont die Wiederverwendbarkeit
*   Modell wird jeweils mit einer DSL formuliert
*   Modell wird entweder durch virtuelle Maschine ausgeführt oder in eine Anwendung übersetzt
*   plattformunabhängige (PIM) und –spezifische Modelle (PSM)
*   hoher Aufwand und komplexe Modelle, aber bessere Integration von Fachexperten
*   leichtere Portierbarkeit, größere Entwicklungseffizienz

## Qualitätsmerkmale

*   Architektur beschäftigt sich mehr mit dem Erreichen von Qualitätszielen als mit Funktionalität
*   Wesentliche NFAs: Skalierbarkeit, Sicherheit, Robustheit, Verfügbarkeit, Performance, Wartbarkeit, Erweiterbarkeit, Bedienbarkeit, Kosten
*   DIN/ISO 9126: Modell für Softwarequalität (unabhängig vom konkreten Prozeß), Inhalt:
	*   **Funktionalität**: besitzt die Software die verlangten Funktionen (z.B. Richtigkeit, Sicherheit, Interoperabilität, Angemessenheit, Ordnungsmäßigkeit)
	*   **Zuverlässigkeit**: kann die SW ihre Leistungen unter festgelegten Bedingungen über einen Zeitraum erhalten (z.B. Fehlertoleranz, Wiederherstellbarkeit)
	*   **Benutzbarkeit**: leichte Bedienung/Erlernbarkeit, Reaktion auf Fehleingaben, Benutzerfreundlichkeit (Verständlichkeit, Erlernbarkeit, Bedienbarkeit)
	*   **Effizienz**: Sparsamkeit bezüglich Ressourcen, Zeitverhalten, Speicherplatz (z.B. Zeitund Verbrauchsverhalten = Performance)
	*   **Änderbarkeit**: Aufwand zur Fehlerbeseitigung bzw. Anpassungen (z.B. Prüfbarkeit, Modifizierbarkeit)
	*   **Übertragbarkeit**: SW sollte auch auf anderen Hardund SW-Systemen einsetzbar sein (z.B. Installierbarkeit, Anpassbarkeit, Austauschbarkeit)
*   SW-Architektur muß weiterhin leicht verständlich, nachvollziehbar, aktuell dokumentiert und korrekt implementiert sein
*   Ergänzend bzw. im IT-Umfeld gebräuchlich:
	*   **Skalierbarkeit**: Anpassungsfähigkeit bei zunehmenden Anforderungen (vertikal – bessere Hardwarekomponenten / horizontal – mehr Server)
	*   **Nachvollziehbarkeit**: alle Anforderungen identifizieren und diese in allen Artefakten verfolgbar machen (Beschreibung/Spez/Implementierung)
	*   **Performance**: wie Effizienz, bezieht sich auf Datendurchsatz, Datenbzw. Transaktionsvolumen, 	Maskenwechselzeit, Durchlauf-/Startzeit
	*   **Portabilität / Kompatibilität**: wie Übertragbarkeit, verschiedene OS/Hardware
	*   **Kosten**: Topmerkmal, besonders für das Management zentral
	*   **Sicherheit**: eigentlich ein Hauptkriterium, Verfeinerung Zugriffsschutz, Unverfälschbarkeit, Nichtangreifbarkeit, Nichtabstreitbarkeit
*   Performance (Latenz, Durchsatz) ist meist auf ein bestimmtes System optimiert, dann ist es oft schwer skalierbar
*   Typische Latenzen:
    *   Zugriff auf L1 Cache : 0,5ns
    *   Zugriff auf L2 cache: 7ns
    *   Mutex lock/unlock: 25ns
    *   Komprimiere 1 kByte Daten: 3000ns
    *   Sende 1 kByte über Netzwerk mit 1GBit/s: 0,01ms
    *   Lese 1MB sequentiell aus RAM: 0,25ms
    *   Lese 1MB sequentiell von SSD: 1ms
    *   Lese 1MB sequentiell von (magnetischer) Festplatte: 20ms
    *   Übertrage 1 Datenpaket zwischen Kalifornien > Holland > Kalifornien: 150ms
*   Hilfreiche Maßnahmen: Profiler, Lasttests, zusätzliche Hardware, weniger Kommunikation (Proxies), weniger Abstraktion
*   Profiling möglichst zunächst auf Subsystemen/Ebenen ausführen ehe das Gesamtsystem entsprechend analysiert wird
*   Skalierbarkeit (Möglichst lineare Steigerung der Performance durch Erweiterung)
*   Verfügbarkeit (Ausfälle/Fehler pro Zeiteinheit, QoS)
*   hilfreiche Maßnahmen: Ausnahmebehandlung (periodisch {Ping} oder kontinierlich {Heartbeat}), Redundanz/Cluster, Transaktionen, Checkpoints
*   Verfügbarkeit wird oft über Speicherpunkte realisiert, die das Zurücksetzen des Systems auf einen Status ermöglichen
*   Höhere Verfügbarkeit hat oft einen negativen Einfluß auf Performance und steigert die Kosten
*   Höhere Performance kann zu erschwerter Pflege des Systems führen
*   Höhere Flexibilität kann Testbarkeit erschweren
*   Höhere Performance kostet Entwicklungszeit Abhilfe durch Lasttests, mehr Hardware, redundante Datenhaltung, weniger systeminterne Kommunikation
*   Flexibilität möglichst eingrenzen:
	*   Funktionalität, Benutzerschnittstellen
	*   Datenstrukturen / Datenmodell
	*   Fremdsoftware, Zielplattform
	*   Schnittstellen zu anderen Systemen
*   **Usability**: Erlernbarkeit, Effizienz, Abläufe
*   **Sicherheit**: Authentifizierung, Zugriffsrechte, Verschlüsselung, Überlastung, Einschleusen von Fremdcode
*   höhere Sicherheit verschlechtert manchmal die Usability (mehr und komplexere Eingaben)
*   Pflegbarkeit: Erweiterung, Veränderung, Austausch von Komponenten / Grundlagen
*   Portabilität: Übertragung auf andere Plattformen
*   Flexibilität: unterscheidet sich nach Funktionalität, Datenstrukturen, GUI, Schnittstellen, Zielplattform
*   Kopplung läßt sich gut im Quellcode über **Dependency Analyzer** messen
*   Wiederverwendbarkeit: Komponenten/Teile des Systems sollen auch woanders funktionieren
*   Integrierbarkeit: Unabhängige Entwicklung von Komponenten
*   Testbarkeit: Sicherstellen der Funktionalität des Systems während und nach der Entwicklung

## Konstruktion – Datentypen und Schnittstellen

*   **Datentypen** definieren Wertebereiche und sind nicht veränderlich (immutable), hat entweder einen gültigen Wert oder ist NULL
*   kennen keine lokalisierte Darstellung (Bsp.: regionenabhängige Datumsanzeige)
*   möglichst nicht zu viele Datentypen in einem System verwenden
*   selbst definierte Datentypen sollten eine möglichst globale Bedeutung haben (z.B. Money)
*   Drei wesentliche Typen:
	*   Aufzähltyp: fester Wertebereich, statisch (z.B. Enums) oder dynamisch (Hinzufügen von Werten, meist über Konstruktor)
	*   Entitätstyp: hat Schlüssel (PK) und Relationen, typisiert, veränderbar, kann persistiert werden, keine Geschäftslogik, muß syntaktisch korrekt sein (Wertebereich, Format), Beispiel: POJO
	*   Transportobjekt: hat (veränderbare) Attribute mit Datentyp, passiver Datencontainer (kennt keine Implementierung), keine fachliche bzw. Berechtigungs-Logik, sind daten(Lesen/Schreiben) oder funktionsorientiert (Berechnung/Aufbereitung)
*   i.d.R. werden Instanzen von Entitätstypen nur beim Mapping erzeugt (also im Anwendungskern: Zugangs-, Geschäftslogikund Geschäftslogikschicht)
*   Werte in Entitätsobjekten und Transportobjekten müssen auf NULL und den zulässigen Wertebereich geprüft werden (Länge von Strings / Zahlenbereiche)
*   in Praxis oft Kompromiß zwischen datenorientierten (umfangreich, imperformant) und funktionsorientierten Objekten (performant, aufwändig)
*   **Composite Transfer Object Pattern:** unterteile Transportobjekte in einfache (keine Attribute mit Beziehungen zu anderen Transportobjekten) und zusammengesetzte Transportobjekte (nur Attribute mit Beziehungen zu anderen Transportobjekten)
*   um Änderungen in (zusammengesetzten) Transportobjekten zu erkennen kann ein Änderungskennzeichen gesetzt werden (z.B. Flag für geändert/gelöscht/hinzugefügt)
*   Datentypen und Transportobjekte sind Teil der Komponentenschnittstelle
*   Entscheidung hinsichtlich zu wählender **Datenstrukturen** bzw. Algorithmen vor allem für Performanz großer Systeme und umfangreicher Suchabfragen wichtig (vgl. Algorithmen)
*   Wesentliche Datenstrukturen:
	*   Balanced Binary Search Tree: kann Suchen, Selektieren, Min/Max, Vorgänger/Nachfolger, Position, sortierte Ausgabe, Einfügen, Löschen
	*   Sorted Array: kann alles wie BBST außer Einfügen und Löschen
	*   Heaps: Können Einfügen, Löschen, Min/Max und sonst nichts, dafür aber extrem effizient
	*   Hash Tables: Können nur Einfügen, Löschen, Suche und sonst nichts, dafür aber extrem effizient
*   **Schnittstelle** ist die Außenansicht einer Komponente
*   wohldefinierter Zugangspunkt eines Systems oder zu dessen Bausteinen
*   ermöglichen die Zusammenarbeit von Komponenten
*   i.d.R. transportieren sie Daten und Steuerungsinformationen zwischen Komponenten und Systemen (ressourcenorientiert)
*   es gibt auch serviceorientierte S. für Abläufe und Prozesse (SOA-Dienstleistung)
*   beschreibt Eigenschaften wie Attribute, Daten(Typen) und Funktionen
*   eingehende Schnittstelle: was benötigt die Komponente von anderen (Aufrufer)
*   ausgehende Schnittstelle: was bietet die Schnittstelle anderen Komponenten (Anbieter)
*   Ausnahme: Angeforderte S. wird vom Anbieter definiert, aber nicht implementiert – dann muß der Anwender diese implementieren (Bsp. Observer-Pattern)
*   S. sollten hinsichtlich folgender Punkte spezifiziert werden:
	*   Abläufe
	*   Mengengerüst
	*   Durchsatz
	*   Verfügbarkeit
	*   Datenformat
	*   Konfigurationsdaten
	*   Protokolle
	*   Berechtigungen
	*   Beispielablauf
*   S. möglichst allgemein ohne Abhängigkeiten definieren, aber so speziell wie nötig
*   eine umfangreiche S. kann oft auch in mehrere spezifische S. zerlegt werden (entweder semantisch oder nach Verantwortungsbereich)
*   hat einen eindeutigen Namen und eine festgelegte Menge an Funktionalitäten
*   für schnittstellenlastige Systeme bzw. komplexe Systemteile empfiehlt sich ein Prototyp
*   Drei wesentliche S.-Arten:
	*   Allgemein: hat keinen definierten Nutzerkreis (potenziell sehr groß)
	*   Spezifisch: wird von beschränktem/bekannten Nutzerkreis genutzt, verwendete Datenstrukturen sind ausgehandelt (daher oft in Subsystemen)
	*   Standardisiert: Höchste Form, klar spezifiziert, Beispiele: JDBC, RMI, EDIFACT
*   Kriterien: Zuverlässigkeit, Fehlertoleranz, Synchron/Asychron, Semantik, Performance
*   Schnittstellen sollten klein und spezifisch sein (ein Verantwortungsbereich = eine Schnittstelle), wird aber schnell unübersichtlich dann besser gruppieren
*   „gehören" grundsätzlich dem Anbieter (Verantwortlich für Gestaltung und Implementierung)
*   können operativ (während des Betriebs) oder administrativ (während der Inbetriebnahme, z.B. Festlegen von Parametern) genutzt werden, Nutzung dementsprechend gruppieren
*   Funktionalitäten können Kommandos (Zustandsänderung, z.B. Kunde erstellen) oder Abfragen (keine Zustandsänderung, z.B. Kunde suchen) sein
*   Funktionalitäten haben zwei Parametertypen:
	*   Referenzen: Objekte, die verändert werden können, (z.B. in PHP / nicht in Java)
	*   Werte: nicht veränderbare Objekte
*   Zustandsänderung möglich potenzielles Risiko, kann Datenhoheit verletzen, daher tendenziell vermeiden und ansonsten in Spez dokumentieren
*   Komponentenschnittstellen für Anwendungskomponenten sollten immer wertorientiert sein (Umsetzung in Java über Interfaces)
*   Funktionalitäten eher grob gestalten und gesammelte Objekte übergeben um Anzahl der Aufrufe zu reduzieren (Beispiel: Operation getClientBirthdayById() zu fein, besser getClientById() / getAllClients() wiederum zu grob)
*   Funktionalitäten kontextfrei gestalten (egal, ob Request/Session/Global/Batch/...)
*   bei Fehlern tendenziell NULL zurückliefern statt -1 oder andere Rückgabekonstrukte
*   bei mehreren möglichen Schnittstellen immer die allgemeinste verwenden (Bsp. Java: nutze Collection statt List, wenn Reihenfolge der Elemente nicht wichtig)

## Konstruktion – Bausteine und Komponenten
*   **Baustein**: zentrales Basiselement der Struktur von Softwaresystemen
*   Verantwortung jedes Bausteins muß in einem (kompakten) Satz formuliert werden können, Baustein sollte nur über Schnittstellen angesprochen werden
*   Hat zumindest die Eigenschaften Name, Zweck (erfüllte Anforderungen), Schnittstelle, Ablageort(des Sourcecodes), weiterhin Variabilität, Leistungsmerkmale
*   evtl. auch noch „offene Punkte“ angeben
*   typische Bausteine: Module, Komponenten, Teilsysteme, Funktionen, Klassen, Interfaces, Bibliotheken, Frameworks, Schichten, Partitionen, Makros
*   gute Heuristik für Auswahl Programmiersprache / Framework / Modul:
    *   Technologie ist aktuell, Funktionsumfang wächst, wird aber bereits in Produktion benutzt
    *   Software ist gepflegt (Maintainer)
    *   Tool läßt sich erweitern
    *   Beachte Community-Aktivität sowie Indikatoren Github, StackOverflow, IRC, Google Trends, ...
*   im Zweifel eher Technologierisiken im Stack minimieren (wenn ich z.B. MongoDB einsetzen will aber noch nicht kenne führe ich nicht auch noch einen neuen Server ein)
*   typische Hierarchie: Methode - Klasse - Bibliothek - Komponente - Service - Inkrement (Produkt)
*   für Konstruktion ist eine Klasse aber in der Regel zu klein (unübersichtlich), stattdessen Komponente als Basis-Entwurfs-Einheit sinnvoller
*   sind die Bausteine zu klein dann sind sie schwer zu überblicken und die Integration wird schwierig
*   sind sie zu groß dann wird es kaum möglich sein, Risiken vorher abzuschätzen
*   bietet Schnittstellen im Sinne eines Vertrages an (quasi Export und Import von S.)
*   kapselt Implementierung und kann somit leicht ersetzt werden
*   teilt ein System in (hierarchische) Einheiten auf (Konfiguration, (De)Komposition), somit lassen sich auch leicht Teams anhand von Bausteinen / Komponenten bilden
*   drei verschiedene Sichten auf Bausteine zur Verfeinerung der Architektursichten
	*   **Blackbox**: folgt dem Geheimnisprinzip, zeigt den Zweck und die importierten/ exportierten Schnittstellen
	*   in die vertiefende Beschreibung gehören Schnittstelle, erfüllte Anforderungen, Ablageort(des Sourcecodes) / weiterhin Variabilität, Leistungsmerkmale, offene Punkte sinnvoll
	*   **Greybox** (Konfiguration): zeigt Verschachtelung importierter S. mit exportierten S. anderer Bausteine
	*   **Whitebox** Einzelteile der Black Box, deren Zusammenwirken eine Aufgabe erfüllt (die Einzelteile können dann wiederum Black Boxen sein)
*   Faustregel: eigene Whitebox-Darstellung für Komponente mit mehr als 3000 Zeilen Quellcode, evtl. natürlich auch weniger
*   in die vertiefende Beschreibung gehören lokale Bausteine, lokale Beziehungen, Entwurfsentscheidungen, Übersichtsdiagramm
*   beschreibt auch Abhängigkeiten der Bausteine durch Beziehungen (Aufruf, Komposition, Vererbung), Delegation der exportierten/importierten S. auf das Innenleben
*   verschiedene Arten von Komponenten:
	*   **Anwendungskomponenten**: kapseln fachliche Gesichtspunkte, gehören zu max. 1 Subsystem
	*   bestehen aus mehreren Teilen (in OOP: Klassen), nutzen meist mehrere Schichten
	*   rufen sich gegenseitig immer nur über Schnittstellen auf
	*   haben Datenhoheit über den fachlichen Datenhaushalt der Anwendung
	*   idealerweise bzw. wenn nötig zur Laufzeit konfigurierbar (**Component Configurator**)
	*   können unabhängig von anderen Komponenten entwickelt und getestet werden
	*   Faustregeln: nicht mehr als 3 MA arbeiten parallel an einer Anwendungskomponente, maximal 20 DB-Objekte, Aufwand zur Umsetzung kleiner als 1/3 der Projektlaufzeit für 1 MA
	*   Wie bilde ich ein Anwendungskomponentenmodell?
		1.  Typ bestimmen: Kandidaten für Adapter finden, eine Datenkomponente für jedes Subsystem, unterscheide nach Dialogund Einbettungskomponenten, Druckausgabe den Datenk. zuordnen
		2.  Schnittstellen bestimmen: Analyse der Anwendungsfälle, daraus Aufrufe des Anwendungskerns ermitteln, welche Funktionen der K. sollen "exportiert" werden
		3.  Verfeinern: Bestimme Interaktion der Komponenten über die Anwendungsfälle, Anwendungslogik in eigene Logikkomponenten, finde Abhängigkeiten, ermittle Änderungswahrscheinlichkeiten, bilde Fassaden für Dialogkomponenten
*   **Dialogkomponente**: bildet einen/mehrere Anwendungsfälle (1 Fenster/1 HTML-Seite) ab, nimmt Eingaben an, steuert Kommunikation mit Benutzer
	*   Dialoge können abhängig (Aufruf aus Hauptdialog) oder unabhängig (eigenständig) sein
	*   Unterdialoge können eingebettet werden oder in eigenem Fenster stehen
	*   Daten und Zustand jedes Dialogs in eigenen Komponenen verwalten (Dialog kann an verschiedenen Stellen mehrfach geöffnet sein)
	*   Darstellungscode von anderen Komponententeilen trennen (Trennung, leichtere Pflege, wichtig auch zur Internationalisierung)
	*   Internationalisierung ermöglicht Sprachanpassungen ohne Änderung am Quelltext
	*   Lokalisierung paßt Anwendung an Region an (RTL, Datumsformate, Währung, Einheiten, ...)
	*   **Validierung** sollte vor jeder Konvertierung von Nutzerdaten stattfinden
	*   mögliche Datenanbindungen: Bei jedem Klick/Tastendruck, beim Verlassen eines Feldes, beim Aufruf einer Funktion/Abschicken des Formulars ( **Observer**)
	*   Benutzeraktionen, die nur Anpassungen der Oberfläche auslösen in Präsentationsschicht verarbeiten, alles andere in Dialogkernschicht (deckt Datenhaltung, Zustandsverwaltung, Aktionsverarbeitung und Dialogsteuerung ab)
	*   es darf immer nur eine Dialogkomponente in einen bestimmten Datenausschnitt schreiben
	*   Dialogabläufe (Wizards) in einer eigenen Einbettungskomponente implementieren
	*   Kommunikation mit Server über definierte Schnittstellen (Proxy zwecks Austauschbarkeit)
*   **Einbettungskomponente**: zur Umsetzung von Dialogszenarien (keine visuelle Darstellung)
	*   oft werden in vielen Dialogen ähnliche Visualisierungen / Steuerungen benötigt – dann eigene Fachkomponenten bauen und generische Dialogkomponenten verwenden
	*   kann in vielen Dialogen verwendet werden und enthält selbst kein Fachlichkeit
	*   häufiger Einsatz bei Wizard-Dialogen (jeder Schritt leitet sich aus K. ab) und bei Listenansicht mit immer feineren Details (Ausklappen)
	*   Umsetzung von Lokalisierung
	*   steuert Zustand der Präsentation sowie die Abfolge der Dialoge, bindet Interaktionen an und verarbeitet diese
*   **Datenkomponente**: verwaltet Entitäten der Zuständigkeit (Lesen/Schreiben/Ändern)
	*   arbeitet immer mit wertorientierten Schnittstellen (typsichere Datentypen)
	*   kann Anteile der Geschäftslogik enthalten (solange keine zusätzlichen Abhängigkeiten erzeugt werden / im Zweifel in eigene Klasse auslagern)
	*   nutzt definierte Schnittstellen anderer Daten-/Adapterdienste
	*   führt keine Validierungen durch (Aufgabe des Client bzw. vorheriger K.)
	*   Abbildung der DB-Daten auf eigene Entitätstypen (z.B. über Mapping-Klassen), bei einfachen Operationen genügt Aufruf des O/R-Mapper
*   **Logikkomponente**: Umsetzung von fachlichen Abläufen, Teil der Zugangsund Geschäftslogik
	*   implementiert Anwendungsfälle und Prozessabläufe, liest nötige Daten über Schnittstellen
	*   keine Datenhoheit, aber Aufruf von Persistenzdiensten möglich
*   **Adapterkomponente**: kapselt Schnittstelle eines Fremdsystems für die Benutzung durch andere Komponenten, können in allen Schichten verwendet werden
	*   können von Schnittstellen des Fremdsystem aufgerufen werden oder rufen diese auf
	*   transformiert Daten des Fremdsystems in Transportobjekte des Systems, stellt Verfügbarkeit des Fremdsystems sicher (evtl. über Caching)
	*   ggf. müssen Entitätsdaten oder auch Geschäftsdaten angepaßt werden (Mapping)
*   **Reportingkomponente**: Daten für Erstellung eines Reports auslesen (evtl. Reporting Engine)
	*   können in allen Schichten verwendet werden, rufen andere K. über Schnittstellen auf
	*   stellt Abfragen zusammen, die dann über Datenzugriffsschicht ausgeführt werden
	*   führt Berechnungen auf den zugelieferten Daten aus (z.B. Summen)
	*   verwaltet und speichert (Caching-) Templates für die Darstellung der Reports
	*   dürfen Daten aller anderen Komponenten lesen aber niemals schreiben
	*   aus Performancegründen muß u.U. die Datenhoheit anderer Komponenten verletzt werden
*   **Fassadenkomponente**: optimiert Schnittstellen für andere Komponenten und bietet kaum/keine eigene Funktionalität
	*   werden nur in Zugangsschicht verwendet
	*   Daten werden transformiert und aggregiert, dabei möglichst wenig Geschäftslogik verwenden
*   **Batchlogikkomponente**: fachlicher Ablauf zur Datenverarbeitung (ohne Interaktion)
	*   prüft Vorbedingungen, überwacht Ressourcenverbrauch und initialisiert den Durchlauf
	*   Ausführungsinstanz eines Batches ist ein Job (hat alle Parameter, definierter Zustand, ein Ergebnis, läuft unter Systemhoheit und kann überwacht werden)
	*   Batchsteuerung: interner Ablauf eines Batches (Konfiguration, Lebenszyklus, Ablaufsteuerung), quasi Prüfung/(parallele) Ausführung/Kontrolle/Aufräumen
	*   Fehlerbehandlung in Batches i.d.R. über Neustart, Abbruch oder Überspringen
	*   Batch-Framework implementiert querschnittlich Steuerung der Batches & Jobverwaltung, Umsetzung oft über Produkt (z.B. Spring Batch, XD Compute Grid) mit Eigenentwicklung
	*   Framework v.a. bei parallelen Jobs zu empfehlen (komplex)
	*   Job-Steuerung (z.B. Quartz/WebSphere Scheduler, ) kümmert sich um Konfiguration der Batchläufe, z.B. Parameter, Begrenzungen, Batchfolgen, regelmäßige Ausführungszeiten
	*   Job-Scheduling wählt Jobs zur Auführung aus (nutzeroder ereignisgesteuerte Ausführung), Verwaltung der Queues, Start/Stop/Pause von Jobs, Lastverteilung
	*   Job-Monitoring liefert Informationen zu Jobs (Kriterien wie Zustand, Startund Endzeitpunkte, auslösender Benutzer, Ressourcenverbrauch, Fehler, Fortschritt)
*   Wie bemerke ich, dass ein Fehler auftritt?
	*   Checkpoint-Logik
	*   Markieren der Eingangsdaten
	*   Löschen von alten Resultaten zu Beginn des Batches
*   Performanceverbesserung durch Parallelisierung, entweder logisch (parallele Jobs bzw. parallele Teilschritte) oder physisch (Threads/CPUs)
*   ansonsten möglichst große Blöcke verwenden, wenige DB-Zugriffe, Caches nutzen

## Domänenzentrierte Entwicklung

*   Sammlung von Prinzipien & Mustern die Entwicklern beim Entwurf von Objektsystemen helfen sollen
*   komplexe Projekte können kaum ganzheitlich betrachtet werden (vgl. Automobilbau/jeder hat Teilaufgabe des großen Ganzen)
*   Ausgangspunkt: Domäne bzw. Fachlichkeit, die ein Spezialist am besten beurteilen kann – Domänenlogik steht im Mittelpunkt der Anwendung, Modell bildet Domänenlogik ab
*   Strukturierung der Fachdomäne nach…
	*   Fachobjekten: komplexe Fachlogik, objektorientiert, Wiederverwendbarkeit wichtig
	*   Benutzertransaktionen: Datenbeschaffung und Operationen, Fremdsysteme, überschaubare Fachlogik
*   Domänenmodell ist rein fachlich und hilft auch bei Formulierung von Anforderungen
*   **Entities**: Kernobjekte, meist persistent und mit eindeutiger Identität und klarem Lebenszyklus (Objekt wie z.B. Person, Ort, …), haben Operationen und Eigenschaften sowie Beziehungen
*   **Value Objects**: beschreiben Zustand anderer Objekte, keine eigene Identität, (möglichst) unveränderlich, sind quasi Attribute von Entities, können Operationen und Beziehungen haben
*   **Services:** Eine Art Verbindungspunkt von Objekten, bauen auf Entities & Value Objects auf
*   unabhängige Einheit die spezifische Funktionalität liefert, oft 1 Team = 1 Service
*   inhaltlich zusammenhängende Operationen die Abläufe/Prozesse der Domäne darstellen und über Interfaces angeboten werden, meist ohne eigenen Zustand
*   ein Service unterstützt ein klar umrissenes Ziel, wird immer in einer bestimmten Rolle (Nutzer) ausgeführt und besteht aus einer oder mehreren Aktivitäten
*   auch Services sollten sauber versioniert sein (z.B. Version als Teil der URL), das erleichtert Migrationen ungemein
*   verschiedene Arten von Services:
    *   Interaktion: meist mit Benutzer aber evtl. auch mit anderem System
    *   Prozess: Service ruft weitere Services auf
    *   Funktional: Service implementiert einen bestimmten Algorithmus
    *   Datenorientiert: CRUD-Operationen mit Daten
*   Software muss die Domäne modellieren, das macht sie flexibler und leichter erweiterbar
*   Domäne organisiert und systematisiert Informationen (Geschäftsanforderungen), unterteilt sie und gruppiert diese in logische Module
*   Methoden können klassisch (Wasserfall, durchdefiniert) oder agil (Scrum, iterativ) sein
*   Beispiel Domänenmodell: Flugsteuerung – Bestandteile:
	*   Flugzeug
	*   Route
	*   Abflug
	*   Ankunft
*   diese zunächst verstehen und dann in ein Verhältnis setzen, dabei immer abstrahieren
*   eine einheitliche, übergreifende Sprache ("ubiquitous language") die Technik und Fachlichkeit verbindet ist wichtig und findet sich später auch in Code und Dokumentation wieder
*   dabei muß der Informationsfluß definiert und klar erkennbar sein (Informationsobjekte schaffen, die den Zustand von Geschäftsobjekten beschreiben - bildet Grundlage der Kommunikation zwischen Geschäft und IT)
*   Beispiel: Statement in der Form "an order is a request of a customer to supply an article"
*   Domänenmodell z.B. durch **CRC Cards** (Class-Responsibility-Collaboration) ermitteln: eine Karteikarte für jede Klasse mit deren Eigenschaften (oben der Name, links die Verantwortlichkeiten, rechts die Relation zu anderen Klassen)
*   Domänenmodell und Code sollten gemeinsam (objektorientiert) entwickelt werden
*   Schichtenmodell (**Layers**) sinnvoll, weil man zum Verständnis einer Schicht kein Verständnis der anderen haben muß / jede Schicht bietet Services an, die über Interfaces erreichbar sind
*   Beispiel Überweisungsvorgang: soll dies eine Funktion des Senders oder des Empfängers sein? Beides ist nicht ganz sauber!
*   Lösung: Service, der Funktionalitäten für Domänenobjekte bietet und möglichst zustandslos ist
*   Beispiel 2: Reportgenerator, benötigt Daten aus DB und ein Template zur Darstellung
*   Service würde passendes Template zum Report holen und Ergebnis an UI übergeben, aber weder das Report- noch das Template-Objekt wäre der richtige Platz für die Funktion
*   **Module** kapseln zusammengehörige E., V.O. und S., sind möglichst lose gekoppelt
*   Zwei Arten von Zusammenhängen:
	*   Kommunikativ: Verschiedene Teile des Moduls arbeiten mit denselben Daten
	*   Funktional: Verschiedene Teile des Moduls lösen ein definiertes Problem
*   **Integrität eines Modells:** Module sollen einerseits abgegrenzt sein, andererseits arbeiten mehrere (Teams) damit – verschiedene Möglichkeiten:
	*   Shared Kernel: Teilmenge des Domänenmodells, dass von (zwei) Teams gemeinsam genutzt wird (soll Duplikate vermeiden)
	*   Customer-Supplier: ein Team ist Dienstleister (wahrscheinlich das mit höherer Datenverantwortung), eines ist Anforderer
	*   Conformist: Wenn Customer/Supplier nicht funktioniert (z.B. wegen Abstimmung, Zeit, Unwilligkeit) kann sich der Customer abspalten, es wird dann eine Übersetzungs-Schicht implementiert, die Customer & Supplier verbindet (ähnlich Shared Kernel, aber Customer kann nichts ändern)
	*   Separate ways: Wenn das alles nicht funktioniert werden zwei Modelle oder gleich zwei Anwendungen implementiert, es bleibt auch noch die Kommunikation via Netzwerk/Protokoll oder eine gemeinsame DB (Notlösung, da keine Semantik)
*   Beispiel: Datenbankschema könnte sich jederzeit ändern, für Shopping-Applikation kein Problem, für Reporting aber schon
*   Verwaltung der Domänenobjekte über Aggregate, Factories oder Repositories
*   **Aggregierung:** Modelle enthalten meist mehrere Domänenobjekte, die voneinander abhängen
*   gruppieren assoziierte Objekte in einer Einheit (zentrales Root-Objekt und Unterobjekte)
*   von außen kann nur das Root-Objekt referenziert werden, dies vermeidet Datenvariationen
*   Unterobjekte können vom Root-Objekt übergeben werden, müssen aber nach der Operation verworfen werden
*   Zwei Arten:
	*   One-to-many: kann teilweise durch Assoziation eines Objektes und einer Sammlung anderer Objekte umgesetzt werden
	*   Many-to-many: schwieriger da teilweise bidirektional, wichtig ist die Unterscheidung Domäne/Modell
*   es sollten so viele Assoziationen wie möglich entfernt und bidirektionale Abhängigkeiten in unidirektionale gewandelt werden
*   Teilweise sind Assoziationen in Fachlichkeit gesetzt, im Modell nicht nötig (Huhn & Ei)
*   Aggregates gut zum zusammenfassen von Entities und Value Objects, eine Entity sollte die Grundlage des Root-Objektes bilden
*   Mögliche Vorgehensweise für ein Domänenmodell:
	1.  (Grobes) Domänenmodell skizzieren
	2.  Entities und Value Objects bestimmen
	3.  Assoziationen festhalten
	4.  Aggregate festlegen
	5.  Repositories definieren
	6.  Objekte erzeugen
*   **Refactoring:** Verbesserung des Codes ohne Änderung des Verhaltens
*   Voraussetzung sind (möglichst automatisierte) Tests, bilden Grundlage Continuous Integration
*   Hilfreich sind auch explizite Constraints (Ausdruck einer Abweichung, auf die geprüft wird)
*   Prozesse werden am besten in einem Service umgesetzt, in dem einem Objekt ein bestimmtes Verhalten hinzugefügt wird
*   Spezifikation testet Objekt nach bestimmten Kriterien, sollte auch in eigenem Objekt mit mehreren Methoden erfolgen
*   **Anticorruption:** Gut für Legacy-/ Blackbox-Anwendungen, es wird eine Übersetzungs-Schicht (Facade) implementiert, die Modell und Legacy-Anwendung verbindet
*   **Bounded Context:** ein Modell hat einen Kontext, bei mehreren Modellen muß für jedes ein Kontext definiert werden (logischer Rahmen für das Modell)
*   Beispiel: eCommerce, unterscheidet zwischen Kaufvorgang und Reporting, beides hat dieselbe DB, Modelle sollten getrennt sein und getrennt "wachsen"
*   Unterschiedliche Aspekte für Warenkorb egal, ob Produkt wieder entfernt wird, für Reporting aber nicht
*   **Context Map:** Dokument, dass die Bounded Contexts zusammenfaßt und abgrenzt
*   **Distillation:** Aufteilung zwischen generischen und speziellen Konzepten (generische Methoden sollten immer in eigenen Module stehen)
*   Kern des Domänenmodells variiert je nach Blickwinkel, sollte kompakt gehalten sein
*   Generische Unterdomänen können mit Fremdbibliotheken, Outsourcing, bestehenden Lösungen (Vererbung) und durch Eigenentwicklung (maximaler Aufwand und Kontrolle) realisiert werden

## Grundlegende (Design-) Patterns
*   Wiederverwendung von Erfahrungswerten
*   gemeinsame Sprache für Zusammenhänge (Wording), leicht zu dokumentieren
*   Patterns handeln von einer Struktur und setzen fachliche Anforderungen (wie Zuständigkeiten, Abhängigkeiten und Beschränkungen) in einer technischen Architektur um
*   Patterns nicht pauschal einsetzen nicht jede Implementierung braucht ein Interface
*   **Interface:** separiert Ansteuerung und Implementierung, ermöglicht Austauschbarkeit, Testen
*   Implementierung bleibt "private" und damit versteckt, nur das Interface ist "public"
*   Abstrakte Klasse ist eine Art Unterform, kann (teilweise) Implementierung enthalten
*   **Extension Interface:** eigenes Interface für jede "Rolle", die eine Komponente haben kann
*   gut zur Weiterentwicklung bei gewährleisteter Abwärtskompatibilität
*   **Iterator:** Zugriff auf eine Zusammenstellung von Objekten (z.B. in einem Array) ohne die Struktur der Zusammenstellung bzw. der Objekte zu kennen
*   manchmal eigene Methode für Iterieren nötig: Enumeration Method
*   **Adapter:** konvertiert zwischen verschiedenen Interfaces, wird meist als Wrapper für Altsysteme eingesetzt
*   sinnvoll wenn existierendes Interface zu viel/zu wenig anbietet oder falsche Typen verwendet
*   empfiehlt sich auch bei inkompatiblen bzw. zeitlich instabilen Schnittstellen (Änderungen/Austausch denkbar)
*   **Bridge:** ähnlich Adapter, kann aber auch Anwendungslogik implementieren
*   trennt Implementierung und Abstraktion (können unabhängig verändert werden), da ansonsten oft eine Implementierung durch Vererbung der Abstraktion realisiert wird
*   gutes Beispiel: abstrakte Klassen
*   ähnlich zu **Strategy**, dieses bestimmt aber eher das Verhalten eines Systems und nicht unbedingt die Struktur der Implementierung
*   **Decorator:** Komponente wird dynamisch (zur Laufzeit) um Funktionalität erweitert ohne die K. selbst zu ändern (Alternative zur Vererbung)
*   Decorator implementiert dabei nur die Extra-Funktionalität (Basisfunktion im Hauptobjekt, Aufrufe werden also ggf. weitergeleitet) > nutzt dasselbe Interface wie die Basisklasse
*   **Observer:** Komponente benachrichtigt andere K. über Zustandsänderung ohne Kenntnis der anderen K. bzw. ohne Angabe, wie viele K. geändert werden müssen
*   Keine feste Bindung zwischen Observer und zu observierendem Objekt – implementiert nur das Observer-Interface
*   Observer können (dynamisch) gesetzt und entfernt werden eine Grundlage von MVC
*   **Proxy (Stellvertreter):** Platzhalter für echte Komponente (identische Schnittstelle), wird aber stattdessen aufgerufen
*   mögliche Ziele entscheiden selbst, ob sie den Request verarbeiten oder leiten ihn weiter
*   Unterteilung:
	*   Remote Proxies: Anfragen auf andere Rechner
	*   Virtual Proxies: lädt Komponente bei Bedarf, löscht diese ggf.
	*   Protection Proxies: prüft Rechte des Zugriffs
*   in Anwendungslogik oft nützlich, um vor bzw. nach der Verwendung der Komponente Zugriffsrechte, Logging/Tracing und Messungen zu prüfen bzw. zu initialisieren
*   im DB-Umfeld enthält Proxy oft nur ID des Elements und lädt Daten bei Bedarf nach
*   **Builder:** erlaubt schrittweise Erstellung/Instanzierung von (komplexen) Objekten
*   Abfolge der Schritte kann (je nach Aufrufer) variieren, gut für optionale Bestandteile
*   **Facade:** Schnittstelle zu einem komplexen System, vereinfachte Sicht
*   Eintrittspunkt in eine Schicht, delegiert Anfragen zum Subsystem, dessen Methoden/Funktionalitäten außen nicht bekannt ist
*   oft auch ein Sammelpunkt für mehrere auszuführende Methoden, die aber nicht einzeln vom Client ausgeführt werden sollen (Performance)
*   Vergleich OOP: kleine Klassen mit kompakten Methoden gut, für Remote-Zugriffe gilt das aber nicht (teuer), daher besser mehrere Aufrufe sammeln (**Remote Facade**)
*   **Factory:** Kapselung der Objekterstellung, vermeidet überladene Konstruktoren
*   Clients können Objekte nicht mehr direkt erstellen sondern nur über Factory (eindeutig)
*   Factories haben keinen Zugriff auf andere Schichten, dienen nur der Konstruktion
*   sinnvoll bei ähnlichen Objekt-Typen (Unterscheidung sonst anhand der Parameter), für einfache Objekte ohne Abhängigkeiten / Hierarchien genügt ein Konstruktor
*   **Abstract Factory:** Kapselt Erstellung mehrerer Objekte, falls diese untergeordnet sind und dem Aufrufer nicht bekannt sein müssen (z.B. Service/API)
*   **Repository:** Problem bei großen Projekten ist meist die Kopplung (Beispiel-Aufgabe: Lies Value Object aus Root-Objekt, Repository liefert die Referenz)
*   Ermöglicht jedem Objekt den Zugriff auf andere Objekte
*   Referenzen können damit aus Cache oder alternativ von DB/Festplatte gelesen werden
*   macht Sinn, wenn viele Queries auf Domänenobjekte (womöglich in verschiedenen DBs) abgesetzt werden müssen
*   jedes Objekt, das global zugänglich sein soll, benötigt dementsprechend ein Service-Objekt (Interface) mit entsprechenden Methoden (CRUD)
*   Unterscheidung Factory/Repository: Factory erstellt Objekte, Repository verwaltet den Zugriff
*   am besten wird Objekt über eine Factory erstellt und dann im Repository abgelegt
*   **Registry:** allgemein bekanntes Objekt, das übergreifende Objekte/Daten sammelt
*   restriktiv nutzen (z.B. bei großer Menge von Objekten, die immer übergeben werden müßten)
*   sollte nur statische Methoden enthalten, Felder als Map/Dictionary speichern
*   Felder sind aber nicht-statisch, damit sie ausgetauscht werden können (Tests)
*   Scope kann unterschiedlich sein: Global, Thread, Session
*   Implementierung meist als Singleton, für Thread-Sicherheit müssen aber alle Daten unveränderlich sein (d.h. nur einmalig gesetzt werden)
*   In Java: thread-spezifische Objekte (ThreadLocal) jeder Thread hat eigene Registry
*   mehrere Registries sind denkbar und manchmal sinnvoll (z.B. für verschiedene Layer)
*   **Gateway:** kapselt Zugriff auf ein System/eine Ressource
*   quasi eine API zum Zugriff auf das Objekt, API umfaßt Operationen, die "von außen" nötig sind
*   erleichtert Testbarkeit, macht Objekte austauschbar
*   gut zur Integration von Legacy-Systemen (kaum invasiv, wenig zusätzliche Last, Kapselung)
*   sollte kompakt sein und für alle Objekte angewendet werden, deren Interface komplex/außergewöhnlich/fremd ist
*   implementierungsbezogen: muß bei Änderungen angepaßt werden
*   Unterschiede zu anderen Patterns: **Adapter** bezieht sich auf Interfaces, **Facade** geht vom Zielsystem aus (Gateway vom Client), **Mediator** kommuniziert zwischen mehreren getrennten Objekten (genannt Colleagues, Gateway kommuniziert nur nur 1:1), **Wrapper** wird auf Plattform des Zielsystems entwickelt
*   **Strategy:** Objekt ändert das Verhalten je nach Zustand bzw. Rahmenbedingungen
*   wird oft bei gemeinsamer "Obermenge" an Operationen aber Varianten im Detail verwendet
*   Mehrere Unter-Patterns für die Implementierung der Strategien:
	*   **State Pattern:** jeder mögliche Zustand wird in einer eigenen Klasse implementiert, die dasselbe Interface implementieren (Nachteil: viele Klassen)
	*   **Methods for States:** in einem Objekt bekommt jeder Zustand eigene Methoden (Nachteil: evtl. unübersichtliche Klasse)
	*   **Collections for States:** clientseitiges State-Management, jeder State hat eigene Collection die alle relevanten Objekte umfaßt (nur für geringe Anzahl States geeignet)
*   **Value Objects:** Objekt, bei denen ein Vergleich Gleichheit ergibt wenn deren Werte (Felder) gleich sind (Beispiel: Datumsfeld ist gleich, wenn Tag, Monat und Jahr gleich sind)
*   sollten unveränderlich sein, also „private“ und nicht vererbt werden (Aliasing Bug: Bei Änderung in einem Objekt ändert sich das andere gleich mit - meist unerwünscht)
*   Value Objects sollten als Embedded Value persistiert werden, in verteilten Systemen gibt es oft Unmengen von Value Objects dann am besten unveränderlich (final) speichern
*   **Entities**: sind „strenger“, diese haben die gleiche Identität (z.B. Sozialversicherungsnummer)
*   **Embedded Value:** Wann immer ein Mutter-Objekt gelesen/gespeichert wird werden auch die Unterobjekte gelesen/gespeichert
*   Unterobjekte haben keine eigenen Persistenz-Funktionen
*   in OOP machen viele kleine insolierte Objekte Sinn, aber nicht in relationalen DBs
*   geradezu zwingend für Value Objects
*   Embedded Value macht bei 1:1-Beziehung zwischen Referenzobjekt und Unterobjekt Sinn, kann auch für mehrere (möglichst wenige) Unterobjekte eingesetzt werden
*   Ähnlich zu **Serialized LOB**, aber nicht binär, daher per SQL abfragbar
*   **Lazy Load:** Objekt enthält nicht alle Daten, weiß aber, woher es sie bekommt
*   Meist nur sinnvoll, wenn Daten in mehreren Schritten ausgelesen werden müssen
*   tendenziell komplex, sollte nur angewendet werden, wenn es nicht anders geht
*   vier sinnvolle Wege:
	*   Lazy Initialization: Zugriff auf ein Feld überprüft auf NULL > wenn NULL, dann "richtigen" Wert auslesen (schafft Abhängigkeit zwischen DB/Objekt)
	*   Virtual Proxy: Objekt, das sich wie Zielobjekt verhält, aber keine Daten enthält, ist besonders bei Verwendung von **Data Mapper** zu empfehlen aber fehleranfällig & schwer zu debuggen)
	*   Value Holder: Einzelner Wrapper um ein Sammelobjekt, über den auf Unterobjekte zugegriffen wird Nachteil: keine strenge Typisierung
	*   Ghost: Echtes Objekt in teilweisem Zustand, d.h. Objekt enthält nur die ID sowie ggf. Teildaten, kann aber zu DB-lastig sein, schwierig zu vererben
*   ein möglicher Kompromiß ist auch das teilweise Laden von Daten in Blöcken/Häppchen (man braucht selten alles sofort)
*   Über **Data Mapper** lassen sich verschiedene Szenarien gut kombinieren: manche Methoden holen alles direkt, manche nutzen Lazy Loading
*   **Unit of Work:** Liste von Objekten die in einer Transaktion (Lesen/Ändern) verarbeitet werden
*   besser als Einzel-Queries, UoW koordiniert Schreibvorgänge/Parallelität
*   theoretisch kann bei jeder Änderung am Model auch eine entsprechende Transaktion ausgelöst werden (teuer, dennoch bis zu einem gewissen Grad zu empfehlen)
*   jedes Objekt sollte bei Unit of Work registriert werden (caller registration), bessere Kontrolle der Schreibvorgänge, wird aber oft vergessen
*   Parallelität wird beim Ausführen über pessimistisches/optimistisches Locking überprüft
*   Unit of Work sammelt alle Änderungen eines Objekts (also alle CRUD-Operationen) und führt diese Änderungen dann in einem Rutsch aus
*   Alternativer Ansatz: Objekte beim Lesen zwischenspeichern und beim Schreiben vergleichen, anschließend gehen nur die Änderungen an die DB
*   ansonsten sollte sich ein Entwickler nicht mit Unit of Work beschäftigen (müssen)
*   Hauptvorteil: Alle Informationen an einer Stelle, idealer Ausgangspunkt für Transaktionen in mehreren Schritten
*   damit die Objekte die Unit of Work zu finden empfiehlt sich eine **Registry**
*   **Client Session State:** Zustand einer Session wird beim Client gesichert, stürzt der Client ab, sind Daten weg (wird meist ohnehin erwartet)
*   Sticky Sessions können dies vermeiden, binden Nutzer aber an einen Server (Anti-Pattern)
*   optimal: alle Session-Daten sind beim Client und der Server ist zustandlos (perfekt skalierbar)
*   Datenübertragung meist über **Data Transfer Object**
*   In Webanwendungen:
	*   URL-Parameter: längenbeschränkt und schlecht für Bookmarks
	*   versteckte Felder: im Sourcecode sichtbar (Ausweg: Serialisierung)
	*   Cookies: beschränkte Datenmenge (4kByte), werden mit jedem Request übertragen, sind evtl. deaktiviert
*   Client Session State vor allem für überschaubare und unverschlüsselte Daten sinnvoll
*   Sessions könnten übernommen werden (Session Riding), daher schützen bzw. neu generieren
*   **Server Session State:** speichert die (serialisierte) Session auf dem Server
*   kann im RAM (ein Server), in DB oder als Datei im Filesystem (Cluster) vorgehalten werden
*   Daten können in Binärform (einfach erstellbar, optimiert) oder als Text (z.B. XML, lesbar, aufwändiger) gesichert werden
*   in der DB am einfachsten umsetzbar über eine Tabelle mit der Session-ID als PK
*   generell sinnvoll bei vielen Nutzern ohne große Aktivität, weniger gut im Cluster (Sync)
*   abgelaufene Sessions müssen wieder entfernt werden (z.B. über Demon-Job oder via Rotation)
*   **Database Session State:** Session-Daten werden in DB persistiert
*   bei jedem Request werden die benötigten Daten aus der DB geholt, der Client macht Änderungen, im folgenden Request erneute Speicherung
*   Implementierung z.B. über isPending-Feld an einem Datensatz
*   gut für die Performance, weil Server zustandslos
*   schlecht für die Performance, weil ständige DB-Abfragen (Flaschenhals ist die DB ohnehin oft)
*   Clustering und Ausfallsicherheit leichter implementierbar als bei Server Session State
*   Kompromiß: Session-Daten beim Client vorhalten und periodisch in DB schreiben

## Patterns in der Architektur
*   A-Patterns sind in erster Linie Literatur, nicht Code
*   Lassen sich in vier wesentliche Kategorien einteilen:
	*   Adaptierbare Systeme (Erweiterungen, Anpassung an geänderte AFOs)
	*   Interaktive Systeme (Strukturierung von Systemen)
	*   Verteilte Systeme (Arbeitsteilung, Kommunikation zwischen Subsystemen)
	*   Vom Chaos zur Struktur (Zerlegung einer Aufgabe in Teilaufgaben)
*   A-Patterns haben großen Einfluß auf Gesamtanwendung (strategisch), Design Patterns helfen eher bei einem bestimmten Problem (taktisch)
*   anhand der Zuständigkeiten und Beschränkungen (einer Komponente) kann oft schnell ein passendes Pattern gefunden werden
*   Kombinationen verschiedener Patterns in einer Anwendung: Pattern-Sprache (setzt Bezug zwischen Patterns in einem System)
*   **Layers:** Das wohl wichtigste technische Grund-Pattern überhaupt
*   bildet zusammen mit Domänenobjekten (Fachlichkeit) die Grundlage jedes Systems
*   Domänenobjekt: abgeschlossene Einheit, bildet eine Funktionalität des Systems ab (Interface und Implementierung)
*   Verantwortlichkeiten in Schichten packen (Three-Tier: DB/Anwendungslogik/Präsentation)
*   Informationsaustausch über Schnittstellen
*   Komponenten mit ähnlicher Verantwortung/Struktur sind in derselben Schicht, jede Schicht kann nur unterliegende Schicht(en) ansprechen
*   Implementierung einzelner Schichten bzw. Änderungen können in getrennten Teams erfolgen
*   folgt dem Prinzip des **Information Hiding**, leichtere Wartung & Austauschbarkeit, ist aber nicht immer effizient (je mehr Schichten desto langsamer, Abhilfe durch **Layer Bridging**)
*   Änderungen in einer Schicht ziehen oft Änderungen in allen Schichten nach sich (z.B. neues Datenfeld)
*   Layers: horizontal / Modularisierung: vertikal (Komponenten einer Schicht)
*   **Pipes and Filters:** Verarbeitung eines Datenstroms mit einem Satz von Filtern (EVA-Prinzip)
*   i.d.R. Parallelverarbeitung von komplexen Rechenoperationen (z.B. Bilderund Videobearbeitung aber auch Compiler und die Unix-Shell)
*   Filter werden (asynchron) über Pipes verkettet, Puffer/Queue nötig
*   Filter sollten auch in anderer Reihenfolge kombiniert werden und parallel laufen können
*   Nachteil: Datenstrukturen zwischen Filtern müssen vereinheitlicht werden, Pipes müssen Daten transformieren (evtl. Overhead)
*   Fehlerbehandlung schwierig, da Filter weitgehend isoliert sind
*   **Model View Controller:** Model bildet die Domain ab, View die Oberfläche, Controller kommuniziert zwischen beiden
*   besonders geeignet für portable, große Systeme (Faustregel: mehr als 20 Masken) die z.B. mehrere parallele Sichten auf einen Datenbestand erlauben sollen
*   Darstellung wird vom Model entkoppelt, ebenso der Controller von der View
*   sinnvoll, weil sich UI oft ändert bzw. verschiedene Nutzer verschiedene Views nutzen
*   Kernaufgaben: URL entschlüsseln, Model erzeugen/lesen/schreiben, View aufrufen und mit den Daten versorgen
*   oft sind mehrere Darstellungen des Model sichtbar, dies schafft Abhängigkeit bei Änderungen, lösbar über Observer Pattern
*   jede View kann einen eigenen Controller (**Page Controller**) haben, üblich ist aber eher ein zentraler **Front Controller,** Mischung in komplexen Anwendungen möglich
*   komponenten-basierte Controller für häufig verwendete/zu aktualisierende Elemente sinnvoll
*   **Page Controller:** jede Seite ein Controller, nur für einfacher Logik oder starken Unterschieden der Eingabemasken sinnvoll
*   **Front Controller**: konsistenter Anlaufpunkt, grundsätzlich thread-safe, gut bei komplexeren Requests, aber auch Single Point of Failure (wird oft um Interception Filter für Authentifizierung, Logging, …erweitert)
*   statische URLs sind simpel und suchmaschinentauglich
*   dynamische URLs erlauben flexible Weiterentwicklung ohne den Controller anzupassen
*   **Application Controller:** zentraler Anlaufpunkt für Navigation, also eine bestimmte Reihenfolge von Screens (Wizard), aber nicht direkt an GUI koppln
*   Reines MVC würde zu Code-Duplikation führen, daher eigener Controller für Ablauf (Flow)
*   Eingabe-Controller liefern Daten, Application Controller verarbeitet und verweist auf Ziel-View
*   **Shared Repository / Blackboard:** vor allem für datengetriebene Anwendungen, alle Daten werden zentral vorgehalten
*   unabhängige Knowledge Source-Komponenten untersuchen das Problem unter einem Aspekt und schicken das Ergebnis wieder ans Blackboard
*   sämtliche Komponenten können auf Daten zugreifen (Algorithmen erkennen passende Daten und verarbeiten sie)
*   unbekannte / unvollständige Daten werden erstmal ignoriert, somit leicht um neue Algorithmen erweiterbar, leichte Pflege
*   Verfügbarkeit, Qualität, Zustand und Anwendungssteuerung des Systems wird maßgeblich von den Daten bestimmt
*   gut für Echtzeitverarbeitung und wenn mehrere Prozesse mit denselben Daten arbeiten sollen
*   Synchronisierung der Ergebnisse und Transaktionen generell schwierig
*   generell recht robust, aber schwer testbar und nicht unbedingt effizient
*   kommt originär aus dem wissenschaftlichen Bereich (AI, Systemüberwachung, Spracherkennung, Biotech)
*   **Presentation Abstraction Control**: Aufbau des UI wird in kooperierende „Agenten“ zerlegt
*   Jeder Agent hat eigenen Controller, Abstraction und View (Beispiel: Eclipse IDE)
*   gut, weil sich sonst oft unterschiedliche Funktionsbereiche vermischen
*   **SOA**: definiert wiederverwendbare, lose gekoppelte und standardisiert zugreifbare Dienste
*   Drei wesentliche Rollen:
	*   Dienstanbieter: bietet Services und registriert sie im Verzeichnisdienst
	*   Verzeichnisdienst veröffentlicht Services
	*   Dienstnutzer sucht Service und ruft ihn über Referenz auf
*   Services sollten zustandsfrei und transaktional abgeschlossen sein und wiederholbare Ergebnisse liefern
*   Vorteile: Funktionalitäten sind isoliert, verringert Anzahl der Verbindungen, erleichtert die Organisation von Teams und Support, verbessert Sicherheit
*   **Microservices** definieren kliene, unabhängige Komponenten die nicht gekoppelt sind und jeweils ein bestimmtes (kleines) Problem lösen
*   Keine einheitliche Programmiersprache notwendig, jeder Microservice existiert "für sich" und sollte stateless sein
*   Kommunikation über sprachunabhängige APIs, z.B. REST
*   Diese Aufteilung kann so weit gehen, dass jede "App" nur noch maximal 100 Zeilen Code enthält (Node-Apps bei PayPal)
*   **Microkernel:** minimaler Funktionskern, der um Funktionen erweitert wird (analog OS)
*   ähnlich wie Layers, aber möglichst minimale Basis-Schicht (Kernel) und die Module werden nicht nur vertikal gekapselt (Plugins)
*   oft teilen sich verschiedene Versionen eines Systems den Microkernel, die dann jeweils unterschiedliche Funktionalitäten anbieten
*   Systeme passen sich dynamisch an veränderte Rahmenbedingungen (z.B. Hardware) an
*   Clients greifen nur via Interfaces auf Funktionen zu (wenn der Kernel eine Funktion nicht hat delegiert er wie weiter Mediator)
*   skaliert gut und ist für portable/flexible Systeme geeignet (alles basiert auf dem Kernel)
*   recht komplex (sowohl Kernel als auch Erweiterungen), nicht zwangsläufig effizient
*   **Messaging:** Clients schicken Nachrichten an Services über einen Kanal (asynchrone many-to-one-Kommunikation)
*   viele Protokolle (z.B. HTTP) erlauben nicht den direkten RemoteAufruf von Methoden sondern kommunizieren über Datenströme (Aufrufe dann in Messages kapseln)
*   M. enthalten Header mit Datentyp, Herkunft, Ziel, Größe, Nutzdaten = strukturierte Datenübertragung
*   ein Service kann auf alle oder bestimmte Kanäle zugreifen und Nachrichten lesen
*   besonders nützlich für unabhängige, verteilte Services, die nicht verkoppelt werden sollen
*   Nachrichten werden oft von einer eigenen Komponente empfangen oder versendet (Invoker)
*   manchmal müssen Messages (bidirektional) für den Datenaustausch zweier Dienste konvertiert werden: Message Endpoint / Message Translator (bidirektional)
*   wesentlicher Vorteil von Messaging: plattformunabhängig, Zielsystem muß nicht permanent online sein, zuverlässig (wahlweise mit Empfangsbestätigung oder nicht)
*   **Publish/Subscribe:** asynchroner Austausch von Informationen (Problem: Overhead)
*   Versender und Empfänger kennen sich oft nicht (one-to-many-Kommunikation)
*   im Unterschied zu Messaging definiert der Subscriber genau was er empfangen möchte
*   wird oft für Zustandsänderungen gebraucht
*   clientseitige Schichten:
	*   Präsentation: visuelle Darstellung, Anbindung an Dialogkern
	*   Dialogkern: fachliche Logik, Steuerungslogik, Dialogzustand (kein visueller Code)
*   serverseitige Schichten:
	*   Zugang: Schnittstelle zur Anwendungskomponente, Validierung
	*   Businesslogik: Umsetzung Fachlichkeit, Prozessabläufe
	*   Datenzugriff: Abbildung Entitäten auf DB (Persistenz), CRUD-Operationen
*   Anwendungslogik: beinhaltet Berechnungen, Verarbeitung von Einund Ausgaben, Validierung, Steuerung (basierend auf Informationen aus der Eingaben)
*   eine kleine Änderung kann Konsequenzen in allen Schichten haben
*   Beispiel für einen Fehler: Änderung im DB-Schema wirkt sich auf UI aus
*   oft ist es schwer, zwischen Domänenlogik und anderen Schichten zu unterscheiden
*   Beispiel Highlighting: Meistverkaufte Produkte sollen einen Stern o.ä. bekommen, dies könnte in der Darstellung oder in Anwendungslogik entwickelt werden (besser letzteres)
*   Beispiel Flugbuchung:
	*   Nutzer wählt Flug in UI
	*   Anwendungsschicht holt relevante Domain-Objekte und ruft sie auf
	*   nach Validierung und Bestätigung wird in DB persistiert

## Dokumentation von Architekturen

*   Schriftliche Kommunikation, die Verständnis bei Beteiligten (Chef, Kunde, Kollegen, ...) schafft
*   Doku richtet sich immer nach (unterschiedlichen) Fähigkeiten der Leser/Stakeholder
*   Ein einheitliches Template bzw. Gliederung schafft Struktur und erleichtert das Verständnis
*   Unnötige Wiederholungen und Mehrdeutigkeiten vermeiden (dieselbe Schnittstelle an 3 Stellen beschreiben)
*   Doku sollte am Anfang grob sein und mit steigender Seitenzahl immer mehr ins Detail gehen
*   Generell eher die Struktur im Großen betrachten und nicht auf Quellcode-Ebene
*   Qualitätsmerkmale für technische Doku: Verständlichkeit, Korrektheit, Effizienz, Aktualität
*   Wesentliche Entscheidungen sowie Annahmen detailliert begründen
*   auch Code darf in eine Doku, sofern er gut verständlich und lesbar ist
*   Doku auch wichtig für Einarbeitung in die Software (auch nach Jahren), legt Regeln für Codierung fest (Styleguide), hilft bei Integration von Erweiterungen
*   Doku sollte mindestens die Ressourcen, Fehlerszenarien, Risiken, Konfiguration, Qualitätsund Entwurfsentscheidungen, deren Herleitung sowie Annahmen umfassen
*   Statt eines großen besser mehrere kleinere (spezialisierte) Dokus erstellen
*   Universelle Fragen müssen beantwortet werden:
	*   Wie fügt sich das System in die Umgebung ein?
	*   Wie ist das System strukturiert?
	*   Wie verhalten sich die Bausteine zur Laufzeit?
*   In eine Spezifikation gehören dagegen Prozesse, Strukturen, Dienste, Komponenten, ...
*   Phasen der Dokumentation:
    *   Planung (Rahmenbedingungen, Dokumentationsplan), etwa 5-10% der Gesamtzeit
    *   Analyse und Konzeption (Zielgruppenanalyse, Tätigkeitsanalyse, Redaktionsleitfaden, Gliederung), etwa 10-30% der Gesamtzeit
    *   Erstellung und Korrektur (Entwürfe / Endfassung)
    *   Produktion, Distribution (Druck, Website, ...)
    *   Evaluierung und Update (Testberichte, Änderungsanforderungen)
*   Allgemeine Dokus sind z.B. Benutzerhandbuch, Tutorial, HOWTO, Administrations/Installationshandbuch, Qucik Start Guide, Reference Card, Online-Doku, readme.txt, Changelog
*   Typische Architektur-Dokumentationen:
	*   Übersichtspräsentation: Grundproblem, Lösung, Funktionsweise, Architektursichten, max. 10-20 Folien in 1h präsentierbar ( für Management: 10 Minuten)
	*   Dokumentenübersicht mit Handbuch als Verzeichnis und Index aller Dokumente und ihrer Abhängigkeiten, enthält Hinweise zur Zielgruppe der Dokumente
	*   Architekturbeschreibung: Referenz/ Kerndokument, hält alle Architekturentscheidungen fest
	*   Architekturüberblick: Kurzfassung der Beschreibung mit den wichtigsten Überblicksdiagrammen (Bausteine, Verteilung, Laufzeit), max. 30 Seiten
	*   Architekturtapete: Gesamtüberblick mit Sichten auf einer Wand
	*   Technische Informationen zum Entwicklungsprozeß (auch für Tester)
	*   Dokumentation externer Schnittstellen, typische Elemente: bereitgestellte Ressourcen, Fehlerszenarien, Konfigurierbarkeit, Qualitätseigenschaften, Entwurfsentscheidungen
*   Architekturbeschreibung ist in unterschiedliche Ebenen gegliedert, die wiederum technisch (z.B. Persistenz) und fachlich (z.B. Ablauf/Prozeß)unterschieden werden können:
	*   Aufgabenstellung, Ziele, Qualitätsanforderungen, Stakeholder
	*   Technische und organisatorische Rahmenbedingungen
	*   Sichten, Entscheidungen, verwendete Patterns
	*   Technische Konzepte
	*   Qualitätsbewertungen
	*   erkannte Risiken
*   fachliche Ebene fokussiert sich auf FAs (also deren Bausteine und Zusammenhänge), technische auf NFAs (oft querschnittliche Lösungsansätze)
*   Grundlegend sind weiterhin ein Architekturstil (z.B. Schichten mit MVC) als grundlegende Metapher sowie die technische Infrastruktur (z.B. Rich Client mit relationaler DB)für die Rahmenbedingungen
*   sinnvolle Elemente: Dokumente, Modelle (CASE, UML), HTML-Seiten/Wikis
*   **Twin Peaks Modell**: Iterative Verzahnung der Schlüsselfaktoren Requirements Engineering und Architekturentwurf (schrittweise Vertiefung & Konkretisierung)
*   Gute Gliederung für eine Architekturbeschreibung:
    *   Gliederung
    *   Zusammenfassung
    *   Beteiligte
    *   Kontext
    *   Geschäftsprozesse (Use Cases)
    *   Funktionale/Nichtfunktionale Anforderungen
    *   Mengengerüst
    *   Einflüsse, Randbedingungen
    *   Verzeichnis der Architektursichten (Kontextsichten, Bausteinsichten, Laufzeitsichten, Verteilungssicht)
    *   Schnittstellen
    *   Globale Entscheidungen
    *   Glossar
*   Wichtigste Grundlage der Doku ist oft das Lastenheft (Forderungen AG an AN, siehe auch DIN 69905). Es sollte folgendes enthalten:
    *   Ausgangssituation und Zielsetzung
    *   Produkteinsatz, Produktübersicht
    *   funktionale und nichtfunktionale Anforderungen
    *   Qualitätskriterien (Benutzbarkeit, Zuverlässigkeit, Effizient, Änderbarkeit, Übertragbarkeit, Wartbarkeit)
    *   Risikoakzeptanz
    *   Skizze Entwicklungszyklus und Systemarchtiektur / Struktogramm
    *   Lieferumfang
    *   Abnahmekriterien
*   Wichtige Dinge ruhig mehrmals beschreiben (Text & Bild, Text & Diagramm (UML), Text anders formuliert an anderer Stelle)
*   **Modell:** Grafische & formale Repräsentation des Systems aus Blickwinkel (z.B. State-Chart)
*   **Diagramm:** Grafische und überblickshafte Erklärung eines Sachverhaltes, z.B. Schichtenmodell
*   Diagramme brauchen immer eine Legende, grundsätzlich alle Elemente (Symbole, Verbindungslinien) erklären
*   Faustregel: In einem Diagramm sollte maximal acht Komponenten enthalten Ausnahme: Architekturtapete
*   Verschiedene Sichten dokumentieren: Use Cases (Blackbox), Nutzer, Struktur (Subsysteme, Komponenten), Deployment, Laufzeit
*   Glossar gut für Begriffe/Konzepte und ihre Bezüge untereinander (es gibt häufig Mißverständnisse wo ein Glossar für eine klare Definition sorgen kann)
*   Auf Patterns verweisen, wo dies möglich ist (Pattern-Dokumentation generell gute Vorlage für eigene Problembeschreibungen)
*   Während der Entwicklung beschreibt Doku die Art und Weise, wie das System entwickelt wird und welche Bausteine/Strukturen verwendet werden
*   Nach der Entwicklung zeigt Doku das System aus verschiedenen Sichten, erklärt Entscheidungen und Zusammenhänge (vgl. Hausbau: Grundriß, Vorderansicht, Elektifizierung)
*   Empfehlenswert: Projekttagebuch > sammelt Zeitpunkt und Ergebnis wesentlicher Projektentscheidungen (Wer Wann Was in Wiki, Blog oder Protokoll sichern)
*   Doku von **REST-Architekturen** wichtig zur Abgrenzung/Entwicklung in Front- und Backend
*   Wesentliche Bestandteile:
	*   Ressourcen-URL (Pfad)
	*   HTTP-Methode
	*   Datentyp Input (z.B. multipart/form-data), evtl. Header
	*   Output (z.B. JSON)
	*   mögliche HTTP-Statuscodes (z.B. bei Fehlern)
	*   weitergehende Beschreibung
*   **WHY-Ansatz** hilfreich bei Definition/Doku von User Stories bzw. Use Cases:
*   In the context of **use case/user story u**, facing **concern c** we decided for **option o** to achieve **quality q**, accepting **downside d**
*   Möglichst relevante und belastbare Entscheidungen sollten im Anbetracht einiger Aspekte dokumentiert werden:
	*   Initiale Doku "schlank" bzw. minimalistisch (eher Entscheidungsvorlage)
	*   Wichtige (vorher getroffenen) Grundlagenentscheidungen erfassen und priorisieren, da sie die Basis (bzw. eine Grundlage) für die aktuelle Entscheiung bilden
	*   Dokumentation erst dann erweitern/untermauern wenn die Entscheidung von allen Beteiligten getroffen wurde und diese halbwegs sicher sind, dass die Entscheidung auch mittelfristig Bestand hat
	*   Zusätzlich bereits vorhandenes Material/Quellen sichten und im angesichts der aktuellen Entscheidung betrachten
	*   im besten Fall kann eine Entscheidung auch in den Anforderungen un im letztliche entstandenen Design bzw. Code nachvollzogen werden (Traceability)
*   A.-Frameworks sammeln Vorgehensweisen, Beschreibungsmittel, Methoden und Werkzeuge:
	*   **arc42**: Template für Beschreibung einer A. mit einer festen Struktur zur Entwicklung, Dokumentation und Kommunikation von SW-Architekturen
	*   **4+1-Framework:** ordnet Anwendungsszenarien anhand von Logical View (funktionale Sicht), Development View (EW-Sicht, z.B. durch UML), Process View (ähnlich Laufzeitsicht)und Physical View (Abbildung SW-System auf technische Systeme) an
	*   **RM-ODP:** besonders für verteilte Systeme geeignet, im Zentrum stehen das System und die Umgebung, verwendet ebenfalls mehrere Viewpoints:
		*   **Enterprise:** Zweck, Nutzung und Regeln des Systems
		*   **Information:** Inhalte und Bedeutung der Daten
		*   **Computational:** System wird in Objekte und deren Schnittstellen zerlegt
		*   **Engineering:** Mechanismen und Funktionen zur verteilten Interaktion
		*   **Technology:** Verteilung und Verbindung der Artefakte auf physische Systeme
	*   **SAGA:** behördlicher Ansatz (BMI), orientiert sich an RM-ODP, wesentliche Ziele: Interoperabilität, Kostenreduktion, Risikoreduktion, Offenheit, Skalierbarkeit, Wiederverwendbarkeit
	*   **TOGAF**: Entwurf, Planung, Implementierung und Wartung von Unternehmens-Architektur (Unternehmen = Sammlung von Organisationseinheiten mit gemeinsamen Zielen):
		*   Geschäftsarchitektur: basiert auf Modellierung der Geschäftsprozesse, betrachtet Strategie, Aufbauorganisation und Business Capabilities
		*   Informationssystemarchitektur: Datenund Anwendungsarchitektur (Datenbeziehungen und ihre Schnittstellen sowie die Anwendungen für die Ausführung der Geschäftsprozesse)
		*   Technologiearchitektur: Aufbau & Betrieb der IT-Infrastruktur
	*   **IEEE-1471** (Recommended Practice for Architectural Description of Software-Intensive Systems)
		*   Dokument, Repository oder sonstige Sammlung (Wiki) zur Beschreibung der A., die in Artefakte gegliedert wird, Beschreibung meist in einem Dokument
		*   Fokussiert sich auf die Anliegen (Concerns) und Beteiligten (Stakeholder) eines Systems
		*   System wird v.a. von Umgebung beeinflußt und umgekehrt
		*   Verschiedene Sichten (Views) der wesentlichen Kriterien wie z.B. Zweck, Risiken, Wartbarkeit werden aus Sicht der Stakeholder getrennt und damit unterschiedlich betrachtet
*   **UML2:** standardisierte grafische Darstellung von Modellen für alle Aspekte einer Software-Architektur, verschiedene Diagramm-Typen:
	*   Struktur: Klasse, Objekt, Paket, Komponente, Kompositionsstruktur, Verteilung
	*   Verhalten: Aktivität, Zustand, Anwendungsfall
	*   Interaktion: Sequenz, Kommunikation, Zeitverhalten, Interaktionsübersicht
*   UML ist ein akzeptierter Standard und gegenüber eigenen Symbolen immer zu bevorzugen
*   Diagramme generell einfach halten (5-9 Elemente), Ausnahme: Architekturtapete
*   **Klassendiagramm** (Name = Klasse):
	*   zeigen Struktur und Beziehungen (z.B. Assoziationen, Aggregationen, Spezialisierungen) zwischen Klassen
	*   Privatkunde/Geschäftskunde implementiert (geschlossener Pfeil) Interface Kunde, offener Pfeil wäre Aufruf
	*   Public (+) und Private (-) können auch gekennzeichnet werden
	*   Beziehungen über X…X (m:n)
*   **Paketdiagramm**:
	*   Sicht auf Strukturen und Abhängigkeiten
	*   Sammelt i.d.R. mehrere Klassen / Interfaces in einem Namensraum
*   **Komponentendiagramm** (Strukturdiagramm):
	*   Zusammenfassung von Bausteinen in UML-Komponenten und Schnittstellen mit ihren Abhängigkeiten (+ evtl. Konnektoren)
	*   geschlossener Kreis ist angebotene Schnittstelle, offener Halbkreis benötigte S.
	*   Stereotypen mit Doppelpfeilen <<>> auszeichnen (z.B. Entity, Interface, Control, View)
	*   Abhängigkeiten mit "access", "import", "merge" oder "use" kennzeichnen
*   **Sequenzdiagramm**:
	*   Zeigen Interaktionen zwischen Instanzen von Bausteinen
	*   zeitabhängiger Ablauf des Systems (Lebensline) mit Ereignissen und Nachrichten zwischen Objekten
*   **Aktivitätsdiagramm**:
	*   Stellen mögliche Abläufe in einem System dar (dynamische Aspekte)
	*   Sinnvoll für Algorithmen, Datenund Kontrollflüsse
	*   Ein- und Ausgabe immer am Rand des Objektflusses
*   Laufzeitkontextdiagramm zur Darstellung des Gesamtsystems mit Akteuren/Nachbarsystemen (gut für öffentliche Schnittstellen)
*   nicht jeder Ablauf kann modelliert werden (sinnvoll: Normalfall, Grenzfall, Ausnahmen)
*   UML-Diagramme gut für Klassen, Pakete (=Menge von Bausteinen), Komponenten, Struktur (Hierarchie), Sequenz (Interaktionen, Testfälle), Zustand (vollständiges Verhalten)
*   verbreitet sind vor allem Klassen-, Status (Zustands)- und Interaktivitätsdiagramme sowie einfache Aktivitätsdiagramme, weiterhin Sequenzdiagramme bei komplexeren dynamischen Aspekten
*   ein Systemkontextdiagramm ist zu Beginn eines Projektes immer hilfreich, ein Kompositionsstrukturdiagramm liefert einen guten Überblick über das Gesamtdesign
*   UML weniger gut für Use Cases, Verhalten, Beschränkungen (Constraints), Aktivitätsdiagramme oft zu kompliziert, Deploymentdiagramme oft überflüssig (Ausnahme: verteilte Systeme)
*   Constraints sind kaum in UML modellierbar, dann einfach einen Kommentar ins Modell setzen
*   UML erlaubt Erstellung von Metamodellen (Stereotypen & tagged values standardisieren), tendenziell aber kompliziert
*   Sinnvolles Template ist arc42, gliedert Doku in folgende Haupt-Teile:
	*   **Einführung und Ziele**: fachliche Aufgabenstellung bestimmen, Erfüllung und Einhaltung der Randbedingungen unter Berücksichtigung der Architekturziele
	*   **Aufgabenstellung**: faßt fachliches Umfeld des Systems zusammen: Was geschieht im Umfeld? Warum ist das System wichtig? Welche Probleme werden gelöst? Kurzbeschreibung der wichtigsten Geschäftsprozesse, FAs, NFAs, Mengengerüste, Top 3 bzw. Top 5 der Qualitätsziele aufstellen
	*   **Randbedingungen**: Einschränkungen im Entwurfsund Entwicklungsprozeß
	*   **Konventionen**: Dokumentation, Programmierung, Versionierung, Namensgebung (sowohl technisch als auch organisatorisch)
	*   **Kontextabgrenzung**: System von Nachbarsystemen unterscheiden, Schnittstellen festlegen, Datenaustausch und kanäle beschreiben, Geschäftsregeln
	*   **Qualitätsszenarien**: systematische Bewertung der Architektur gegen vorgegebene Qualitätsziele, sollte Qualitätsbaum(ATAM) enthalten, verschiedene Bewertungsszenarien beschreiben, also wie etwas auf einen bestimmten Auslöser reagiert (Nutzungsszenarien, Änderungsszenarien, Grenz/Streß-Szenarien )
	*   **Risiken**: nach Priorität geordnete Liste der erkannten Risiken (inklusive Wahrscheinlichkeiten und Schadenshöhe)
	*   **Glossar**: sammelt die wichtigsten Begriffe der Architektur alphabetisch

## Architekturen bewerten

*   nur was meßbar ist kann bewertet werden (Projektziele)
*   Architekturanalyse ermittelt, inwieweit Qualitätsmerkmale erfüllt werden (QS) und steigert langfristig die Effektivität der Entwicklung (Bugs und Schwachstellen werden entdeckt)
*   Architekturen veralten prinzipiell, Weiterentwicklung verändert die A., Mitarbeiter verlassen das Projekt/die Firma
*   originale und existierende Architektur auf Konsistenz prüfen, Realisierung über Ermittlung von Komponenten und ihrer Bestandteile (Welche Interfaces? Abhängigkeiten? Datentypen?)
*   Prozesse bewerten: Entwicklung und Betrieb
*   Artefakte bewerten: Anforderungen (und die zugehörige Analyse), Dokumentation, Code, Bugtracker
*   Architektur kann qualitativ (Qualitätsmerkmale) und quantitativ bewertet werden, weiterhin sollten Tests berücksichtigt werden (Abdeckung Code, FAs und NFAs)
*   Quantitative Metriken:
	*   Vermessung und Bewertung (Code)
	*   Prozessbetrachtung (z.B. Verhältnis Anzahl EW/PL, Änderungshäufigkeiten)
	*   Überprüfung der Umsetzung (Architekturregeln)
	*   Analysen zum Software-Repository (z.B. Code-Duplikate)
*   Typische Metriken:
	*   Anforderungen: Anzahl geänderter Anforderungen/Zeiteinheit
	*   Code: Anzahl Codezeilen, Kopplung, statischer Methoden, Verhältnis Code/Kommentarzeilen, Anzahl Methoden/Klasse, Vererbungstiefe
	*   Erstellungsprozeß: implementierte/getestete Features pro Zeiteinheit, Relation Meetings/Gesamtzeit, Korrektheit der Schätzungen
	*   Fehler: Durchschnittszeit zur Behebung von Fehlern, gefundene Fehler/Paket
	*   Test: Anzahl Testfälle, Testabdeckung
	*   Design: Abhängigkeiten, Abstraktheit, Instabilität
	*   System: Ressourcenverbrauch, Zeit für Abarbeitung bestimmter Funktionen/Anwendungsfälle
*   Generell lassen sich viele Qualitätsmerkmale kaum messen, dies können dann erfahrene Architekten dann i.d.R. am besten beurteilen
*   Was möglich ist sollte aber gemssen werden (in Konstruktion beachten), sinnvolle Verbesserungen beruhen oft auf Messungen (Bsp. justin.tv: 500% erhöhtes Sharing durch Reduktion der Menütiefe)
*   Ein System läßt sich eigentlich nie komplett testen, es müssen daher Prioritäten gesetzt werden (Anhaltspunkt: Risikobetrachtung), meist bilden die Anforderungen auch die Basis für (funktionale) Testfälle
*   Tests müssen stets automatisiert ablaufen (können) und somit auch reproduzierbar sein (vermeidet Regression, Unsicherheit, schlechtes Design)
*   Unit-Tests sollten nicht länger als 20 Zeilen sein
*   Abgrenzung zwischen funktionalen und Akzeptanz-Tests nicht immer möglich, ersteres ist eher eine Verifizierung (Funktionieren die Szenarien?), letzteres eine Validierung (Sind die Ergebnisse/Daten korrekt?)
*   Funktionale Tests müssen nicht in endgültiger Umgebung laufen, Akzeptanztests sollten schon (Absprache mit Kunden)
*   Gutes Muster für Tests ist Arrange-Act-Assert:
    *   Arrange: Vorbereitungen treffen, Umgebung konfigurieren, Instanzen aller Objekte erzeugen
    *   Act: einzelne Aktion durchführen (stets nur eine, sonst mehrere Fehlerquellen)
    *   Assert: Prüfen aller Nachbedingungen
    *   Teardown: Manchmal nötig (bes. bei funktionalen Tests), Wiederherstellen des Zustands vor dem Test
*   Testautomatisierung lohnt sich meist recht schnell (vgl. manuelle Tests mit entsprechenden MAs)
*   Es sollten alle drei wesentlichen Testarten vorhanden sein:
    *   Unit-Tests: Testen einzelne Methoden/Basisfunktionalitätem auf Korrektheit, meist Aufgabe des Entwicklers, wird lokal und auf CI-Umgebung ausgeführt, hohe Anzahl von Testfällen, kurze Ausführungszeit
    *   Integrations-Tests: Testet die Interaktion mehrerer Klassen und simuliert dabei auch externe Abhängigkeiten, wird oft auf eigener Testumgebung ausgeführt (evtl. CI)
    *   AcceptanceStage-Tests: Testen die Funktionalität der Anwendung (meist clientseitig, also z.B. im Browser), oft über vordefinierte Pfade ("happy flow"), findet oft auf Zielsystem statt, meist nur wenige Testfälle
*   Alle Tests sollten in einer Continuous Integration-Umgebung ausgeführt werden, die idealerweise folgende Bestandteile hat:
    *   Commit-Stage (Unit-Tests, Codeanalyse)
    *   Acceptance-Stage (Smoke-Tests, AcceptanceStage-Tests)
    *   Performance-Stage (Performance- und Lasttests)
    *   Abnahme und Release (Zielumgebung konfigurieren, Smoke-Tests ausführen)
*   Subsysteme sollten getestet werden sobald die Arbeiten an ihnen abgeschlossen sind (mit eigenen Tests und Testdaten)
*   Auch nichtfunktionale Tests (z.B. Lasttests) sollten so früh wie möglich durchgeführt werden
*   Die Verantwortung für alle Testarten liegt in den jeweiligen Teams, dort sollten auch die Tests geschrieben werden
*   zyklomatische Komplexität: Maß für Komplexität, ermittelt die minimal nötigen Wege durch ein Modul bzw. maximale Anzahl von Testfällen zur Abdeckung aller Aspekte
*   Ermittlung dieser Kennzahlen über
	*   statische Code-Analyse: wertet Code aus (z.B. Sotograph, Sonar), kennt keine Semantik oder Fachlichkeit und ist daher begrenzt
	*   Simulation: Erfüllt eine Entscheidung die gesetzten Qualitätskriterien, Beispiel: welche Middleware ermöglicht 10000 Verarbeitungen/Sekunde? Prototyp bauen!
*   Qualitätsmodell SQALE beschreibt genauer, worin die technische Schuld besteht und ermittelt "Kosten" für deren Beseitigung (auch als Plugin für Sonar verfügbar)
*   Vier wesentliche Arten von Prototypen:
	*   Demo: visuelle Darstellung, meist für Akquisition
	*   Vorschau: zeigt verschiedene Aspekte der UI oder von bestimmten Funktionalitäten (dient zur Analyse)
	*   Labormuster: experimentell, beantwortet konstruktionsbedingte Fragen (Simulation)
	*   Pilotsystem: bildet Kern des Produkts sowie evtl. auch Basis für Weiterentwicklung (alle anderen Prototyp-Arten werden verworfen)
*   Gute Tools für UI-Prototyping und Abläufe: Balsamiq Mockups, Axure, Invision
*   findet i.d.R. im Nachgang eines Projektes statt:
	*   Stimmt Implementierung mit Architektur überein?
	*   Sind funktionale Anforderungen korrekt zugeordnet?
	*   Wurden Qualitätsanforderungen umgesetzt?
	*   Stimmen die Prozesse? (Orga, Betrieb, EW, Ressourceneinsatz)
*   Vorhandenes prüfen (keine neuen Features hinzufügen) aber keine MA bewerten
*   Architektur erkennen: Was war der initiale Ansatz? Wie hat sich die A. verändert? Nötig bei fehlender Doku und abwesenden MAs
*   wichtig ist dabei immer der Vergleich mit anderen Projekten, Metriken allein sagen nichts über Funktionsweise/Qualität zur Laufzeit aus
*   einige Tools erlauben sogar ein virtuelles Refactoring (Auswirkungen nicht auf Produktiv-Code testen sondern in einer Art "Sandbox")
*   zwei Arten für qualitative Reviews (liefern eher Prosa):
	*   erfahrungsbasiert: Stärken/Schwächen/Chancen/Risiken einer Architektur ermitteln
	*   szenariobasiert: Welche Probleme könnten auftreten? Welche Änderungen wären vorzunehmen?
*   erfahrungsbasierte Reviews sind recht umfangreich (> 15 Tage) und werden meist von externen erfahrenen Architekten gemacht – drei Phasen:
	*   Scoping: Was soll das Review, Was sind die Anforderungen, Welche Quellen brauche ich für das Review (Doku, Leute)
	*   Information Collection: Sammle Beschreibungen, Code, Beispiele, Interviews mit allen Stakeholdern (einzeln und vertraulich)
	*   Evaluation: SWOT zusammenstellen, Maßnahmen für Schwächen überlegen, erste Version des Reports auch an alle Stakeholder schicken, Abschluß-Workshop am Ende
*   **Active Design Reviews** werden oft über konkrete Aufgaben umgesetzt (z.B. nimm Bibliothek X, baue ein Tool Y damit, wie lange hat es gedauert?)
*   gut für punktuelle Probleme oder eigene Frameworks geeignet
*   erfahrungsbasierte Reviews liefern Erkenntnisse und Maßnahmen, steigern aber nicht das gemeinsame Verständnis eines Systems (im Gegensatz zu SAAM und ATAM)
*   Nützlich sind auch vordefinierte Quality Gates, die zu verschiedenen Zeitpunkten und unabhängig vom Projekt geprüft / verglichen werden können (ggf. auch extern), diese prüfen konkreten Inhalt und keine "Formalien"
*   Bewertungsmaß ist immer die Qualität, definiert am besten über Szenarien & Qualitätsbäume
*   **Szenarien:** eine Quelle löst etwas aus, wie reagiert das System (Auswirkungen auf Qualität)
*   Sechs Teilaspekte von Szenarien:
	*   Auslöser: Ereignis beim Zusammenspiel zwischen Stakeholder & System
	*   Quelle des Auslösers: intern/extern/Benutzer/Admin/Manager
	*   Umgebung: Zustand des Systems (Normal/Änderung/ Stress)
	*   betroffener Systembestandteil
	*   Antwort: Reaktion
	*   Antwortmetrik: Meßbarkeit (Bewertungsmodell für Qualität der Antwort)
*   Typen von Szenarien:
	*   Nutzungsszenario: zur Laufzeit
	*   Änderungsszenario: Modifikationen, Updates
	*   Stress-/Grenzszenario: Last, Stromausfall, ...
*   Entscheidungen basierend auf Szenarien immer begründen (Warum/Welche Kompromisse/Einfluß auf Ziele/Risiken/Analysen/Prototypen)
*   Szenarien oft für weitere Entwicklung relevant (z.B. Mandantenfähigkeit, Skalierung, ...)
*   szenariobasierte Ansätze sind z.B. SAAM oder ATAM (beide recht formal)
*   **Qualitätsbäume:** Hierarchische Darstellung der Qualitätsmerkmale, Allgemeines links, Spezielles rechts (z.B. Performance Latenz - Hops), dann priorisieren
*   aus den Qualitätsbäumen lassen sich oft Szenarien erstellen
*   Häufige (inhaltliche Fehler) in Architekturen und Projekten:
	*   Umfang: zu viele/wenige Funktionen im System
	*   NFAs: Abwägung / Priorisierung wichtig
	*   Nichtssagende Modelle: Systemdiagramme oft sehr komplex (A3-Seite) oder zu knapp, Code ist oft nützlicher weil er meist hinterfragt und immer nachvollzogen werden kann
	*   Entwicklung beginnt zu spät: viel Zeit geht in Spez, Konzepte sind wichtig, aber Implementierung muß von Anfang an beachtet werden
	*   Zielplattform unklar: Plattformunabhängigkeit ist nicht konsequent durchzuhalten (Festlegung nötig), Abhängigkeiten müssen klar sein (z.B. Versionskonflikt: funktioniert mit 9.1, aber nicht 9.2), Isolation von plattformspezifischen Lösungen
	*   zu viele Annahmen: Benchmarks sind so gut wie nie übertragbar, eigene Tests (ggf. mit Mockups / Prototypen) früh und Lasttests ggf. mit simulierten Daten durchführen
	*   Sicherheit selbst implementiert: Grundkenntnisse genügen nicht, teure Produkte sind meist aus gutem Grund teuer (Sicherheit elementar)
	*   Keine Fehlerszenarien: Es ist nie vorhersehbar was ausfällt, jedes Element muß auf Redundanz/Ausfallsicherheit geprüft werden
	*   Kein Fallback: Es gibt keine Möglichkeit zum Umschalten/Zurückschalten
*   Oft müssen Frameworks evaluiert werden - auch für diese gibt es z.B. folgende generische Bewertungskriterien:
	*   Bestehendes Technologie-Invest
	*   Server-Roundtrips und Usability, Abhängigkeiten (z.B. Browser, Runtime)
	*   Entwickler-internes Know-How und Recruiting
	*   Performance
	*   Wiederverwendbarkeit
	*   IDE-Support
	*   Testautomatisierung
	*   Zukunftsfähigkeit
	*   Entwicklungskosten + Wartung
*   hilfreich zur weiteren Analyse/Vergleich: Google Trends, Github Committer/Stars/Aktivität, Job Trends (indeed), Hacker News, LinkedIn/Xing-Profile, Fragen auf stackoverflow

## Projekte schätzen
*   typische Einflüsse auf Schätzung eines Gesamtprojektes, die einen Puffer in jeder Schätzung nötig machen:
	*   Anforderungen werden hinzugefügt
	*   Team nicht zum benötigten Zeitpunkt gestaffed/vorbereitet
	*   weniger erfahrene Teammitglieder als geplant
	*   geänderte Anforderungen
	*   Teammitglieder müssen auch in alten Projekten/strategischen Themen arbeiten
	*   instabile Funktionalitäten werden wieder angepasst/refactored
*   typische Punkte die in Schätzungen "vergessen" werden - FAs:
	*   Setup und Installation
	*   Datenkonvertierung/Import
	*   Glue code für 3rd party Komponenten
	*   Hilfe
	*   Deployment
	*   Schnittstellen zu externen Systemen
*   typische Punkte die in Schätzungen "vergessen" werden - NFAs: Genauigkeit, Interoperabilität, Modifizierbarkeit, Performance, Portabilität, Zuverlässigkeit, effiziente Bedienbarkeit, Wiederverwendung, Skalierbarkeit, Sicherheit, Usability
*   Vorab-Spezifikiation vs. iterativ: viele Teams finden einen Mittelweg, der die Kernfunktionalitäten beschreibt aber Design/Konstruktion/Test/Release erfolgen iterativ - damit auch belastbare Schätzung möglich
*   Einordnung ein Projekt in Größe (T-Shirt-Sizing):
	*   Klein: 5 oder weniger MA, konstante Teamgröße, Schätzungen am besten "Bottom-Up"
	*   Mittel: 5-25 MA, Dauer 3-12 Monate
	*   Groß: 25 MA, 6-12 Monate, Schätzungen eher "Top-Down"
*   T-Shirt-Sizing für Features auch wichtig um EW-Aufwände mit Business Value gegenüberzustellen - daraus kann man leicht Prioritäten ableiten (quick win)
*   typische Projektgrößen in LoC/MA-Jahr nach Cocomo 2 (relevant ist mehr der Trend, weniger die konkrete Zahl):
	*   10K: 2000-25000 (Durchschnitt 3200)
	*   100K: 1000-20000 (Durchschnitt 2600)
	*   1M: 700-10000 (Durchschnitt 2000)
	*   10M: 300-5000 (Durchschnitt 1600)
*   realistische Größen sind zwischen 10 bis 50 Lines of Code/Entwickler/Tag
*   Vergleichsgrößen: Quake 3 300.000 LoC / Windows XP 40.000.000 / 
*   Faktoren die eine Schätzung beeinfussen nach Cocomo 2, gelistet nach Bedeutung:
	*   Komplexität des Produktes (wichtigster Faktor, vor allem bestimmt durch den Typ der Software und den gesamten Funktionsumfang)
	*   Anforderungsanalyse (Verständnis der Afos, Priorisierung, Abstimmung kann Aufwand signifikant senken)
	*   Qualität der Entwickler (Erfahrung, Vielseitigkeit, Geschwindigkeit)
	*   Zeitbeschränkungen (erhöhter Aufwand für Echtzeitsysteme oder System-Software)
	*   Konstantes Team (hohe Fluktuation senkt Produktivität drastisch)
	*   Offshoring / Verteilung des Teams (mehrere Standorte erhöhen den Aufwand um 56% vgl. mit einem Ort)
	*   Erwartete Zuverlässigkeit (erhöhte Zuverlässigkeit kostet Zeit, vgl. Embedded Systems vs. Portal-Projekte)
	*   Umfang der Dokumentation (Aufwand)
	*   Erfahrung in der Domäne (Geschäftsbereich und Prozesse sollten klar sein, erhöht sonst Einarbeitung)
	*   Software Tools (moderne Tools/Libraries können Aufwand deutlich senken)
	*   Volatilität der Plattform (Änderungen in Frameworks / Bugfixes der Plattform verzögern das Projekt)
	*   Einschränkungen Speicherplatz (Optimierung hinsichlich RAM/HD kostet Zeit)
	*   Erfahrung in Programmiersprache und Tooling (neue IDEs, Build-Systeme führen zu steilerer Lernkurve)
	*   Vertrauter Prozess (Einfache EW-Prozesse senken tendenziell den Aufwand, verbessern aber nicht unbedingt die Qualität)
	*   Größe der DB (große DBs erhöhen den Aufwand für alles in der Folge)
	*   Erfahrung mit EW-Plattform (bekannter Technologiestack senkt den Aufwand)
	*   Architektur und Risikobewertung (Risiken und Entscheidungspfade vorher ermitteln um vorbereitet zu sein)
	*   Vorhersehbarkeit/Ähnlichkeit (ähnliche Systeme zu existierenden senken den Aufwand)
	*   Wiederverwendung (weniger Aufwand für isolierte Lösung, Wiederverwendung scheitert tendenziell oft)
	*   Teamgeist (kooperative EW sparen Zeit)
	*   Flexibilität der Afos (exakte Umsetzung aufwändiger als wenn Spielraum vorhanden ist)
*   weitere eher generelle Punkte die auftreten können bzw. werden:
	*   administrativer. bzw. Buchungsaufwand: zusätzlich 5-10%
	*   IT support (Einrichtung Rechner, Installation) 2-4% extra
	*   Konfigurationsmanagement und Build 2-8% extra
	*   1-4% für zusätzliche Anforderungen pro Monat
	*   Arbeit an verteilten Standorten: 25% extra
	*   Entwicklung mit neuen Tools/Programmiersprachen kostet 20-40% im Gegensatz zu vertrauter Umgebung
*   Generall in Schätzungen: Wenn möglich **zählen**, ansonsten **berechnen**, nur wenn es nicht anders geht **schätzen**
*   Zählen kann man z.B. folgendes:
	*   Anforderungen (Aufwand in Stunden pro Afo für EW, Test, Doku, technische Spez)
	*   Features, Use Cases, Stories (Stunden/Feature)
	*   Funktionspunkte (Aufwand hinsichtlich EW/Test/Doku pro Punkt)
	*   CRs (EW/Test/Doku pro CR)
	*   Webseiten (Aufwand für UI und dahinterliegendes Backend)
	*   Reports
	*   Dialogelemente
	*   DB-Tabellen
	*   Klassen (bei OOP, auch Zeit für Code-Review berücksichtigen)
	*   gefundene Fehler (Stunden/Fehlerbehebung, Zahl Regressionen)
	*   Anzahl Konfigurationseinstellungen (z.B. Properties)
	*   LoC
	*   Anzahl der Testfälle
*   folgende Daten sollten im Laufe eines Projektes gesammelt werden: Größe (z.B. LoC), Aufwand (MA-Monate), Zeit (Monate), Fehler (eingeordnet nach Wichtigkeit)
*   nach einiger Zeit kann ein Projekt dann kalibiriert werden:
	*   Unsere EW schaffen X LoC/Monat
	*   Ein team mit drei Pewrsonen schafft X Stories/Monat
	*   Unser Team benötigt X Stunden für EW/Test/Doku der Use Cases
	*   Unser Team benötig X LoC/Funktionspunkt in Java und X LoC/FP in C++
*   generell korreliert ein größeres Team nicht mitgesteigerter Produktivität (ideal laut Putnam: Team aus 5-7 MA), größere Teams arbeiten z.B. wg. erhöhtem Abstimmungsbedarf kaum schneller
*   Checkliste für Schätzungen:
	*   Ist klar definiert, was geschätzt werden soll?
	*   Beinhaltet die Schätzung alle Teilaufgaben?
	*   Sind alle Funktionsbereiche enthalten?
	*   Ist die Schätzung granular genug so dass keine "Hintergrundarbeit" nötig ist?
	*   Wurde auf Erfahrungswerte geachtet statt einfach "au dem bauch heraus" zu schätzen?
	*   Erfolgt die Schätzung durch die Person die die letztliche Arbeit leistet bzw. wird sie von dieser akzeptiert?
	*   Ist die angenommene Leistung ähnlich zu der in vergangenen ähnlichen Aufgaben?
	*   Beinhaltet die Schätzung einen Worst/Best/Most likely Case?
	*   Wird der erwartete Umfang aus Best/Worst/Most likely Case berechnet?
	*   Wurden die Annahmen in der Schätzung dokumentiert?
	*   Haben sich Rahmenbedingungen seit der Vorbereitung der Schätzung geändert?
*   Das "Gesetz großer Zahlen": Mehrere Einzelschätzungen gleichen Fehler eher aus als eine einzelne Komplettschätzung und sind darum genauer
*   Eine Schätzung basierend auf Analogie läuft in etwa wie folgt ab:
	*   Kennzahlen eines vorherigen Projektes ermitteln (z.B. DB-Größe, UI, Reports, Basisklassen, Geschätsregeln)
	*   Größen hinsichtlich des aktuellen Projektes einordnen (daraus folgen Faktoren für Multiplikation)
	*   Schätzung des neuen Projektes prozentual aus den alten Daten ermitteln
	*   Schätzung anhand der benötigten Zeit des Vorgängerprojektes abschließen, dabei Annahmen überprüfen und ggf. Schätzfaktoren einbeziehen
*   Zeitplan kann ebenfalls aus vergangenen (vergleichbaren) Projekten ermittelt werden, dafür einfach pro Projekt die Faktoren LoC, Dauer, Aufwand (MA-Monate) und Produktivität (z.B. LoC/Monat) in einer Tabelle gegenüberstellen
*   auch Fuzzy Logic kann genutzt werden um LoC für Neuprojekt aus füheren Projekten heraus zu ermitteln
*   dazu durchschnittliche LoC/Feature ermitteln (dabei Feature-Größe in sehr klein/klein/mittel/... unterteilen) und mit Anzahl der Features des Neuprojektes multiplizieren
*   LoC als Grundlage durchaus umstritten - Vorteile: leicht zu ernitteln, gut vergleichbar, viele hostorische Daten verfügbar, laut Studien auch zwischen verschiedenen Programmiersprachen gut vergleichbar
*   Nachteile: misst keine Produktivität/Effizienz, berücksichtigt Komplexität eines Projektes nicht, können kaum "direkt" geschätzt werden, Regln nötig (Leerzeilen/Zeilenlänge/3rd party/...)
*   letztlich basieren auch viele kommerzielle Schätz-Tools auf LoC
*   Messung nach Funktionspunkten basiert auf folgenden Elementen:
	*   Externe Eingaben: Views, Formulare, Dialoge, Eingangssignale
	*   Externe Ausgaben: Views, Reports, Graphen, Ausgangssignale
	*   Externe Queries: I/O-Kombinationen die in direkter Ausgabe resultieren z.B. Suche (involviert meist DB und Anwendungslogik zur Aufbereitung)
	*   Interne Logik: logische Gruppen von Daten zum Endnutzer z.B. als File oder in DB-Tabelle
	*   Externe Schnittstellen: Daten die von anderen Programmen verwaltet werden
*   für Schätzung kann es hilfreich sein, einfach nur die Menge der GUI-Elemente zu zählen (Fenster, Report, Datei, Schnittstelle) und hinsichtlich Komplexität zu bewerten
*   je nach Domäne unterschiedliches Verhältnis Entwickler/Tester, Beispiele:
	*   Geschäftsanwendung, z.B. Intranet oder Informationssystem: 3:1 bis 20:1
	*   kommerzielle Systeme, z.B. öffentlicher Shop: 1:1 bis 5:1
	*   wissenschaftliche/Entwicklungsprojekte: 5:1 bis 20:1
	*   Systemprojekte: 1:1 bis 5:1
	*   sicherheitskritische Systeme: 5:1 bis 1:2
	*   Windows 2000: 1:2
	*   NASA Space Shuttle Software: 1:10
*   Typischer Stage Gate-Prozess:
	*   Entdecken (Marktchance, erste technische Einschätzung, Business Case)
	*   Scope ermitteln (Produktvision, Anforderungen Marketing, Konzepte mit Kunden validieren)
	*   Planung (Afos ausarbeiten, EW-Plan, Budget schätzen, finaler Business Case)
	*   Entwicklung (EW-Lifecycle, Launch-Plan durch Marketing, finaler Testplan)
	*   Test/Validierung (Test durchführen, Entscheidung für Release)
	*   Launch (Marketing Rollout-Plan, Projekt abschließen, Feedback und Fehler sammeln, Geschäftsergebnisse monitoren)

## Fehlerbehandlung zur Laufzeit und Vorsorge für robuste Systeme
* Fehler zur Laufzeit werden passieren, fehlerfreie Systeme gibt es nicht, Bugs können nicht vermiedn sondern müssen überlebt werden
* oberste Priorität: Wiederherstellung - wenn sich nebenbei Daten zur Analyse sammeln lassen (z.B. Heap-/Thread-Dump) umso besser
* weitere wichtige Anhaltspunkte (gesondert zu sichern): Logfiles, Konfigurationsdateien
* Log files sollten immer rotieren und nie länger als nötig auf dem Produktivsystem archiviert werden (generell alle Arten von Reporting nicht auf Prod-Maschinen durchführen)
* Profiler können Gold wert sein, liefern konkrete Anhaltspunkte über Fehler im Code (Deadlocks)
* eine der häufigsten Fehlerursachen sind Aufrufe auf externe Systeme
* extrem viele mögliche Fehler - eine Auswahl:
	* Verbindungsaufbau schlägt fehl
	* Verbindungsaufbau sehr langsam
	* Abbruch der verbindung
	* keine Response
	* falsche Response
	* langsame Response
	* sehr viele parallele Requests
	* Festplatte voll
* jeder Socket/Prozess/Remote Call kann (und wird) mal hängenbleiben
* Fehlerkaskadierung unbedingt zu vermeiden (also ein Fehler bringt das ganze System zum Absturz / Unbenutzbarkeit), Lösungen hierfür:
	* Circuit Breaker (z.B. Hystrix)
	* Timeouts (für alle Integrationspunkte)
	* direkter Retry oft nicht nützlich (erhöht Last), evtl. ein verzögerter Retry sinnvoll
	* Health Checks helfen fehlerhafte Systeme über einen simplen Service-Call zu erkennen
* Circuit Breaker letztlich nur ein Wrapper für den eigentlichen Aufruf, vergleichbar zu einer Sicherung im Stromkreis (wenn "offen" fließt kein Strom, normalerweise geschlossen)
* Circuit Breaker sollten immer geschkossen werden können und "breaks" automatisch loggen
* in Java können sog. `SoftReferences` für große Objekte genutzt werden (geben Speicher bei garbage Collection frei)
* für java auch gute Dokumentation zu GC tuning
* Erhöhtes vertrauen in Aufrufe zu Fremdsystemen über **Test Harness**, also einen Ersatz für einen "echten" Service-Call
* dieses sollte folgende Fehlerszenarien abdecken:
	* Balehnung der Verbindung
	* Timeout
	* Service antwortet mit SYN/ACK aber sendet keine Daten
	* Service sendet stets RESET
	* Service bestätigt keinen Empfnag (führt zu dauerhaften Retransmits)
	* Service akzeptiert Requests sendet aber nur Response Header und keinen Body
	* Service sendet falschen MIME-Type
	* Service sendet viel größere Datenmenge als erwartet
	* Service lehnt sämtliche Zugsangsdaten ab
* Skalierung bei Punkt-zu-Punkt-Kommunikation generall eher schlecht, besser:
	* UPD broadcast, TCP/UDP Multicast
	* Publish/Subscribe Messaging
	* Message queues
* am besten skaliert immer eine "Shared Nothing"-Architektur (Problem: Failover) 
* SQL-Queries sollten immer mit LIMIT / ROWNUM begrenzt werden (Risiko: fhelerhafter Prozess müllt DB zu, jedes SELECT dann plötzlich viel langsamer)
* es ist gut SQLs vom DBA abnehmen zu lassen (laugh-test)
* jede Tablle sollte eine Revisionsnummer haben (so kann Anwendung sicherstellen, dass Datenmodell zur Programmversion passt), auch hilfreich bei Zero-Downtime-Deployment
* für schnelles Deployment neue Spalten mit NULL auffüllen, Constraints nicht direkt sondern nach dem Deployment setzen
* Trigger können genutzt werden um alte Daten in neues Schema zu überführen (Daten damit immer synchron)
* Remote-Verbindungen in DBs anderer Systeme generell nicht empfohlen (Datenhoheit) obowhl technisch möglich (vgl. Oracle)
* Daten in Testumgebung sollten inhaltlich ähnlich und von der Menge vergleichbar zur Produktion sein
* Testumgebung hat selten denselben Stand wie Prod, Infrastruktur sollte sich über VMs aber simulieren lassen
* hier hilft auch ein Blue/Green-Deployment bei dem immer eine Instanz live ist während die andere als Testsystem dient (bei Release wid geswitcht) 
* Metriken helfen bei Erstanalyse und im täglichen Betrieb, nützlich sind u.a.
	* Speicher (min/max heap size)
	* Garbage Collection (wie oft, Größe, freigegebener Speicher)
	* Threads (idle/busy/wie lang busy, max. concurrent in use)
	* DB / Connection pools (Anzahl, Nutzung, high/low water mark, Verfügbarkeit, Freigabe)
	* Traffic (gesamte Requests, Durchschnittliche Responsetime, Datenvolumen, Abbrüche, Timeouts, Requests/Sekunde)
	* Cache (Größe, Hit rate, Limit)
	* Circuit Breaker
* neben technischen Metriken helfen auch fachliche Metriken - Auswahl:
	* geschäftliche Transaktionen (Typ, Wert, Zeitraum, conversion, completion)
	* Nutzer (Anzahl, Demografie, Anteil registrierter Nutzer, Fehler)
	* Integrationspunkte (Interaktionen mit Fremdsystemen) 
* öffentliche Anwendungen immer dem Risiko von Angreifern ausgesetzt
* typisches Pattern: mehrere Calls kurz hintereinander von derselben IP (und ggf. unterschiedlichen Browsern)

## Anforderungsanalyse

*   oft sind Anforderungen nicht bekannt, daher verändern sie sich im Laufe des Projekts problematisch hinsichtlich Zeit & Budget (2/3 aller Softwareprojekte scheitern)
*   Aufgabe der Anforderungsanalyse ist es die Anforderungen und auch Herausforderungen des Kunden zu verstehen und diese sinnvoll zu bearbeiten - dies bildet die Grundlage für die weitere Struktur der Lösung, Datenmodelle und Implementierung
*   Kosten, Nutzen und Zeit(plan) konkurrieren oft mit strukturellen und operativen A.
*   Wenn die Lebenszeit des Produktes eher kurz sein wird verringert sich auch der Bedarf hinsichtlich der Anforderungsanalyse (frühe Bestimmung notwendig)
*   Hierarchie von Anforderungen/Features z.B. je nach aktuellem/zukünftigen Nutzen sowie Implementierungsund Pflegeaufwand
*   Analyse macht ein Projekt vorhersehbar, verringert Doppelarbeit und unnötigen Aufwand, erhöht aber natürlich den Gesamtaufwand (oft etwa 10-25% des Gesamtaufwands)
*   Anforderungen sind oft falsch, nicht meßbar, nicht testbar, fehlen ganz oder ändern sich zu stark
*   Anforderungsanalyse kann auch als eine Art Risikomanagement gesehen werden – sie behandelt auch und gerade den Umgang mit Änderungen (+daraus folgende Maßnahmen)
*   Aufgaben: Was soll das System tun? Was ist der Mehrwert? Wie fassen wir die Anforderungen zusammen?
*   Schablone für funktionale A.: Das System MUSS / SOLLTE / (WEM) DIE MÖGLICHKEIT BIETEN / FÄHIG SEIN + Prozesswort (ein Verb, z.B. "drucken")
*   Funktionale A. sollte stets nur ein Verb enthalten (Mehrdeutigkeit)
*   Eventuell kann noch eine Bedingung ergänzt werden
*   man muß nicht alle Anforderungen vor dem Projektstart beschreiben, aber zumindest die Architektur-relevanten sowie die NFAs
*   **Earned Value**: Graph mit X = Zeit und Y = umgesetzte Anforderungen, wobei jede Anforderung ungefähr den gleichen Umfang haben sollte (sonst entsprechend runden)
*   Werkzeuge: Modeling Tools, Tabellen, Wikis, Tracking-Tools mit Versionierung
*   Anforderungskategorien
	*   Nutzeranforderungen (eher extern): Was soll das System tun? Was ist das Geschäftsziel?
	*   Produktanforderungen (eher intern): Wie wird das Geschäftsziel verfolgt? Was kann das System anbieten?
	*   Komponentenanforderungen: Wie werden Produktanforderungen in Software umgesetzt?
*   Aktivitäten/Phasen der Anforderungsanalyse
	*   Finden der A.: über Interviews mit Stakeholdern, Workshops, Testnutzer, Simulationen
	*   Analyse der A.: Kosten/Effizienz der A. abwägen, Aufwand klären, Anforderungen priorisieren, Umsetzung andenken
	*   Spezifikation der A.: Was soll wie getan werden? Modelle und Szenarien entwickeln, Verhalten beschreiben (schriftliche Grundlage der Kommunikation)
	*   Validierung der A.: Wie gut paßt die Implementierung zu den Nutzeranforderungen (geht gut über Testfälle, die die Nutzeranforderungen abdecken)
	*   Bestätigung der Analyse: Abstimmung der Anforderungen mit dem Kunden (Abnahme), Einordnung der A. in Releases
*   Letztendlich müssen also alle Stakeholder am Tisch sitzen, das Problem muß sinnvoll strukturiert werden und es mjuß klar sein, dass alle das Problem verstanden haben
*   Am Ende steht eine "Vision" des Systems, die klarmacht, was die Anwendung grundsätzlich tun wird und die Probleme in Use Cases und Szenarien strukturiert
*   Anforderungen müssen nicht über Use Cases ermittelt werden, da sich aus diesen oft schwer konkrete Artefakte ableiten lassen - Alternative: Interaktionsszenarien (User Events mit Reaktion der Anwendung)
*   Die Analyse muß auf jeden Fall auch deutlich machen, ob der Einsatz von Standardprodukten, Frameworks oder existierenden (Teil-)Komponenten möglich und sinnvoll ist
*   Spezifikation bildet die Projektreferenz, Grundlage für alle Stakeholder, jegliche Änderungen im Projekt werden mit Spez abgeglichen, hilft bei Priorisierung
*   Spezifikation muß einfach, verständlich und klar strukturiert sein (z.B. **IEEE 830**) und ein Glossar enthalten (gern auch grafisch für die Erklärung der Zusammenhänge)

## ATAM

*   Architecture Tradeoff Analysis Method, analysiert Architektur-Entscheidungen hinsichtlich der Erfüllung von Qualitätsmerkmalen (Risikoerkennung)
*   Kernaspekte sind die Geschäftsziele und deren technische Umsetzung
*   kann in Konzeptionsphase als auch auf bestehende Systeme angewandt werden (Voraussetzung: Doku der Architektur), Ziel ist die Aufklärung aller Beteiligten über die Qualitätsanforderungen und -merkmale
*   Basisfragen zur Ermittlung der Qualitätsmerkmale:
	*   Welche Auslöser wirken auf die Architektur?
	*   Wie wird das Qualitätsmerkmal gemessen?
	*   Welche Entscheidungen beeinflussen das Qualitätsmerkmal?
*   ATAM liefert vor allem Risiken, aber keinen Maßnahmenkatalog
*   Vorteil von ATAM:
	*   eindeutige Qualitätsanforderungen
	*   verbesserte Doku der Architektur, Grundlage für A.-Entscheidungen
	*   Risiken können früh identifiziert werden
	*   Verbesserte Kommunikation zwischen den Beteiligten
*   vier wesentliche Phasen:
	*   Vorbereitung: Stakeholder identifizieren (durch Kunde)
	*   Kick-Off-Phase: ATAM sowie Geschäftsziele, A. und A.-Ziele vorstellen
	*   Bewertungshase: Qualitätsbaum & Szenarien erstellen, Analyse bzgl. der Szenarien
	*   Abschluß: Resultate präsentieren
*   alle Entscheidungen in vier Aspekte einteilen:
	*   Risiken: Gefährdung der Geschäftsziele
	*   Empfindliche Stellen (Sensitivity): geringe Änderungen mit weitreichenden Folgen
	*   Kompromisse: wechselseitige Beeinflussung von Qualitätsmerkmalen
	*   Nicht-Risiken: Szenarien werden risikolos erreicht
*   oft recht hoher Aufwand und eher „akademisch“ (etwa vier Tage Workshop, 30-40 Tage Vorbereitung und Projektarbeit)
*   ATAM basiert ebenfalls auf Szenarien (kurze Aussage, wer wie mit dem System interagiert)
*   Drei Szenario-Arten:
	*   **Anwendungsfall**(zur Laufzeit): Nutzer ändert Diagrammstil wie lange dauert das Rendern des Graphen, neuer Benutzer muß neue Funktion in max. 15 Minuten finden
	*   **Wachstum**: Veränderungen/Erweiterungen des Systems, Beispiel: Füge einen neuen Nachrichtentyp zu einem Message-basierten System innerhalb einer Woche hinzu
	*   **Erprobung**: Stress-Tests, Beispiel: Die Hälfte der Server fallen aus und das System läuft weiter, Beispiel 2: Stromausfall
*   Ergebnis ist ein Utility Tree:
	*   ähnlich Qualitätsbaum priorisierte Qualitätsmerkmale mit zugehörigen Szenarien
	*   alle Merkmale und ihre Szenarien werden hinsichtlich zweier Prioritäten sortiert (in High/Medium/Low):
		*   Bedeutung für das Geschäft Stakeholder
		*   Komplexität der (technischen) Umsetzung – Architekt
*   eine Bewertung muß immer auf Architekturentscheidungen gestützt sein (ggf. durch Analysen, Prototypen, Untersuchungen belegen)
*   am Ende erhält man einen guten Überblick zu folgenden Punkten:
	*   Qualität der Architektur in Bezug auf die Szenarien & Architekturziele
	*   Risiken bei Umsetzung, Maßnahmen zur Verhinderung
	*   risikolose Szenarien
*   Utility Trees werden meist im kleineren Kreis erstellt und evaluiert, daraus folgt dann das Brainstorming zu (weiteren) Szenarien mit allen Stakeholdern
*   Testfälle werden aus den Szenarien gebildet, die am höchsten priorisiert wurden
*   jedes Qualitätsmerkmal kann in drei Bereichen untersucht werden:
	*   externe Auslöser
	*   Architektur-Entscheidungen
	*   Antworten auf Auslöser
*   Beispiel: Türen des Fahrzeugs müssen auf Knopfdruck innerhalb 1 Sekunde geöffnet werden
*   resultierende Fragen: Ist 1 Sekunde eine harte Deadline? Welche Folgen hat die Nicht-Erfüllung der Deadline? Welche Komponenten sind vom Knopfdruck betroffen? Wie schnell reagieren die Komponenten? Wo liegen die Komponenten (physisch)? Was passiert bei vielen (parallelen) Auslösevorgängen in kurzer Zeit?
*   Attribute zur **Performance:**
	*   Auslöser:
		*   Modus: Normal/Überlast
		*   Quelle: internes Event, Unterbrechung, externes Event
		*   Frequenz: periodisch, unregelmäßig (sporadisch bzw. zufällig)
	*   Parameter:
		*   Ressource: CPU, Speicher, Festplatte, Netzwerk, …
		*   Ressourcenverwaltung: Queue (online, offline, Prioritäten, Beziehungen) oder Verteilung (geteilt oder gesperrt)
	*   Antworten:
		*   Latenz: Best/Worst Case, Kritikalität, Jitter
		*   Durchsatz: Kritikalität, Best/Worst Case
		*   Vorrang: Kritikalität, Ordnung (partiell/total)
*   Typische generelle Fragen zur Performance: Umgang mit Threads? Wie wird priorisiert? Wo ist die Hardware (physisch/geografisch)? Protokoll synchron/asynchron? Wie wird gecached? Wieviele parallele Sessions/User sind möglich? Wie wird mit Überlast umgegangen? Wie wird lastverteilt und überwacht?
*   Attribute zur **Modifizierbarkeit**:
	*   Auslöser: Änderungen an der Software
	*   Parameter: Kapselung, Aufteilung, Zuordnung
	*   Antworten: Komponenten, Konnektoren und Interfaces werden hinzugefügt, geändert oder entfernt – Auswirkung auf Komplexität!
*   typische Fragen zur Modifizierbarkeit: Gibt es ein Schichtenmodell? Gibt es ein Datenlager? Wieviele Teile der Architektur kennen die Datenstrukturen? Welche Teile der Architektur müssen bei Änderungen im Datenmodell bearbeitet werden?
*   Attribute zur **Verfügbarkeit**:
	*   Auslöser: Quelle (Hardware-/Softwarefehler), Typ (Zeit, Wert, Ende)
	*   Parameter: Hardware-/Software-Redundanz (Schweregrad, Fehlerrate, Reparaturrate, Fehler-Erkennungszeit), Wiederholbarkeit, Failover
	*   Antworten: Verfügbarkeit, Zuverlässigkeit, durchschnittliche Ausfallzeit
*   typische Fragen zur Verfügbarkeit: Welche Teile sind redundant und wie ist dies umgesetzt? Wie werden Fehler erkannt? Können aktive und passive Fehler erkannt werden? Wie lange dauert das Umschalten zwischen redundanten Komponenten?
*   ATAM vor allem zur Risikodokumentation sinnvoll: Begründung für die Auswirkung einer Entscheidung auf die beeinflußten Qualitätsmerkmale
*   in Architekturentscheidungen auch sensible Punkte und Tradeoffs erläutern
*   Beispiel: Verschlüsselungsstärke hängt von Länge des Schlüssels ab
*   ATAM ist in neun Schritte unterteilt, die in zwei Phasen ablaufen:
	*   Phase 1: Informationen beschaffen (Schritte 1-6)
	*   Phase 2: Auseinandersetzung mit den Stakeholdern (Schritte 7-9)
		1. Präsentation von ATAM für alle Stakeholder (Verständnis für alle Bestandteile von ATAM schaffen)
		2. Geschäftsanforderungen präsentieren (ca. 12 Slides, PL oder Kunde) Welche Ziele sollen mit dem System erreicht werden, was ist der Auslöser, Motivation, Geschichte, Marktumfeld, Einschränkungen
		3. Architektur präsentieren (ca. 20 Slides) Darstellung der gesamten Architektur, Anforderungen, technische Rahmenbedingungen, Interaktion mit weiteren Systemen, Schichten, Komponenten, Prozesse, Anwendungsfälle
		4. Architekturansätze identifizieren wichtigste Strukturen nennen und beschreiben, wie sie sich hinsichtlich zukünftiger Veränderungen verhalten (Wachstum, Austausch, Angriffe, Integration in Systemlandschaft)
		5. Utility Tree erstellen (priorisierte Qualitätsmerkmale anhand passender Szenarien gliedern)
		6. Architekturansätze analysieren Dokumentation der Risiken, sensiblen Punkte und Tradeoffs (z.B. in Form einer Liste) anhand der Szenarien und der jeweiligen Umgebung (z.B. Betrieb, Test, ...)
		7. Brainstorming & Priorisierung die wesentlichen Szenarien aller Art mit allen Stakeholdern durchsprechen und priorisieren (z.B. über Abstimmung)
		8. Architekturansätze erneut analysieren (Wiederholung von Schritt 6 anhand der aktualisierten Informationen)
		9. Ergebnisse präsentieren Zusammenfassung des Prozesses als Präsentation, evtl. ergänzt durch Textdokument

## Fehlerbehandlung in Architekturen
*   ein Fehler verhindert das korrekte Funktionieren eines Systems
*   SW-Architektur behandelt vor allem den Umgang mit Fehlern zur Laufzeit
*   Typische Schwerpunkte:
	*   Fehler identifizieren
	*   Fehler unterscheiden (fachlich/technisch), kategorisieren, reagieren
	*   Auswirkungen begrenzen
	*   Diagnose erleichtern (Was? Wo? Warum?)
	*   Technologien zur Fehlerbehandlung festlegen (Exceptions)
*   bis zu 80% des Programmcodes sind Routinen zur Fehlerbehandlung bzw. Ausnahmen
*   Fehlerarten: Bugs, fehlerhafte Eingaben, Infrastruktur (Festplatte voll, Rechte, Netz)
*   Mögliche Reaktionen:
	*   Abbruch der Operation
	*   Neustart des Systems
	*   Neutralisieren des Fehlers (Fortfahren mit Alternativweg oder Ignorieren)
*   fehlerhafte Eingaben sollten erwartet und behandelt werden, Bugs sind dagegen unerwartet
*   drei wesentliche Interessengruppen: Nutzer, Admin, Entwickler
*   Protokollierung unterscheidet
	*   **Tracing**: Nachvollziehen des Programmablaufs für Entwickler, möglichst mit Timestamp und Variableninhalt (Fehlersuche und Analyse)
	*   **Logging**: speichert Fehler und Systemzustände für Betrieb (frühzeitige Abstimmung), eigens definierte Fehlernummern kommunizieren (Beispiel: LinkedIn hat mehrere 100 Event-Typen)
*   beim Logging sollte jede Komponente einen Statusreport abgeben können
*   Logger sollte überall verfügbar sein und eines/mehrere Ziele (Konsole, Datei) haben
*   am besten eine einheitliche Library (z.B. log4j) verwenden
*   zwei Arten der Fehlerbehandlung:
	*   lokal: Klassen- und methodenspezifisch, führt oft zu Unmengen an Catch-Blocks (unübersichtlich, schlecht pflegbar, wenig nützlich)
	*   applikationsweit: jede Fehlermeldung wird gesammelt, globale Fehlerbehandlung
*   Es macht keinen Sinn, Bugs oder Infrastruktur-Fehler (unerwartete Exceptions) lokal abzufangen (hat Einfluß auf Funktion des gesamten Programms)
*   Erwartete Exceptions (z.B Failover auf andere DB) können natürlich lokal abgefangen werden
*   idealerweise werden unerwartete Fehler der Anwendungskomponente in erwartete Fehler der technischen Infrastruktur umgewandelt (z.B. ServerError)
*   Unterscheidung erwartet/unerwartet oft schwierig, Beispiel: fehlgeschlagene Authentifizierung (kann nicht nur beim Login passieren)
*   Validierungsfehler (Nutzereingabe) ebenfalls sammeln da oft mehrere Eingaben auf einer Seite
*   widerspricht dem Layers-Pattern (jede Klasse soll nur Fehler für sich selbst erzeugen), ist auch korrekt, aber Klassen oft sehr granular
*   Praxisbeispiel - LinkedIn nutzt Kafka als zentrale Logging-Engine (log-centric engine) und speichert damit bis zu 75TB pro Datacenter (bis zu 172.000 Messages/Sekunde)
*   Logging dann auch sinnvoll zur Erfassung von Benutzeraktivitäten in Echtzeit
*   Logging-Engine v.a. sinnvoll wenn mehrere Log-Quellen vorhanden sind
*   verteiltes Logging geht nur über Partitionierung (ähnlich wie bei DBs)
*   **High Level Catch Block:** quasi ein Catch-Block über allem (aber nicht für Exceptions mißbrauchen, die einen lokalen Bezug haben und wiederholbar sind)
*   Alternative: alle erwarteten Fehler in einer (projektspezifischen) Fehlerklasse implementieren werden (lokalisierbar, eigene fachliche Fehlernummern definierbar)
*   **Monitoring:** zur Problemanalyse, Nachweis NFAs, Nachweis SLAs, Nutzungsprofil
	*   Technisch: sammelt Daten auf Basis der technischen Artefakte und bereitet diese auf (Tools: InfraRed, Dynatrace, Tivoli), fachlicher Kontext wichtig (Bsp.: langsame Suche)
	*   Fachliche: sammelt Daten auf Basis der Anwendungsfälle (protokolliert auch Kontext)
*   zu erfassende Daten: Identifikation (z.B. Dialog-Name), ID, Host/IP, Parameter, Return-Werte, Laufzeit, Status, Startzeitpunkt, Timestamp
*   Daten sollten in Levels konfigurierbar sein und geordnet agreggiert/rotiert/gelöscht werden
*   Benutzerkennungen sind aus Datenschutzgründen zu anonymisieren
*   Zwei wesentliche Wege zum Speichern von Monitoring-Daten:
	*   Dateisystem: einfacher, schneller, nicht agreggiert, verteilt
	*   DB: SQL, konsolidiert, optimierbar, Performance-Overhead (beste Option für Cluster)
*   Meßpunkte im Code einbauen (z.B. Inund Output an Grenzen der Schicht/Komponente)
*   wichtig ist konsistentes Verfahren der Fehlerbehandlung in der gesamten Anwendung
*   in verteilten Systemen ist dies nur begrenzt anwendbar, Fehler sollten auf dem betroffenen System geloggt werden ( **Log at System Boundaries**)
*   in Hochverfügbarkeitsanwendungen sollten eher Annahmen getroffen als Fehler erzeugt werden (Fehler "sanft" abfangen, System sollte immer noch weitgehend funktionieren)
*   Beispiel: Fehler im Flugzeug (Funktionalitäten reduzieren, aber weiterfliegen)
*   Gegenteil: Embedded Systems (besser Programm anhalten als weitere Fehler zu erzeugen)
*   man unterscheidet verschiedene "Levels of Guarantee":
	*   Level 1 (Fundamental): Code ist stabil (definierter Zustand des Objekts), kann erneut aufgerufen werden, keine Ressourcen bleiben offen (Resource Leak) - jeder Produktiv-Code sollte dies erfüllen (Umsetzung z.B. über finally-Block)
	*   Level 2 (Basic): Wie Level 1, aber ein Objekt muß auch benutzbar sein (am leichtesten über zustandslose Komponenten realisierbar)
	*   Level 3 (Strong): Wie Level 2, aber ein Objekt muß im Fehlerfall reversibel sein (Rollback), am leichtesten mit unveränderlichen (immutable) Objekten realisierbar
	*   Level 4 (No-Throw): Wie Level 3, aber Objekt garantiert, dass es keinen Fehler erzeugt (quasi unmöglich, nur in systemnahen Teilen bzw. Embedded Systems denkbar)
*   jede Komponente sollte in ein Level eingestuft werden (Ausgangsbasis für Verbesserungen)
*   Fehler sollten sich möglichst von selbst dokumentieren, Exceptions dürfen nie "groß" sein
*   Exceptions sind tendenziell langsam, dennoch niemals weglassen (Robustheit eines Systems wesentlich wichtiger als die Performance, im Zweifel messen)
*   **Collection of Parameter**: Alternative zu Exception, Collection mit Fehlern wird als Parameter übergeben, bei einem Fehler werden in der Methode (neue) Fehler zur Collection hinzugefügt
*   Gut zur Sammlung von Fehlern, sehr gut für Validierung von Nutzerdaten geeignet

## Datenbanken und Persistenz

*   Grundregeln: so wenige Queries wie möglich, Datentypen klein wie möglich / groß wie nötig
*   im Wesentlichen drei DB-Typen:
	*   relational: Holt mittels PK eine Zeile in Tabelle und sucht darin den gewünschten Wert
	*   spaltenorientiert: Holt den Wert anhand von PK & Spaltenname in einem Schritt aus der Tabelle (schneller, da nur "Datenteile" geholt werden)
	*   Key/Value-Store: sehr einfach, simple Zuordnung Bezeichner/Wert (Voldemort, Redis)
*   relationale DBs sind tendenziell flexibel, aber Abfrage sind durch JOINs oft teuer
*   in anderen (dokumentenorientierten) DBs gibt es keine JOINs schnellere Abfragen
*   viele Features der RDBs in NoSQL nicht verfügbar (Beispiel: FK-Constraint)
*   DB-Verbindungen explizit verwenden (möglichst nicht als Parameter) & am Ende schließen
*   DB-Entwicklung nie isoliert betrachten, im selben Intervall wie die Anwendungslogik entwickeln (z.B. sechswöchige Iterationen, Platzhalterdaten verwenden)
*   **Transaktionen:** Sammlung von Arbeitsschritten, die das **ACID**-Theorem erfüllen sollten:
	*   Atomicity: T. ganz oder gar nicht ausführen
	*   Consistency: T. schafft Übergang von konsistenten in einen konsistenten Zustand
	*   Isolation: Keine gegenseitige Beeinflussung der T.
	*   Durability: Zustand bleibt dauerhaft in DB
*   ACID v.a. für lokale Systeme anwendbar, für verteilte Anwendungen eher **BASE**:
	*   basically available: funktioniert scheinbar immer (Ausfallsicherheit)
	*   soft state: Nicht immer konsistent (evtl. aber auch nicht-persistierte Daten wiederherstellbar)
	*   eventually consistent: Konsistenz wird irgendwann erreicht
*   **CAP-Theorem:** nur 2 von 3 Kriterien sind in verteilten Systemen möglich
	*   Konsistenz (Consistency): Daten in (verteilten) Systemen sind konsistent, d.h. bei Aktualisierungen sind alle Datensätze auf allen Systemen aktuell
	*   Verfügbarkeit (Availability): Antwortzeiten sind auch bei Lastspitzen möglichst gering
	*   Stabilität (Partition Tolerance): bei Ausfall eines Servers läuft der Rest sauber weiter
*   relationale DBs sind in der Regel CA oder CP, NoSQL dagegen eher AP
*   Strategien: Alles auf eine Maschine (P), oder warte bis alle Daten synchron sind (C und A)
*   große (Web-)Anbieter verzichten am ehesten auf C (kompletter/teilweiser Verzicht auf Konsistenz oder Implementierung auf Anwendungsebene)
*   **Datenmodell:** Menge aller Entitätstypen eines Systems und deren Beziehungen, sollte korrekt, einfach, erweiterbar und redundanzfrei sein (Faustregel: 3. Normalform genügt)
	1. Normalform: Kein Wert sollte in weitere sinnvolle Teilbereiche aufgeteilt werden können (Bsp. 1 Feld „Adresse“ würde Straße, Hausnummer und PLZ speichern)
	2. NF: wie 1. NF, weiterhin ist jedes Attribut (wenn es kein PK ist) dann von allen funktionalen Schlüsseln abhängig (Unique PK für jede Zeile, Fremdbeziehung über FK)
	3. NF: wie 2. NF, weiterhin muß jedes mehrfach auftretende Attribut durch einen PK ersetzt werden (Bsp.: Künstler, Album, Albumtitel mit PK aber nicht der Songtitel)
*   Vererbung möglichst nicht verwenden (ggf. durch Assoziationen/Kompositionen ersetzen)
*   Einfache Implementierung: jede Tabelle hat eine Klasse (vgl**. Table Module**/**Gateway**)
*   Relationale DBs sind gut bei maximal einigen hundert Tabellen mit möglichst kurzen Transaktionen (weniger als 1 Stunde)
*   Bei Many-to-many-Beziehungen verwendet man eine eigene Assoziationstabelle zur Verknüpfung der Daten (vgl. **Association Table Mapping**)
*   Beziehungs-Abhängigkeiten aus Performancegründen möglichst klein halten
*   Datentypen für Indizes besonders sorgfältig wählen (Geschwindigkeit, Plattenplatz)
*   Indizes eignen sich besonders für Tabellen von denen viel gelesen wird (dann auf die Felder legen welche mit WHERE-Bedingungen abgefragt werden), bei häufigen Schreibzugriffen können sie dagegen sogar bremsen (mögl. Ausweg: parallele Hints)
*   in RDBMS ist Pflege der Indizes ein Problem: bei Tabellen mit mehreren Millionen Einträgen dauert sowohl das Anlegen als auch das Entfernen (!) von Indizes oft mehrere Stunden (Downtime) - oft werden daher "kreative" Lösungen gefunden, das Gleiche gilt für Schema-Änderungen
*   Lösung kann dann oft ein Key/Value-Store sein (vgl. Friendfeed "bag of words")
*   Effektivität von Queries über EXPLAIN SELECT prüfen
*   Kein SELECT * verwenden und beim Mapping die Spalten benennen (keine Integer-Offsets - schlecht wartbar)
*   String-Concatenation für Queries schlecht, alternativ Prepared Statements / Stored Procedures
*   generell ist eine Abfrage mit vielen auch (womöglich) nicht nötigen Informationen besser als mehrere Abfragen mit exakten Filtern (=komplexe Queries)
*   zur Optimierung sollten über einige Zeit alle Queries von der DB gelogged werden (leichte Erkennung häufiger Operationen)
*   Abfragen, die Ergebnisreihen sortieren sind generell teurer als unsortierte SELECTs
*   DBs sind auf maximal 3-4 JOINs/Query optimiert
*   Maps sollten als Datenspeicher vermieden werden, stattdessen explizite DTOs verwenden
*   Connection Pooling: parallel geöffnete Verbindungen, die bei Queries benutzt und anschließend direkt freigegeben werden (sehr effizient)
*   **Temporalität**: Fachlich begrenzte zeitliche Gültigkeit einzelner Datensätze, Abbildung in RDBMS nicht einfach
*   Beziehung ist dann nicht mehr 1:1 (z.B. eine Person > eine Adresse) sondern 1:n, Gültigkeit muss dann aber eindeutig sein (also nicht mehrere Adressen in einem Zeitraum - dies wäre dann Bitemporalität)
*   Manchmal muss auch ermittelt werden können, welchen Stand ein Datensatz an einem beliebigen Datum hatte (Audit - also nicht die eigentliche Gültigkeit sondern der aktuelle Datensatz z.B. am 12.04.2003)
*   hilfreiche Frameworks z.B. DAOFusion, Hibernate Envers, Spring Data
*   Vollständige Isolation von Transaktionen kaum machbar, daher verschiedene Stufen:
	*   Serializable: erneute Ausführung bringt dasselbe Ergebnis (höchste Isolationsebene)
	*   Repeatable Read: Gleiche Abfragen haben immer das gleiche Ergebnis, u.U. können Phantome auftreten (nicht alle neuen Daten direkt sichtbar)
	*   Read Committed: neue Daten werden nach Commit sichtbar (die meisten kommerziellen DBs verwenden dies)
	*   Dirty Reads/Read Uncommited: nicht-festgeschrieben Daten werden u.U. gelesen
*   Daher typische Probleme:
	*   zwei T. modifizieren denselben Datensatz, nur die letzte Änderung wird übernommen
	*   Daten von nicht abgeschlossenen T. werden gelesen
	*   Gleiche Lesevorgänge liefern zu verschiedenen Zeitpunkten verschiedene Ergebnisse
*   aktuelle DBs sind auf kurze Transaktionen optimiert (möglichst immer nur 1 Request)
*   T. können fachlich (Anwendung ist Transaktionsressource, z.B. Überweisung) oder technisch (Sicht aus der Implementierung heraus, nur vom Server) sein
*   **Late Transaction:** für komplexe T., sammelt alle Schritte und führt diese gebündelt aus
*   Alternative 1: Daten in lokalen Puffer speichern und in parallelem Thread schreiben
*   Alternative 2: Offline Concurrency (Aufteilung von Transaktionen in einzelne Schritte)
*   **Eventual Consistency**: in einem verteilten System wird ein Update auf einem Node erst nach und nach auf anderen Nodes nachgezogen
*   **Consistent Hashing**: Daten werden partitioniert (Sharding), jede Partition wird einem Node zugewiesen wobei jeder Node zu jeder ID befragt werden kann (verweist ggf. weiter)
*   **Hash Node-Verfahren**: Segmentierung anhand eines Kreises, bei Ausfall eines Knotens wird nur dieses Segment neu verteilt (Ring), Ansatz eignet sich auch gut für spaltenorientierte DBs
*   wenn der Knoten wieder verfügbar ist wird das Delta automatisch übertragen
*   Sicherung der Partitionen kann meist konfiguriert werden (P. wird zwecks Ausfallsicherheit auf mehreren Knoten gespeichert), dadurch skaliert die DB weitgehend beliebig
*   **NoSQL:** alternative Datenbanken ohne relationales Datenmodell, dynamische Queries (also SQL) sind kaum vorgesehen (es muß immer eine Art View berechnet werden), Unterstützung für Transaktionen oft nicht gegeben, komplexe Relationen über SQL (naturgemäß) besser abbildbar
*   Keine Standard-Abfragesprache, Datenformat oft JSON, wenige grafische Tools (NoSQL wg. Anleihen bei OOP für Entwickler gut zugänglich, SQL eher für Analysten)
*   Skalierung & Parallelverarbeitung tendenziell besser als bei relationalen DBs, oft kostenfrei
*   erlauben massive Skalierung (Terabyte+), meist schnelle Schreibvorgänge, flexible Schemen und Datentypen
*   Wesentliche NoSQL-Vertreter:
    *   Redis: beherrscht neben Key/Value auch Listen, schnell (>30.000 Reads/Writes pro Sekunde ohne Optimierung auf billigem Laptop), alle Daten im Hauptspeicher, alle Operationen atomar, besonders gut für Statistiken und History geeignet
    *   Gut für Echtzeit-Statistiken, Publish/Subscribe, Tag-Clouds aber auch für Locking, Zustandsverwaltung zwischen Prozessen, Zufallsauswahl, A/B-Tests oder inkrementelle Counter einsetzbar
    *   MongoDB (dokumententorientiert): zusammengehörige Daten werden in beliebiger Struktur gespeichert, keine referenzielle Integrität, Indizes möglich, SQL-ähnliche Abfragesprache, gut dokumentiert
    *   CouchDB: reines HTTP (gutes Caching), Dokumente haben eine Revisionsnummer und werden in einzelne Zweige verteilt, neue Daten werden immer nur angehangen, Daten stets auf der Festplatte (gut replizierbar), sehr universal aber in Erlang geschrieben
*   Einsatzszenarien:
    *   große Datenmengen ohne Transaktionen (alle Arten von Logs, Nutzerinteraktionen)
    *   schnelle Reaktionszeiten auch bei massiver Last (v.a. InMemory-Systeme
    *   Archivierung (bes. bei Dokumenten gut möglich, da keine Schema-Änderung notwendig)
    *   Echtzeit-Inserts, Updates, Queries (auch MapReduce)
    *   hierarchische Daten (Diskussionen, soziale Netze)
    *   Voting, Echtzeit-Counter (z.B. Anzahl aktiver Nutzer)
    *   Nutzerdaten, Profile, Session-Daten
    *   Embedded Systems (wenig Overhead, schlank, schnell)
*   es macht durchaus Sinn, verschiedene NoSQL-DBs für verschiedene Zwecke einzusetzen
*   NoSQL-DBs können MapReduce (z.B. MongoDB), dedizierte Systeme wie Hadoop aber flexibler (alle möglichen Datenquellen)
*   Mögliche MapReduce-Jobs:
    *   Wie viele Requests pro Tag oder auch Stunde, wie viele Suchabfragen
    *   Verhältnis erfolgreicher Antworten zu Fehlern (z.B. 404)
    *   Ermittlung der durchschnittlichen Latenz
    *   Anzahl der unique user, geografische Verteilung
    *   Einsatz welcher Clients (Desktop / mobil / App / API / Partner)
    *   Erkennung von Duplikaten im (gesamten) Datenbestand
    *   Eingabekorrekturen für Suche, Suchvorschläge (z.B. für Autocomplete)

## Polyglot Persistence

*   Mongo ist "made to scale", für eine erste Version eines Projekts super geeignet (ähnlich SQL aber mit NoSQL-Vorteilen), Migration auf andere DB-Engine gut machbar
*   größere Anwendungen nutzen bzw. werden mehrere DB-Engines nutzen (Hauptgrund: verschiedene Anwendungsszenarien)
*   gleichzeitig steigt der Aufwand für Infrastruktur - alternativlos (Big Data), Betrieb wird z.B. durch Cloud Provider wiederum leichter (Speicherplatz und Rechenleistung einfach verfügbar)
*   Aber: Zuverlässigkeit von Cloud-Systemen meist eher mäßig (AWS), bei großer Last teurer und vor allem erheblich langsamer als eigene Hardware doch die gewonnene Flexibilität allein gleicht dies oft aus
*   Kosten bei Cloud-Services bestehen im Wesentlichen aus Gebühr für Instanz, Datenspeicher und der genutzten Bandbreite (Out)
*   Daten sollten unbedingt regelmäßig in-house gesichert werden (Cron-Job), Monitoring-System für die Instanzen macht oft Sinn (sonst schnell unübersichtlich - was läuft wo und mit welcher Last?)
*   Nutzer rufen sehr teure Queries auf, die aber zahlenmäßig überschaubar sind - dann Query-Ergebnisse in Redis/Memcache zwischenspeichern (Cache)
*   wesentliche Punkte bei Auswahl der DB-Engine: Rechtliche Fragen, Kosten, Community und/oder (kommerzieller) Support, typische Abfrage-Patterns, Mengengerüst für Abfragen und Speichern bzw. Backup, Verschlüsselung, Fehlertoleranz, Monitoring
*   wichtig sind auch die zu verwendenden Programmiersprachen - Beispiel: Wahl zwischen HBase und Cassandra, Entscheidung für Cassandra wg. hervorragendem Python-Treiber, node.js-Treiber dagegen schlecht (damals)
*   Einfaches Beispiel für ein Abfrage-Pattern: Rufe alle Produkte auf, filtere daraus die mit roter Farbe - kommt dies häufig vor? Wie ist die Performance?
*   Weg des Datenimports ebenfalls sehr wichtig (Batch/Agreggierung/Verfügbarkeit wann)
*   generell fällt es Start-Ups leichter, Technologien zu wechseln (wenig Legacy-Code)
*   Zugriff auf mehrere (interne) DBs gut über (interne) API machbar, die sich im Hintergrund an die korrekte DB wenden - dies funktioniert sehr gut für READs, bei WRITEs dagegen doch starke Verzögerungen
*   gut für Protokollierung: Hash der Abfrage bilden, zusammen mit der Ausführungszeit in eigener Logging-Tabelle speichern, dies analysieren
*   auf diese Art können Veränderungen auch gut simuliert werden: zunächst werden alle Operationen an zwei Rechner geschickt und anschließend die Logs verglichen / somit gibt es keine Downtime, es muß ja am Ende nur ein Rechner entfernt werden
*   Schema-Migrationen können ebenfalls gut unter API "versteckt" werden
*   Konsistenz zwischen verschiedenen DB-Engines schwierig - ein Ausweg sind Skripte und Tests zum Vergleich der Datenkonsistenz, visuelle Ausgabe wichtig (Charts)
*   alle Daten sollten notfalls von einer "Master-Instanz" einer Engine wiederherstellbar sein (diese Engine muß verteilt und fehlertolerant sein, parallele Read/Writes müssen sehr performant sein)

## Parallelität, Performance und verteilte Architekturen

*   Drei Basis-Level für verteilte Systeme:
	*   Ad Hoc: interne Prozesse (IPCs) kommunizieren über Sockets, Pipes & Speicher
	*   Structured Communication: kapselt Hardware-Ebene und macht diese in Anwendungslogik verfügbar (RPC-Calls)
	*   Middleware: integriert Legacyund eigene Komponenten, ermöglicht flexibles Deployment, freie Platzierung/Austausch von Systemteilen
*   Middleware tendenziell immer zu bevorzugen, ist aber nur "Postbote"
*   Netzwerk- und Serverausfälle müssen abgefangen werden
*   Messung Datendurchsatz: Menge (Bytes/sec) oder (DB-)Transaktionen (Transactions/sec)
*   Grundatz: Computer lesen und schreiben Daten - für die Performance ist also entscheidend, wie viele Daten verschoben werden müssen und wohin
*   Generell sollten nur möglichst viele, aber natürlich nur relevante Punkte in einem System dauerhaft gemessen werden (also nicht pauschal jedes SELECT), sonst unübersichtlich und nicht zweckmäßig
*   Jegliche Optimierung muss klar aussagen, auf welche Ressource sie sich bezieht, welche Stellen optimiert werden sollen und welches Ergebnis erwartet wird (Grundlage: Messungen)
*   "Beiläufige" Performanceverbesserungen (also unerwartete) kritisch betrachten - vielleicht ist einfach nur die Fehlerrate angestiegen oder ein Service/Feature funktioniert nicht mehr oder es werden keine Daten mehr zurückgegeben
*   Parallelisierung v.a. getrieben durch Anforderungen an Skalierung und Performance
*   früher war CPU viel schneller als I/O (Grundlage für Multi-Tasking, quasi virtuelle Parallelität)
*   Parallelisierung durch mehrere Threads aktueller CPUs (Faustregel für Obergrenze: 12)
*   P. bei langen Transaktionen und GUI-basierten Systemen quasi Pflicht, Risiken:
    *   Datenverlust
    *   Inkonsistenzen: mehrere Threads bearbeiten dieselben Daten (Race Condition)
    *   Deadlocks: Thread löst einen Lock nicht (Anwendungslogik, Workaround: Timeout)
*   Die Art des Locking sollte über Interface gesetzt werden können/austauschbar sein (**Strategy**)
*   Entscheidung für ein Locking anhand der Anforderungen an Parallelität, Anwendungslogik und Code-Komplexität
*   Lock Manager verwaltet die einmal festgelegten Locks, sollte nicht mehr als eine Map mit PKs (betroffene Datensätze) und Nutzern sein
*   Lock Manager kann z.B. über **Singleton** realisiert werden (in Cluster-Anwendungen aber besser in der DB)
*   Anwendungslogik arbeitet nur mit dem Lock Manager, nie mit dem (gesperrten) Objekt selbst
*   Locks müssen nach Abschluß der Transaktion freigegeben werden
*   Locks sollten gesetzt werden bevor der Nutzer die Datensätze bearbeitet
*   **Deadlock**:
	*   Zwei Nutzer brauchen sowohl A als auch B
	*   Nutzer 1 sperrt A
	*   Nutzer 2 sperrt B
	*   Beide warten nun (ewig) auf das jeweils andere Objekt A oder B.
*   Grundproblem: Locks werden gern vergessen, führt zu schwer nachvollziehbaren Fehlern
*   Tool für verbesserte statische Analyse von Concurrency-Issues: ThreadSafe (Java)
*   Locks müssen systemweit gesetzt/freigegeben und bekannt sein, dafür bietet der **Implicit Lock** einen einheitlichen Anlaufpunkt (vgl. zu **Identity Map**)
*   Ansonsten sind Timeouts wichtig, viele Application Server unterstützen das direkt
*   Alternative: Timestamp beim Locking
*   Synchronisierung der Prozesse nach dem Ende der Parallelverarbeitung z.B. über **Critical** **Section** (abschließender Prozess, der die Ergebnisse aller Prozesse zusammenträgt)
*   Event-getriebene Anwendungen haben sehr viele parallele Prozesse, datengetriebene Anwendungen arbeiten dagegen eher mit Batches
*   eine Session sollte in einem eigenen Prozeß laufen (skalierbar, robust)
*   Ansatz von Enterprise Java Beans: Isolierte Datenbereiche für jeden Thread
*   Java-Methoden/Variablen sind mit "synchronized" in allen Threads gleich, Gegenteil: "volatile"
*   jede Session sollte alle Objekte "frisch" erstellen und nicht übernehmen (bessere Skalierbarkeit, Vermeidung von Parallelitäts-Fehlern)
*   für einen "globalen" Speicher eignet sich das Registry-Pattern, Singletons und statische Variablen (müssen synchron sein) dagegen nicht
*   Queues sind immer gut, wenn Prozesse entkoppelt werden sollen, führen aber oft zu Speicherproblemen und erhöhen Latenz und Jitter
*   Viele Patterns mit Fokus auf Parallelität:
	*   **Semaphores:** geschützte Variablen zur Synchronisierung mehrerer Threads, auch Mutex/Lock, Lock kann von jedem Thread gesetzt/gelöst werden
	*   **Half Sync/Half Async**: synchrone & asynchrone Funktionen werden gemischt und müssen koordiniert werden (Entkopplung über Queueing Layer, oft Message Queue), skaliert sehr gut
	*   **Leader/Follower:** Verarbeitung von (parallelen) Events aus verschiedenen Quellen, oft über Pool (Haupt-Thread vergibt Aufgaben an untergeordnete Threads), nur für kurze und wiederholbare Aktionen, skaliert nicht gut
	*   **Active Object**: kapseln Threads in eigener Komponente, sammeln eingehende Requests und Ergebnisse in Queue (Request startet nicht direkt neuen Thread)
	*   **Future Object**: Active Object generiert Platzhalter für das Ergebnis, der dann nach der Verarbeitung gefüllt wird (blockiert weitere Verarbeitung nicht)
	*   **Optimistic Offline Lock:** Erkennt Datenkonflikt beim Schreiben und macht alle Änderungen rückgängig (sinnvoll, wenn Konflikt unwahrscheinlich)
*   Schlimmster Fall: Nutzer ändert Daten in einem epischen Formular, erst am Ende wird erkannt, dass bereits ein anderer Nutzer aktiv war
*   Implementierung oft über Versionsnummer (kein Timestamp – zu ungenau) im Datensatz, beim Commit wird Version der Session mit DB-Version verglichen
*   Versionsnummer muß bei jedem UPDATE oder DELETE aktualisiert werden aber auch bei manchen Lesezugriffen (Beispiel: Steuerberechnung für Kunde, ein Satz pro Bundesland Berechnung evtl. falsch, wenn Adressdaten geändert)
*   leichter zu implementieren als pessimistisches Locking und weniger fehleranfällig
*   **Pessimistic Offline Lock:** Datensatz steht nur einem Prozess zur gleichen Zeit zur Verfügung (sinnvoll, wenn Konflikt sehr wahrscheinlich und Transaktion nicht in einem Schritt abzuwickeln)
*   einfache Implementierung: Lock erhalten, wenn eine Zeile in eine Tabelle eingefügt werden kann / Lock abgeben beim Löschen einer Zeile
*   **Write Lock**: sperrt Datensatz beim Bearbeiten von Daten (simpel, führt aber schnell zu veralteten Daten beim Lesen)
*   **Read Lock**: Transaktion sperrt Datensatz beim Lesen, schlecht für die Parallelität (quasi unmöglich), Daten sind aber immer aktuell
*   **Read/Write Lock**: Datensatz kann nicht gesperrt werden, wenn ein anderer Prozeß einen Leseschutz auf dem Datensatz gesetzt hat und umgekehrt (beste Lösung), gleichzeitige Read Locks werden dabei akzeptiert (verhindert Schreibvorgänge)
*   **Condition Variable**: Lock wird z.B. nicht gesetzt, solange eine Bedingung nicht erfüllt ist (**Monitor Object**, das thread-übergreifend funktioniert)
*   **Temporal Reads**: Daten werden mit einem Timestamp oder einer anderen unveränderlichen Information ergänzt (Protokoll der Änderungen)
*   **Coarse-Grained Lock:** Sperrt zusammenhängende Objekte in einem Lock (nur bei Abhängigkeiten sinnvoll z.B. mehrere Adressen eines Kunden)
*   zusammengehörige Objekte sollten dieselbe Version haben, Versionsnummer wird erhöht & Gruppe gesperrt, Zugang nur über ein Root-Element (z.B. **Repository**, erleichtert das Setzen/Entfernen von Locks)
*   **Implicit Lock:** ermöglicht Locking für Frameworks/übergeordneten Code
*   **Double Checked Locking:** Hilfreich für parallelisierbares Singleton, vemeidet ein pauschal teures "synchronized"
*   **Scoped Locking**: Kapselt den Lock in Konstruktor und den Release in Destruktor
*   **Guarded Suspension**: Thread darf zu einem Zeitpunkt X auf eine Methode zugreifen, andere Threads werden nicht geblockt sondern verzögert ausgeführt
*   **Thread-Safe Interface**: Interface-Methoden setzen zuerst Lock, führen Operationen aus und lösen den Lock (in Java z.B. über Proxy oder abstrakte Klassen)
*   **Counting Handle**: Einziger Zugriffsweg zu Objekt/Ressource, leitet Zugriffe weiter, speichert die Anzahl der (parallelen) Zugriffe und schließt ggf. die Ressource
*   **Reactor**: Wartet auf mehrere Prozesse bzw. löst Prozesse aus einzelnem Thread heraus aus, nicht unbedingt performant (1 Thread blockiert alles), genügt aber für kleinere Systeme, wird oft in Kombination mit Pool oder Leader/Follower genutzt
*   **Proactor**: asynchrone I/O zur Parallelverarbeitung von Events, sehr effizient aber auch kompliziert (für größere Systeme), gut für langwierige Operationen
*   **Verteilung:** wenn möglich immer vermeiden, Alternative: Clustering
*   Sehr schnell: ein Aufruf in einem Prozess
*   Langsam: ein Aufruf zwischen verschiedenen Prozessen
*   Quälend langsam: ein Aufruf auf entfernter Maschine
*   Entfernte Objekte sind meist aufwändig (Erstellen, Zerstören, Finden, Aufrufen, Referenzen auflösen, Garbage Collection)
*   **Broker:** verteilte Komponenten können sich finden und aufeinander zugreifen als wären sie auf einem einzelnen System (Bsp.: Corba, Java RMI, .NET Remoting)
*   alle Dienste müssen sich beim Broker registrieren, werden über Service Interface aufgerufen
*   separiert die Kommunikation (ein Broker pro Knoten)
*   Zugriff auf einen Client sollte nicht direkt via Host/IP sondern über ein Client Proxy-Objekt erfolgen (vgl. Fassade/Gateway)
*   Broker tendiert zu enger Kopplung der Komponenten nicht unbedingt empfehlenswert, daher werden nun eher Message-basierte Systeme bevorzugt
*   oft haben nur wenige Teile eines Systems besondere Verfügbarkeitsund Fehlertoleranz-Anforderungen, dafür braucht es nicht zwingend ein Backup-System
*   Lösung: **Replicated Component Group**, d.h. kritische Komponenten auf mehreren Knoten einspielen (erhöht Koordinationsaufwand, da Zustand immer gleich sein muß)
*   evtl. macht es wg. der Performance Sinn, Objekte "aufzuteilen"
*   alles, was nicht lokal ausgeführt werden kann in eigenes Objekt packen, Rest läuft lokal
*   Web und Application Server sollten ruhig in einem gemeinsamen Prozeß laufen
*   XML-basierter Datentransfer (SOAP) weitgehend standardisiert, flexibel (zwischen mehreren Systemen) und gut lesbar, Remote API aber u.U. spürbar schneller
*   Web Services sollten asynchron und nachrichtenbasiert sein, übertragene Datenmenge möglichst klein halten (im Zweifel den Server mehr belasten als häufigere Abfragen schicken)
*   verschiedene (synchrone/asynchrone) Kommunikationsarten in verteilten Systemen:
	*   RPC / RMI (Remote Methode Invocation)
	*   Broadcast (gut für Infos über Dienste/dynamische Interaktionen)
	*   Publish/Sunscribe (gut über Systemgrenzen hinaus & bei Änderungen der technischen Infrastruktur)
*   asynchron gut für Performance sowie falls nicht alle Systeme immer online/verfügbar sind sowie bei manueller Nachbearbeitung der Daten
*   relevant sind weiterhin vor allem Protokoll und Encodierung
*   idealerweise skaliert ein System proportional zu den hinzugefügten Ressourcen (wird in der Praxis nie erreicht)
*   Typische Flaschenhälse:
    *   Datenbank, Caching
    *   I/O (Betriebssystem, Dateisystem)
    *   Arbeitsspeicher, RAID
*   Messungen auf Nicht-Produktionssystemen sind oft Muster ohne Wert (Mengengerüst - Hardware - Netzanbindung)
*   Stabilität und verläßliche Performance zeigt sich in der Praxis vor allem durch geringe Abweichungen von den Mittelwerten (Ziel)
*   Live-Auslastung lässt sich z.B. mit einer Teilmenge der Live-Server testen, diese stetig mehr auslasten bis sie am definierten Maximum sind - bleibt alles stabil?
*   funktioniert auch für Releases - diese zunächst auf einigen Instanzen deployen und dann die Lastwerte mit den anderen Instanzen vergleichen - Abweichungen? Muster?
*   dabei Aktualisierung der DNS-Server beachten - dauert oft N Minuten (üblicherweise nach N Minuten ca. 50% des Traffic, 2N ca. 75%, 3N ca. 98% usw.)
*   Ein allgemein einsehbares Dashboard hilft bei der Überwachung, dabei Anzahl der Charts reduzieren (Bsp. OP-Saal: alle Kennzahlen des Menschen lassen sich mit zehn Metriken darstellen), ggf. Schwellwerte für Alarm definieren
*   Auf dem Dashboard können z.B. folgende Metriken angezeigt werden: Fehlerrate, Latenzen (auch gemittelt), Netzwerk Ein- und Ausgang (Bytes), Requests/Sekunde, aktive Nutzer, aktive Server, Serverauslastung (CPU, RAM, I/O), DB-Queries, Cache Hit/Miss-Ratio
*   jede Messung (idealerweise jeder gemessene Request) sollte folgende Metadaten enthalten: Timestamp, Servername, Build, Statuscode, A/B-Test (sofern vorhanden), Nutzer-ID (sofern vorhanden), Ziel
*   das "Ziel" ist nur weich definiert, das kann ein Skript sei oder der Controller bei MVC oder der Pfad in der URL oder die API-Methode oder ...
*   die Nutzdaten einer Messung sind z.B. folgende: allgemeine Ausführungsdauer (z.B. gemessen vom Ausführungsbeginn in der Methode bis zur Rückgabe des Ergebnis), CPU-Ausführungsdauer, Speicherauslastung, ausgehende Bytes, DB-Zähler, eingehende Bytes DB, DB-Ausführungszeit, Cache-Count, Cache Hit oder Miss
*   sinnvolle Messungen für Web-Performance z.B. Anzahl Requests, langsamste Response, Median Response, Anzahl Redirects, time to first/last byte, cache hits/misses, Requests pro Domain, global variables, ...
*   (automatisierte) Ermittlung dieser Werte z.B. über Phantomas oder PageSpeed
*   viele Kennzahlen müssen nicht Millisekunden-genau sein - manchmal genügt z.B. der Mittelwert der CPU-Last in einer Minute
*   Für den Beginn ist es meist ausreichend, alle Daten in einer einzigen Tabelle des jeweiligen Systems zu speichern (Queries einfach und schnell, keine Abhängigkeiten) - mittelfristig Aufteilung Metadaten / Nutzdaten natürlich sinnvoll
*   Rohdaten wenn möglich niemals löschen (wer weiß, was wann mal gefragt wird...), in der DB aber nur die Daten der letzten Wochen/Monate sichern (wird sonst zu schnell zu langsam)
*   DB mit Performance-Daten muss Grundfunktionen (Aggregationen z.B. Count/Average/Sum/Deviation/Percentile) beherrschen, die für Auswertung wichtig sind
*   Performance immer auch unter Kosten/Nutzen-Aspekt betrachten, es gibt (wie z.B. auch bei Sicherheit und Testen) auch ein "zu viel", effektiv vor allem bei "gewachsenen" Systemen deren Architektur sich nicht (mehr) so häufig ändert
*   Performance ist kein Selbstzweck, sollte auch nie wichtiger als Sicherheit sein
*   SSDs sollten nicht als teure Festplatten sondern eher als billiger Arbeitsspeicher gesehen werden
*   Hardware ist generell eher "billig", wogegen Personal teuer ist
*   Widerspruch "Datensparsamkeit" (Speichere nur, was nötig ist, auch wg. Privatsphäre) und "Store first, ask questions later" wo erstmal alles persistiert wird (Kosten gering, zukünftige Fragen nicht absehbar)
*   DB-Caching leicht zu implementieren, Caching der Anwendungslogik flexibler aber komplexer, InMemory-Cache bei ausreichend RAM eigentlich immer zu empfehlen
*   immer bedenken, dass es auch einen Weg geben muss den Cache zu invalidieren
*   immer davon ausgehen das alles/vieles ausfällt (everything fails in its own way, daher schnelle Wiederherstellung, selbständige Konfiguration)
*   viele etablierte Technologien (.NET/EJB) skalieren hinsichtlich (sehr) großer (Web-) Projekte schlecht, sind tendenziell langsam & teuer
*   Faustregel für gute Architektur: Wachstum kann bewältigt werden indem man einfach mehr von dem bestehenden hinzufügt (Hardware)
*   Beispiele für Stacks verteilter Web-Architekturen aus der Praxis (Stand 2011/2013):
    *   **Youtube**
        *   Stack: Apache, Python, mySQL, lighttpd (für Videoauslieferung, da Apche zu viel Overhead)
        *   Apache läuft mit mod-Fast_cgi, C extensions für komplexe Algorithmen (z.B. Verschlüsselung)
        *   NetScaler zur Lastverteilung und Cache statischer Inhalte
        *   populärste Inhalte werden von CDN ausgeliefert, dort dann meist aus RAM
        *   Lesen und Scheiben auf verschiedenen Systemen (vgl. flickr)
        *   Thumbnails waren sehr herausfordernd (kleine Files, viele disk seeks), problematisches Verzeichnislimit (Ext3)
        *   durch die Vielzahl an Bildern verzögerte sich sogar das Booten neuer Machinen, Lösung durch BigTable (mehrere Bilder werden in einer "Datei" zusammengefaßt und in DB gespeichert, quasi ein verteilter Cache)
        *   Traffic-Priorisierung entsprechend des Geschäfts - Video ist die Hauptfunktion, dafür also die meisten Ressourcen / Sharing weniger wichtig, kann auf "langsameren" Clustern laufen
    *   **Pinterest**
        *   viele Technologien ausprobiert, etabliert haben sich MySQL, Solr, Memcache und Redis
        *   Cassandra und MongoDB wurden dagegen verworfen
        *   Stack: EC2, S3, 180 web engines, 240 API engines, 88 MySQL DBs, 110 Redis-Instanzen, 200 Memcache-Instanzen, geshardeter Solr
        *   Amazon recht zuverlässig mit gutem Reporting & Support, leichte Kapazitätsplanung aber teils eingeschränkte Flexibilität (SSDs)
        *   MySQL sehr zuverlässig, kein Datenverlust, guter Software-Support (XtraBackup, Innotop, Maatkit)
        *   Memcache sehr ausgereift, einfach, schnell, nie abgestürzt
        *   Redis kann Persistenz und Replikation, dabei sehr flexibel (z.B. Drei-Stunden-Persistenz)
        *   Solr funktioniert out-of-the-box, skaliert aber nicht, Elastic Search hatte probleme mit kleinen Dokumenten und vielen parallelen Queries
        *   Cluster hat keinen SPOF, aber kompliziert, wenig Community-Support, Updates schwierig, es kam oft zu Datenverlusten
        *   Cluster-Manager wiederum ist SPOF, wenig Möglichkeiten bei ungleichmäßigem Balancing und Datenverlusten
        *   Sharding: mehr Aufwand, manuelle Datenverteilung, aber gut vorhersehbar, unterstützt Trabsaktionen nicht, Constraints und Joins müssen auf Anwendungsebene geprüft(ausgeführt) werden, Daten "wandern" nicht mehr zwischen DBs wie im Cluster
        *   eigener Algorithus zur Datenverteilung ist SPOF, aber leicht verständlich (wenig Code), neue Nutzer werden zufällig auf Shards verteilt, jeder Shard hat alle Tabellen
        *   massives Caching aller DB-Queries
        *   jede Anwendung hat Konfigurationsdatei mit dem Mapping eines Shards zum virtuellen Host (dabei einfaches Namensschema)
        *   kein Sharding der Benutzertabelle
        *   Migration: Alle Writes auf beiden Infrastrukturen, allein die Datenmigration dauerte fünf Monate
        *   System eher einfch halten (Daten im RAM speichern, periodisch persistieren), bei Crash sind einige Daten weg, aber dies ist nicht so schlimm und vereinfacht die Architektur drastisch
    *   **Salesforce**
        *   täglich über 1,3 Milliarden Transaktionen, 24000 / Sekunde, mehr als 15000 Maschinen, 17 Instanzen in Nordamerika, 4 in EMEA, 2 APAC
        *   Stack: Linux für Dev und Produktion, Solaris mit ZFS, Jetty (vorher Resin), Solr, Memcache, Puppet, Perl und Python
        *   jeder Server mit eigener JVM und 14 GB RAM
        *   sehr DB-lastig, daher Entwicklung eines eigenen Cursor-Managers bzw. Cache (ACS)
        *   Suche läuft auf Linux-Maschinen mit SSDs, Index wird auf diesem gespeichert, QFS dateisystem erlaubt einzelnen Schreib- und mehrere parallele Lesevorgänge
        *   Binärdaten in eigenem Storage ähnlich S3, BLOBs < 32 kB bleiben in DB
        *   Einführung von Solr geplant bzw. bereits erfolgt
    *   **Twitter**
        *   Stack: Cassandra, Memcached, Netty, node.js (vermehrt anstelle von Ruby on Rails), Python, Drupal, Lucene, Hadoop
        *   über 150 Millionen Nutzer, Outstream von etwa 22 Mbyte/s, 400 Milliionen Tweets / Tag
        *   über 300.000 Lese- und nur 6.000 Schreibzugriffe pro Sekunde
        *   dadurch ein schreiblastiger Ansatz: Anwendungslogik wird beim Write ausgeführt (z.B. wohin die Tweets gehen sollen), keinerlei Berechnungen bei Lesezugriffen
        *   konkret: Neuer Tweet geschrieben, System schaut bei allen Followern nach und persistiert die Tweet-ID in deren Timeline (viele INSERTs)
        *   jeder Tweet wird drei Mal auf drei verschiedenen Maschinen repliziert (da täglich hohe Ausfallraten), Timeline der User selbst wird gecached

        *   Aktive Nutzer (angemeldet innerhalb der letzten 30 Tage) sind im RAM zur Verringerung der Latenz
        *   Ziel: jeder Tweet soll innerhalb von 5 Sekunden sichtbar sein (derzeit v.a. bei Promis nicht machbar, vor allem nicht, wenn sich diese untereinander schreiben was durchaus häufig passiert)
        *   T. sieht sich selbst als Set von APIs und Realtime-Event-Bus
        *   Timeline in Redis-Cluster persistiert (derzeit max. 800 Einträge), dieser hat mehrere TByte RAM
        *   Suche funktioniert anders - hier werden alle Berechnungen beim Lesen ausgeführt (modifiziertes Lucene)
    *   **Groupon**
        *   Migration auf node.js anstelle Ruby on Rails verbesserte die Performance (fast 50%) und verringerte die Hardware-Anforderungen
        *   europäische Infrastruktur (Zukauf Citydeal) lange von US getrennt, Vereinheitlichung wurde zugunsten des schnellen Wachstums zurückgestellt, nur über API Zugriff auf beide
        *   Zunächst nur ein MySQL-Cluster, später dann Aufteilung nach Services
        *   monolithische Web-Anwendung wurde ebenfalls in 20 einzelne Anwendungen für jedes Produkt unterteilt
        *   API-Layer ursprünglich nur für mobile Anwendungen geschrieben
        *   inzwischen auch ein einheitlicher Frontend-Stack
        *   eigener Routing-Service für nginx, wird besonders für A/B-Tests benutzt
    *   **ESPN**
        *   einige hundert Server, etwa 100.000 Requests/Sekunde, Java-Stack (Oracle- und MS-SQL, WebSphere MQ, EJBs)
        *   Fachlicher Schnitt anhand der Sportarten (z.B. eine DB für NHL, MLB, ...), ein Service / Sportart, Ziel ist eine einheitliche API für jede Sportart
        *   skaliert durch massives Cachen (never touch the database), HTML-Seiten und -Fragmente qerden gecached, Varnish als Proxy, Expiration über TTLs für jede URI, bei Änderungen im CMS wird über einen zentralen Service ein "Expires" an jeden Client gesendet
        *   Performanceverbesserung durch Cache Push, d.h. neue Daten werden asynchron persistiert und im Cluster verteilt
        *   Massiver Datenbestand an Statistiken, wird über Batch-Prozesse aktualisiert
    *   **Justin.tv**
        *   über 30 Millionen Visits/Monat, uploaden etwa 30h Video pro Minute, jederzeit bis zu 2000 eingehende Streams, 200 Video-Server mit Sendekapazität von je 1 Gbps, jeder kann dabei Edge oder Origin sein
        *   Stack: Dateisystem XFS, Ruby on rails, Nginx, PostgreSQL, MongoDB, MemcacheDB, RabbitMQ (job system), Wowza, S3 (statische Inhalte, z.B. Benutzbilder)
        *   besonders empfindlich hinsichtlich Bandbreiten-Schwankungen (Live-Video)
        *   eigenes Balancing-Tool verteilt Nutzer, die nicht mit den eigenen Kapazitäten versorgt werden können, automatisch an ein CDN (besonders wichtig bei "flash crowds", d.h. vielen Nutzern eines Streams)
        *   kein Multicasting da die ISPs der (externen) Nutzer es nicht unterstützen und intern genug Bandbreite verfügbar ist
        *   eigener Player unterstützt beim Load-Balancing, mit HTML5 so nicht möglich
        *   CDN am teuersten, AWS deutlich billiger (aber Probleme mit wechselnden Bandbreiten), eigene Infrastruktur aber mittlerweile am billigsten (kalkuliere Cost-per-Customer)
        *   massives Caching aller HTML-Seiten, Monitoring von jedem Klick / Page view /Aktion zur Verbesserung des Angebots
        *   PostgreSQL hatte Schwierigkeiten mit vielen parallelen Writes (z.B. Anzahl der Views eines Videos), dafür jetzt MemcacheDB
        *   Server werden weitgehend automatisch mit Puppet aufgesetzt und konfiguriert
        *   jedes Release wird von QA abgesegnet (dauert nur etwa 5-10 Minuten)
    *   **Tumblr**
        *   18 Milliarden Page Views/Monat, 120 Millionen Unique Visitors/Monat, 60 Millionen neue Posts/Tag
        *   Backend-Team arbeitet im Wesentlichen mit Scala (nutzt u.a. Finagle), Product Team mit LAMP
        *   zunächst recht monolithisch mit einer DB, konnte bald mit Anzahl neuer Posts nicht mithalten (Flaschenhals: Schreiben), Ausweg: Sharding
        *   dies war nicht unbedingt vorhersehbar aufgrund häufiger Änderungen des Kernprodukts (sollte immer im Fokus stehen)
        *   mittelfristig soll alles in HBase gespeichert werden

## Sicherheit in Architekturen

*   betrifft alle Ebenen einer Anwendung, hat Auswirkung auf Organisation (Rechte und Rollen)
*   übliche Schwerpunkte und Zieles:
	*   Authentifizierung, Identifikation (Verwaltung von Rechten und Rollen)
	*   Autorisierung (Sicherung gegen unbefugten Zugriff)
	*   Integrität (Manipulationen vermeiden bzw. erkennen, Echtheit von Daten prüfen)
	*   Vertraulichkeit (sensible Daten vor Mißbrauch schützen)
	*   Unleugbarkeit (Beleg für bestimmte Aktionen wie z.B. Nachrichten)
	*   Verfügbarkeit (Vermeidung bzw. Toleranz gegenüber Systemstörungen)
*   besonders wichtig bei der Datenübertragung (gegens. Vertrauen der Kommunikationspartner)
*   typische Herausforderungen:
	*   Firewall, Kryptographie (public/private key)
	*   Hardware (Treiber)
	*   gesetzliche Rahmenbedingungen
*   übertragen auf das OSI-Modell:
	*   Sicherheit in OSI-3 (Netzwerk): unabhängig von Software, meist in VPNs
	*   Sicherheit in OSI-4 (Transport): durch Protokolle wie SSL (anwendungsseitig nutzen)
	*   Sicherheit in OSI-7 (Anwendung): z.B. bei -Mails S/MIME, anwendungsabhängig, maximale Kontrolle aber auch erhöhter Aufwand und Risiko
*   Sicherheitsmaßnahmen haben immer Einfluß auf Performance, User Experience, Kommunikation/Verteilung sowie auf das Logging (sensible Daten in Protokolldateien)
*   Klartextkommunikation von sensiblen Daten ist unter allen Umständen zu vermeiden
*   es muß stets klar erkennbar sein, von wem eine Information kommt
*   Fehlerausgaben und Versionsinformationen generell unterdrücken, QA muß Teil des Entwicklungsprozesses sein
*   zwei wesentliche Verschlüsselungsarten:
	*   symmetrisch: gleicher Schlüssel für Verund Entschlüsselung
	*   asymmetrisch: Schlüsselpaar public/private z.B. RSA, sicherer aber deutlich langsamer, Public und Private Key sind dabei über ein mathematisches Verfahren verbunden
*   Hybridverfahren: z.B. über zufälligen symmetrischen Sitzungsschlüssel
*   digitale Signaturen basieren auf asymmetrischer Verschlüsselung
*   Funktionsweise asymmetrischer Verschlüsselung:
	1.  Hash der Nachricht erstellen (z.B. MD5)
	2.  Hash mit Private Key verschlüsseln
	3.  Daten übertragen
	4.  Daten mit Public Key des Absenders entschlüsseln
	5.  Hash der Daten vergleichen
*   erste Ansatzpunkte für Sicherheitsprobleme in Webanwendungen:
	*   Nutzereingaben, die ausgegeben werden
	*   IDs (z.B. Bestellnummer) die einem System folgen (andere IDs leicht ermittelbar)
	*   Backup-Dateien werden auf Produktivsystem „gesichert“ (Parser greift nicht daher direkte Textausgabe
*   Sinnvoll: eigener Secure Deployment Process (entferne Kommentare, Backup-Dateien, ...)
*   Nicht-authentifizierte Nutzer sollten ggf. gar nicht erst zur Datenbank vorgelassen werden (im Frontend prüfbar), spart Ressourcen
*   Häufigste Security-Leaks sind z.B. in OWASP Top Ten zusammengefasst (bieten auch Tools zu Analyse/Verbesserung an)
*   Analyse für Web-Anwendungen: Mozilla Stooge
*   **SQL-Injection**: Login mit Nutzer „admin“, Passwort „;'' (kommentiert Rest des Statements aus)
*   Frameworks helfen kaum, besser parametrisierte Übergabe und/oder Stored Procedures
*   **Cross-Site-Scripting:** sehr einfach über Kommando javascript: in Texteingaben
*   Beispiel: javascript:alert(document.cookie); gibt Session-ID aus
*   Entsteht hauptsächlich durch fehlende Validierung/Escaping von Eingabewerten (muss serverseitig passieren, clientseitig gesendete Daten sind per se immer ein Risiko)
*   **Cross-Site-Request-Forgeries**: setzt angemeldeten Nutzer voraus und führt im Hintergrund (iframe, manipuliertes img-Tag) einen manipulierten Request aus
*   funktioniert nur, wenn der Nutzer z.B. vorher einen präparierten Link angeklickt hat
*   all dies nicht mit Firewalls, SSL o.ä. zu beseitigen – Anwendungslogik (hilfreich: FindBugs)
*   Eine ausgereifte Eingabevalidierung vermeidet fast alle Risiken (HTTP-Header beachten)
*   Sessions müssen nach einer gewissen zeit automatisch beendet werden (Timeouts), sonst Risiko Session-Diebstahl
*   HTTPS bietet zumindest eine Transportverschlüsselung, zusätzliche Inhaltsverschlüsselung bei kritischen Daten empfehlenswert
*   Authentifizierung einfach halten (evtl. eigene URLs für verschiedene Rollen)
*   laut FBI-Studie wurden 77% der Unternehmen von eigenen Mitarbeitern angegriffen, 28% von Konkurrenz, 25% von fremden Regierungen
*   gute Web Application Firewalls filtern „böse“ Zeichen schon auf HTTP-Ebene
*   Unternehmen sollten eine Application Security Policy aufstellen, die aber auch konkret ist (keine Phrasen aber auch kein Code, da sicher dieser zu schnell ändert)
*   Security wird gerade in heißen Projektphasen meist vernachlässigt daher machen externe Dienstleister Sinn (sind meist auch auf dem neuesten Stand)

## Architektur auf dem Client (Web, GUI, Internationalisierung)

*   Im Web höhere Anforderungen an Skalierbarkeit als in Enterprise-Anwendungen (Nutzerzahl)
*   Generell haben Web-Apps große Vortile: keine Installtion, automatische Updates, gewohnte Umgebung (Browser), Integration mit anderen Anwendungen möglich, Bookmarks / Links
*   Programmiersprachen/Frameworks nachrangig und eher bei Entwicklung zu diskutieren
*   Anzahl an Requests sowie übertragene Datenmenge zwischen Client/Server minimieren
*   AJAX erhöht eher die Anzahl der Requests, erhöht aber auch die "gefühlte" Geschwindigkeit
*   Größte Stellschraube für Performance: **Caching** , Grundprinzip: Daten, die schon einmal angefordert wurden, werden bestimmt nochmal angefordert (Umsetzung z.B. über localStorage)
*   Distributed Cache: verteilter Cache auf mehreren Systemen, schönes Gleichnis: Süßigkeiten evtl. in der Küche, im Schreibtisch oder im Kühlschrank, wenn nirgendwo dann bleibt nur der Gang zum Supermarkt (quasi die DB, „Zugriff“ ist teuer)
*   Auf DB-Seite wird sehr oft memcached für Caching genutzt (facebook)
*   i.d.R. viele parallele Requests, daher Skalierung auch eher horizontal (= mehr Server)
*   Caching kann bei Deployment ein Problem sein, da die Ressourcen erst "irgendwann" expiren, Beispiel Release-Prozess AOL
	1.  Neue statische Inhalte werden parallel zu "alten" im CDN abgelegt
	2.  "Alte" HTMLs werden nun schrittweise umgestellt, so dass sie auf die "neuen" Ressourcen verweisen (sind abwärtskompatibel)
	3.  Neuer Code wird nun auf Tomcats deployed, diese werden dazu angehalten (fallen dadurch aus dem Load Balancer) und anschließend neu gestartet
*   Dies dauert bei AOL etwa 20-30 Minuten für etwa 2000 Server. Problem: Abwärtskompatibilität alter/neuer Ressourcen, "Mischbetrieb"
*   Pragmatische Alternative: index.html nie cachen, neue Ressourcen parallel zu alten anlegen (mit eigenen Pfaden), da HTML nicht gecached wird werden bei Reload automatisch die neuen Ressourcen geladen
*   Differenzierung zwischen Website/Webapp kaum sinnvoll (tendenziell ist Webapp aber „interaktiver“, vgl. facebook), native Apps sind plattformspezifisch (eigene Code-Basis)
*   wirklich neu ist bei mobilen Seiten/Apps nur die Eingabemethode "touch" und damit verbundene Gesten sowie Push-Services
*   angesichts der Bedeutung von Smartphones gilt heutzutage "mobile first", dazu eigene Serverlogs beachten
*   Responsive Design bringt quasi die Desktop-UI für umsonst mit
*   dennoch sind die Performance-Anforderungen bei mobilen Umgebungen wesentlich höher (JSON oder Protocol Buffers statt SOAP, umsetzbar z.B. über Content Negotiation)
*   Einschränkungen und best Practices bei Mobilgeräten:
    *   Unzuverlässiges Netz (Offline-Fähigkeit wichtig)
    *   schnelle Ladezeit durch geringe Dateigrößen, wenige Requests, aggressives Caching (Edge / 3G / LTE nicht so schnell wie LAN)
    *   Debugging erfordert Logging (nötig v.a. durch Gerätevielfalt, wenn etwas nicht geht muß man die Rahmenbedingungen kennen)
    *   Minimierung von Nutzereingaben (immer kompliziert), Buttons groß gestalten und hervorheben
*   früher gab es eine Framework-Schwemme um Schwächen des Browsers auszugleichen
*   generell darf eine URI nicht nur der einzige Punkt einer Anwendung sein (Hyperlink!)
*   Frameworks können in drei Kategorien unterteilt werden:
	*   Komponentenframeworks: "verstecken" elementare Webtechnologien, oft eher stateful, aus einer Zeit langsamer Clients ohne Javascript ( JSF, Wicket, ASP.NET)
	*   Request/Response Frameworks: tendenziell stateless (Java Servlet-API, Spring MVC, Struts, RoR, ASP.NET MVC)
	*   Clientseitige Frameworks: Javascript-basierte Frameworks (JS mittlerweile schnell, portabel), quasi eine Runtime (Single-Page-Application), z.B. backbone.js, AngularJS, Ember
*   Diese Frameworks lösen sich von der DOM-Manipulation (jQuery) und verwalten selbst alle Zustandsänderungen die (z.B.) durch Interaktion des Nutzers auftreten in einem Model - vollwertiges MVC
*   Dadurch auch einfachere Umsetzung von Architekturprinzipien (fachlicher Schnitt)
*   Auch in JavaScript am besten eigene "Klassen" (Skripte) für fachliche Objekte erstellen und in einem Build-Prozeß zusammenführen
*   Webserver sind vor allem gut für statische Inhalte, dabei ist z.B. nginx wesentlich performanter als Apache, leichter zu konfigurieren, stateless I/O (eignet sich für viele parallele Nutzer)
*   Reverse Proxy Cache: beschleunigt Webauslieferung mit fertig gerenderten Seiten im RAM (z.B. Squish, Varnish), CDNs sind quasi weltweite Reverse Proxy Caches
*   Stresstests über Apache Benchmark, JMeter oder Selenium Grid
*   **ROCA**: Ansatz zur Entwicklung von Webanwendungen bei Fokussierung auf Standards
*   ROCA eignet sich für (fast) alles außer Seiten mit besonderen (Javascript-) Anforderungen, z.B. 3D-Game, IDE- oder CAD-Anwendung im Browser oder Offline-Anwendungen
*   Zwingende Anforderungen: REST-Orientierung, alles hat eigene URL, HTTP-Methoden, zustandslos (keine Sessions), Server generiert strukturiertes HTML, Anwendungslogik nur auf Server ausführen, Anwendungslogik funktioniert außerhalb des Browsers (Curl, wget, Lynx), JS folgt dem Prinzip des progressive enhancement
*   Empfehlungen: jede Ressource darf andere Repräsentationen haben (z.B. Ergebnis auch JSON für Nutzdaten), History-API sollte funktionieren (Änderung URI ohne Refresh, Beispiel: Github), SSL verwenden, HTTP-Sicherheitsmechanismen nutzen (z.B. BasicAuth sicher, aber Eingabedialog häßlich und kein Logout möglich)
*   Verbote: Cookies nur für Authentifizierung verwenden, Back/Forward/Refresh-Buttons müssen immer funktionieren, Verlinkbarkeit darf nicht auf variablen Hash-Informationen (#) basieren (vollständige URLs)
*   Javascript sollte weitgehend statisch sein (möglichst unabhängig vom gerenderten Layout, nicht auf fixe IDs sondern auf Klassen triggern)
*   interessanter Ansatz: Seite lädt mit allen Inhalten, Inhaltselemente sind mit CSS-Klasse versehen, Javascript reagiert auf CSS-Klasse und "erweitert" den Inhalt
*   wichtigste Informationen immer im oberen Teil von Eingabemasken anordnen
*   Elemente gruppieren und einheitlich anordnen (Raster) sowie von anderen Gruppen abgrenzen, Strukturen visualisieren, Symbole nutzen (wenn möglich)
*   es sollte immer eine Möglichkeit zum Zurückspringen geben (Undo)
*   Statusanzeigen sollten an der gleichen Stelle sein und durch Symbole / Betonung (Farbe) gekennzeichnet werden, Anwender soll jederzeit Rückmeldung erhalten wenn etwas passiert
*   sinnvolle Default-Werte erleichtern die Eingabe, Mehrfachauswahl von Objekten zulassen, frühzeitig Anwendertests durchführen
*   Benutzeroberfläche immer eine Sammlung von Metaphern:
	*   Fabrik-Metapher: Mehrere Arbeitsschritte wobei das Endprodukt eines Schrittes die Ausgangsbasis des nächsten ist (feste Reihenfolge, gut zur Erfassung vieler Daten)
	*   Werkzeug-Material-Metapher: Mensch hat mehrere Werkzeuge zur Erfüllung einer Aufgabe, freier als Fabrik (kreativer Arbeitsablauf ohne feste Reihenfolge), eher für Experten (optimale Nutzung)
	*   Formular-Metapher: Erfassung einer Vielzahl von Daten in verdichteter Form
*   Daraus ergeben sich verschiedene Interaktionsziele für eine Anwendung:
	*   Objektorientiert: Anwender wählt Objekt und bearbeitet es, oft kontextorientierte Menüs, sinnvoll für grafisch orientierte Anwendungen (Werkzeug-Material-Metapher, d.h. Werkzeug ist Hilfsmittel und Material der Gegenstand der Tätigkeit)
	*   Frage-Antwort: sequenzieller Arbeitsablauf mit konfigurierten/programmierten Übergängen (Wizards), auch für Micro-Systeme (Handys) geeignet, entspricht der Fabrik-Metapher (Zustandsautomat)
	*   Formularbasiert: Anwendungsdaten als Text, erzeugen Recherchen/Ausgabe
*   Menüs und Fenster: Arbeitsabläufe meist in baumartiger Struktur abgebildet, meist mehrere Alternativen für nächsten Schritt (Netz mit Einund Ausstiegspunkt), oft in Formular-Dialogen
*   verdichtete Informationen (z.B. Fahrplan) möglichst in einer Ansicht darstellen, kleine Schrift, Schriftfarbe und Typen zur Strukturierung einsetzen
*   Tabellendarstellung (z.B. Stückliste, Suchergebnis) nach logischen Kriterien sortieren, optische Anker setzen (fette Schrift), absteigende Wichtigkeit von links nach rechts
*   Hierarchie (z.B. Organigramm) zum schnellen Wiederfinden von Daten (Baumstruktur)
*   im Formular (z.B. Bestellung) die Pflichteingaben hervorheben und Standard-Werte vorgeben, Ausgabefelder klar von Eingaben abgrenzen
*   Expertensysteme (z.B. Bildbearbeitung) müssen in der Darstellung konfigurierbar sein und mit möglichst wenigen Arbeitsschritten auskommen, viel Platz für Arbeitsgegenstände, Statusinformationen/Werkzeuge am Rand
*   wesentliche Parameter der **Internationalisierung**:
	*   Sprachen: Welche? Schriftzeichen? LTR/RTL?
	*   Maßeinheiten: z.B. Währungen, Metrik
	*   Zeiten: Länder- und Zeitzonen
	*   Regeln: z.B. Rechtsverkehr
	*   kulturelle Unterschiede: z.B. Bedeutung von Farben, Tastaturkürzel
*   neben den Texten variiert oft die Formatierung (Datumsangaben) und Interpunktion (spanische Fragezeichen), Reihenfolge im Alphabet kann ebenfalls variieren
*   Texte extern vorhalten, kein statisches GUI-Layout ( Komponenten sinnvoll)
*   Fehlermeldungen, Hilfetexte und Tooltips werden gern vergessen (Pflegeaufwand!)
*   auch bei einsprachigen Projekten möglichst überall UTF-8-Encodierung verwenden
*   Dynamische Informationen müssen als Teil des Workflows übersetzt werden (kein Release ohne vorhandene Übersetzung)

## Modellgetriebene Entwicklung (MDD und DSLs)

*   Modellierung greift einen Aspekt aus dem System heraus & macht ihn erfaßbar (Abstraktion)
*   Modellierung hat immer ein Ziel (i.d.R. generierbaren Code), ist aber auch Kommunikationsmedium zwischen Technik und Fachlichkeit
*   Ein Modell sollte nicht zu früh zu formal sein (Kunde versteht das nicht, doch wir müssen den Kunden verstehen)
*   Warum modellieren:
	*   Zeit sparen (Faustregel: min. 5 Leute arbeiten einige Monate an langlebigem Projekt)
	*   Qualität erhöhen
	*   Austauschbarkeit fördern (Produktlinien)
	*   Kommunikationsbasis schaffen
*   Grundidee: Entwicklung soll domänenspezifisch sein (Abstraktion für Finanzanwendungen, Versicherungen, Multimediales, ...)
*   Tools helfen bei der Generierung des jeweiligen Modelle (Vorteil: Struktur kann z.B. in Powerpoint visualisiert werden, aber es entsteht auch Code daraus)
*   Werkzeuge können Modell verarbeiten, benötigen klare Strukturen, Semantik, Zuständigkeiten
*   Modeling Language notwendig, UML bietet sich an ist aber nicht genau genug
*   Eine DSL hält alles fest, was im Modell möglich ist (immer auf eine Domäne beschränkt)
*   DSL ist eine Sprache, immer von einem Computer ausgeführt wird, daher immer kurz halten (leicht zu parsen)
*   DSL ist oft nur eine Fassade für ein komplexes Model, erleichtern die Zugänglichkeit
*   DSL beschreibt z.B. folgendes Szenario: Verbinde Port X von Komponente Y mit allen Komponenten, die das Interface Z anbieten und suche alle 60 Sekunden über einen Service, welche Instanzen verfügbar sind
*   Unterschied zwischen DSLs/APIs/Frameworks kaum definierbar, ein API-Call steht aber für sich während eine interne DSL aus Sätzen zusammengesetzt wird (ein Satz steht nicht für sich)
*   Zwei Arten von DSLs:
	*   intern: kein Parser, eher für Techniker
	*   extern: Parser nötig, gut für Fachlichkeit
*   idealerweise muß die Anwendungslogik bei Änderung an den DSLs nicht angepaßt werden
*   Gleichnis: DSL hilft bei Entwicklung wie RegEx bei der Suche (geht auch ohne aber schwer)
*   Umsetzung einer DSL über grafische Tools oder textuelle Beschreibung
*   Text meist produktiver da erweiterbar, Versionierung/Diff und spätere Migration möglich
*   Domäne wird analysiert, Kernkonzept ermittelt, Abhängigkeiten und Eigenschaften werden festgehalten (Meta-Modell)
*   Beispiel: In der Entwicklung ist die Grundlage oft ein POJO, um das POJO zu erzeugen braucht es ein Meta-Modell (enthält Dinge wie Definition, Attribute, ...)
*   Meta-Modell (Sammlung von Eigenschaften) beschreibt das Konzept, nicht die Repräsentation, das übernimmt die konkrete Syntax (Grafik oder Text)
*   Modelle müssen transformiert werden (entweder in andere Modelle oder in Code)
*   schon das Entwickeln des Generators hilft beim Verständnis der Architektur
*   komplexe Architekturen enthalten sehr viele Komponenten mit vielerlei Abhängigkeiten, Modell kann diese technischen Aspekte abstrahieren (Komponenten, Interfaces, Instanzierung, Abhängigkeiten, Prozessdefinition)
*   Klassendiagramme mit Stereotypen kann dies umsetzen (UML Profile), Codegenerierung setzt diese Basisklassen dann um
*   Anwendungslogik dann in Klassen, die von generierten Klassen erben
*   auch für Geschäftsprozesse anwendbar Generierung aus UML-Zustandsdiagrammen heraus, meist Process Engine nötig (z.B. JBPM)
*   UML hilft vor allem bei Datenstrukturen und Service-Tools (Dokumentation, Kommunikation), wird dennoch sehr oft als Code-Generator genutzt
*   dieses Vorgehen ist üblich, aber nicht domänenspezifisch (zentrische Architektur, MDSD)
*   zwei Rollen:
	*   zunächst die Meta-Modelle definieren, Generatoren erstellen
	*   dann die Modelle verwenden um Anwendung umzusetzen (Koordination oft schwierig)
*   MDSD spart nicht unbedingt Zeit/Geld, lohnt sich vor allem bei mehreren ähnlichen Projekten (Product Lines), es sollte sich aber immer auch für einzelnes Projekt lohnen
*   hilft auch bei veränderten technischen Rahmenbedingungen (z.B. Migration von J2EE-Version hat nur zentrale Anpassung an einer Stelle zur Folge)
*   Anpassung von Feldbezeichnungen ebenfalls nur an einer Stelle, alles weitere wird generiert
*   testgetriebene Entwicklung ebenfalls möglich (dafür zunächst Model entwickeln und Interfaces generieren, anschließend Tests schreiben und dann alles weitere implementieren)
*   Vorteile: Erweiterung eines Systems leichter (klar definierter Rahmen), Automatisierung, Standard-Komponenten (z.B. Hibernate-Connector) können generalisiert werden
*   Bessere Frameworks (Spring) reduzieren Bedarf an Generatoren (zumindest für Laufzeit-Komponenten)
*   MDA versucht eine Basisform von MDD zu standardisieren (basiert im wesentlichen auf DSLs, die via UML-Profiles generiert werden)
*   MDA-Schritte: Modell der Fachdomäne (PIM), Transformation des Modells in plattformspezifisches Modell (PSM), Übersetzung in Quellcode (PSM)
*   MDA erlaubt die Generierung von Anwendungen aus UML-Modellen heraus
*   in der Praxis wird aus dem UML-Modell meist der Großteil des Codes generiert und durch selbstprogrammierte Fragmente ergänzt
*   DSLs schon gut via UML erstellbar, UML in XMI transformieren, XMI in Code transformieren
*   verbreitete Tools:
	*   Xtext: etabliert, Codegenerierung erfolgt über Xpand
	*   MPS: kann DSLs konstruieren, bietet Validierung, Generator und Spracherweiterung für einige Programmiersprachen
	*   Eclipse EMF: kostenfrei, schnell einsetzbar, eher eine Basis für ein Metamodell
*   modellgetriebenes Testing über BDD-Tools wie Cucumber, Twist, JBehave

## Weitere Themen & Patterns

*   **Command:** kapsle Request auf ein Objekt in einem eigenen Objekt, das ein allgemeines Interface hat
*   gut für Undo-Mechanismus geeignet
*   eine Steigerung ist (Komponenten-)**Container:** Komponente läuft auf jeder Infrastruktur wenn das kapselnde Objekt die Rahmenbedingungen abdeckt (Zugriff auf Hardware, I/O, DB, ...)
*   Herausforderung ist dabei oft die Parallelität (zentraler Ansatz)
*   **Command Processor:** Anwendung verarbeitet Requests mehrerer Clients, die Aufgaben wie Logging, Undo/Redo oder auch Scheduling auslösen sollen
*   Clients sollten diese Funktionen nicht direkt sondern über Zwischenschicht (Command Processor) auslösen, dieser kann auch den Status der Komponenten abfragen
*   ähnlich: Firewall Proxy bzw. Authorization, schützt (öffentlich erreichbare) Funktionen (z.B. durch Rechteabfragen) und erlaubt keinen "direkten" Aufruf
*   **Dynamic Discovery:** Beim Hinzufügen neuer Systeme/Komponenten müssen diese von der bestehenden Infrastruktur erkannt werden
*   oft ist vertikale Skalierung günstiger und risikoärmer als Optimierung der Anwendungslogik
*   Umgebung für Staging/Tests muß möglichst ein Duplikat der Live-Umgebung sein
*   mögliche Umsetzung: Testumgebung auf Produktivsystem aber in eigener Partition (riskant)
*   Anderer Ansatz: Eine funktionierende Testplattform wird nach Abnahme zur Live-Plattform
*   Nutzerdaten sollten von Systemdaten getrennt werden (z.B. verschiedene DBs), erleichtert Migration (Systemdaten können i.d.R. neu geschrieben werden, Nutzerdaten nicht)
*   **Pooling:** Vorhalten von Ressourcen im RAM, sinnvoll vor allem für kurzzeitige Operationen (sonst: Batch), Beispiele: Connection Pool, Singleton/Registry-Pattern, Netzlaufwerk
*   Ressourcen Manager teilt Ressourcen zwischen Verbrauchern auf, erleichtert die Pflege, führt zu Problemen mit Parallelität/Performance
*   Ressourcen immer möglichst früh freigeben / für Daten die sich nicht oft ändern: **Caching**
*   Es sollten gezielte Limits gesetzt werden (tendenziell nur eine bestimmte Zahl an Nutzern zulassen statt alles immer langsamer werden zu lassen)
*   **Plugin:** verknüpft Klassen in der Konfiguration statt zur Laufzeit/Compilierung
*   wird benötigt, wenn basierend auf Laufzeitbedingungen verschiedene Implementierungen genutzt werden können (ähnlich Strategy-Pattern)
*   funktioniert am besten in Sprachen mit Reflection
*   **Interceptor:** Callbacks, die bei bestimmten Systemzuständen ausgelöst werden
*   wird oft in Frameworks/Middleware eingesetzt, da es die interne Struktur nicht verändert aber bestimmte Hooks erlaubt
*   ähnlich sind auch **Lifecycle Callbacks:** zur Laufzeit (z.B. Erstellung, Verarbeitung, Abschluß) werden Events ausgelöst – besonders gut für Logging, UI, …
*   **Transaction Script:** jede Prozedur verarbeitet einen Request
*   validiert Eingabe, speichert Daten, führt Funktionen aus
*   sehr einfach, aber u.U. redundanter Code (mehrere ähnliche Transaktionen), meist wird alles in einer Klasse zusammengefaßt
*   **Domain Model:** Eigene Klassen für alle miteinander verbundenen Akteure, ähnlich wie OOP, Umsetzung oft mit Data Mappern aber für kleine Systeme eher zu komplex (sehr granular)
*   komplizierter, aber gerade in Großprojekten sehr flexibel und gut erweiterbar (Vererbung, Strategy-Pattern) da es sich bewußt von der Tabellenstruktur löst
*   Grundlegendes Code-Beispiel:

<code>
public Cargo(TrackingId trackingId, RouteSpecification routeSpecification) {
	Validate.notNull(trackingId, "Tracking ID required");
	Validate.notNull(routeSpecification, "Route specification required");

	this.trackingId = trackingId;
	this.origin = routeSpecification.origin();
	this.routeSpecification = routeSpecification;

	this.delivery = Delivery.derivedFrom(
		this.routeSpecification, this.itinerary, HandlingHistory.EMPTY
	);
}
</code>

*   heutzutage eigentlich Standard (bis auf kleine/alte Systeme)
*   **Table Module:** eine einzelne Instanz für die Anwendungslogik jeder Tabelle, d.h. die Datenstrukturen bilden den Mittelpunkt der Anwendung
*   arbeitet aber immer mit Record Sets als Ergebnis
*   Kompromiß zwischen Transaction Script & Domain Model, gut für kleine und mittlere Systeme
*   Vererbung aber quasi unmöglich
*   Faustregel: verwenden, wenn nicht mehr als 50 fachliche Klassen/Tabellen im Projekt
*   Objekt zur Datenübermittlung zwischen Prozessen um die Zahl der Methodenaufrufe zu reduzieren
*   **Service Layer:** Service Layer deckt meist die CRUD-Operationen ab, wird oft in POJO bzw. zustandsloser Klasse abgebildet, üblicherweise wird unterschieden
	*   Domänenlogik: z.B. Berechnung eines Vertrages
	*   Anwendungslogik: z.B. die Benachrichtigung über die Berechnung
*   Umsetzung z.B. über
	*   Domain Facade: Domänenmodell, implementiert keine Anwendungslogik direkt
	*   Operation Facade: direkte Implementierung der Anwendungslogik
*   Service Layer sollten sowohl intern als auch von außen (remote) ansprechbar sein, dennoch empfiehlt sich zunächst eine lokale Implementierung
*   Jedes (Sub-) System sollte einen Service Layer haben, es sei denn, es gibt nur ein einzelnes User Interface und nur sehr wenige Transaktionen
*   **Remote Facade:** ähnlich wie Service aber Remote, verbessert Effizienz der Datenübertragung
*   Beispiel: Web Service (=Interface für entfernte Zugriffe)
*   Objekte haben kein direktes Remote-Interface, nur das Facade-Objekt wird angesteuert
*   zustandslose Remote Facade kann auch gepooled werden nochmals bessere Performance
*   auch nützlich zur Rechtekontrolle (Sicherheit), Transaktionssteuerung kann ähnlich wie in Unit of Work gesammelt werden, sollte aber grundsätzlich keine Anwendungslogik enthalten
*   **Record Set:** Äquivalent zu Tabellendaten einer DB im lokalen Speicher
*   entspricht dem Ergebnis eines SQL-Queries, kann durch Anwendungslogik bearbeitet werden
*   Record Set kann natürlich von der Datenquelle getrennt werden (Übertragung, Serialisierung)
*   Implizite Interfaces (Methoden mit Offset-Parameter) können für verschiedene Datentypen verwendet werden, sind aber wenig aussagekräftig
*   Explizite Interfaces haben klare Bezeichner (Spaltennamen) und sind daher zu bevorzugen
*   gut zum Austausch mit Table Module Daten lesen, an Table Module übertragen, im Client ändern, im Table Module speichern, committen
*   **Table Data Gateway:** bündelt Methoden für übliche CRUD-Operationen in einem Objekt
*   paßt gut zum Table Module-Pattern
*   kann Domänenobjekte zurückliefern (führt aber zu Kopplung zwischen Domäne & Gateway)
*   funktioniert sowohl für direkte SQLs als auch Stored Procedures
*   **Row Data Gateway:** Objekt, dass genauso "aussieht" wie der Tabelleninhalt und auf das über die jeweilige Programmiersprache zugegriffen wird
*   jede Spalte wird ein Feld, praktisch eine 1:1-Beziehung zwischen Tabellenzeile und Objekt
*   paßt gut zum Transaction Script-Pattern, empfiehlt sich nicht für Domänenobjekte
*   **Active Record:** Wrapper für Ergebniszeilen einer Tabelle
*   Datenstruktur auch hier wie in der DB: jede Spalte ist ein Feld (keine Konvertierung), aber eigene Methoden für CRUD-Operationen gemäß dem Domänenmodell
*   Anwendungslogik arbeitet wie beim Data Mapper mit Methoden, die vom Active Record-Objekt in DB-Operationen umgesetzt werden
*   Domänenlogik besser nicht zu komplex (Active Record = Row Data Gateway + Domänenlogik)
*   insgesamt ist Active Record recht einfach, neigt aber zu Kopplung und Code-Duplikation
*   **Data Mapper:** Zwischenschicht zum Bewegen von Daten zwischen DB und Objekten
*   ermöglicht die Kommunikation zwischen unabhängigen Objekten (Unterschied zu **Mediator**, denn da sind die Objekte bekannt)
*   macht insbesondere bei Verwendung einen Domänenmodells Sinn
*   jedes Objekt hat dabei eigenen Mapper, der mindestens die Basisfunktionen (CRUD) abdeckt
*   bei vielen Objekten macht **Lazy Load** Sinn, um Objekte nur bei Bedarf nachzuladen (also zum spätesten möglichen Zeitpunkt)
*   Objekte werden entweder über einen langen Konstruktor (mit allen nötigen Feldern) oder via Komposition erzeugt
*   Hauptvorteil: Datenbank und Objektmodell können sich unabhängig entwickeln
*   **Data Transfer Objects:** entspricht oft einem POJO-Objekt (Felder mit Gettern und Settern)
*   Anwendung sinnvoll, wenn mehrere Datenobjekte zwischen zwei Prozessen in einem Aufruf übertragen werden sollen (auch zwischen mehreren Schichten)
*   enthält oft mehr Daten als eigentlich gebraucht werden, aber das spart Requests
*   bei asynchronen Zugriffen empfiehlt sich die Kombination mit **Lazy Load**
*   oft ist es sinnvoll, mehrere Datenobjekte die gebraucht werden (könnten) in einem DTO zu bündeln statt viele kleine Requests zu schicken (vgl. **Remote Facade**)
*   muß serialisierbar sein, enthaltene Objekte sollten simpel und wenig verschachtelt sein
*   Struktur entspricht oft einer View (GUI/Website), DTOs sind oft unveränderlich
*   wird oft als Collection umgesetzt, dann ist aber die Namensgebung nicht eindeutig, daher besser als Objekt speichern (eindeutige Bezeichner)
*   Serialisierung oft problematisch (bei Änderungen am Objekt scheitert die Deserialisierung), daher wird inzwischen meist XML verwendet
*   in Java kann JAXB zur simplen Wandlung zwischen XML/Objekt verwendet werden
*   **Single Table Inheritance:** Vererbungshierarchie für alle Klassen in einer einzigen Tabelle
*   jede Klasse speichert alle relevanten Daten in einer Zeile der Tabelle
*   alle überhaupt möglichen Felder aller Objekte sind eine Spalte, Objekte lassen nicht benötigte Spalten einfach frei (kann ineffizient sein, kein Namespacing)
*   einfach und benötigt keine JOINs, erschwert aber Übersicht (viele Felder, verschwendet Platz)
*   **Class Table Inheritance:** Vererbungshierarchie für alle Klassen mit einer Tabelle pro Klasse
*   Umsetzung meist mit identischen Primärschlüsseln (Tabelle) bzw. ID (Klasse)
*   Vorteile: recht effizient, Zusammenhang Domänenmodell/DB sehr leicht verständlich
*   Nachteile: Auslesen von Daten aus mehreren Tabellen/Klassen erfordert JOINs, oft ist nicht klar, welche Tabellen überhaupt gejoint werden müssen
*   Refactoring der Klasse erfordert Änderungen an der Tabelle
*   **Concrete Table Inheritance:** Vererbungshierarchie für alle Klassen mit einer Tabelle pro konkreter Klasse (Implementierung eines übergeordneten Objekts)
*   Beispiel: Fußballer, Handballer, Radfahrer sind Implementierungen der Klasse Sportler
*   PKs der einzelnen Tabellen müssen eindeutig sein (sonst mehrere Ergebnisse bei Abfragen), DB-seitig generierte PKs genügen nicht
*   Vorteile: Keine überflüssigen Felder, keine JOINs beim Lesen aus einer Tabelle
*   Nachteile: Evtl. häufige JOINs über alle Tabellen nötig (finde alle Sportler), PKs kompliziert, Refactoring der Klasse erfordert Änderungen an der Tabelle
*   Generell empfiehlt sich Single Table Inheritance, aber eine Mischung der Ansätze natürlich möglich und auch sinnvoll
*   **Identity Field:** Speichert den Inhalt einer DB-Spalte in ein Feld eines Objektes
*   Entscheidend: Schlüssel, kann mit Bedeutung (z.B. Versichertennummer) oder ohne (z.B. generierte Zahl) sein, letzteres tendenziell besser weil eindeutig
*   Es gibt auch zusammengesetzte Schlüssel (mehrere Felder), könnten aber mehrfach vorkommen (z.B. Kombination aus Bestellund Kundennummer)
*   zusammengesetzte Keys am besten in eigener Klasse generieren
*   Schlüssel sollten entweder für Tabelle oder ganze DB einzigartig sein (z.B. via Sequenz)
*   Keys können automatisch hochgezählt werden, dann aber unklar, welcher Key gesetzt wurde
*   pragmatischer Ansatz für Non-Oracle: eigene Schüsseltabelle (simuliert quasi eine Sequenz)
*   Datentyp sollte long Integer sein
*   Alternative ist GUID (globally unique identifier), dieser leider sehr groß und i.d.R. String
*   **Identity Map:** stellt sicher, dass (gleiche) Objekte nicht mehrmals geladen werden (passiert oft bei vielen Lesevorängen)
*   Key sollte der Primary Key sein (unveränderlich)
*   üblich ist entweder eine Map/Klasse oder eine Map/Session (letzteres bei PK zu empfehlen, da eindeutig und einfach zu implementieren)
*   Map/Klasse am besten in **Unit of Work** oder **Registry** speichern
*   **Foreign Key Mapping:** Verknüpfung zwischen Objekten zu einem Fremdschlüssel, Mehrfachbeziehung (one-to-many), funktioniert aber nicht für many-to-many
*   Beispiel: Änderung an Reihenfolge einer Liste betrifft alle Listenobjekte, 3 Möglichkeiten:
	*   Löschen und Einfügen: Lösche alle Objekte und füge sie in richtiger Reihenfolge wieder hinzu (funktioniert nur, wenn keine äußeren Abhängigkeiten der Objekte)
	*   Zeiger einfügen: Ergänzt Verknüpfung zwischen Objekt und Liste (Kopplung)
	*   Abgleich: Abgleich mit Status Quo oder zum Zeitpunkt, als Liste gelesen wurde
*   Faustregel: Alle neuen Objekte für die DB sollten z.B. über **Identity Map** überprüft werden (evtl. sind sie bereits vorhanden)
*   Ringreferenzen: Objekt hat evtl. untergeordnete Objekte, die wiederum auf die Liste verweisen
*   Lösung z.B. über Aufteilung in mehrere Module oder Schnittstellen
*   **Association Table Mapping:** Verknüpfung mehrerer Objekte mit mehreren Tabellen
*   Extra-Tabelle, um diese Mehrfachbeziehung (many-to-many) über Joins zu erfassen
*   PK ist die Verbindung der zwei PKs der jeweiligen Tabellen
*   zum Lesen werden zwei Queries gebraucht: einer sucht die Schlüssel, der zweite die Werte
*   Beispiel Tabelle der Mitarbeiter:
	*   Query 1 findet alle Reihen mit Daten zum Mitarbeiter
	*   Query 2 das benötigte Feld (z.B. Alter)
*   zur Optimierung der Queries können **Method Objects** eingesetzt werden (Methode wird zum Objekt gewandelt, Werte sind Felder statt Parameter)
*   **Dependent Mapping:** Eine Klasse vollzieht das DB-Mapping für eine untergeordnete Klasse
*   wenn Reihen nur in einer Tabelle referenziert werden dann kann der Mapper der Tabelle auch das Mapping der Reihen übernehmen
*   Objekte haben wiederum keine Referenz zur übergeordneten Collection (erleichtert Persistenz und vereinfacht DB-Mapping)
*   sollte nicht zusammen mit **Unit of Work** eingesetzt werden
*   **Serialized LOB:** speichert Objektgraph als Binärdaten in einem einzelnen Feld einer DB
*   macht vor allem bei komplizierteren Abhängigkeiten zwischen mehreren Objekten Sinn, entspricht praktisch dem **Memento**-Pattern (aktuellen Zustand speichern)
*   einfach zu entwickeln, ressourcenschonend, kann aber nicht ohne zugehörige Klasse wiederhergestellt werden
*   Wartung und Pflege schwierig (Objekt u.U. nicht kompatibel zur weiter entwickelten Klasse)
*   Alternativ kann ein CLOB (langer Text-String z.B. als XML) eingesetzt werden, benötigt Parser
*   **Layer Supertype:** übergeordnetes Objekt für alle Objekte einer Schicht
*   wird vor allem verwendet um duplizierte Methoden zu verwenden / Methoden werden nur einmalig in Superklasse definiert (ähnlich zur Vererbung)
*   **Activator:** eigener Service für das serverseitige Aktivieren/Deaktivieren von Services (wenn z.B. kein Client mehr zugreift)
*   kann auch automatische Garbage Collection anstoßen
*   **Evictor:** Service, der peridisch kontrolliert, ob eine bestimmte Ressource genutzt wird (kann dies dem Activator signalisieren)
*   Evictor hilft nicht bei Absturz/Verbindungsverlust des Clients, daher immer auch einen Timeout (Leasing) festlegen
*   **Context Object:** speichern Daten, die zur Laufzeit in allen Schichten zugänglich sein sollen
*   nützlich für Logging, Session
*   ist ebenso umstritten wie Singleton oder globale Variablen (Anti-Pattern)
*   **Money:** Geldwert, entspricht einem Objekt mit einem Feld "Zahl" und einem Feld "Währung"
*   Basisproblem: Auf- oder abrunden, also was tun bei 3.5 Cent?
*   sollte wg. Rundungsfehlern nie als Fließkommazahl sondern immer als (Long) Integer gespeichert werden (Bsp.: $9,99 als 9990)
*   eine solche Speicherung hilft vor allem bei Rabattaktionen (halber Preis) und Umrechnungen
*   kann auch für andere Daten angewendet werden, solange alle Beteiligten dieselben Einheiten verwenden und die Genauigkeit nicht reduziert wird
*   da eh eine API verwendet wird / verwendet werden sollte bekommt der Anwender davon nichts mit
*   das Mischen verschiedener Währungen kann pauschal verboten oder erlaubt sein (dann alles erstmal sammeln, "Money Bag")
*   kann ignoriert oder über Regeln erfaßt werden (Allocator, bestimmt für jede Berechnung das gewünschte Rundungsverhalten)
*   für Wandlungen zwischen den Währungen empfiehlt sich ein eigenes Converter Object (kapselt Umrechnung)
*   sollte in DB als Embedded Value gespeichert werden (ein Feld für Betrag, eines für Währung)
*   **Special Case:** Unterklasse mit Verhalten für vordefinierte Sonderfälle
*   Beispiel: Wie soll beim Wert Null für Objekt "Kunde" reagiert werden kein Kunde? Unbekannter Kunde?
*   Special Case könnte jeweils passendes Objekt statt einfach nur "Null" zurückliefern
*   **Service Stub:** Löst Abhängigkeiten beim Testen durch Dummy-Objekte
*   vor allem für Abhängigkeiten zu Fremdsystemen (z.B. Wechselkurs-Rechner, Steuersätze) nützlich, in (lokalen) Tests werden Fremdsysteme durch lokale Mock-Objekte ersetzt
*   Gateway bzw. Interfaces machen es leicht, zwischen Fremdsystem und Stub zu wechseln
*   **Asynchronous Completion Token**: minimale Information, wie mit einer Response/Message umzugehen ist, besonders bei verschiedenen Datentypen und asynchronen Abfragen nützlich
*   **Service Locator:** Kapselt JNDI-Lookup, Objekte nicht direkt ablegen, jeder Komponententyp hat dabei eine Factory (ähnlich zum Lookup-Pattern = Service, der alle (verteilten) Services erreichbar macht ohne das ein ESB oder Broadcast eingerichtet werden muß)
*   **Transfer/Value Object:** Remote oder lokal, kapselt Nutzdaten zum Datenaustausch zwischen Methoden
*   **Chain of Responsibility:** manchmal kann ein Request von mehreren Komponenten/Objekten verarbeitet werden (sollte dann seriell verarbeitet werden)
*   **Visitor:** trennt einen Algorithmus von einer Struktur, ähnlich dem **Command-Pattern**
*   Ergänzt Operationen bei existierenden Objekte ohne Änderungen an den Klassen
*   Emulierung von Multimethods, ist z.B. in Closure direkt enthalten
*   **Template View:** definierte Marker werden bei Laufzeit/Compilierung durch dynamischen Code ersetzt
*   vermischt Design und Logik, macht Seiten schwer pflegbar (besonders für Nicht-Programmierer), kaum testbar, Exceptions kaum zu erkennen, anfällig für Code-Duplizierung, dynamisches Verhalten (Bedingungen, Schleifen) oft möglich aber unsauber
*   besser eine eigene Helper-Klasse zwischen Anwendungslogik und View nutzen
*   **Transform View:** rendert jedes Datenelement einzeln aus dem Model
*   transformiert Metadaten (meist via XSLT) in HTML
*   geht im Gegensatz zu Template View von der Datenquelle aus
*   macht vor allem bei (vielen) vorhandenen XML-Daten Sinn, ist plattformübergreifend
*   **Two-Step-View:** Domain-Daten werden in zwei Schritten verarbeitet:
	1.  Wandlung in XML
	2.  Konvertierung via XSLT in HTML
*   macht nur Sinn, wenn viele Seiten mit ähnlichem Layout vorhanden sind (und in einem Rutsch überarbeitet werden sollen)
*   ziemlich hoher Entwicklungsaufwand, heutzutage sinnvoller über CSS umsetzbar
*   **State Machine:** weniger Pattern als Beschreibung für zustands-/regelbasierte Systeme
*   vermeidet ellenlange switch-Anweisungen oder ständige if/else-Verschachtelungen
*   löst Abhängigkeiten zwischen Zuständen auf, evtl. haben die Zustände kaum Gemeinsamkeiten
*   **Workflow:** Anwendung wird in zustandslose Services/Prozesse aufgeteilt
*   Workflow-Engine (z.B. BPEL) ruft diese Services auf > SOA
*   unterscheidet zwischen Prozessen (werden in Komponenten isoliert) und Services, Nachteil und Vorteil zugleich
*   leicht konfigurierund erweiterbar, fördert die Wiederverwendung von Komponenten
*   **Frameworks:** sammeln verschiedene Klassen die zusammenhängenden Zweck verfolgen
*   Unterschied zu Library: Framework basiert auf Callbacks (Reaktion)
*   Generische Frameworks sind meist sehr komplex
*   **Workflow-Management-System (WMS)**: System, das mit Hilfe von Software auf Workflow Engines Prozesse definiert, erzeugt und steuert
*   WMS regeln Dienste, die "außen" erreichbar sind und spiegeln i.d.R. Geschäftsprozesse wider
*   WMS arbeiten häufig mit (automatisierbar verarbeitbaren) Stammdaten und Vorgängen
*   typische Funktionen von WMS: Grafische Modellierung von Prozessen und deren Parameter, Aufruf von Fremdsystemen, Administrationskomponente, Protokollierung über Berichte

## Hintergrund: Grundprinzipien agiler Entwicklung (minimal ergänztes agiles Manifest)

*   agile Entwicklung benennt oft keinen expliziten Architekten, er begleitet das Projekt statt v.a. Aufbauarbeit zu leisten (Unterschied zum V-Modell)
*   Individuen und Interaktionen sind wichtiger als Prozesse und Werkzeuge
*   Funktionierende Software ist wichtiger als umfassende Doku - z.B. Use Cases nicht (nur) in langen Dokumenten festhalten sondern besser (auch) visualisieren
*   Austausch mit dem Kunden ist wichtiger als verhandelte Verträge
*   Veränderungen akzeptieren statt einem festen Plan zu folgen
*   der Kunde soll möglichst jederzeit zufrieden sein (funktionierende Software so früh und regelmäßig wie möglich liefern, zumindest alle X Wochen)
*   auch im Laufe der Entwicklung sind veränderte Anforderungen zu akzeptieren
*   agile Prozesse fördern nachhaltige Entwicklung, alle Beteiligten sollten ihre Aufgaben in fixen Intervallen umsetzen können
*   Teams organisieren sich selbst und tauschen sich regelmäßig aus, sie versuchend dabei stets, ihre Effizienz zu steigern
*   Einfache Lösungen sind stets zu bevorzugen, während der gesamten Entwicklung immer auf technische Exzellenz und gutes Design achten
*   das Team braucht eine angemessene Umgebung und Support, Management, PL und Entwickler sollten im 
*   Projekt auf einer Ebene (täglich) zusammenarbeiten
*   Informationsaustausch geschieht am besten durch direkte (face-to-face) Kommunikation
*   Funktionierende Software ist der wichtigste Gradmesser des Erfolgs (also immer noch besser "do it right" statt "do it fast")

## Hintergrund: Minifesto (gekürzt)

*   Befolge das Pareto-Prinzip (mit 20% Aufwand 80% der Lösung erzielen)
*   Minimalismus heißt nicht Dinge zu tun, sondern die wichtigen Dinge zuerst in Angriff zu nehmen
*   Strebe nicht sofort nach Perfektion: Finde zunächst eine funktionierende Lösung, dann eine gute, dann die beste
*   Verwirf alte/schlechte Lösungen und beginne von vorn ("killing the baby"), lerne schnell durch Versagen
*   Lege zuerst Grundlagen fest und folge beim Entwurf dem Top-Down-Prinzip
*   Halte alles so einfach wie möglich und vermeide Komplexität wo immer es geht

## Hintergrund: Das OSI-Modell

*   Schicht 1 (Physical – z.B. Ethernet): überträgt Bits
*   Schicht 2 (Data Link – z.B. Ethernet): Fehlererkennung und Korrektur
*   Schicht 3 (Network – z.B. IP): Bestimmt Route zwischen Sender und Empfänger
*   Schicht 4 (Transport – z.B. TCP): Teilt Nachrichten in Pakete, garantiert die Übertragung
*   Schicht 5 (Session – z.B. HTTP): Dialogkontrolle, Synchronisation, Beispiel: HTTP
*   Schicht 6 (Presentation – z.B. HTTP): Struktur und Semantik
*   Schicht 7 (Application – z.B. HTTP): Sonstige Protokolle zur Verfügung stellen