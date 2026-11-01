# Fishing Pressure Table

A zero-backend GitHub Pages site that takes the coordinates of your fishing spot, pulls the barometric pressure forecast from [Open-Meteo](https://open-meteo.com/), and builds a 24-hour pressure table so you can see whether pressure is rising or falling.

## How to use it

1. Open [Google Maps](https://maps.google.com/) and right-click the spot where you intend to fish.
2. Click the latitude/longitude coordinates to copy them.
3. Paste them into the coordinates box on the page.
4. Click **Get Pressure Data**. The page requests the data directly from Open-Meteo and fills in the table.
5. Click **Copy Table** if you want to paste the results somewhere else.

### Accepted coordinate formats

- Decimal degrees: `39.539394, -77.911750`
- Google Maps degrees/minutes/seconds (DMS): `40°47'00.2"N 73°53'01.1"W`

## What the table shows

| Column | Meaning |
| --- | --- |
| **TIME (ET)** | Forecast hour, shown in Eastern Time |
| **PRESSURE (inHg)** | Mean sea level pressure, converted from hPa, to 2 decimals |
| **Trend** | Change from the previous row: ↑ rising (red), ↓ falling (green), — no change |

## Logic

- Requests `hourly.pressure_msl` for the next 25 hours (`forecast_hours=25`) with the timezone set to `America/New_York`.
- Uses hourly indices 0, 2, 4, ... 24, which gives 13 rows in 2-hour steps.
- Converts hPa to inHg using the factor `0.0295299830714`.
- The change is calculated from the unrounded inHg values and then displayed to 2 decimals. This is intentional, so a displayed change can differ by 0.01 from subtracting the two displayed pressures.
- The first row has no change, so it shows a dash.
- If the page doesn't get at least 25 hourly entries, it shows an error instead of a table.

## Data source

Pressure data comes from the Open-Meteo forecast API (`https://api.open-meteo.com/v1/forecast`), called directly from the browser. No API key or backend is needed. To use the GFS/HRRR model instead, swap the endpoint in `index.html` to `https://api.open-meteo.com/v1/gfs`.

