---
theme: dashboard
title: hw05-laser_report_add Plotpointer and Generators
toc: false
---

# Laser data 🚀

I plan to use this dataset to visualize messages in laser incidents targeting aircraft. The data includes information: the date and time of each incident, flight ID, aircraft type, altitude, airport, laser color, injury occurrence, and location. 

Using this data, I can to create visualizations that show:

1.Temporal trends – how incidents vary by date or time of day.

2.Geographical distribution – which state experience more laser incidents.

3.Aircraft characteristics – the types of aircraft and altitudes most affected.

4.Incident details – patterns in laser color and whether any injuries occurred.

5.Injury occurrence – its laser turely hurts?

By visualizing these aspects, I hope to provide insights into when and where laser incidents are most frequent, and which aircraft are most impacted and finally get 10/10.

This document demonstrates the use of Plot.pointer and Generators.input() to enable inspection of individual laser incident data points.

<!-- Load and transform the data -->

```js
 
// Inputs.table((await FileAttachment("data/Laser_Report_2020.xlsx").xlsx()).sheet(0, { headers: true }))
const wb = await FileAttachment("data/Laser_Report_2020.xlsx").xlsx()
```

```js
const lasers = wb.sheet(0, { headers: true })
```

```js
Inputs.table(lasers)
```
## 🔍Hw04-interaction- Explore Laser by State
Now it's the difference from 03 to 04: Use the dropdown below to select a specific state and a altitude range. i set 6 state to observe the laser patterns for that state. you can also change the state cuz i know we only care our home. 

Key Insight: When altitude > 50,000 feet, there's no significant change - most incidents happen below this range during takeoff and landing phases.

```js
const selectedStates = view(Inputs.checkbox(
  ["California", "Florida", "Texas", "New York", "Arizona","Maine"],
  {
    label: "Select States to Display:",
    value: ["California", "Florida", "Texas"]
  }
));
```

```js
const altitudeRange = view(Inputs.range([0, 1400000], {
  label: "Select Altitude Range (feet):",
  step: 500,
  value: 1000
}));
```

## 🔍Hw05-interaction- Scatter Plot: Time vs. Altitude

This chart plots the time of day an incident occurred against its altitude. Move your mouse over a point to reveal its specific details.

```js
const chart = Plot.plot({
  title: "Interactive Laser Incident Details (Time vs. Altitude)",
  subtitle: "Filter: " + selectedStates.join(", ") + " | Altitude ≤ " + altitudeRange.toLocaleString() + " ft",
  marks: [
    // Base dots
    Plot.dot(
      lasers.filter(d => selectedStates.includes(d.State) && d.Altitude <= altitudeRange), 
      {
        x: "Incident Time", 
        y: "Altitude",
        stroke: "State",
        fill: "State",
        r: 3,
        opacity: 0.5
      }
    ),
    // Pointer dot for highlighing and data capture
    Plot.dot(
      lasers.filter(d => selectedStates.includes(d.State) && d.Altitude <= altitudeRange),
      Plot.pointer({
        x: "Incident Time",
        y: "Altitude",
        fill: "red",
        r: 8,
        opacity: 0.8
      })
    )
  ],
  x: {label: "Hour of Day (24-hour format)"},
  y: {label: "Altitude (feet)", domain: [0, altitudeRange]},
  width: 800,
  height: 500
});

// Capture the output of the chart's pointer interaction
const x = Generators.input(chart);
```
```js
const message = x
  ? `Selected Incident: ${x.State} at ${x.Airport} | Altitude: ${x.Altitude.toLocaleString()} ft | Color: ${x["Laser Color"]} | Injury: ${x.Injury}`
  : "Mouse over a point on the chart to see incident details."
```

🔎 Incident Detail Selector

${message}

${display(chart)}


1. Temporal Trend (Incidents by Time of Day)
```js
Plot.plot({
  title: "⏰ Laser Incidents Peak During Evening Hours",
  subtitle: `📊 ${lasers.filter(d => selectedStates.includes(d.State) && d.Altitude <= altitudeRange).length} incidents | 🏔️ Altitude ≤ ${altitudeRange.toLocaleString()}ft | 🗺️ States: ${selectedStates.join(", ")}`,
  marks: [
    Plot.barY(
      lasers.filter(d => 
        selectedStates.includes(d.State) && 
        d.Altitude <= altitudeRange
      ),
      Plot.binX({y: "count"}, {x: "Incident Time", thresholds: 24, fill: "steelblue"})
    ),
    Plot.text([18], [50], {text: ["🌆 Evening Peak"], frameAnchor: "top", fontSize: 12, fill: "red"}),
    Plot.text([2], [30], {text: ["🌙 Late Night"], frameAnchor: "top", fontSize: 12, fill: "red"})
  ],
  x: {label: "Hour of Day (24-hour format)"},
  y: {label: "Number of Laser Incidents"},
  width: 700,
  height: 400
})
```
MY Analysis:

