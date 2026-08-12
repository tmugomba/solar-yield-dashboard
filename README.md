# ☀️ Solar Yield Dashboard

A live, single-file solar PV monitoring and financial dashboard — modelled on real inverter-monitoring platforms (SolarEdge, Solis, Fronius) — that turns live weather data into a real-time production model, a residential payback calculator, and a province-by-province solar economics comparison, for any location.

**[Live demo →](https://tmugomba.github.io/solar-yield-dashboard/)**

![Status](https://img.shields.io/badge/status-complete-brightgreen) ![Stack](https://img.shields.io/badge/stack-HTML%2FCSS%2FJS-f2b705)

---

## What it does

Enter (or geolocate to) any location and the dashboard pulls live and forecast weather data to model a solar PV system's output in real time, then layers on financial modelling and provincial comparisons — no backend, no build step, no API key required.

**Dashboard tab**
- Live system flow diagram — sun → array → inverter → home/grid, animated in sync with modelled power output, with a redesigned peaked-roof house icon
- KPI cards — power right now, energy produced today, live irradiance, CO₂ avoided
- Today's production chart — toggle between instantaneous **power (kW)** and cumulative **energy (kWh)**, with a live explanatory note so the very different shapes (bell curve vs. rising S-curve) don't read as a bug
- Production calendar — pick any date range and see modelled output, using real historical weather for past dates, live forecast for the next ~16 days, and last year's same dates as an estimate beyond that
- System config — system size (typeable number input *or* slider, 1–10,000 kWp), performance ratio, and orientation (tilt/azimuth presets or fully custom, with a tooltip explaining what tilt and azimuth mean)

**Regional tab**
- City-by-city Nova Scotia comparison and a full interactive Canada solar resource map
- Notable Canadian solar companies
- Electricity price vs. illustrative utility-scale solar LCOE, by province — a fully editable 13-row table **or** a horizontal bar chart (toggle between the two), with the province matching your Savings-tab selection highlighted in both views

**Components tab**
- An interactive, properly-centered anatomy diagram of a grid-tied solar system, hover-linked to explainer cards for each part

**Savings tab**
- A year-by-year payback calculator (not a simple linear formula), driven by your own **expected annual production** (kWh) rather than a generic provincial default — the provincial irradiance estimate is shown alongside purely for comparison, clearly labelled as such
- **Your solar cost of energy (LCOE)** — a standout hero metric implementing the standard residential LCOE formula (project cost, incentives, loan payments, O&M, discounted energy output over a 25-year system life), compared live against your electricity rate
- Advanced mode covering financing, inflation, panel degradation, maintenance, inverter replacement (with its own highlighted row + footnote in the Excel export), and an editable discount rate for the LCOE figure
- **Export to Excel** — a styled, multi-sheet workbook (KPI summary with an embedded chart image, full inputs list with units, and a year-by-year cash-flow table) generated entirely client-side

**Resources tab**
- Full methodology write-up, including both LCOE formulas (utility-scale and residential) with every variable defined
- Curated links for going further

## Data sources

- **[Open-Meteo](https://open-meteo.com/)** — live conditions, hourly forecast, and historical archive weather (geocoding, forecast, and archive APIs), free and keyless
- **Natural Resources Canada (NRCan)** solar resource maps — long-term average irradiance by province, used for the regional comparison, Canada solar map, and as the (comparison-only) irradiance baseline in the Savings tab

## How the model works

**Power output:**
```
Power (kW) = system size (kWp) × (live irradiance ÷ 1000 W/m²) × performance ratio × orientation factor
```
Orientation factor uses a simplified cosine model relative to tilt-vs-latitude and azimuth-vs-true-south — not a full transposition model (e.g. HDKR/Perez) — so it's a solid illustrative estimate rather than a bankable production forecast.

**Payback & LCOE (Savings tab):** driven by your entered expected annual production, degraded year-over-year, compared against a year-by-year cost stream (upfront cost or loan payments, plus maintenance/inverter replacement), all over a shared 25-year system life. The residential LCOE follows the standard formula — present value of every dollar of cost, divided by present value of every kWh produced — with performance-based incentives and loan-interest tax deductions treated as zero (not typically applicable to Canadian residential solar). Full formula and variable definitions are in the Resources tab.

Full caveats for every figure are documented inline in the dashboard itself, via the small "i" tooltips throughout.

## Tech

Single HTML file — HTML, CSS, and vanilla JavaScript. [Chart.js](https://www.chartjs.org/) for charts, [ExcelJS](https://github.com/exceljs/exceljs) for the styled Excel export. No framework, no build step, both libraries loaded via CDN. Deployed as a static site via GitHub Pages.

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
