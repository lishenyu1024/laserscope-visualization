# LaserScope: Interactive Visualization and Analysis of Aircraft Laser Incidents

This is an [Observable Framework](https://observablehq.com/framework/) application for visualizing aircraft laser incident data from the FAA.

## Quick Start

### Installation

Install the required dependencies:

```bash
npm install
```

### Development

Start the local preview server:

```bash
npm run dev
```

Then visit [http://localhost:3000](http://localhost:3000) to preview your app.

### Production Build

Build your static site:

```bash
npm run build
```

This generates the `./dist` directory with the production-ready site.

### Deploy

Deploy your app to Observable:

```bash
npm run deploy
```

## Project Structure

```
.
├── src
│   ├── components
│   │   └── timeline.js           # Timeline visualization component
│   ├── data
│   │   ├── Laser_Report_2020.xlsx  # FAA laser incident data (Excel format)
│   │   ├── events.json           # Static event data
│   │   └── launches.csv.js        # Data loader for launches
│   ├── index.md                  # Home page
│   └── viz.md                    # Main visualization dashboard
├── .gitignore
├── observablehq.config.js        # App configuration file
├── package.json
└── README.md
```

## Key Files

**`src/viz.md`** - Main visualization dashboard featuring:
- Interactive scatter plots with pointer interaction
- Temporal trend analysis
- Geographical distribution charts
- Altitude analysis
- Laser color distribution
- Injury occurrence statistics

**`src/index.md`** - Home page with project overview

**`src/components/timeline.js`** - Reusable timeline visualization component

**`src/data/Laser_Report_2020.xlsx`** - Primary data source containing FAA laser incident reports

**`observablehq.config.js`** - Framework configuration including:
- App title
- Sidebar navigation
- Theme settings
- Custom head content

## Command Reference

| Command           | Description                                              |
| ----------------- | -------------------------------------------------------- |
| `npm install`     | Install or reinstall dependencies                        |
| `npm run dev`     | Start local preview server                               |
| `npm run build`   | Build your static site, generating `./dist`              |
| `npm run deploy`  | Deploy your app to Observable                            |
| `npm run clean`   | Clear the local data loader cache                        |
| `npm run observable` | Run commands like `observable help`                      |

## Features

### Interactive Visualizations

- **Plot.pointer()** - Enables hover interactions on scatter plots
- **Generators.input()** - Captures pointer events for data inspection
- **Inputs.checkbox()** - Multi-state filtering
- **Inputs.range()** - Altitude range filtering

### Data Loading

The app uses Observable Framework's data loaders to process Excel files:

```javascript
const wb = await FileAttachment("data/Laser_Report_2020.xlsx").xlsx()
const lasers = wb.sheet(0, { headers: true })
```

## Dependencies

- `@observablehq/framework` - Observable Framework core
- `d3-dsv` - CSV/TSV parsing utilities
- `d3-time-format` - Time formatting functions

## Learn More

- [Observable Framework Documentation](https://observablehq.com/framework/getting-started)
- [Observable Plot Documentation](https://observablehq.com/plot/)
- [Framework Examples](https://github.com/observablehq/framework/tree/main/examples)
