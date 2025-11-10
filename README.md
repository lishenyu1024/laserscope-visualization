# LaserScope: Interactive Visualization and Analysis of Aircraft Laser Incidents

An interactive data visualization dashboard built with [Observable Framework](https://observablehq.com/framework/) that explores laser incidents targeting aircraft in the United States. This project provides comprehensive insights into temporal patterns, geographical distribution, aircraft characteristics, and safety implications of laser attacks on aviation.

## 🎯 Overview

This visualization analyzes FAA laser incident reports from 2020, examining when, where, and how laser attacks occur. The dashboard features interactive charts that allow users to explore incident patterns across different states, altitude ranges, and time periods.

## ✨ Features

### Interactive Visualizations

1. **Interactive Scatter Plot (Time vs. Altitude)**
   - Hover over data points to reveal detailed incident information
   - Uses `Plot.pointer` and `Generators.input()` for real-time data inspection
   - Filterable by state and altitude range

2. **Temporal Trend Analysis**
   - Visualizes laser incidents by time of day
   - Reveals peak incident hours (evening and late night)
   - Highlights low-light period concentration

3. **Geographical Distribution**
   - State-by-state comparison of laser incidents
   - Identifies hotspots (California leads in incidents)
   - Multi-state filtering capability

4. **Aircraft Altitude Analysis**
   - Distribution of incidents across altitude ranges
   - Focuses on critical safety zones below 5,000 feet
   - Highlights takeoff/landing phase vulnerability

5. **Laser Color Distribution**
   - Analysis of laser colors used in incidents
   - Green laser dominance (99% of incidents)

6. **Injury Occurrence Analysis**
   - Rare but critical safety events
   - Injury rate statistics and patterns

### Key Insights

- **Peak Times**: Incidents concentrate during evening hours and late night when laser visibility increases
- **Critical Altitude**: Most incidents occur below 5,000 feet during takeoff and landing phases
- **Geographic Hotspot**: California experiences the highest number of laser incidents
- **Color Preference**: Green lasers dominate (99% of all incidents)
- **Safety Impact**: While injuries are rare (20 out of 6,852 incidents), they represent serious threats to aviation safety

## 🚀 Getting Started

### Prerequisites

- Node.js >= 18
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd aircraft-laser-incidents-visualization-main
```

2. Navigate to the Framework app directory:
```bash
cd hello-framework
```

3. Install dependencies:
```bash
npm install
```

### Running the Application

Start the local development server:
```bash
npm run dev
```

Then visit [http://localhost:3000](http://localhost:3000) to view the dashboard.

### Building for Production

Build the static site:
```bash
npm run build
```

Deploy to Observable:
```bash
npm run deploy
```

## 📁 Project Structure

```
hello-framework/
├── src/
│   ├── components/
│   │   └── timeline.js          # Timeline visualization component
│   ├── data/
│   │   ├── Laser_Report_2020.xlsx  # FAA laser incident data (Excel)
│   │   ├── events.json          # Static event data
│   │   └── launches.csv.js      # Data loader for launches
│   ├── index.md                 # Home page
│   └── viz.md                   # Main visualization dashboard
├── observablehq.config.js       # Framework configuration
├── package.json                 # Dependencies and scripts
└── README.md                    # This file
```

## 🛠️ Technology Stack

- **[Observable Framework](https://observablehq.com/framework/)** - Web framework for data visualization
- **[Observable Plot](https://observablehq.com/plot/)** - JavaScript library for data visualization
- **D3.js** (via Observable Plot) - Data manipulation and visualization
- **d3-dsv** - CSV/TSV parsing
- **d3-time-format** - Time formatting utilities

## 📊 Data Source

The visualization uses data from the **FAA Laser Reports** dataset (2020). The dataset includes:

- Date and time of incidents
- Flight ID and aircraft type
- Altitude and airport information
- Laser color
- Injury occurrence
- Geographic location (state)

**Data Inspiration**: [FAA Laser Reports Data](https://observablehq.com/@observablehq/faa-laser-reports-data?collection=@observablehq/datasets)

## 🎨 Interactive Features

### State Filtering
Select multiple states from a checkbox list to compare laser incident patterns across different regions.

### Altitude Range Slider
Adjust the altitude range filter to focus on specific flight phases (e.g., takeoff/landing vs. cruising altitude).

### Pointer Interaction
Hover over data points in the scatter plot to see detailed information about individual incidents, including:
- State and airport location
- Altitude
- Laser color
- Injury status

## 📈 Usage

1. **Select States**: Use the checkbox controls to select one or more states to analyze
2. **Adjust Altitude**: Use the range slider to filter incidents by altitude
3. **Explore Charts**: Navigate through different visualizations to understand various aspects of laser incidents
4. **Interact**: Hover over data points in the scatter plot to see detailed incident information

## 🔍 Analysis Highlights

- **Temporal Patterns**: Laser incidents peak during low-light periods (evening and late night)
- **Geographic Concentration**: California leads in laser incidents, followed by Florida and Texas
- **Safety Zones**: Critical incidents occur primarily below 5,000 feet during takeoff and landing
- **Color Dominance**: Green lasers account for 99% of all incidents
- **Injury Rate**: Approximately 0.3% of incidents result in injuries (20 out of 6,852)

## 📝 Notes

- Time zone differences may affect temporal analysis across different regions
- The visualization focuses on incidents from 2020
- Most incidents are visually disruptive rather than physically harmful, but concentration during critical flight phases demands attention

## 🤝 Contributing

This project was created as part of a data visualization course assignment. Contributions and improvements are welcome!

## 📄 License

This project uses publicly available FAA data. Please refer to the original data source for licensing information.

## 🙏 Acknowledgments

- Data provided by the Federal Aviation Administration (FAA)
- Built with Observable Framework and Plot
- Inspired by the [Observable Datasets collection](https://observablehq.com/@observablehq/curated-datasets)
