# GDS Sorter

A small static web app for comparing postal facilities against the airport mail office (APTMO/TMO) that handles their air routing.

Pick two facilities and the app tells you whether they share an airport (and therefore an IATA air route), or which airports each one goes through.

## Features

- **Searchable pickers** — type to filter facilities by name, group, or IATA code, with keyboard navigation.
- **Match / no-match result** — green when both facilities route via the same airport, red when they don't, with the route details spelled out.
- **No duplicate picks** — the facility already selected on one side is excluded from the other.
- **Light/dark theme** — follows the OS preference by default, with a toggle in the header; the choice is remembered.
- **Haptic feedback** — short vibration on supported devices.

## Running it

No build step and no dependencies to install. Either:

```sh
open index.html          # or just double-click it
```

or serve the folder:

```sh
python3 -m http.server
# then visit http://localhost:8000
```

## Project structure

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles, data, and logic |
| `data.json` | Dataset as groups of facilities |
| `data.csv` | Same dataset flattened, one row per facility |
| `list.jpeg` | Photo of the printed source sheet the data was transcribed from |

## Data

The source is an NSH airside routing sheet containing **81 facilities across 7 groups**:

| Group | Airport | IATA | Facilities |
| --- | --- | --- | --- |
| DELHI APTMO | Indira Gandhi International Airport | DEL | 30 |
| APTMO MUMBAI | Chhatrapati Shivaji Maharaj International Airport | BOM | 21 |
| GUWAHATI TMO | Lokpriya Gopinath Bordoloi International Airport | GAU | 8 |
| SHAMSHABAD TMO | Rajiv Gandhi International Airport | HYD | 6 |
| KOLKATA APTMO | Netaji Subhas Chandra Bose International Airport | CCU | 5 |
| BENGALURU NSH | Kempegowda International Airport | BLR | 7 |
| AHMEDABAD TMO | Sardar Vallabhbhai Patel International Airport | AMD | 4 |

Each facility belongs to exactly one group, and a group maps to a single airport/IATA code — so the comparison is simply "do both facilities resolve to the same IATA code?"

> **Note:** `index.html` currently embeds its own copy of the data so it works when opened directly from disk. If you change the data, update `index.html`, `data.json`, and `data.csv` together.

## Tech

- Vanilla JavaScript — no framework, no bundler
- [Bootstrap 5.3](https://getbootstrap.com/) via CDN for styling and theming
- Single-file deployment; suitable for GitHub Pages
