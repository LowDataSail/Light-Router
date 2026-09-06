# Literature Review

## Current Solutions

### Commercial Tools
| Tool | Algorithm | Data Source | Data Usage | AI/ML | Offline | Open Source |
|------|-----------|-------------|------------|-------|--------|------------|
| PredictWind | Isochrone + Wave | NOAA, ECMWF | 200-500 KB/day | No | No | No |
| SailGrib WR | Isochrone | NOAA, Meteo France | 100-300 KB/day | No | Yes | No |
| StormGeo AWT | Proprietary | Proprietary | 500-1000+ KB/day | No evidence | No | No |
| qtVlm | Isochrone | NOAA, OpenSkiron | 500-1000 KB/day | No | Yes | Yes |

### Open Source
| Project | Language | Algorithm | Data Format | AI Support | Maturity |
|---------|----------|-----------|------------|------------|----------|
| libweatherrouting | Python | Isochrone, Modular | GRIB1/2 | Designed for extension | High |
| qtVlm | C++/Qt | Isochrone + Simulation | GRIB | No | High |

### Academic Research
| Approach | Institution | Algorithm | Data Efficiency | Performance | Real-World Testing |
|----------|-------------|-----------|-----------------|------------|------------------|
| Deep RL | MDPI | Actor-Critic | Medium | High | No |
| Hybrid RL+Graph | Berkeley | Q-Learning + A* | High | Very High | No |

## Gaps

### Data Efficiency
Current tools use 100-1000 KB/day. Target: <10 KB/day.

### Extreme Event Prediction
No commercial tool offers rogue wave or microburst detection.

### Edge Deployment
Most tools require desktop environments. Target: Raspberry Pi compatible.
