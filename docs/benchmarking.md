# Benchmarking Methodology

## Dimensions

### 1. Data Efficiency
Measure bytes downloaded per day and per update.

### 2. Route Quality
Compare route time and safety against top commercial solutions.

### 3. Extreme Event Prediction
Validate detection accuracy for storms, rogue waves, icebergs, microbursts.

### 4. Computational Efficiency
Test on Raspberry Pi: inference time, memory usage, battery impact.

## Test Methods

### Data Efficiency
- Controlled comparison: same route, same weather data
- Satellite simulation: throttle to Iridium (2-5 KB/s) and Starlink (50-100 KB/s) speeds
- Offline performance: cache 7 days of forecasts, measure degradation

### Route Quality
- Head-to-head: same conditions against PredictWind, SailGrib WR, qtVlm
- Historical replay: use archived race data, compare against actual winners
- Synthetic scenarios: Gulf Stream crossing, Southern Ocean storms, Cape Horn, Doldrums, Iceberg Alley
- Monte Carlo: 1000+ simulations with forecast noise (10%, 20%, 30% error)

### Extreme Event Prediction
- Storm detection: historical storm tracks (NOAA, ECMWF)
- Rogue wave prediction: wave buoy data (NOAA, MetOffice)
- Iceberg detection: satellite imagery (SAR, optical), AIS tracking
- Microburst detection: high-resolution wind data, Doppler radar

### Computational Efficiency
- Hardware tests: Raspberry Pi 4/5, Jetson Nano
- Algorithm complexity: scale with waypoints, forecast length, resolution
- Battery tests: measure Wh per update