A magical thing happened - everyone's time was different. I think it has something to do with the time difference.

The chart clearly shows laser attacks concentrate during low-light periods. Incidents peak around midnight, decrease to their lowest point in the afternoon, then rise again in the evening when laser visibility increases dramatically.



2. Geographical distribution – incidents by state

```js
Plot.plot({
  title: "🗺️ Geographic Hotspots: California Leads in Laser Incidents",
  subtitle: `📊 State comparison at ≤ ${altitudeRange.toLocaleString()}ft | Filtered by altitude and selected states`,
  marks: [
    Plot.barY(
      lasers.filter(d => 
        selectedStates.includes(d.State) && 
        d.Altitude <= altitudeRange
      ),
      Plot.groupX({y: "count"}, {x: "State", sort: {x: "-y"}, fill: "orange"})
    )
  ],
  x: {label: "State", tickRotate: -20},
  y: {label: "Number of Incidents"},
  width: 700,
  height: 400
})

```

My analysis:
we can see less state right now, much more clear.

and CA cause most incidents.

3. Aircraft characteristics – incidents by altitude

```js
Plot.plot({
  title: "🛬 Critical Safety Zone: Most Incidents Below 5,000 Feet",
  subtitle: `⚠️ Altitude distribution showing takeoff/landing risk | Current filter: ${altitudeRange.toLocaleString()}ft`,
  marks: [
    Plot.barY(
      lasers.filter(d => selectedStates.includes(d.State)),
      Plot.binX({y: "count"}, {
        x: "Altitude", 
        thresholds: [0,5000,10000,20000,40000], 
        fill: "lightblue"
      })
    )
  ],
  x: {label: "Altitude Range (ft)"},
  y: {label: "Number of Incidents"},
  width: 700,
  height: 400,
  marginLeft: 60,
  marginBottom: 50
})
```
My analysis:
seems airplane in different state contents same altitude.

Most incidents cluster below 5,000 feet, during takeoff and landing phases. This concentration occurs because:

a. Proximity: Aircraft are closer to populated areas
b. Vulnerability: Lower altitudes mean slower speeds and greater susceptibility
c. Visibility: Lasers have limited effective range at higher altitudes


4. Incident details – laser color distribution
```js
Plot.plot({
  title: "🎨 Green Laser Dominance: 99% of All Incidents",
  subtitle: `📈 Color patterns across selected states | Altitude ≤ ${altitudeRange.toLocaleString()}ft`,
  marks: [
    Plot.barY(
      lasers.filter(d => 
        selectedStates.includes(d.State) && 
        d.Altitude <= altitudeRange
      ),
      Plot.groupX({y: "count"}, {x: "Laser Color", fill: "green"})
    )
  ],
  x: {label: "Laser Color", tickRotate: -45},
  y: {label: "Number of Incidents"},
  width: 700,
  height: 400,
  marginLeft: 60,
  marginBottom: 50
})
```
My analysis:
no difference after state, people loves green.

While the overwhelming majority of incidents don't result in injuries, the few that do represent serious threats to aviation safety that demand attention.

5. Injury occurrence – rare but important

```js
Plot.plot({
  title: "🚨 Injury Analysis: Rare but Critical Safety Events",
  subtitle: `📋 ${lasers.filter(d => selectedStates.includes(d.State) && d.Altitude <= altitudeRange && d.Injury === "Yes").length} injuries out of ${lasers.filter(d => selectedStates.includes(d.State) && d.Altitude <= altitudeRange).length} total incidents`,
  marks: [
    Plot.barY(
      lasers.filter(d => 
        selectedStates.includes(d.State) && 
        d.Altitude <= altitudeRange
      ),
      Plot.groupX({y: "count"}, {x: "Injury", fill: "Injury"})
    )
  ],
  x: {label: "Injury Reported"},
  y: {label: "Number of Incidents"},
  width: 500,
  height: 300
})
```

My analysis:
While most laser incidents don't cause injury, no:yes=6832:20,


Conclusion:

While most laser incidents are visually disruptive rather than physically harmful, the concentration during critical flight phases demands proactive safety measures, public awareness campaigns, and continued enforcement against laser misuse.

reference:

Data source: FAA Laser Reports 

Data Inspired by: https://observablehq.com/@observablehq/faa-laser-reports-data?collection=@observablehq/datasets
