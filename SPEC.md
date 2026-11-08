# SPEC.md · Stadtteilbibliothek Nord

Quelle: Meeting 1 mit der Leiterin Petra Lorenz (Demo, 12 Nachrichten). Zu jeder Regel steht die Nachricht, aus der sie stammt.

## Entitäten

| Entität | Attribute |
|---|---|
| Buch | isbn, titel, autor, erscheinungsjahr |
| Exemplar | exemplar_nr, buch → Buch, medientyp (Buch, Spiel), status (verfügbar, verliehen, vorgemerkt) |
| Leser | leser_nr, name, geburtsdatum, ausweis_gueltig_bis |
| Ausleihe | ausleihe_id, leser → Leser, exemplar → Exemplar, ausgeliehen_am, faellig_am, zurueck_am |
| Gebühr | gebuehr_id, ausleihe → Ausleihe, betrag, bezahlt |
| Vormerkung | vormerkung_id, leser → Leser, buch → Buch, vorgemerkt_am |
| Mitarbeiter | name, rolle (Fest, Ehrenamt) |

## Beziehungen

- Buch 1:n Exemplar
- Leser n:m Exemplar über Ausleihe
- Ausleihe 1:0..1 Gebühr
- Leser 1:n Vormerkung n:1 Buch

## Business Rules

- **BR1** Leihfrist 21 Tage, Spiele 7 Tage (Nachricht 2, 7)
- **BR2** 50 Cent pro Tag Verzug, höchstens 10 € je Ausleihe, Kinder unter 14 zahlen nichts (Nachricht 4, 5)
- **BR3** Höchstens 10 Exemplare gleichzeitig je Leser (Nachricht 6)

## Widersprüche

- **W1** „Wir verleihen nur Bücher“ (Nachr. 3) vs. Spiele (Nachr. 7) → aufgelöst über `medientyp`
- **W2** „Wir sind zu dritt“ vs. Ehrenamtliche im Bücherbus → aufgelöst über `rolle`

## Prioritäten

1. Ausleihe und Rückgabe (v1)
2. Gebühren (v1)
3. Vormerkung (später)

## Offene Fragen

- Veranstaltungen mit Anmeldung (Meeting 2)
