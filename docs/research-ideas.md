# Research Ideas

*Open research directions and hypotheses worth investigating. These are working notes, not commitments — each item needs validation before it becomes an objective.*

---

## **🧭 Model Specialization**

### Specializing models across geographic zones

Different ocean basins have distinct weather regimes (trade winds, doldrums, Southern Ocean depressions, high-latitude ice). A single global model may underperform in specific zones.

- **Hypothesis:** Zone-specialized models (e.g. Atlantic, Indian Ocean, Southern Ocean) outperform a single global model within their zone, at the cost of extra storage and the need for zone switching logic.
- **Open questions:** How to define zone boundaries? Is the gain large enough to justify per-zone models on a low-data, edge-deployed device? Can a single model with a geographic embedding match specialized models?
- **Related:** [Meteorological Information Transfer](meteorological-info-transfer.md), [Routing Algorithms](routing-algorithms.md)

### Specializing models on specific boats — or exposing it as a feature?

Boat performance is captured by the polar diagram, which varies widely across hulls (monohull vs. multihull, displacement vs. planing, cruiser vs. racer). The question is whether the routing model itself should be boat-specialized.

- **Hypothesis A (specialization):** Boat-specific models capture nuances the polar diagram misses (trim response, sea-state-dependent speed, helm behavior) and route better for that boat.
- **Hypothesis B (feature):** Boat behavior is fully described by the polar diagram + a small set of parameters, so a single model parameterized by the polar is sufficient and boat-specialization is unnecessary.
- **Compromise to test:** Treat the polar as a model input/feature rather than baking it into a specialized model — generalizes across boats without per-boat training, and per-boat tuning (if needed) becomes a feature the user supplies.
- **Open questions:** Is there residual boat-specific signal beyond the polar? How much per-boat data is needed for specialization to pay off? This decision affects data collection strategy.
- **Related:** [Routing Algorithms](routing-algorithms.md) (polar diagrams, isochrone method)

---

## **🎯 Ground Truth & Benchmarking Strategy**

Training and evaluating routing models requires a notion of the "correct" route. The candidates below are not mutually exclusive.

### Ground truth = SOTA routers on past data

Run state-of-the-art routers (PredictWind, StormGeo AWT, qtVlm, OpenCPN Weather Routing) on archived forecasts and use their outputs as reference labels.

- **Use:** Cheap, reproducible labels at scale; lets us benchmark our low-data model against full-data SOTA without depending on those services at inference time.
- **Risk:** We inherit the SOTA routers' biases and errors — labels are only as good as the reference router. Best used to measure *relative* route quality (the existing ">90% of commercial solutions" target), not absolute optimality.
- **Related:** [Benchmarking](benchmarking.md), [Literature Review](literature-review.md)

### Ideal route algorithms with a posteriori data

Compute the truly optimal route using *actual* (a posteriori / hindcast) weather rather than forecast weather. This gives an upper bound on achievable performance and quantifies the gap due to forecast error alone.

- **Use:** Aspirational reference — measures how much routing loss comes from forecast uncertainty vs. from our algorithm/model. Useful to decompose error sources.
- **Risk:** "Ideal" assumes a perfect cost model (exact polars, no tactical/comfort tradeoffs), so it is a theoretical optimum, not necessarily a route a human would sail.
- **Related:** [Routing Algorithms](routing-algorithms.md), [Benchmarking](benchmarking.md)

### Real-world skippers' trajectories

Collect actual sailed tracks (race trackers, AIS, onboard logs) as demonstration data.

- **Use:** Direct human-expert signal — grounds the model in what experienced sailors actually do, including tactical and comfort decisions that cost models miss. Natural input for imitation learning.
- **Risk:** Real trajectories reflect constraints the model may not know (gear failures, strategy, crew fatigue, fuel for motor-sailing) and may be *suboptimal* — they are demonstrations, not optima. Best combined with the cost-based references above.
- **Related:** [Routing Algorithms](routing-algorithms.md) (imitation learning), [Benchmarking](benchmarking.md)

---

## **🔗 How these connect**

The three ground-truth sources form a layered evaluation framework:

1. **A posteriori ideal** — theoretical optimum, upper bound on performance.
2. **SOTA routers on past data** — practical reference for the ">90% of commercial" target; reproducible at scale.
3. **Real skipper trajectories** — human-expert demonstration data; captures real-world constraints and objectives.

Reconciling the differences between these three is itself a research question: where skippers diverge from the a posteriori ideal, the gap may be either suboptimal play or legitimate objectives (safety, comfort) our cost model fails to capture.

Model specialization (geographic zones, specific boats) interacts with all three: specialized models need zone- or boat-specific training labels, which in turn shapes what ground-truth data must be collected per zone/boat.

---

**© 2026 LowDataSailing**
