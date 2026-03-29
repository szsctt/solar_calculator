# Solar Battery Calculator

Simulates battery performance and financial payback using a year of NEM12 smart-meter interval data.

## Scripts

| Script | Purpose |
|---|---|
| `solar_calculator.py` | Core tool — prints Year 1 and multi-year payback summary |
| `find_max_battery.py` | Binary-searches for the largest battery that pays back within N years |
| `plot_export_vs_battery.py` | Plots grid export, import, cost, and grid-import days vs battery size |
| `plot_opportunity_cost.py` | Compares buying a battery vs investing the same cash upfront |

## Quick start

```bash
# Activate environment
micromamba activate /path/to/envs/solar_calculator

# Basic payback analysis
python solar_calculator.py --battery-size 24 --battery-cost 14000

# Opportunity cost comparison over 15 years
python plot_opportunity_cost.py --battery-size 24 --battery-cost 14000 --years 15 --investment-return 0.10

# Battery sweep plots
python plot_export_vs_battery.py
```

See `run.sh` for example invocations with real quotes.

## Key defaults

| Parameter | Default |
|---|---|
| Energy rate | $0.3524/kWh |
| Daily supply charge | $1.4287/day |
| Feed-in tariff | $0.03/kWh (not inflation-adjusted) |
| Energy inflation | 3%/yr (applies to import and supply only) |
| Battery reserve | 20% |
| Round-trip efficiency | 90% |

## Model assumptions

- NEM12 data: 288 × 5-minute intervals per day, channels B1 (solar), E1 (consumption), E2 (controlled load)
- E2 (hot water) is removed from the grid and redistributed to a daytime solar window (10 am–2 pm)
- Battery charges from solar surplus; discharges to cover house load; no overnight export
- Opportunity cost model: Scenario A invests annual bill savings from year 1; Scenario B compounds the battery purchase price as a pure investment
