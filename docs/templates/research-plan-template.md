# Analyse-Plan: [ANALYSE_THEMA]

## Metadaten

- **Story ID**: MPRJ-nnn
- **Erstellt**: YYYY-MM-DD
- **Status**: ENTWURF | IN_BEARBEITUNG | ABGESCHLOSSEN
- **Geschätzter Aufwand**: X Story Points / Stunden
- **Analyst**: [Agent/Entwickler Name]
- **Typ**: Analyse-/Research-Story

## Geschäftskontext

### Analyseziel

[Klare Beschreibung WARUM diese Analyse benötigt wird und welchen Geschäftswert sie liefert]

### Analysebereich

[Detaillierte Beschreibung WAS analysiert werden muss, einschließlich Grenzen und Einschränkungen]

### Erfolgskriterien

- [ ] EK1: [Spezifisches, messbares Kriterium für Analyseabschluss]
- [ ] EK2: [Spezifisches, messbares Kriterium für Analyseabschluss]
- [ ] EK3: [Spezifisches, messbares Kriterium für Analyseabschluss]

## Technischer Analysekontext

### Zu untersuchende Architekturbereiche

- **Primäre Domäne**: [Welche Domäne/Bounded Context zu analysieren]
- **Verwandte Komponenten**: [Liste der zu untersuchenden Komponenten]
- **Externe Abhängigkeiten**: [Liste externer Systeme zu berücksichtigen]
- **Zu prüfende Dokumentation**:
    - [ ] @/docs/ARCHITECTURE.md
    - [ ] @/docs/[RELEVANTE_DOC].md
    - [ ] Confluence: [Link zu relevanten Seiten]

### Forschungsfragen

- **Frage 1**: [Spezifische Forschungsfrage, die beantwortet werden soll]
- **Frage 2**: [Spezifische Forschungsfrage, die beantwortet werden soll]
- **Frage 3**: [Spezifische Forschungsfrage, die beantwortet werden soll]

## Analysemethodik

### Phase 1: Ist-Zustand-Analyse

```
ANWEISUNG: Systematische Bestandsaufnahme bestehender Implementierungen
```

- [ ] **Schritt 1.1**: Alle relevanten Services/Komponenten identifizieren
- [ ] **Schritt 1.2**: Bestehende Patterns und Implementierungen katalogisieren
- [ ] **Schritt 1.3**: Aktuelle Fehlerbehandlungsansätze dokumentieren
- [ ] **Schritt 1.4**: Abhängigkeiten und Integrationspunkte kartieren
- [ ] **Schritt 1.5**: Lücken und Inkonsistenzen identifizieren

### Phase 2: Code-Basis-Untersuchung

```
ANWEISUNG: Tiefgreifende Analyse der Implementierungsdetails
```

- [ ] **Schritt 2.1**: Kern-Implementierungspatterns analysieren
- [ ] **Schritt 2.2**: Fehlerszenarien und -behandlung dokumentieren
- [ ] **Schritt 2.3**: Technical Debt und Probleme identifizieren
- [ ] **Schritt 2.4**: Wiederverwendbare Patterns und Anti-Patterns extrahieren
- [ ] **Schritt 2.5**: Architekturdiagramme des Ist-Zustands erstellen

### Phase 3: Dokumentations-Research

```
ANWEISUNG: Umfassende Prüfung bestehender Dokumentation
```

- [ ] **Schritt 3.1**: Interne Dokumentation prüfen (@/docs/)
- [ ] **Schritt 3.2**: Confluence-Seiten und Wikis analysieren
- [ ] **Schritt 3.3**: Inline-Code-Dokumentation untersuchen
- [ ] **Schritt 3.4**: Dokumentationslücken identifizieren
- [ ] **Schritt 3.5**: Best Practices aus Dokumentation sammeln

### Phase 4: Externes Research

```
ANWEISUNG: Industriestandards und Best Practices recherchieren
```

- [ ] **Schritt 4.1**: Industrie-Best-Practices recherchieren
- [ ] **Schritt 4.2**: Framework-spezifische Empfehlungen prüfen
- [ ] **Schritt 4.3**: Ähnliche Open-Source-Implementierungen analysieren
- [ ] **Schritt 4.4**: Benchmarks und Metriken sammeln
- [ ] **Schritt 4.5**: Anwendbare Patterns dokumentieren

### Phase 5: Gap-Analyse

```
ANWEISUNG: Ist-Zustand mit Best Practices vergleichen
```

- [ ] **Schritt 5.1**: Aktuelle Patterns gegen Best Practices mappen
- [ ] **Schritt 5.2**: Verbesserungsmöglichkeiten identifizieren
- [ ] **Schritt 5.3**: Erkenntnisse nach Impact und Aufwand priorisieren
- [ ] **Schritt 5.4**: Ziel-Architektur definieren
- [ ] **Schritt 5.5**: Verbesserungs-Roadmap erstellen

