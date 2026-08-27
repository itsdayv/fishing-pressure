# Fishing Pressure Table

A zero-backend GitHub Pages site that accepts a pasted weather JSON report and generates a pressure table.

## Logic

- Ignores `current.time` and `current.pressure_msl`.
- Uses `hourly.time[0]` / `hourly.pressure_msl[0]` as TIME 0.
- Uses hourly indices 0, 2, 4, ... 24.
- Labels those rows TIME 0, 2, 4, ... 24.
- Converts hPa to inHg using the standard conversion factor.
- Displays PRESSURE to 2 decimal places.
- CHANGE is the difference between consecutive converted inHg values, displayed to 2 decimals.
- TIME 0 gets a dash for CHANGE.

## GitHub Pages

1. Create a GitHub repository.
2. Upload `index.html`.
3. Go to **Settings → Pages**.
4. Set deployment to the repository's main branch and root folder.
5. Save. GitHub will publish the page.
