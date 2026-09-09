# Light Router - Project Description

---

## **🎯 Core Objectives**

### **1. Low Data Routing**
Develop a sailing router that operates with **<10 KB/day** data consumption, making it viable for satellite-constrained environments (Iridium, Starlink).

**Key Techniques:**
- Delta encoding (transmit only forecast changes)
- Region filtering (download only route corridor data)
- Temporal downsampling (lower resolution for distant forecasts)
- Predictive caching (pre-fetch likely needed data)

**Target:** 10-50x reduction compared to best existing filtered tools (Saildocs at ~30 KB/request, PredictWind at ~150 KB/day); 1000x+ reduction vs. raw global GRIB downloads

---

### **2. Extreme Event Prediction**
Build robust prediction models to identify and avoid dangerous weather events during circumnavigation.

**Focus Areas:**
- Storm detection and avoidance
- Rogue wave prediction
- Iceberg and shallow water detection
- Sudden wind shifts and microbursts

**Target:** 99%+ safety with early warning systems

---

## **🌍 Use Cases**

### **Primary**
- **Circumnavigation 2027** - Real-world validation in extreme conditions
- **Offshore Racing** - Limited satellite bandwidth scenarios
- **Long-distance Cruising** - Cost-sensitive data usage

### **Secondary**
- **Research Vessels** - Remote operations with intermittent connectivity
- **Autonomous Boats** - Fully automated navigation
- **Commercial Shipping** - Route optimization with safety constraints

---

## **🏗️ Technical Approach**

### **Architecture Overview**
```
┌─────────────────────────────────────────────┐
│              Light Router                     │
├─────────────────┬─────────────────┬─────────┤
│  Data Pipeline   │ Routing Engine  │ AI Layer │
├─────────────────┼─────────────────┼─────────┤
│ - Multi-source     │ - Isochrone     │ - Forecast│
│   Data Pipeline    │   Algorithm     │   Error  │
│ - Delta Encoding   │ - Hierarchical  │   Modeling│
│ - Region Filter    │   A*            │ - Extreme│
│ - Cache            │ - Incremental   │   Event  │
│                    │   Updates       │   Detection│
└─────────────────┴─────────────────┴─────────┘
```

### **Data Pipeline**
- **Input:** Weather data from multiple sources (NOAA GFS, ECMWF IFS, CMEMS for waves/currents; delivered via Saildocs, NOMADS Grib Filter, or direct HTTP)
- **Processing:** Delta encoding, route-aware region filtering, temporal downsampling
- **Output:** Optimized weather data for routing (<10 KB/day)

### **Routing Engine**
- **Base Algorithm:** Hierarchical A* for coarse-to-fine optimization
- **Updates:** Incremental route adjustments as forecasts change
- **Constraints:** Hard constraints for safety (storms, shallow water, icebergs)

### **AI Layer**
- **Forecast Error Modeling:** Learn and compensate for systematic errors
- **Extreme Event Detection:** Identify dangerous patterns in weather data
- **Probabilistic Routing:** Account for forecast uncertainty

---

## **📊 Key Metrics**

| **Category**       | **Metric**               | **Target**          |
|--------------------|--------------------------|---------------------|
| **Data**          | Daily consumption        | <10 KB/day          |
| **Data**          | Per-update consumption   | <5 KB               |
| **Safety**        | Extreme event detection  | 99%+ accuracy        |
| **Safety**        | Route reliability        | 99%+ success rate   |
| **Performance**   | Route quality            | <5% from optimal    |
| **Performance**   | Inference time           | <1 minute            |

---

## **🧪 Validation Strategy**

### **Platforms**
1. **Freewinds.world** - Potential simulation and showcase platform (virtual sailing, route validation)
2. **OpenCPN** - Open source integration for community testing
3. **Custom Simulator** - Full control for edge cases

### **Methodology**
- **Head-to-Head Racing:** Compare against PredictWind, SailGrib, qtVlm
- **Historical Replay:** Test with past race data (GGR 2022, Vendée Globe 2020)
- **Synthetic Scenarios:** Gulf Stream crossing, Southern Ocean storms, Cape Horn
- **Monte Carlo:** 1000+ simulations with perturbed weather data

---

## **🤝 Potential Collaborations**

### **Weather Data Sources**
- **NOAA NOMADS:** Free GFS data with server-side Grib Filter subsetting
- **ECMWF Open Data:** Free 9 km IFS forecasts since October 2025
- **Copernicus Marine Service (CMEMS):** Wave and current data
- **Saildocs:** Email-based GRIB delivery for low-bandwidth scenarios
- **Infoclimat:** Potential primary data provider — GRIB2, wave models, real-time forecasts (not yet contacted)

### **Simulation and Testing**
- **Freewinds.world:** Potential simulation platform for virtual race testing and route validation (not yet contacted)

### **Open Source Community**
- **libweatherrouting:** [https://github.com/dakk/libweatherrouting](https://github.com/dakk/libweatherrouting) — Python routing library
- **OpenCPN Weather Routing:** [https://opencpn.org/OpenCPN/plugins/weatherroute.html](https://opencpn.org/OpenCPN/plugins/weatherroute.html) — Open source isochrone routing
- **SIMROUTE:** [https://github.com/ManelGrifoll/SIMROUTE](https://github.com/ManelGrifoll/SIMROUTE) — A* routing with CMEMS data

---

## **📅 Roadmap**

### **Phase 1: Foundation**
- Set up data access (NOAA NOMADS, ECMWF open data, Saildocs)
- Implement data pipeline (delta encoding, route-aware region filtering)
- Develop baseline routing engine

### **Phase 2: Core Features**
- Integrate weather data sources (NOAA, ECMWF, CMEMS)
- Implement safety constraints
- Develop extreme event detection

### **Phase 3: Optimization**
- Optimize for edge deployment (Raspberry Pi)
- Fine-tune AI models
- Validate with real-world testing

### **Phase 4: Showcase**
- Deploy on Freewinds.world (if collaboration established)
- Publish benchmark results
- Engage sailing community

---

## **📚 Additional Documentation**
- [Objectives](objectives.md)
- [Literature Review](literature-review.md)
- [Meteorological Information Transfer](meteorological-info-transfer.md)
- [Routing Algorithms](routing-algorithms.md)
- [Benchmarking Methodology](benchmarking.md)
- [Market Positioning](market-positioning.md)

---

## **🔗 Related Resources**
- [NOAA NOMADS](https://nomads.ncep.noaa.gov) — Free weather data
- [ECMWF Open Data](https://data.ecmwf.int) — Free since October 2025
- [Copernicus Marine Service](https://marine.copernicus.eu) — Wave and current data
- [Saildocs](http://www.saildocs.com) — Email-based GRIB service
- [Infoclimat](https://www.infoclimat.fr) — Potential data provider
- [Freewinds.world](https://freewinds.world) — Potential simulation platform
- [Golden Globe Race 2026](https://goldengloberace.com) — Starts September 6, 2026

---

**© 2026 LowDataSailing**