### Phase 6: Empfehlungsentwicklung

```
ANWEISUNG: Umsetzbare Empfehlungen erstellen
```

- [ ] **Schritt 6.1**: Standardisierte Ansätze definieren
- [ ] **Schritt 6.2**: Implementierungsleitfäden erstellen
- [ ] **Schritt 6.3**: Validierungsstrategien entwerfen
- [ ] **Schritt 6.4**: Follow-up Stories/Tasks identifizieren
- [ ] **Schritt 6.5**: Entscheidungs-Framework erstellen

### Phase 7: Dokumentation & Deliverables

```
ANWEISUNG: Umfassende Research-Deliverables erstellen
```

- [ ] **Schritt 7.1**: Analyseergebnisse-Dokument erstellen
- [ ] **Schritt 7.2**: Implementierungsleitfäden entwickeln
- [ ] **Schritt 7.3**: Architekturdokumentation aktualisieren
- [ ] **Schritt 7.4**: Confluence-Wissensseiten erstellen
- [ ] **Schritt 7.5**: Follow-up JIRA Stories definieren
- [ ] **Schritt 7.6**: Erkenntnisse an Stakeholder präsentieren

## Analyse-Qualitätsprüfungen

### Nach jeder Phase

- [ ] Alle Forschungsfragen für diese Phase adressiert
- [ ] Erkenntnisse mit Belegen dokumentiert
- [ ] Patterns und Beispiele gesammelt
- [ ] Architekturauswirkungen verstanden
- [ ] Voraussetzungen für nächste Phase erfüllt

### Definition of Done

- [ ] Alle Erfolgskriterien erfüllt
- [ ] Forschungsfragen umfassend beantwortet
- [ ] Ist-Zustand vollständig dokumentiert
- [ ] Best Practices identifiziert und dokumentiert
- [ ] Umsetzbare Empfehlungen bereitgestellt
- [ ] Follow-up Stories definiert
- [ ] Wissen an Team transferiert
- [ ] JIRA Story aktualisiert

## Analyse-Ausführungsanweisungen

### Verarbeitung dieses Plans

1. Gesamten Analyseplan vor Beginn lesen
2. Phasen sequenziell ausführen
3. Alle Schritte einer Phase vor Übergang zur nächsten abschließen
4. Erkenntnisse kontinuierlich während der Analyse dokumentieren
5. Bei Blockern EINE spezifische Frage stellen und auf Antwort warten
6. Checkbox-Status beim Fortschritt aktualisieren
7. Abschluss jeder Phase melden

### Dokumentationsstandards für Analysen

```
Für JEDEN Befund:
1. Mit Belegen dokumentieren (Code-Snippets, Links)
2. Nach Wichtigkeit und Impact kategorisieren
3. Mit Architekturprinzipien verknüpfen
4. Umsetzbare Empfehlungen bereitstellen
5. Beispiele wo anwendbar einschließen
```

## Fortschrittsverfolgung

### Aktueller Status

- **Aktuelle Phase**: [Phase X]
- **Aktueller Schritt**: [Schritt X.Y]
- **Blocker**: [Liste aller Blocker]
- **Wichtige Erkenntnisse**: [Liste der wichtigsten Erkenntnisse bisher]

### Abschluss-Log

| Phase   | Abgeschlossen | Dauer | Wichtige Erkenntnisse |
|---------|---------------|-------|-----------------------|
| Phase 1 | ⬜            | -     | -                     |
| Phase 2 | ⬜            | -     | -                     |
| Phase 3 | ⬜            | -     | -                     |
| Phase 4 | ⬜            | -     | -                     |
| Phase 5 | ⬜            | -     | -                     |
| Phase 6 | ⬜            | -     | -                     |
| Phase 7 | ⬜            | -     | -                     |

## Analyse-Deliverables

### Hauptergebnisse

- [ ] **Ist-Zustand-Analysebericht**: Umfassender Überblick bestehender Implementierungen
- [ ] **Best-Practices-Leitfaden**: Empfohlene Patterns und Ansätze
- [ ] **Gap-Analyse**: Unterschiede zwischen Ist- und Soll-Zustand
- [ ] **Implementierungs-Roadmap**: Priorisierter Verbesserungsplan
- [ ] **Follow-up Stories**: Spezifische JIRA Stories für Implementierung

### Nebenergebnisse

- [ ] **Architektur-Diagramme**: Visuelle Darstellung von Ist- und Ziel-Zustand
- [ ] **Code-Beispiele**: Konkrete Implementierungspatterns
- [ ] **Entscheidungs-Framework**: Leitlinien für künftige Entscheidungen
- [ ] **Wissensbasis**: Confluence-Seiten mit Analyseergebnissen
