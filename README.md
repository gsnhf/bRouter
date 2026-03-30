# BRouter Running Profile

This repository contains a BRouter foot profile for running routes.

## Files

- `running.brf`: Running profile for BRouter and bikerouter.de.

## Goal of the Profile

The profile is intended to:

- prefer runnable paths,
- avoid main roads as much as possible,
- account for moderate surface and elevation differences,
- display a more realistic running time on bikerouter.de.

## Important Parameter

For foot profiles in BRouter, the displayed time is determined mainly by `maxSpeed`.
In this profile, `maxSpeed` is therefore derived from the desired pace:

```brf
assign running_pace = 5
assign maxSpeed divide 71.5 running_pace
```

Examples:

- `5` corresponds to approximately `5:00 min/km`
- `5.5` corresponds to approximately `5:30 min/km`
- `4.75` corresponds to approximately `4:45 min/km`

The factor `71.5` is a calibration value for BRouter's foot model so that the time shown on bikerouter.de is closer to actual running time.

## Additional Switches

- `allow_steps`: allow or avoid steps
- `allow_ferries`: allow or avoid ferries
- `wet_mode`: penalize unpaved paths more strongly in wet conditions
- `consider_elevation`: include elevation gain in route selection

## Usage on bikerouter.de

1. Open or upload [running.brf](running.brf) in the profile editor.
2. Set `running_pace` to the desired target pace.
3. Recalculate the route.

Straight line segments (`straight=` in the URL, or the straight-line toggle in BRouter-Web/bikerouter.de) are not controlled by the profile alone. They are requested by the web client or request URL.

This profile now enables `add_beeline`, which helps BRouter output a beeline connection when a start or via point is matched to a more distant road during dynamic range search. That improves off-road cases, but it is not a replacement for explicit straight-line segments.

If the displayed time does not change, the profile usually has not been reloaded in the browser yet. In that case, paste the profile again and fully recalculate the route.

## Calibration Notes

- If the ETA is too high, set `running_pace` lower, for example from `5.0` to `4.9`.
- If the ETA is too low, set `running_pace` higher.
- Changes to `road_penalty`, `surface_penalty`, and the elevation costs primarily affect route selection, not the displayed time directly.