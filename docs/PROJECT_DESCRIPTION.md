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

**Target:** 100-1000x reduction compared to existing solutions (1-10 MB/day)

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
│ - Infoclimat API │ - Isochrone     │ - Forecast│
│ - Delta Encoding │   Algorithm     │   Error  │
│ - Region Filter  │ - Hierarchical  │   Modeling│
│ - Cache          │   A*            │ - Extreme│
│                 │ - Incremental   │   Event  │
│                 │   Updates       │   Detection│
└─────────────────┴─────────────────┴─────────┘
```

### **Data Pipeline**
- **Input:** Infoclimat GRIB2 weather data (wind, waves, currents, pressure)
- **Processing:** Delta encoding, region filtering, temporal downsampling
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
1. **Freewinds.world** - Primary showcase (Golden Globe Race 2026 virtual race)
2. **qtVlm** - Open-source integration for offline testing
3. **Custom Simulator** - Full control for edge cases

### **Methodology**
- **Head-to-Head Racing:** Compare against PredictWind, SailGrib, qtVlm
- **Historical Replay:** Test with past race data (GGR 2022, Vendée Globe 2020)
- **Synthetic Scenarios:** Gulf Stream crossing, Southern Ocean storms, Cape Horn
- **Monte Carlo:** 1000+ simulations with perturbed weather data

---

## **🤝 Partnerships**

### **Infoclimat**
- **Role:** Primary weather data provider
- **Data:** GRIB2 files, wave models, real-time forecasts
- **Status:** Partnership established

### **Freewinds.world**
- **Role:** Primary testing and showcase platform
- **Platform:** Golden Globe Race 2026 virtual race
- **Status:** Registration submitted

---

## **📅 Roadmap**

### **Phase 1: Foundation**
- Set up Infoclimat API access
- Implement data pipeline (delta encoding, region filtering)
- Develop baseline routing engine

### **Phase 2: Core Features**
- Integrate Infoclimat data
- Implement safety constraints
- Develop extreme event detection

### **Phase 3: Optimization**
- Optimize for edge deployment (Raspberry Pi)
- Fine-tune AI models
- Validate with real-world testing

### **Phase 4: Showcase**
- Deploy on Freewinds.world
- Publish benchmark results
- Engage sailing community

---

## **📚 Additional Documentation**

- [Technical Architecture](ARCHITECTURE.md)
- [Benchmarking Methodology](BENCHMARKING.md)
- [API Documentation](API.md)
- [User Guide](USER_GUIDE.md)

---

## **🔗 Related Resources**

- [Infoclimat](https://www.infoclimat.fr)
- [Freewinds.world](https://freewinds.world)
- [Golden Globe Race 2026](https://goldengloberace.com)

---

**© 2026 LowDataSail**
