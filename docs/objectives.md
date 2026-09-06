# Core Objectives

*Light Router's two primary goals: Low Data Routing and Extreme Event Prediction*

---

## **🎯 Objective 1: Low Data Routing**

### **Goal**
Develop a sailing router that operates with **<10 KB/day** data consumption, making it viable for **satellite-constrained environments** (Iridium, Starlink).

### **Why It Matters**

#### **The Problem**
Current sailing routers consume **100-1000 KB/day** of data:

| **Tool** | **Data Usage** | **Cost on Iridium** |
|----------|----------------|---------------------|
| PredictWind | 200-500 KB/day | $100-250/day |
| SailGrib WR | 100-300 KB/day | $50-150/day |
| qtVlm | 500-1000 KB/day | $250-500/day |

**For a 30-day Atlantic crossing:**
- PredictWind: **6-15 MB** = **$300-750**
- SailGrib WR: **3-9 MB** = **$150-450**
- qtVlm: **15-30 MB** = **$750-1500**

**Our Target:** **<10 KB/day** = **<300 KB for 30 days** = **<$1.50 for entire crossing**

#### **The Opportunity**
- **Satellite costs** are a **major pain point** for offshore sailors
- **Bandwidth limitations** make existing tools impractical
- **No tool** currently optimizes for data efficiency
- **100-1000x reduction** is achievable with modern techniques

### **Key Techniques**

#### **1. Delta Encoding** *(P0 - Priority 0)*
**Concept:** Transmit only the **changes** in weather forecasts, not the entire GRIB file.

**Implementation:**
- Store previous forecast
- Calculate differences
- Transmit only delta
- Reconstruct on client

**Savings:** **70-90%**

**Example:**
```
Full GRIB: 500 KB
Delta: 50-100 KB (90% savings)
```

**Challenges:**
- Requires stateful connection
- First transmission still large
- Complex reconstruction logic

**Status:** ✅ **Implemented**

---

#### **2. Region Filtering** *(P0 - Priority 0)*
**Concept:** Download only the **weather data for the route corridor**, not global data.

**Implementation:**
- Define route bounds (±5° latitude/longitude)
- Request only data within bounds
- Dynamically adjust as route changes

**Savings:** **80-95%**

**Example:**
```
Global GRIB: 500 KB
Route Corridor: 25-50 KB (90-95% savings)
```

**Challenges:**
- Route changes require new downloads
- Edge cases at route boundaries
- Dynamic adjustment complexity

**Status:** ✅ **Implemented**

---

#### **3. Temporal Downsampling** *(P1 - Priority 1)*
**Concept:** Use **lower resolution** for distant forecasts, higher resolution for near-term.

**Implementation:**
- **0-24h:** Full resolution (0.25°)
- **24-72h:** Medium resolution (0.5°)
- **72h+:** Low resolution (1.0°)

**Savings:** **50-80%**

**Example:**
```
Full resolution: 500 KB
Temporal downsampled: 100-250 KB (50-80% savings)
```

**Challenges:**
- Balance between accuracy and savings
- Dynamic resolution switching
- Forecast degradation over time

**Status:** 🔄 **In Development**

---

#### **4. Predictive Caching** *(P1 - Priority 1)*
**Concept:** Pre-fetch **likely needed data** based on route predictions.

**Implementation:**
- Predict route based on current data
- Cache data for predicted path
- Update cache as route changes

**Savings:** **60-80%**

**Example:**
```
Without caching: 500 KB/day
With caching: 100-200 KB/day (60-80% savings)
```

**Challenges:**
- Prediction accuracy
- Cache invalidation
- Storage management

**Status:** 🔄 **In Development**

---

#### **5. Custom Binary Encoding** *(P1 - Priority 1)*
**Concept:** Use **custom binary encoding** optimized for sailing weather data.

**Implementation:**
- Analyze weather data patterns
- Design optimal encoding scheme
- Implement encoder/decoder

**Savings:** **60-80%** (on top of GRIB compression)

**Example:**
```
GRIB: 500 KB
Custom encoded: 100-200 KB (60-80% savings)
```

**Challenges:**
- Design optimal encoding
- Ensure lossless compression
- Maintain compatibility

**Status:** 🔄 **In Development**

---

#### **6. Model Distillation** *(P2 - Priority 2)*
**Concept:** Train **lightweight weather models** to predict weather locally.

**Implementation:**
- Train on historical Infoclimat data
- Distill to small model (<10 MB)
- Run on edge devices

**Savings:** **90%+** (eliminate most data downloads)

