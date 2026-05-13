# Flight Parameter Prediction Dataset under Changing Atmospheric Conditions

This repository provides flight-parameter time-series data used for evaluating reliable aircraft flight-parameter prediction under changing atmospheric conditions. The released data cover four representative flight scenarios, including strong crosswind, persistent gust disturbance, in-flight icing, and sustained hot-updraft flight. These scenarios are intended to support reproducible evaluation of time-series forecasting models under realistic and dynamically varying flight regimes.

## Dataset Overview

The dataset consists of four CSV files:

| File name | Flight scenario | Description |
|---|---|---|
| `Flight_1.csv` | Strong crosswind takeoff and landing | Flight data collected under strong crosswind conditions, where lateral disturbance and heading correction are prominent. |
| `Flight_2.csv` | Persistent gust flight | Flight data collected under sustained gust disturbance, characterized by repeated multi-axis fluctuations. |
| `Flight_3.csv` | In-flight icing | Flight data collected under in-flight icing conditions, where aerodynamic changes may induce persistent deviations in aircraft responses. |
| `Flight_4.csv` | Sustained hot-updraft flight | Flight data collected under sustained thermal updraft conditions, where vertical load variations and abrupt dynamic responses are observed. |

All files are sampled at a temporal resolution of **1 second**. Each row corresponds to one timestamped flight state.

## File Format

Each CSV file follows the same structure:

```csv
Time,Sideslip_Angle,Longitudinal_Load_Factor,Normal_Load_Factor,Lateral_Load_Factor,Pitch_Rate,Roll_Rate,Yaw_Rate
0,99.1375661,-0.0052819,0.0013047,0.9977169,0.042489,0.0376089,0.0045858
1,90.3968254,-0.0051233,0.0014638,0.9972412,0.0397478,0.0395883,0.012993
2,88.4126984,-0.005504,0.000175,0.9955289,0.035636,0.0257324,0.0045858
```

The rows are chronologically ordered by `Time`.

## Column Description

| Column | Physical meaning | Symbol | Description |
|---|---|---|---|
| `Time` | Time | \(t\) | Timestamp index. The sampling interval is 1 second. |
| `Sideslip_Angle` | Sideslip angle | \(\beta\) | Angle related to lateral airflow and aircraft heading deviation, commonly used to characterize crosswind- or sideslip-induced lateral dynamics. |
| `Longitudinal_Load_Factor` | Longitudinal load factor | \(n_x\) | Load factor along the longitudinal body-axis direction. |
| `Normal_Load_Factor` | Normal load factor | \(n_z\) | Load factor along the normal or vertical body-axis direction, reflecting vertical dynamic response. |
| `Lateral_Load_Factor` | Lateral load factor | \(n_y\) | Load factor along the lateral body-axis direction, reflecting side-force or lateral disturbance effects. |
| `Pitch_Rate` | Pitch rate | \(q\) | Angular velocity around the aircraft lateral axis, describing pitch motion. |
| `Roll_Rate` | Roll rate | \(p\) | Angular velocity around the aircraft longitudinal axis, describing roll motion. |
| `Yaw_Rate` | Yaw rate | \(r\) | Angular velocity around the aircraft vertical axis, describing yaw motion. |

The released variables are key flight-dynamics responses associated with six-degree-of-freedom aircraft motion. In a standard six-degree-of-freedom formulation, aircraft motion consists of three translational degrees of freedom and three rotational degrees of freedom. The variables in this dataset capture important lateral, longitudinal, vertical, and angular-rate responses that are relevant to flight-parameter prediction under changing atmospheric conditions.

## Six-Degree-of-Freedom Flight-Dynamics Context

Aircraft six-degree-of-freedom motion is typically described in a body-fixed coordinate system:

- The \(X\)-axis points forward along the fuselage.
- The \(Y\)-axis points toward the right wing.
- The \(Z\)-axis points downward.

The six basic degrees of freedom include:

| Type | Motion direction | Position or attitude variable | Velocity or angular-rate variable |
|---|---|---|---|
| Translation | Forward/backward | \(x\) | \(u\), forward velocity |
| Translation | Left/right | \(y\) | \(v\), lateral velocity |
| Translation | Up/down | \(z\), or altitude \(h\) | \(w\), vertical velocity |
| Rotation | Roll | \(\phi\), roll angle | \(p\), roll rate |
| Rotation | Pitch | \(\theta\), pitch angle | \(q\), pitch rate |
| Rotation | Yaw | \(\psi\), yaw angle | \(r\), yaw rate |

The present dataset provides a subset of flight-dynamics variables closely related to this six-degree-of-freedom framework, including sideslip angle, load factors, and body-axis angular rates.

## Suggested Usage

This dataset can be used for multivariate time-series forecasting, flight-parameter prediction, robustness evaluation, and surrogate modeling under dynamically changing flight conditions. A typical forecasting task is to use a historical window of flight parameters to predict future values of one or more flight-response variables.

Example loading code:

```python
import pandas as pd

data = pd.read_csv("Flight_1.csv")

print(data.head())
print(data.columns)
```

For chronological forecasting evaluation, users are encouraged to split each flight sequence according to time order rather than using random shuffling.

## Data Ethics and Availability

The released data contain flight-parameter time series and do not involve human subjects or personally identifiable information. The data are provided for academic research and reproducibility purposes.

## Citation

If you use this dataset, please cite the corresponding paper:

```bibtex
@article{your_paper_key,
  title   = {Your Paper Title},
  author  = {Author Names},
  journal = {Communications Engineering},
  year    = {Year}
}
```

## Contact

For questions about the dataset, please contact the corresponding author of the paper.
