# Circumnavigation 2027: AI-Powered Low-Data Sailing Router

![Project Banner](https://img.shields.io/badge/Status-Active-brightgreen) [![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE) [![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/downloads/)

**An AI-native sailing router optimized for ultra-low data consumption (<10 KB/day) and extreme conditions, designed for Circumnavigation 2027.**

---

## 🌍 **Project Overview**

This project develops an **AI-powered sailing router** for **Circumnavigation 2027**, optimized for **satellite-constrained environments** (Iridium/Starlink) and powered by **Infoclimat’s high-precision weather data**. The router automates navigation decisions while consuming **<10 KB/day**—a **100–1000x reduction** compared to existing solutions (1–10 MB/day).

### **Key Features**
✅ **Ultra-Low Data Consumption** – Delta encoding, region filtering, and predictive caching reduce data usage by **90–99%**.  
✅ **AI-Native Design** – Forecast error modeling, route imitation learning, and adaptive polars for **10–40% better routes**.  
✅ **Edge-Optimized** – Runs on **Raspberry Pi** with **<1 Wh/update** and **<1 min/calculation**.  
✅ **Satellite-Ready** – Designed for **Iridium (2–5 KB/s)** and **Starlink (50–100 KB/s)**.  
✅ **Open-Source** – Transparent, auditable, and extensible.  

---

## 🚀 **Why This Project?**

### **The Problem**
Current sailing routers (PredictWind, SailGrib, qtVlm) prioritize features over **data efficiency**, making them impractical for **offshore sailing** where:
- **Satellite costs** are **$0.50–5.00/MB** (Iridium).
- **Bandwidth** is **2–5 KB/s** (Iridium) or **50–100 KB/s** (Starlink).
- **GRIB files** are **10–500 KB** per forecast, downloaded **4–8x/day** (1–10 MB/day total).

### **Our Solution**
| **Metric**               | **Industry Standard** | **Our Target** | **Improvement** |
|--------------------------|-----------------------|----------------|----------------|
| **Data Usage**           | 1–10 MB/day           | **<10 KB/day** | **100–1000x**  |
| **Route Quality**        | 0–10% of optimal      | **<5%**        | **2x better**  |
| **Computation Time**     | 1–10 min/update       | **<1 min**     | **10x faster** |
| **Battery Usage**        | 10–100 Wh/update      | **<1 Wh**      | **100x better**|

---

## 🏗️ **Technical Architecture**

```
┌───────────────────────────────────────────────────────────────┐
│                     AI-Powered Sailing Router                     │
├───────────────────┬───────────────────┬───────────────────────┤
│   Data Pipeline    │   Routing Engine   │   AI/ML Layer          │
├───────────────────┼───────────────────┼───────────────────────┤
│ - Infoclimat API   │ - libweatherrouting│ - Forecast Error Model │
│ - Delta Encoding   │   (forked)         │ - Route Imitation      │
│ - Region Filtering │ - Hierarchical A*  │ - Adaptive Polars      │
│ - Temporal Downsampling│ - Incremental Updates│ - Anomaly Detection   │
│ - Predictive Cache │ - Multi-Objective  │                       │
│                   │   Optimization     │                       │
└─────────┬─────────┴─────────┬─────────┴──────────┬────────────┘
          │                   │                   │
          ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────┐ ┌─────────────────┐
│  Freewinds.world │ │    qtVlm     │ │  Custom Simulator│
│ (Primary Showcase)│ │ (Integration) │ │ (Fallback)        │
└─────────────────┘ └─────────────┘ └─────────────────┘
```

---

## 📦 **Data Efficiency Techniques**

| **Technique**            | **Savings**       | **Description**                                                                 |
|--------------------------|-------------------|---------------------------------------------------------------------------------|
| **Delta Encoding**       | 70–90%            | Transmit only forecast *changes* (not full GRIB files).                          |
| **Region Filtering**     | 80–95%            | Download only the **route corridor** (not global data).                          |
| **Temporal Downsampling**| 50–80%            | Lower resolution for **distant forecasts** (higher for near-term).              |
| **Predictive Caching**   | 60–80%            | Pre-fetch likely needed data based on route predictions.                        |
| **Model Distillation**   | 90%+              | Lightweight weather models trained on Infoclimat data.                        |

---

## 🤖 **AI/ML Enhancements**

| **Feature**               | **Technique**               | **Impact**                          | **Data Required**               |
|---------------------------|----------------------------|-------------------------------------|----------------------------------|
| Forecast Error Modeling   | Learn Infoclimat’s biases  | **15–30% better routes**           | Historical forecasts + actuals  |
| Route Imitation Learning  | Mimic expert sailors       | **10–25% improvement**             | Historical optimal routes      |
| Adaptive Polars           | Learn true boat performance| **5–20% more accurate**           | Sensor data + weather           |
| Probabilistic Routing     | Account for uncertainty     | **20–40% better safety**           | Forecast patterns               |
| Anomaly Detection         | Identify dangerous weather | Early warning system              | Forecast patterns               |

---

## 🎯 **Benchmarking Strategy**

### **Showcasing Platforms**
| **Platform**       | **Type**       | **Purpose**                          | **Timeline**       |
|-------------------|----------------|--------------------------------------|--------------------|
| **Freewinds.world** | Web (GGR 2026) | **Primary:** Public leaderboard, real-world performance | **Immediate (Weeks 1–4)** |
| **qtVlm**          | Desktop        | Integration, offline testing         | Weeks 2–6          |
| **PredictWind**    | Web            | Head-to-head comparison              | Weeks 3–6          |

### **Key Metrics**

#### **Route Quality**
| **Metric**               | **Target**               | **Measurement**                     |
|--------------------------|--------------------------|--------------------------------------|
| Time to Destination      | Within **5% of optimal** | Compare with theoretical minimum     |
| Distance Sailed          | Within **10% of great-circle** | Compare with direct path      |
| Safety Score             | **Maximize**             | Penalize storms, shallow water, icebergs |
| Comfort Score            | **Maximize**             | Penalize extreme weather, rough seas |

#### **Data Efficiency**
| **Metric**               | **Target**               | **Measurement**                     |
|--------------------------|--------------------------|--------------------------------------|
| Daily Data Usage         | **<10 KB/day**           | Monitor API calls + file sizes       |
| Per-Update Usage         | **<5 KB**                | Measure GRIB file sizes              |
| Compression Ratio        | **10:1+**                | Raw GRIB vs. encoded data            |

#### **Computation Efficiency**
| **Metric**               | **Target**               | **Measurement**                     |
|--------------------------|--------------------------|--------------------------------------|
| Inference Time           | **<1 min/update**         | Wall-clock time per calculation      |
| Memory Usage             | **<500 MB**              | Monitor RAM during routing           |
| Battery Impact           | **<1 Wh/update**          | Measure power draw on Raspberry Pi   |

---

## 📅 **Project Timeline**

### **Phase 1: Foundation (Weeks 1–2)**
- [ ] Register for **Freewinds.world GGR 2026**
- [ ] Secure **Infoclimat API access** (GRIB2, wave data)
- [ ] Set up **development environment** (Python, `cfgrib`, `xarray`)
- [ ] Implement **minimal GRIB parser**
- [ ] Develop **delta encoding** and **region filtering**
- [ ] Fork **libweatherrouting** and strip to essentials

### **Phase 2: Baseline Router (Weeks 3–4)**
- [ ] Integrate **Infoclimat data** (GRIB2 + wave data)
- [ ] Integrate **boat polars** (sailboat performance curves)
- [ ] Implement **basic safety constraints**
- [ ] Run **first head-to-head tests** (vs. PredictWind, SailGrib, qtVlm)
- [ ] Publish **initial benchmarking scripts**

### **Phase 3: AI Enhancements (Weeks 5–8)**
- [ ] Develop **forecast error modeling**
- [ ] Implement **incremental route updates**
- [ ] Add **multi-objective optimization** (Pareto front)
- [ ] Implement **probabilistic routing**
- [ ] Test on **Raspberry Pi**

### **Phase 4: Optimization & Showcase (Weeks 9–12)**
- [ ] Optimize for **satellite bandwidth**
- [ ] Optimize for **battery usage**
- [ ] Develop **user interface**
- [ ] Publish **benchmark report**
- [ ] Create **video demos**

---

## 🛠️ **Setup & Installation**

### **Prerequisites**
- Python **3.10+**
- Git
- [Optional] Docker (for containerized development)

### **Installation**
```bash
# Clone the repository
git clone https://github.com/LilianBsc/circumnavigation-2027-router.git
cd circumnavigation-2027-router

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### **Dependencies**
- `numpy` – Numerical computations
- `pandas` – Data analysis
- `xarray` – GRIB data handling
- `cfgrib` – GRIB file parsing
- `pygrib` – Alternative GRIB parsing
- `scipy` – Scientific computing
- `matplotlib` – Visualization
- `plotly` – Interactive plots
- `folium` – Interactive maps
- `libweatherrouting` – Base routing engine (forked)

---

## 📂 **Project Structure**

```
circumnavigation-2027-router/
├── docs/                      # Documentation (benchmarking reports, user guides)
│   ├── PROJECT_DESCRIPTION.md # Full project description
│   ├── BENCHMARKING.md        # Benchmarking methodology
│   └── API_DOCUMENTATION.md   # API docs for integrators
│
├── src/                       # Source code
│   ├── data_pipeline/         # Data ingestion, encoding, caching
│   │   ├── grib_parser.py     # Minimal GRIB parser
│   │   ├── delta_encoder.py   # Delta encoding for weather data
│   │   ├── region_filter.py   # Region-based filtering
│   │   └── cache_manager.py  # Predictive caching
│   │
│   ├── routing_engine/        # Core routing algorithms
│   │   ├── isochrone.py       # Isochrone routing (baseline)
│   │   ├── hierarchical_astar.py # Hierarchical A* routing
│   │   ├── incremental.py     # Incremental updates
│   │   └── multi_objective.py # Multi-objective optimization
│   │
│   ├── ai_models/             # AI/ML models
│   │   ├── forecast_error.py  # Forecast error modeling
│   │   ├── route_imitation.py # Route imitation learning
│   │   ├── adaptive_polars.py # Adaptive polar learning
│   │   └── anomaly_detection.py # Anomaly detection
│   │
│   └── utils/                 # Utility functions
│       ├── weather_utils.py  # Weather data utilities
│       ├── boat_utils.py     # Boat performance utilities
│       └── visualization.py   # Plotting and visualization
│
├── tests/                     # Unit and integration tests
│   ├── test_data_pipeline.py  # Data pipeline tests
│   ├── test_routing.py        # Routing engine tests
│   └── test_ai_models.py      # AI model tests
│
├── benchmarks/                # Benchmarking scripts and results
│   ├── freewinds/             # Freewinds.world integration
│   ├── qtvlm/                # qtVlm integration
│   ├── head_to_head.py        # Head-to-head comparison scripts
│   ├── historical_replay.py   # Historical route replay
│   └── results/               # Benchmark outputs
│
├── notebooks/                 # Jupyter notebooks for exploration
│   ├── data_analysis.ipynb    # Weather data analysis
│   ├── route_comparison.ipynb # Route comparison visualizations
│   └── ai_training.ipynb      # AI model training
│
├── configs/                   # Configuration files
│   ├── boat_polars.yaml        # Boat performance curves
│   ├── infoclimat_config.yaml # Infoclimat API settings
│   └── routing_settings.yaml  # Routing parameters
│
├── scripts/                   # Helper scripts
│   ├── setup_environment.sh   # Environment setup script
│   ├── run_benchmarks.sh      # Benchmark runner
│   └── deploy_edge.sh         # Edge deployment script
│
├── Dockerfile                 # Docker configuration
├── requirements.txt           # Python dependencies
├── pyproject.toml             # Project metadata
├── LICENSE                    # MIT License
└── README.md                  # This file
```

---

## 🚀 **Getting Started**

### **1. Set Up Infoclimat API Access**
1. Request API access from [Infoclimat](https://www.infoclimat.fr).
2. Configure your API key in `configs/infoclimat_config.yaml`:
   ```yaml
   api_key: "YOUR_INFOCLIMAT_API_KEY"
   base_url: "https://api.infoclimat.fr"
   update_frequency: 6  # hours
   ```

### **2. Run Your First Route Calculation**
```python
from src.data_pipeline.grib_parser import parse_grib
from src.routing_engine.isochrone import IsochroneRouter

# Load weather data
weather_data = parse_grib("path/to/grib_file.grb2")

# Initialize router
router = IsochroneRouter(weather_data, boat_polars="configs/boat_polars.yaml")

# Calculate route
start = (48.8566, -2.3522)  # Paris
end = (40.7128, -74.0060)   # New York
route = router.calculate_route(start, end)

# Visualize
router.plot_route(route)
```

### **3. Benchmark Against Existing Tools**
```bash
# Run head-to-head comparison
python benchmarks/head_to_head.py --router yours --opponent predictwind --route atlantic_crossing

# Generate benchmark report
python benchmarks/generate_report.py --output docs/BENCHMARKING.md
```

---

## 📊 **Benchmarking Results (Target)**

### **Freewinds.world Performance**
| **Metric**               | **Your Router** | **Default Freewinds** | **PredictWind** | **SailGrib WR** |
|--------------------------|-----------------|-----------------------|-----------------|------------------|
| **Leaderboard Rank**     | Top 25%         | Baseline              | Top 50%         | Top 40%          |
| **Data Usage (KB/day)**  | **<10**         | 500–1000              | 200–500         | 100–300          |
| **Route Time (days)**    | +5%             | Baseline              | +10%            | +8%              |
| **Safety Incidents**     | 0               | 1–2                   | 0–1             | 1–3              |

### **Data Efficiency Comparison**
| **Tool**               | **Data Usage (KB/day)** | **Route Quality** | **Computation Time** |
|------------------------|--------------------------|-------------------|----------------------|
| **Your Router**        | **<10**                 | <5% of optimal    | <1 min               |
| PredictWind            | 200–500                 | 0–10%             | 1–5 min              |
| SailGrib WR            | 100–300                 | 5–15%             | 1–3 min              |
| qtVlm                  | 500–1000                | 0–5%              | 2–10 min             |

---

## 🤝 **Partnerships & Integrations**

### **Infoclimat**
- **Role:** Primary weather data provider (GRIB2, wave models, real-time forecasts).
- **Status:** Partnership confirmed (API access requested).
- **Website:** [https://www.infoclimat.fr](https://www.infoclimat.fr)

### **Freewinds.world**
- **Role:** Primary showcase platform (Golden Globe Race 2026 virtual race).
- **Status:** Registration submitted (API access requested).
- **Website:** [https://freewinds.world](https://freewinds.world)

### **qtVlm**
- **Role:** Open-source integration for offline testing.
- **Status:** Fork planned for custom routing plugin.
- **Website:** [https://www.virtual-winds.org/](https://www.virtual-winds.org/)

---

## 📜 **License**

This project is licensed under the **MIT License** – see [LICENSE](LICENSE) for details.

---

## 🙌 **Contributing**

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### **How to Contribute**
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a Pull Request.

---

## 📞 **Contact**

- **Author:** [Lilian Bosc](https://github.com/LilianBsc)
- **Email:** contactlilian3@gmail.com
- **Project Link:** [https://github.com/LilianBsc/circumnavigation-2027-router](https://github.com/LilianBsc/circumnavigation-2027-router)

---

## 📚 **Acknowledgments**

- **Infoclimat** for providing high-quality weather data.
- **Freewinds.world** for the virtual sailing platform.
- **qtVlm** for the open-source routing engine.
- **Golden Globe Race** for the inspiration and real-world validation.

---

## 🔗 **Related Resources**

- [Infoclimat API Documentation](https://www.infoclimat.fr/api)
- [Freewinds.world](https://freewinds.world)
- [qtVlm GitHub](https://github.com/virtual-winds/qtVlm)
- [libweatherrouting](https://github.com/WeatherRouting/libweatherrouting)
- [GRIB File Format](https://www.wmo.int/pages/prog/www/WDM/Guides/Guide-binary-2.html)
- [NOAA Weather Data](https://www.noaa.gov/)
- [Golden Globe Race 2026](https://goldengloberace.com)

---

**© 2026 Lilian Bosc**
