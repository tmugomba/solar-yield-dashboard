# ☀️ Solar Yield Dashboard

A live, single-file solar PV monitoring dashboard — modelled on real inverter-monitoring platforms (SolarEdge, Solis, Fronius) — that turns live weather data into a real-time production model for any location.

**[Live demo →](https://tmugomba.github.io/solar-yield-dashboard/)** https://tmugomba.github.io/solar-yield-dashboard/

![Status](https://img.shields.io/badge/status-complete-brightgreen) ![Stack](https://img.shields.io/badge/stack-HTML%2FCSS%2FJS-f2b705)

---

## What it does

Enter (or geolocate to) any location and the dashboard pulls live and forecast weather data to model a solar PV system's output in real time — no backend, no build step, no API key required.

- **Live system flow diagram** — sun → array → inverter → home/grid, animated in sync with modelled power output
- **KPI cards** — power right now, energy produced today, live irradiance, CO₂ avoided
- **Today's production chart** — toggle between instantaneous **power (kW)** and cumulative **energy (kWh)**, with a clear split between actual (solid) and forecast (dashed) hours
- **Production calendar** — pick any date range and see modelled output, using real historical weather for past dates, live forecast for the next ~16 days, and last year's same dates as an estimate beyond that
- **System config** — system size (typeable or slider, 1–10,000 kWp), performance ratio, and orientation (tilt/azimuth, with presets for optimal/flat roof/east/west or fully custom), all feeding the model live
- **Regional tab** — city-by-city Nova Scotia comparison, a full interactive Canada solar resource map, and notable Canadian solar companies
- **Components tab** — an interactive anatomy diagram of a grid-tied solar system, hover-linked to explainer cards for each part
- **Savings tab** — a year-by-year payback calculator (not a simple linear formula) with an Advanced mode covering financing, inflation, panel degradation, maintenance, and inverter replacement
- **Resources tab** — curated links for going further

## Data sources

- **[Open-Meteo](https://open-meteo.com/)** — live conditions, hourly forecast, and historical archive weather (geocoding, forecast, and archive APIs), free and keyless
- **Natural Resources Canada (NRCan)** solar resource maps — long-term average irradiance by province, used for the regional comparison and Canada solar map (static reference data, not live)

## How the model works

Power (kW) = system size (kWp) × (live irradiance ÷ 1000 W/m²) × performance ratio × orientation factor

Orientation factor uses a simplified cosine model relative to tilt-vs-latitude and azimuth-vs-true-south — not a full transposition model (e.g. HDKR/Perez) — so it's a solid illustrative estimate rather than a bankable production forecast. Energy figures integrate that formula across hourly irradiance values. Full caveats are documented inline in the dashboard itself.

## Tech

Single HTML file — HTML, CSS, and vanilla JavaScript, with [Chart.js](https://www.chartjs.org/) for charts. No framework, no build step, no dependencies beyond a CDN script tag. Deployed as a static site via GitHub Pages.

## Run it locally

Just open `index.html` in a browser — or serve it locally if you prefer:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

---

## About the author

**Tendekai Mugomba** — Electrical engineering student building data-driven tools for the renewable energy sector, with hands-on solar PV analytics experience.

- LinkedIn: [linkedin.com/in/tendekai-mugomba](https://www.linkedin.com/in/tendekai-mugomba)
- GitHub: [github.com/tmugomba](https://github.com/tmugomba)
