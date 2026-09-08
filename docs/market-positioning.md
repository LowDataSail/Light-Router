# Market Positioning

## Market Size
- Professional Racing: 500-1000 teams
- Offshore Cruising: 10,000-50,000 boats
- Research Vessels: 500-1000 vessels

## Competitors
| Tool | Data Usage | AI/ML | Offline | Open Source |
|------|------------|-------|--------|------------|
| PredictWind | ~150 KB/day (Iridium GO!) | No | Yes (mobile) | No |
| SailGrib WR | 100-300 KB/day | No | Yes | No |
| StormGeo AWT | 500-1000+ KB/day | Not documented | No | No |
| qtVlm | 500-1000 KB/day | No | Yes | No (free, proprietary) |
| OpenCPN Weather Routing | Varies | No | Yes | Yes |
| Saildocs | 2-30 KB/request (manual) | No | Yes (email) | No |

## Target Segments
### Primary
- Offshore Racers: need speed, reliability, satellite optimization
- Long-Distance Cruisers: need safety, cost-effectiveness
- Research Vessels: need autonomy, remote operations

### Secondary
- Autonomous Boat Developers: need AI-native, edge-optimized
- Commercial Shipping: need fuel savings, fleet management

## Potential Collaborations
- NOAA / ECMWF / Copernicus: public data access (free weather, wave, and current data)
- Open source community: libweatherrouting, OpenCPN Weather Routing plugin, SIMROUTE
- Saildocs: existing low-bandwidth GRIB delivery infrastructure

## Differentiation
- Data efficiency: target <10 KB/day vs. best existing filtered tools at ~150 KB/day (PredictWind) to ~30 KB/request (Saildocs, manual)
- AI-native: no sailing tool uses AI for routing or data optimization
- Route-aware automation: Saildocs requires manual region/variable specification; Light Router automates this
- Ensemble-based: no sailing tool uses ensemble forecasts for probabilistic routing
- Edge-optimized: Raspberry Pi compatible, low power
- Open source: MIT License
