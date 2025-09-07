# Architekturüberblick

## Systemkontext

TODO: Beschreibe kurz den Systemkontext

Das System ist Microservice-basiert, die Kommunikation erfolgt über Google Pub/Sub (Events) und REST-APIs. Die
Persistenz erfolgt in mehreren Postgres-Datenbanken.

## Architekturdiagramm

![Architekturdiagramm](image.png)

## Architekturprinzipien

### Event Driven Architecture (EDA)

- **Kernidee:** Die Businesslogik wird durch Ereignisse (Events) gesteuert, die bereits stattgefunden haben. Komponenten
  sind über Events entkoppelt.
- **Vorteile:** Starke Entkopplung, bessere Änderbarkeit und Erweiterbarkeit, neue Consumer können jederzeit hinzugefügt
  werden.
- **Event Carried State Transfer:** Events enthalten alle relevanten Daten, damit Consumer nicht synchron beim Producer
  nachfragen müssen.
- **Commands vs. Events:**
  - **Event:** Fakt in der Vergangenheit, kann nicht abgelehnt werden, hat 0-n Consumer.
  - **Command:** Aufforderung, kann abgelehnt werden, hat einen Adressaten.
- **Patterns:**
  - **Transactional Outbox:** Events werden zusammen mit der Entität in einer Outbox gespeichert und asynchron
    versendet.
  - **Inbox/Resequencing:** Jeder Service hat eine Inbox, um Events in der richtigen Reihenfolge zu verarbeiten.
- **Idempotenz:** Events müssen idempotent verarbeitet werden, d.h. wiederholte Verarbeitung darf keine Seiteneffekte
  haben.
- **Read/Write Model & Eventual Consistency:** Verschiedene Datenbanken für verschiedene Usecases, Read-Model kann
  temporär inkonsistent sein.

**Commands** lösen Aktionen gezielt aus und können abgelehnt werden, während **Events** vergangene Fakten darstellen und
nicht abgelehnt werden können.

### Clean & Hexagonale Architektur

- **Dependency Rule:** Abhängigkeiten zeigen immer nach innen (zur Domain).
- **Ports & Adapter:** Ports definieren die API, Adapter implementieren die Ports und kapseln externe Technologien.
- **Best Practices:**
  - Domain-Objekte enthalten keine Framework-Annotationen.
  - DTOs für Kommunikation über Adapter verwenden.
  - Interface Segregation Principle bei Ports.
  - Dependency Injection für lose Kopplung.
- **Packagestruktur:** Klare Trennung von Domain, Usecases, Adaptern (Input/Output), Modellen.
- Strikte Trennung von Domain, Use Cases, Adaptern (Input/Output) und Konfiguration.
- Adapter kapseln externe Technologien (REST, Pub/Sub, JPA).
- Die Geschäftslogik ist unabhängig von Frameworks und Infrastruktur, was Testbarkeit und Wartbarkeit erhöht.

### Domain Driven Design (DDD)

- **Ubiquitous Language:** Gemeinsame Sprache zwischen Entwicklern und Fachexperten, die sich im Code widerspiegelt.
- **Kernkonzepte:**
  - **Entity:** Hat Identität, ist veränderlich, wird über ID verglichen.
  - **Value Object:** Identitätslos, immutable, wird über alle Attribute verglichen.
  - **Aggregate Root:** Kontrolliert Konsistenz und Zugriff auf enthaltene Entities/Value Objects.
  - **Repository:** Schnittstelle zum Laden/Speichern von Aggregates.
  - **Domain Service:** Geschäftslogik, die nicht zu einer einzelnen Entity gehört.
  - **Bounded Context:** Klare Abgrenzung von Domänenmodellen in Modulen/Packages.

## Komponentenübersicht

TODO: alle Komponenten aufführen

- **backend-verarbeitung1:** ...
- **backend-verarbeitung1:** ...
- **shared-domain-models:** Eine gemeinsame Bibliothek, die kanonische Domain-Modelle (z.B. ...) enthält, die
  von mehreren Services genutzt werden.
- **umsystem-simulation:** Simulation externer Systeme, Event-Integration
- **frontend:** Angular-UI, REST-Kommunikation mit allen relevanten Services

## Teststrategie

Die Teststrategie umfasst vier Stufen:

- **Usecase bzw. Komponententests:** fachliche Komponententests mittels Cucumber der fachlichen Logik (Domain, Use
  Cases) mit Fake-Adaptern.
- **Adapter Integrationstests**: technische Integrationstests mittels JUnit der Input-Adapter (z.B. REST-Controller)
  gegen die fachliche Logik und der Output-Adapter (z.B. Datenbank, Pub/Sub.
- **End 2 End bzw. Systemintegrationtests** fachliche End-to-End-Tests mittels Cucumber mit produktiven Adaptern und
  Infrastruktur im e2e Verzeichnis.

Ziel ist eine hohe Testabdeckung und Absicherung der Kernfunktionalität auf allen Ebenen. Die Tests werden überwiegend
mit Cucumber als Blackbox-Tests umgesetzt.

## Praxisbeispiele

### Beispiel: DDD-Konzepte in Java

```java
// Entity
public class Kunde {
    private final KundenId id;
    private String name;
    // equals/hashCode nur über id
}

// Value Object
public record Adresse(String strasse, String stadt) {
}

// Aggregate Root
public class Bestellung {
    private final BestellungId id;
    private final List<BestellPosition> positionen;

    public void fuegePositionHinzu(...) { ...}
}

// Repository
public interface BestellungRepository {
    Bestellung findById(BestellungId id);

    void save(Bestellung bestellung);
}

// Domain Service
public class BestellungVerarbeitungsService {
    public void verarbeiteBestellung(Bestellung bestellung) { ...}
}
```

### Beispiel: Packagestruktur Hexagonale Architektur

```
de.mein.projekt.meinservice/
  adapters/
    input/
      MeinController.java
    output/
      MeinRepositoryImpl.java
  domain/
    model/
      MeinAggregate.java
    outputports/
      MeinRepository.java
    usecases/
      MeinUseCase.java
    MeinUseCaseImpl.java
```
