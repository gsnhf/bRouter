# BRouter Running Profile

Dieses Repository enthält ein BRouter-Fußprofil für Laufstrecken.

## Dateien

- `running.brf`: Laufprofil für BRouter und bikerouter.de.

## Ziel des Profils

Das Profil soll:

- laufbare Wege bevorzugen,
- Hauptstraßen möglichst vermeiden,
- moderate Oberflächen- und Höhenunterschiede berücksichtigen,
- eine realistischere Laufzeit auf bikerouter.de anzeigen.

## Wichtiger Parameter

Die angezeigte Zeit wird in BRouter bei Fußprofilen im Wesentlichen über `maxSpeed` bestimmt.
Im Profil wird `maxSpeed` daher aus der gewünschten Pace abgeleitet:

```brf
assign running_pace = 5
assign maxSpeed divide 71.5 running_pace
```

Beispiele:

- `5` entspricht ungefähr `5:00 min/km`
- `5.5` entspricht ungefähr `5:30 min/km`
- `4.75` entspricht ungefähr `4:45 min/km`

Der Faktor `71.5` ist eine Kalibrierung für das Fußmodell von BRouter, damit die auf bikerouter.de angezeigte Zeit näher an der realen Laufzeit liegt.

## Weitere Schalter

- `allow_steps`: Treppen erlauben oder vermeiden
- `allow_ferries`: Fähren erlauben oder vermeiden
- `wet_mode`: unbefestigte Wege bei Nässe stärker bestrafen
- `consider_elevation`: Höhenmeter in der Routenwahl berücksichtigen

## Nutzung auf bikerouter.de

1. [running.brf](running.brf) im Profil-Editor öffnen oder hochladen.
2. `running_pace` auf die gewünschte Zielpace setzen.
3. Route neu berechnen.

Wenn sich die angezeigte Zeit nicht ändert, liegt es meist daran, dass das Profil im Browser noch nicht neu geladen wurde. In dem Fall das Profil erneut einfügen und die Route vollständig neu berechnen.

## Hinweise zur Kalibrierung

- Wenn die ETA zu hoch ist, `running_pace` kleiner setzen, zum Beispiel von `5.0` auf `4.9`.
- Wenn die ETA zu niedrig ist, `running_pace` größer setzen.
- Änderungen an `road_penalty`, `surface_penalty` und den Höhenkosten beeinflussen primär die Routenwahl, nicht direkt die angezeigte Zeit.