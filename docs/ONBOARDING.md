# Onboarding & Lokale Entwicklung

## Architektur-Grundlagen und Best Practices

Die zentralen Architekturprinzipien (Event Driven Architecture, Domain Driven Design, Clean/Hexagonale Architektur) sind
ausschließlich und aktuell in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md:1) dokumentiert.
Bitte konsultiere für Details und weiterführende Informationen dieses Dokument.

---

## Teststrategie & Komponententests

### Teststufen

- **Usecase bzw. Komponententests:** fachliche Komponententests mittels Cucumber der fachlichen Logik (Domain, Use
  Cases) mit Fake-Adaptern.
- **Adapter Integrationstests**: technische Integrationstests mittels JUnit der Input-Adapter (z.B. REST-Controller)
  gegen die fachliche Logik und der Output-Adapter (z.B. Datenbank, Pub/Sub.
- **End 2 End bzw. Systemintegrationtests** fachliche End-to-End-Tests mittels Cucumber mit produktiven Adaptern und
  Infrastruktur im e2e Verzeichnis.

### Vorgehen für neue Features/Adapter

1. **Feature/Usecase als Cucumber-Feature beschreiben.**
2. **Step-Definitionen anlegen und Usecase-Interface erweitern.**
3. **Fake-Implementierungen für Adapter erstellen (Usecase bzw. Komponententest des Usecases).**
4. **Produktive Adapter für Input (R2T) und Output (T2R) implementieren (test first!).**
5. **End-to-End-Test (E2E / SIT) mit echten Adaptern durchführen.**
6. **Tests regelmäßig ausführen und auf allen Stufen grün halten.**

### Praktische Hinweise

- Cucumber und Blackbox-Tests sind Standard für Komponententests.
- Testabdeckung > 80% anstreben, aber nicht jede Funktion auf jeder Stufe doppelt testen.
- Schritt-für-Schritt-Anleitungen für neue Features und Adapter siehe unten.

---

## Praxisbeispiele & HowTos

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

### Beispiel: Schritt-für-Schritt für neue Komponententests

1. **Feature als Cucumber-Feature anlegen**
   (z.B. `src/test/resources/features/meinfeature.feature`)
2. **Step-Definitionen anlegen**
   (z.B. `MeinFeatureSteps.java`)
3. **Usecase-Interface und -Implementierung erweitern**
4. **Fake-Adapter für T2T-Tests erstellen**
5. **Produktive Adapter mittels Adapterintegrationstests implementieren**
6. **E2E Tests schreiben und ausführen**

---

### Beispiel: Erweiterung eines bestehenden Usecases mittels Komponententests

Siehe [howtos/komponententests.md](howtos/komponententests.md)

## Technologiewechsel & Systemaufbau

- **Technologie:** Wechsel auf Microservices, Google Cloud, Pub/Sub, PostgreSQL, Angular, Terraform.
- **Systemaufbau:** Microservices & Module statt Monolith, Events statt Batch, Cloud Run statt JBoss, Apigee statt Tibco
  Mashery.
- **Fachliche Kontexte:** Werden als Bounded Contexts und Module abgebildet.

---

## Weitere Hinweise

- **Commit-Konventionen:** Englisch, Imperativ, KUNDE-Fachbegriffe nicht übersetzen.
- **Trunk Based Development:** Arbeiten auf main, Feature Toggles nutzen, regelmäßig rebasen.
- **Logging:** Log-Nachrichten auf Deutsch, Sätze enden mit Punkt, Log-Level sinnvoll wählen.
- **Testing:** UnitTests benennen, Mocking nur für Services/Komponenten, E2E mit Playwright Assertions.
- **SQL/Hibernate:** Logging über Log-Level, nicht über hibernate.show_sql.

---

Diese Übersicht enthält die wichtigsten Grundlagen, Prinzipien und Praxisbeispiele für die Entwicklung im
KUNDE-Projekt. Für tiefergehende HowTos und Beispiele kann eine eigene Datei im `docs`-Verzeichnis angelegt
werden.

## Umgebung und Instanzen

TODO: Umbebung dokumentieren
(Erste Anfrage kann dauern da Cloud Run erst den Container startet ~30s - 1min)

## Einrichtung lokale Entwicklungsumgebung

### Voraussetzung

Für die lokale Entwicklung, muss die folgende Software installiert sein:

- JDK
- Podman (Docker)
- gcloud CLI

### Installation JDK

Für die Installation des benötigten JDKs kann [SDKMAN](https://sdkman.io/) verwendet werden.
Im Projekt ist eine [.sdkmanrc](.sdkmanrc) hinterlegt.
Das darin definierte JDK kann mit dem folgenden Befehl installiert werden: `sdk env install`

### Setup

Nach der Installation der benötigten Software, die folgenden Schritte ausführen.

#### Annotation Processing

In den IntelliJ Settings unter `"Build, Execution Deployment>Compiler>Annotation Processors"`
`Enable Annotation Processing` aktivieren.

#### Code Style

Wir nutzen zur Code Style Formatierung https://editorconfig.org/. Dazu gibt es jeweils eine Konfiguration für unser
Angular Frontend [.editorconfig](frontend/.editorconfig) und unsere Java Backend
Services [.editorconfig](services/.editorconfig).

##### Einrichtung

1. Intellij EditorConfig Plugin installieren
2. In den Intellij Settings anpassen
   1. Falls vorhanden die Custom Project Code Style Datei löschen `.idea/codeStyles/Project.xml`
   2. Sicherstellen, dass das `Intellij Code Style Default Scheme` mit den Default Einstellungen konfiguriert ist und
      andernfalls diese mit Restore Defaults wiederherstellen, siehe
      auch https://www.jetbrains.com/help/idea/configuring-code-style.html
   3. `Editor>CodeStyle` die Option `Enable EditorConfig Support` aktivieren
   4. `Editor>CodeStyle` als Code Style Scheme `Project` auswählen

#### In GCP einloggen und docker konfigurieren

`gcloud auth login` um sich bei der GCP anzumelden.
`gcloud auth application-default login` um das GCP SDK verwenden zu können.
`gcloud auth configure-docker europe-west3-docker.pkg.dev` um Docker mit dem gcloud credential helper zu konfigurieren,
damit es auf die GCP Container Registry zugreifen kann.

#### Docker Container erstellen und starten

Im Projekt ist eine [docker-compose.yaml](infrastructure/docker-compose.yaml) hinterlegt mit der alle lokal benötigten
Dienste wie z.B. die Datenbank bereitgestellt werden.
Der folgende Befehl startet Docker-Container für die Datenbank, Pub/Sub und den Umsystem-Simulator:

```bash
docker-compose --profile local -f infrastructure/docker-compose.yaml up
```

#### Erster Build

`mvn clean install` um Bibliotheken wie mech-eingang-events zu installieren.

#### 😎 Happy Coding! 😎

## Einzelne Applikation starten

1. Zuerst Docker-Container starten (siehe oben)
2. Applikation starten mit `mvn spring-boot:run -pl :<SERVICE_NAME>`

## Einzelne Applikation testen

1. Zuerst Docker-Container starten (siehe oben)
2. Alle Tests ausführen: `mvn test -pl :<SERVICE_NAME>`
3. Alle Component-Tests ausführen: entsprechende Run Configuration auswählen

Component-Tests verwenden eine Datenbank, die dynamisch über Testcontainers gestartet wird. Um sich damit zu verbinden,
kann die JDBC-URL aus dem Log-Output ausgelesen werden, indem man nach "Container is started" sucht.

## Mehrere Applikationen starten und miteinander integrieren

(Siehe README.md für weitere Hinweise)

---

## Architekturüberblick & Entwicklungsparadigmen

Die zentralen Prinzipien und Patterns zu Event Driven Architecture, Teststrategie, Clean/Hexagonale Architektur und
Domain Driven Design sind ausführlich und aktuell in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md:1) dokumentiert.

Bitte konsultiere für Details und weiterführende Informationen ausschließlich dieses Dokument.

Spezifische Hinweise zum Onboarding und zur lokalen Entwicklung findest du weiterhin in diesem Onboarding-Dokument.

## Best Practices für Entwickler (Auszug aus dem Entwicklerhandbuch)

- **Qualität & Zusammenarbeit**

  - Tests sind Spezifikation. Testgetriebene Entwicklung (TDD) und Pair Programming sind Standard.
  - Wer die Pipeline rot macht, macht sie auch wieder grün (CI/CD).
  - Collective Ownership: Jeder darf und soll Code verbessern.
  - Refactoring ist Pflicht: Hinterlasse Code immer sauberer als vorgefunden.
  - Schreibe langweiligen, gut lesbaren Code ("Keep it boring").

- **DevOps & Workflows**

  - Github Actions steuern Build, Test, Deploy, Release und Destroy.
  - Artefakt-Registries: Dev/Test nutzen eigene Registry, Abnahme/Prod die zentrale KUNDE-Registry.
  - Maven-Konfiguration für neue Submodule beachten (siehe Entwicklerhandbuch für Details).
  - Wichtige Env-Variablen: DOCKER_REGISTRY, ENVIRONMENT_FILE_PREFIX, FOLDER_SERVICE_ACCOUNT, GCP_PROJECT,
    GOOGLE_IMPERSONATE_SERVICE_ACCOUNT.

- **Coding-Guidelines**

  - POJOs: Keine Objekte mit nur null-Properties, leere Listen statt null.
  - JPA: @Entity endet auf Entity, @Embeddable auf Embeddable.
  - Liquibase: TEXT statt VARCHAR(255).
  - Namenskonventionen: Fachbegriffe auf Deutsch, technische Begriffe auf Englisch.
  - Kommentare auf Deutsch, aber nur wenn nötig – sprechende Namen bevorzugen.
  - Sonar: NoSonarIssues im Code deaktivieren.
  - Lombok: Args-Konstruktoren erlaubt, keine Setter/Builder im Domain Model.

- **Frontend**

  - Chrome ist Referenzbrowser, Firefox wird unterstützt.
  - Tooltips für Abkürzungen/Icons, Platzhalter für fehlende Inhalte.
  - Testing mit Spectator und Jest, keine CSS IDs/Classes für Tests.

- **Domain Design**

  - Value Objects als Java Records, immutable.
  - Keine Setter, keine Builder.

- **Git & Commit-Konventionen**

  - Trunk Based Development: Arbeiten auf main, Feature Toggles nutzen, regelmäßig rebasen.
  - Commit Messages auf Englisch im Imperativ, KUNDE-Fachbegriffe nicht übersetzen.

- **Logging**

  - Log Level: DEBUG (Details), INFO (Normalbetrieb), WARN (Ausnahmen), ERROR (Fehler).
  - Log-Nachrichten auf Deutsch, Sätze enden mit Punkt.

- **Testing**

  - UnitTests: Instanz als testee benennen, nur eine Klasse pro Test.
  - Mocking: Nur Services/Komponenten mocken, keine Datenobjekte.
  - E2E: Playwright Assertions nutzen.

- **SQL/Hibernate**
  - Logging über Log-Level, nicht über hibernate.show_sql.
