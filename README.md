# Whole-Building AI-IoT Retrofit Research
### Quantifying the Economic–Environmental Trade-offs of Retrofitting Legacy Commercial Buildings

[![Python 3.12](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![EnergyPlus 25.1.0](https://img.shields.io/badge/EnergyPlus-v25.1.0-orange.svg)](https://energyplus.net/)
[![Sinergym 3.12.2](https://img.shields.io/badge/Sinergym-v3.12.2-green.svg)](https://ugr-sail.github.io/sinergym/)
[![PyTorch](https://img.shields.io/badge/PyTorch-v2.1+-ee4c2c.svg)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

🔗 **GitHub Repository:** [https://github.com/RajKumar369369369/Legacy-Building-AI-IoT-Retrofit-Research](https://github.com/RajKumar369369369/Legacy-Building-AI-IoT-Retrofit-Research)

---

## 👥 Group Members & Contributions

| Name | Roll Number | Contribution |
| :--- | :--- | :--- |
| **BOKKISAM RAJ KUMAR** | `U23AI113` | **EnergyPlus / Sinergym Physics & PPO Control:** Automated 10-step IDF upgrade (`v9.3 → v25.1`), Surat TMYx weather adaptation, `2.0°C` deadband & actuator binding, custom reward wrapper, and PPO RL training (`cost_first` / `carbon_first`). |
| **MOHAMMAD MUZAMMIL** | `U23AI105` | **Measured Data Pipeline & XGBoost Baseline:** LBNL Building 59 ingestion (27 CSVs, 26,305 hrs), sub-meter auditing (`ele.csv`), lag/calendar feature engineering, and chronological GPU XGBoost baseline (`R² = 0.8249`). |
| **MAKAM LOKESH** | `U23AI093` | **Sensor Health & Anomaly Detection (PyTorch VAE):** Multivariate VAE architecture on GPU, validation threshold calibration, synthetic drift testing, and per-sensor fault attribution (`RTU-002` isolation). |
| **ANSHUL REDDY KOTHA** | `U23AI107` | **Lifecycle Scorecard & NSGA-II Optimization:** 10-year financial/carbon modeling (Surat ToD tariff, CEA grid factor, NPV, Payback, CFPG) and constrained `pymoo` NSGA-II Pareto frontier optimization. |
| **SRIRAMAKAVACHAM NRUPENDRA** | `U23AI055` | **Supervisory Tiers, Provenance & Reporting:** Tier 1/Tier 2 rule-based policy verification, result visualization & Pareto plotting, `run_provenance.json` artifact auditing, IEEE conference report, and presentation. |

---

## 📌 Project Overview

Commercial buildings constructed before 1980 represent a significant share of urban building stock and energy consumption. Traditional deep architectural retrofits (facade replacement, chiller plant overhauls) carry prohibitive capital expenditures and substantial embodied carbon.

This repository provides an end-to-end, reproducible research pipeline that couples **empirical sensor validation from real buildings** with **high-fidelity physical simulation (EnergyPlus)**, **Deep Reinforcement Learning (PPO)**, and **Multi-Objective Evolutionary Optimization (NSGA-II)** to rigorously evaluate digital-first, non-invasive AI-IoT retrofits.

```
       ┌────────────────────────────────────────────────────────┐
       │   Empirical Validation Layer (LBNL Building 59 Data)   │
       │   27 CSV Feeds • Submeters • Weather • Temp • CO2 • Occ│
       └──────────────────────────┬─────────────────────────────┘
                                  │
                 ┌────────────────┴────────────────┐
                 ▼                                 ▼
       ┌───────────────────┐             ┌───────────────────┐
       │  XGBoost Baseline │             │ PyTorch VAE Fault │
       │  Demand Estimator │             │ Anomaly Detector  │
       │    (R² = 0.8249)  │             │ (RTU-002 Isolated)│
       └───────────────────┘             └───────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │ Physical Thermal Simulation (DOE Pre-1980 Medium Office)│
       │ 18 Zones • 4,982 m² • Surat TMYx Weather • Sinergym E+ │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                 ┌────────────────┴────────────────┐
                 ▼                                 ▼
       ┌───────────────────┐             ┌───────────────────┐
       │  Tier 1 & Tier 2  │             │   Tier 3 (PPO)    │
       │ Supervisory Rules │             │  RL Agent Control │
       │ (ToD / Occ / CO2) │             │ (Cost & Carbon)   │
       └─────────┬─────────┘             └─────────┬─────────┘
                 └────────────────┬────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │      Lifecycle Scorecard & NSGA-II Pareto Search       │
       │  10-Yr NPV (₹) • Simple Payback • Net Carbon • CFPG    │
       └────────────────────────────────────────────────────────┘
```

---

## 🏆 Key Empirical Results

### 1. Measured Demand Baseline (LBNL Building 59 — GPU XGBoost)
* **Performance:** $R^2 = 0.8249$, $\text{MAE} = 4.62\text{ kWh}$, $\text{RMSE} = 6.28\text{ kWh}$ across $3,631$ chronological held-out hours.
* Fully compliant with **ASHRAE Guideline 14** validation thresholds ($CV(RMSE) \le 15\%$).

### 2. Multivariate Sensor Anomaly Detection (PyTorch VAE)
* **Architecture:** 6-channel input $\to$ Encoder $\to$ Latent Bottleneck ($z=3$) $\to$ Decoder.
* **Operational Fault Attribution:** Identified real degradation in Rooftop Unit 2 (`RTU-002`) with peak reconstruction loss reaching **20.61** on Oct 14, 2020 (normal 99th percentile threshold $\le 0.62$).

### 3. Full-Year Physical Simulation (18-Zone DOE Medium Office, 4,982.19 m², Surat TMYx Weather, 52,560 Timesteps)
* **Tier 2 (`Occupancy + CO₂ + ToD Demand Response, cost_first`) — Pareto Optimal:**
  * **Energy Reduction:** **-30.9%** annual electricity savings.
  * **Financial Return:** 10-year Net Present Value (NPV) of **₹30.58 Million**.
  * **Thermal Comfort:** Compliant at **800.2** comfort-degree-hours/year (well inside the 1,200 deg-hr constraint).
  * **Carbon Payback:** $\text{CFPG} = 0.465\text{ years}$ (~5.6 months).
* **Tier 1 (`Smart Scheduling & Night Setback`) — Pareto Optimal:**
  * **Energy Reduction:** **-29.7%** annual electricity savings.
  * **Decarbonization:** Avoids **3,826 $tCO_2e$** net over 10 years.
  * **Payback:** Instant **0.20 year** (~2.4 months) financial payback; $\text{CFPG} = 0.183\text{ years}$.
* **Tier 3 (`PPO Continuous Control`) — NSGA-II Filtered Out:**
  * Achieved **-51.3%** gross energy reduction, but exceeded the comfort threshold ($7,927.8\text{ deg-hrs}$) when trained on a short winter budget, demonstrating the necessity of constrained multi-objective optimization.

---

## 📂 Repository Structure

```
├── README.md                                         # Comprehensive research documentation
├── .gitignore                                        # Clean Git ignore rules (filters large caches)
├── Whole_Building_AI_IoT_Retrofit__(2)_(2)_new.ipynb # Master Google Colab & local research notebook
├── data/
│   ├── sensor_hourly_processed.csv                  # Aligned 8,760-hour operational dataset
│   └── building_59/                                 # LBNL Building 59 clean sensor feeds
│       ├── ele.csv                                  # Sub-metered & whole-building power (kW)
│       ├── site_weather.csv                         # Ambient drybulb, RH, solar radiation
│       ├── zone_temp_interior.csv                   # Interior zone temperature loggers
│       ├── occ.csv                                  # Occupancy count time-series
│       └── zone_co2.csv                             # Indoor air quality (CO2 ppm)
└── outputs/
    ├── ppo_cost_first.zip                           # Trained PPO RL model (Cost priority)
    ├── ppo_carbon_first.zip                         # Trained PPO RL model (Carbon priority)
    ├── economic_lifecycle_results.csv               # Complete 10/15-year lifecycle financial metrics
    ├── nsga2_pareto_results.csv                     # NSGA-II Pareto non-dominated configurations
    ├── retrofit_economic_carbon_summary.csv         # Comparative tier scorecard
    └── final_validation_report.json                 # Machine-readable provenance & audit log
```

---

## 🔬 Methodology & Pipeline Stages

The master research notebook is structured into modular stages:

1. **Stage 0–1 (Runtime & Configuration):** Initializes hardware, verifies GPU/CPU acceleration, establishes project area ($4,982.19\text{ m}^2$), Surat Time-of-Day (ToD) electricity tariffs, and CEA grid carbon intensity factors.
2. **Stage 2–4 (Empirical Data Ingestion & Quality Audit):** Unpacks and audits LBNL Building 59 telemetry, verifying meter boundary completeness across plug loads, lighting, and HVAC chillers/fans.
3. **Stage 5 (Whole-Building Energy Baseline):** Chronological holdout training with XGBoost Regressor.
4. **Stage 6 (Sensor Anomaly Detection):** Trains PyTorch VAE on normal building telemetry to establish the fault detection threshold.
5. **Stage 7–12 (Physical Model Ingestion & Verification):** Converts legacy archetype IDFs to EnergyPlus 25.1.0, applies Surat TMYx weather, and runs a zero-overlay baseline reference run.
6. **Stage 13–15 (Sinergym Gym Environment & Reward Wrapper):** Establishes observation space, continuous setpoint actuators ($2.0^\circ\text{C}$ deadband), and composite reward wrapper:
   $$R_t = -\left[ w_{\text{cost}} \cdot \text{Cost}_t + w_{\text{carbon}} \cdot \text{Carbon}_t + w_{\text{comfort}} \cdot \text{Discomfort}_t \right]$$
7. **Stage 16–17 (Supervisory Policies & PPO Training):** Trains multi-objective PPO agents with Stable-Baselines3 and formalizes Tier 1 and Tier 2 rule-based policies.
8. **Stage 18–19 (Multi-Tier Physical Simulation & Financial Evaluation):** Simulates all candidate strategies across the full annual cycle; computes Simple Payback, Net Present Value (NPV), and Carbon Payback Period (CFPG).
9. **Stage 20 (NSGA-II Pareto Optimization):** Solves the constrained multi-objective problem using `pymoo`, identifying non-dominated solutions on the economic cost vs. net carbon frontier.

---

## 🚀 Getting Started

### Option 1: Run in Google Colab (Recommended for GPU / Cloud)
1. Open Google Colab: [colab.research.google.com](https://colab.research.google.com/)
2. Upload `Whole_Building_AI_IoT_Retrofit__(2)_(2)_new.ipynb`.
3. Select **Runtime → Change runtime type → T4 GPU**.
4. Run cells sequentially.

### Option 2: Run Locally (Windows / Linux / macOS)
1. Clone this repository:
   ```bash
   git clone https://github.com/RajKumar369369369/Legacy-Building-AI-IoT-Retrofit-Research.git
   cd Legacy-Building-AI-IoT-Retrofit-Research
   ```
2. Create and activate a Python 3.12 virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate       # Linux / macOS
   .\venv\Scripts\activate        # Windows
   ```
3. Install required packages:
   ```bash
   pip install xgboost scikit-learn torch gymnasium stable-baselines3 pymoo matplotlib seaborn pandas numpy
   ```
4. Launch Jupyter Notebook:
   ```bash
   jupyter notebook "Whole_Building_AI_IoT_Retrofit__(2)_(2)_new.ipynb"
   ```

---

## 📜 References & Datasets

* **LBNL Building 59 Dataset:** [Zenodo Record 5951008](https://zenodo.org/records/5951008) | DOI: `10.7941/D1N33Q`
* **DOE Commercial Reference Buildings:** [US Department of Energy Archetypes](https://www.energy.gov/cmei/buildings/existing-commercial-reference-buildings-constructed-1980)
* **Climate.OneBuilding Weather Data:** [India/Gujarat TMYx Weather](https://climate.onebuilding.org/WMO_Region_2_Asia/IND_India/)
* **Sinergym Documentation:** [ugr-sail.github.io/sinergym](https://ugr-sail.github.io/sinergym/)
* **ASHRAE Standard 55 & Guideline 14:** Thermal Environmental Conditions & Measurement of Energy Savings