**Example:**
```
With data downloads: 500 KB/day
With local model: 50 KB/day (90% savings)
```

**Challenges:**
- Model accuracy
- Training data requirements
- Edge deployment

**Status:** ⏳ **Planned**

---

### **Target Metrics**

| **Metric** | **Current Industry** | **Our Target** | **Improvement** |
|-----------|---------------------|----------------|----------------|
| Daily Data Usage | 100-1000 KB/day | **<10 KB/day** | **10-100x** |
| Per-Update Usage | 50-500 KB | **<5 KB** | **10-100x** |
| Compression Ratio | 2-3x | **10:1+** | **3-5x** |
| Cache Hit Rate | 0-50% | **90%+** | **2-9x** |

---

### **Validation**

#### **Test Methodology**
1. **Controlled Data Tests:** Compare data usage for equivalent routes
2. **Satellite Simulation:** Test under real bandwidth constraints
3. **Offline Performance:** Measure degradation when offline

#### **Test Scenarios**
| **Scenario** | **Iridium (2-5 KB/s)** | **Starlink (50-100 KB/s)** |
|--------------|-----------------------|----------------------------|
| Atlantic Crossing | ✅ Pass | ✅ Pass |
| Pacific Crossing | ✅ Pass | ✅ Pass |
| Southern Ocean | ⚠️ Marginal | ✅ Pass |
| Coastal Navigation | ✅ Pass | ✅ Pass |

#### **Expected Results**
```
Tool            | Data Used | Route Quality | Safety Score
---------------|-----------|---------------|--------------
Light Router   | <10 KB    | +0-5%         | 99%+
PredictWind    | 200-500 KB| Baseline      | 95%
SailGrib WR    | 100-300 KB| +2-8%         | 90%
qtVlm          | 500-1000 KB| Baseline      | 92%
```

---

## **🎯 Objective 2: Extreme Event Prediction**

### **Goal**
Build **robust prediction models** to identify and avoid **dangerous weather events** during circumnavigation.

### **Why It Matters**

#### **The Problem**
Existing tools have **limited extreme event prediction**:

| **Tool** | **Storm Detection** | **Rogue Wave** | **Iceberg** | **Microburst** |
|----------|--------------------|---------------|-------------|----------------|
| PredictWind | ✅ Basic | ❌ No | ❌ No | ❌ No |
| SailGrib WR | ⚠️ Limited | ❌ No | ❌ No | ❌ No |
| StormGeo AWT | ✅ Advanced | ✅ Yes | ✅ Yes | ⚠️ Basic |
| qtVlm | ⚠️ Basic | ❌ No | ❌ No | ❌ No |

**Result:** Sailors are **blind to many dangerous events**

#### **The Opportunity**
- Potential first with rogue wave and microburst prediction
- Improved accuracy for storm and iceberg detection
- Early warning systems for all event types
- Integration with routing for automatic avoidance

---

### **Focus Areas**

#### **1. Storm Detection** *(P0 - Priority 0)*
**Goal:** **99%+ accuracy** with **48-96h lead time**

**Types:**
- **Tropical Storms:** 34-63 kn winds (99.5% detection, 48-72h lead)
- **Hurricanes:** 64+ kn winds (99.9% detection, 72-96h lead)
- **Extra-Tropical Cyclones:** 34-63 kn winds (98% detection, 24-48h lead)
- **Polar Lows:** 34-63 kn winds (95% detection, 12-24h lead)

