---
theme: dashboard
title: Atlas
toc: true
---

## Plots in cards

<!-- <div class="hero">
  <h1>Politica</h1>
  <h2>Welcome to your new app! Edit&nbsp;<code style="font-size: 90%;">src/index.md</code> to change this page.</h2>
  <a href="https://observablehq.com/framework/getting-started">Get started<span style="display: inline-block; margin-left: 0.25rem;">↗︎</span></a>
</div> -->

<div class="grid grid-cols-2" style="grid-auto-rows: 504px;">
  <div class="card">${
    resize((width) => Plot.plot({
      title: "Your awesomeness over time 🚀",
      subtitle: "Up and to the right!",
      width,
      y: {grid: true, label: "Awesomeness"},
      marks: [
        Plot.ruleY([0]),
        Plot.lineY(aapl, {x: "Date", y: "Close", tip: true})
      ]
    }))
  }</div>
  <div class="card">${
    resize((width) => Plot.plot({
      title: "How big are penguins, anyway? 🐧",
      width,
      grid: true,
      x: {label: "Body mass (g)"},
      y: {label: "Flipper length (mm)"},
      color: {legend: true},
      marks: [
        Plot.linearRegressionY(penguins, {x: "body_mass_g", y: "flipper_length_mm", stroke: "species"}),
        Plot.dot(penguins, {x: "body_mass_g", y: "flipper_length_mm", stroke: "species", tip: true})
      ]
    }))
  }</div>
</div>

---

## Rocket launches 🚀

<!-- Load and transform the data -->

```js
const launches = FileAttachment("data/launches.csv").csv({typed: true});
```

<!-- A shared color scale for consistency, sorted by the number of launches -->

```js
const color = Plot.scale({
  color: {
    type: "categorical",
    domain: d3.groupSort(launches, (D) => -D.length, (d) => d.state).filter((d) => d !== "Other"),
    unknown: "var(--theme-foreground-muted)"
  }
});
```
### Cards with big numbers
<!-- Cards with big numbers -->

<div class="grid grid-cols-4">
  <div class="card">
    <h2>United States 🇺🇸</h2>
    <span class="big">${launches.filter((d) => d.stateId === "US").length.toLocaleString("en-US")}</span>
  </div>
  <div class="card">
    <h2>Russia 🇷🇺 <span class="muted">/ Soviet Union</span></h2>
    <span class="big">${launches.filter((d) => d.stateId === "SU" || d.stateId === "RU").length.toLocaleString("en-US")}</span>
  </div>
  <div class="card">
    <h2>China 🇨🇳</h2>
    <span class="big">${launches.filter((d) => d.stateId === "CN").length.toLocaleString("en-US")}</span>
  </div>
  <div class="card">
    <h2>Other</h2>
    <span class="big">${launches.filter((d) => d.stateId !== "US" && d.stateId !== "SU" && d.stateId !== "RU" && d.stateId !== "CN").length.toLocaleString("en-US")}</span>
  </div>
</div>

### Plot of launch history
<!-- Plot of launch history -->

```js
function launchTimeline(data, {width} = {}) {
  return Plot.plot({
    title: "Launches over the years",
    width,
    height: 300,
    y: {grid: true, label: "Launches"},
    color: {...color, legend: true},
    marks: [
      Plot.rectY(data, Plot.binX({y: "count"}, {x: "date", fill: "state", interval: "year", tip: true})),
      Plot.ruleY([0])
    ]
  });
}
```

<div class="grid grid-cols-1">
  <div class="card">
    ${resize((width) => launchTimeline(launches, {width}))}
  </div>
</div>

### Plot of launch vehicles
<!-- Plot of launch vehicles -->
```js
function vehicleChart(data, {width}) {
  return Plot.plot({
    title: "Popular launch vehicles",
    width,
    height: 300,
    marginTop: 0,
    marginLeft: 50,
    x: {grid: true, label: "Launches"},
    y: {label: null},
    color: {...color, legend: true},
    marks: [
      Plot.rectX(data, Plot.groupY({x: "count"}, {y: "family", fill: "state", tip: true, sort: {y: "-x"}})),
      Plot.ruleX([0])
    ]
  });
}
```
<div class="grid grid-cols-1">
  <div class="card">
    ${resize((width) => vehicleChart(launches, {width}))}
  </div>
</div>

Data: Jonathan C. McDowell, [General Catalog of Artificial Space Objects](https://planet4589.org/space/gcat)


## Next steps

Here are some ideas of things you could try…

<div class="grid grid-cols-4">
  <div class="card">
    Chart your own data using <a href="https://observablehq.com/framework/lib/plot"><code>Plot</code></a> and <a href="https://observablehq.com/framework/files"><code>FileAttachment</code></a>. Make it responsive using <a href="https://observablehq.com/framework/javascript#resize(render)"><code>resize</code></a>.
  </div>
  <div class="card">
    Create a <a href="https://observablehq.com/framework/project-structure">new page</a> by adding a Markdown file (<code>whatever.md</code>) to the <code>src</code> folder.
  </div>
  <div class="card">
    Add a drop-down menu using <a href="https://observablehq.com/framework/inputs/select"><code>Inputs.select</code></a> and use it to filter the data shown in a chart.
  </div>
  <div class="card">
    Write a <a href="https://observablehq.com/framework/loaders">data loader</a> that queries a local database or API, generating a data snapshot on build.
  </div>
  <div class="card">
    Import a <a href="https://observablehq.com/framework/imports">recommended library</a> from npm, such as <a href="https://observablehq.com/framework/lib/leaflet">Leaflet</a>, <a href="https://observablehq.com/framework/lib/dot">GraphViz</a>, <a href="https://observablehq.com/framework/lib/tex">TeX</a>, or <a href="https://observablehq.com/framework/lib/duckdb">DuckDB</a>.
  </div>
  <div class="card">
    Ask for help, or share your work or ideas, on our <a href="https://github.com/observablehq/framework/discussions">GitHub discussions</a>.
  </div>
  <div class="card">
    Visit <a href="https://github.com/observablehq/framework">Framework on GitHub</a> and give us a star. Or file an issue if you’ve found a bug!
  </div>
</div>

## Conclusion

.

.

.

.

<style>

.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: var(--sans-serif);
  margin: 4rem 0 8rem;
  text-wrap: balance;
  text-align: center;
}

.hero h1 {
  margin: 1rem 0;
  padding: 1rem 0;
  max-width: none;
  font-size: 14vw;
  font-weight: 900;
  line-height: 1;
  background: linear-gradient(30deg, var(--theme-foreground-focus), currentColor);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero h2 {
  margin: 0;
  max-width: 34em;
  font-size: 20px;
  font-style: initial;
  font-weight: 500;
  line-height: 1.5;
  color: var(--theme-foreground-muted);
}

@media (min-width: 640px) {
  .hero h1 {
    font-size: 90px;
  }
}

</style>
