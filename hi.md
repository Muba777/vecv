# TRACK 3 - LOW ENGINE OIL PRESSURE

**Author:** Mubashira A U

## Introduction
To improve vehicle reliability and reduce unexpected service interruptions, a proactive monitoring framework is being designed for low engine oil pressure analysis. Historical sensor data, evaluated using engine operating hours as a reference and RPM binning, was analyzed to detect early pressure irregularities.

## Objective
Enable early identification of low engine oil pressure issues by monitoring subtle changes in pressure relative to engine behavior. By detecting abnormal patterns before system alerts are triggered, vehicles can be proactively flagged for inspection. This allows scheduled visits to the workshop at convenient times, rather than sudden stoppages on the road — turning "Stop Now" cases into "Visit Soon" opportunities.

## Methodology
- Engine telemetry from healthy vehicles was analyzed to understand normal oil pressure behavior over time.
- This baseline was used to compare with vehicles that later experienced issues.
- Data was segmented and analyzed by engine speed (RPM) and operating hours, creating a normalized view of vehicle behavior over time.
- Any significant deviation in pressure within that RPM bin is monitored as a potential risk.
- Healthy vehicle data was used to create a statistical baseline using z-scores, which measure how far oil pressure readings deviate from expected values at each RPM for DTC-triggered VINs.
- If pressure behaves normally over operating hours, the vehicle is considered stable.
- If pressure trends down despite stable RPM, a deviation is likely.

## Key Findings
- Many vehicles remained stable until about 48 operating hours before failure.
- A steady decline in pressure was recorded from 48 to 84 operating hours prior to the actual fault.
- A critical detection window was identified: 0 to 12 hours before failure, where intervention could be planned.

| Time Window Before Fault | Deviation Level | Interpretation |
|--------------------------|-----------------|----------------|
| 0–12 operating hrs       | Very High       | Too Late       |
| 12–24 operating hrs      | Moderate        | Monitoring     |
| 24–36 operating hrs      | Moderate        | Monitoring     |
| 48–84 operating hrs      | High            | Degrading      |

## Next Steps
- A method is being developed to quantify how often oil pressure readings cross critical thresholds based on z-score deviation from healthy patterns.
- For each unhealthy vehicle, z-scores were already computed using the healthy vehicle baseline.
- The goal is to count the number of times these z-scores exceed ±2σ and ±3σ in the hours leading up to a fault (DTC).
- Special attention will be given to violations that occur at least 12 hours before the DTC, as these offer the highest value for early warning.
- The density and timing of these threshold-crossing points will be analyzed to identify patterns or clusters.
- Based on these patterns, a predictive scoring method or model may be developed to proactively assess risk — even before any fault code is triggered.