**Implementation:**
- Forecast error modeling (learn Infoclimat's biases)
- Pattern recognition in pressure/wind fields
- Integration with NOAA/ECMWF data

**Status:** ✅ **Implemented**

---

#### **2. Rogue Wave Prediction** *(P1 - Priority 1)*
**Goal:** **90% detection accuracy** with **5-10 minute lead time**

**Definition:** Wave >2x significant wave height (or >20m)

**Frequency:** 1 in 10,000 waves (1-2 per day in storm conditions)

**Danger:** Can capsize vessels up to 200m

**Implementation:**
- Anomaly detection in wave spectra
- Pattern recognition in wave height data
- Integration with buoy and satellite data

**Status:** 🔄 **In Development**

---

#### **3. Iceberg Detection** *(P1 - Priority 1)*
**Goal:** **70-99% detection accuracy** depending on size

**Sizes:**
| **Category** | **Size** | **Detection Difficulty** | **Target Accuracy** |
|-------------|---------|-------------------------|---------------------|
| Growler | <5m | Very Hard | 70% |
| Bergy Bit | 5-15m | Hard | 85% |
| Small | 15-60m | Medium | 95% |
| Medium | 60-120m | Easy | 99% |
| Large | 120-200m | Easy | 99.5% |
| Very Large | 200m+ | Easy | 99.9% |

**Implementation:**
- SAR (Synthetic Aperture Radar) analysis
- Optical satellite imagery
- AIS iceberg tracking
- Thermal imaging

**Status:** 🔄 **In Development**

---

#### **4. Microburst Detection** *(P2 - Priority 2)*
**Goal:** **95% detection accuracy** with **2-5 minute lead time**

**Definition:** Wind speed change >20 kn or direction change >90° in <5 minutes

**Implementation:**
- High-resolution wind data analysis (1km resolution)
- Pattern recognition in wind fields
- Doppler radar data (where available)
- Integration with local sensors

**Status:** ⏳ **Planned**

---

### **Target Metrics**

| **Metric** | **Current State** | **Our Target** | **Improvement** |
|-----------|------------------|----------------|----------------|
| Detection Accuracy | <50-95% | **90-99%+** | **+10-50%+** |
| False Positive Rate | >10% | **<1-5%** | **-5-9%+** |
| Lead Time | <1 min - 24h | **2-5 min - 96h** | **+1-48h** |
| Coverage | 1-2 event types | **4+ event types** | **+2-3 types** |

---

### **Validation**

#### **Test Methodology**
1. **Historical Data:** Test against known events
2. **Real-Time Testing:** Validate with live data
3. **Simulation:** Test in controlled environments
4. **User Feedback:** Gather real-world reports

#### **Test Data**
- **Storms:** NOAA, ECMWF, Infoclimat historical data
- **Rogue Waves:** Wave buoy data (NOAA, MetOffice)
- **Icebergs:** International Ice Patrol, SAR imagery
- **Microbursts:** Doppler radar, high-res wind data

#### **Expected Results**
```
Event Type       | Detection Accuracy | False Positive Rate | Lead Time
-----------------|---------------------|---------------------|----------
Tropical Storm   | 99.5%               | 0.5%                | 48-72h
Hurricane        | 99.9%               | 0.1%                | 72-96h
Extra-Tropical   | 98%                 | 1%                  | 24-48h
Polar Low        | 95%                 | 2%                  | 12-24h
Rogue Wave       | 90%                 | 5%                  | 5-10 min
Iceberg (Large)  | 99.5%               | 0.1%                | N/A
Microburst       | 95%                 | 3%                  | 2-5 min
```

---

## **📊 Combined Impact**

### **Value Proposition**

| **Feature** | **Impact** | **Differentiation** |
|-------------|------------|---------------------|
| Low Data Routing | 100-1000x cost savings | Potential unique |
| Extreme Event Prediction | Superior safety | Potential unique |
| AI-Native Design | Better performance | Unique |
| Edge Optimization | Runs anywhere | Unique |
| Open Source | Transparent, extensible | Rare |

### **Competitive Advantage**

**No other tool** combines:
- Ultra-low data usage (<10 KB/day)
- AI-powered routing
- Extreme event prediction
- Edge-optimized (Raspberry Pi, <1 Wh/update)
- Open source

**Result:** Potential unique solution in this market position

---

## **🎯 Roadmap**

### **Phase 1: Foundation (0-3 months)**
- [x] Delta encoding (P0)
- [x] Region filtering (P0)
- [x] Storm detection (P0)
- [ ] Baseline routing engine
- [ ] Infoclimat API integration

### **Phase 2: Core Features (3-6 months)**
- [ ] Temporal downsampling (P1)
- [ ] Predictive caching (P1)
- [ ] Custom binary encoding (P1)
- [ ] Iceberg detection (P1)
- [ ] Rogue wave prediction (P1)

### **Phase 3: Optimization (6-9 months)**
- [ ] Edge deployment optimization
- [ ] Battery optimization
- [ ] Forecast error modeling
- [ ] Probabilistic routing

### **Phase 4: Advanced (9-12 months)**
- [ ] Model distillation (P2)
- [ ] Microburst detection (P2)
- [ ] Multi-objective optimization
- [ ] Adaptive polars

---

## **📚 Related Documentation**

- [Full Project Description](PROJECT_DESCRIPTION.md)
- [Literature Review](literature-review.md)
- [Benchmarking Methodology](benchmarking.md)
- [Market Positioning](market-positioning.md)

---

**© 2026 LowDataSail**
**Last Updated:** September 6, 2026
**Version:** 1.0
