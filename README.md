# Smart Lake Flood Forecaster

**Live demo:** https://shawarmawithgarlicsauce.github.io/itpm-project/

A proof of concept for the "Innovation Sprint" deliverable of a TFB3033 IT Project Management group project (September 2026 trimester). The project designs a Smart Lake Monitoring System for a 4-acre recreational lake in Malaysia.

The innovation is a flash-flood forecaster that runs on the lake's edge gateway (a Raspberry Pi). It predicts the water level 3 hours ahead from rainfall and level history, so the park team and the Department of Environment are warned before the lake overflows. Because the model runs on site, the warning still works when a thunderstorm cuts the 4G link.

## What the demo shows

- A live hydrograph: the last 6 hours of measured water level and rainfall, plus a 3-hour forecast with an error band.
- Buttons that start a thunderstorm or a monsoon downpour, and one that cuts the 4G link.
- Forecast alerts issued before the level reaches the warning (130 cm) and flood (145 cm) lines, alongside the threshold alerts a basic system would raise, with the warning time gained.
- Store-and-forward during outages: readings and alerts are buffered on the gateway and sent when the link returns.

## How the model works

A linear model predicts the change in water level every 5 minutes from:

- rain in the current 5 minutes,
- rain over the last hour,
- rain 1 to 3 hours ago,
- the current level, which sets the spillway and outlet outflow.

It is first fitted by least squares to 30 days of archived readings. It then updates itself after every new reading with recursive least squares, so it adapts as the lake's behaviour changes. The 3-hour forecast runs the model forward, assuming the current rain intensity tapers off with a 30-minute half-life.

## Notes

- All data is simulated by a water-balance model of the lake and a 26 ha park catchment. No real sensor data is used.
- Everything is a single `index.html` file with no build step and no dependencies apart from Google Fonts.
