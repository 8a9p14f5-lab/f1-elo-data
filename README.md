# F1 ELO Data

Scraped race data from [statsf1.com](https://statsf1.com) covering the **2021 Bahrain Grand Prix → 2026 Barcelona-Catalunya Grand Prix**.

## Structure

```
data/
  2021.json
  2022.json
  2023.json
  2024.json
  2025.json
  2026.json
```

## Per-race fields (per driver entry)

| Field | Description |
|---|---|
| `finishing_position` | Final race position (null if DNF/DNS) |
| `status` | Finished / DNF / DNS / Not Classified / DSQ |
| `dnf_reason` | Text reason if DNF |
| `dnf_fault` | driver / mechanical / unknown / null |
| `laps_completed` | Laps completed |
| `points_scored` | Championship points scored |
| `gap_to_winner_seconds` | Gap to winner in seconds (classified finishers) |
| `grid_position` | Starting grid position |
| `qualifying_time` | Best qualifying lap time |
| `gap_to_pole_seconds` | Gap to pole in seconds |
| `pct_off_pole` | % off pole time |
| `positions_gained` | Grid position minus finish position |
| `had_fastest_lap` | Boolean |
| `fastest_lap_time` | Fastest lap time |
| `fastest_lap_number` | Lap on which fastest lap was set |
| `laps_led` | Total laps led |
| `teammate` | Teammate name |
| `total_classified_finishers` | Total classified finishers in race |

## ELO System (5 pillars + composite)

| ELO | Weight | Description |
|---|---|---|
| ELO 1 — Pure Position | 20% | Round-robin head-to-heads on finishing position |
| ELO 2 — Points-Weighted | 20% | K-factor scales with position gap |
| ELO 3 — Grid-Adjusted | 25% | Win signal boosted/penalised by qualifying delta |
| ELO 4 — Teammate H2H | 15% | Driver vs direct teammate only |
| ELO 5 — Performance/Dominance | 20% | Gap-based, laps led, % off pole |

**Composite** = (ELO1×0.20) + (ELO2×0.20) + (ELO3×0.25) + (ELO4×0.15) + (ELO5×0.20)

## Weekend events (each updates ELOs independently)
1. Sprint Qualifying (sprint weekends only)
2. Sprint Race (sprint weekends only)
3. Qualifying
4. Grand Prix
