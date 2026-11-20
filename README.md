# Legacy-Building-AI-IoT-Retrofit-Research
# Whole-Building AI-IoT Retrofit Research
**Quantifying the Economic–Environmental Trade-offs of Retrofitting Legacy Commercial Buildings**

🔗 **GitHub Repository:** `https://github.com/[YOUR_USERNAME]/[YOUR_REPO_NAME]`

---


## 👥 Group Members

| Name | Roll Number | Contribution |
| :--- | :--- | :--- |
| `[BOKKISAM RAJ KUMAR]` | `[U23AI113]` | **EnergyPlus / Sinergym Physics & PPO Control:** Automated 10-step IDF upgrade (`v9.3 → v25.1`), Surat TMYx weather adaptation, `2.0°C` deadband & actuator binding, custom reward wrapper, and PPO RL training (`cost_first` / `carbon_first`) |
| `[MOHAMMAD MUZAMMIL]` | `[U23AI105]` | **Measured Data Pipeline & XGBoost Baseline:** LBNL Building 59 ingestion (27 CSVs, 26,305 hrs), sub-meter auditing (`ele.csv`), lag/calendar feature engineering, and chronological GPU XGBoost baseline (`R² = 0.8249`) |
| `[MAKAM LOKESH]` | `[U23AI093]` | **Sensor Health & Anomaly Detection (PyTorch VAE):** Multivariate VAE architecture on GPU, validation threshold calibration, synthetic drift testing, and per-sensor fault attribution (`RTU-002` isolation) |
| `[ANSHUL REDDY KOTHA]` | `[U23AI107]` | **Lifecycle Scorecard & NSGA-II Optimization:** 10-year financial/carbon modeling (Surat ToD tariff, CEA grid factor, NPV, Payback, CFPG) and constrained `pymoo` NSGA-II Pareto frontier optimization |
| `[SRIRAMAKAVACHAM NRUPENDRA]` | `[U23AI055]` | **Supervisory Tiers, Provenance & Reporting:** Tier 1/Tier 2 rule-based policy verification, result visualization & Pareto plotting, `run_provenance.json` artifact auditing, IEEE conference report, and presentation |

---

## 📌 Project Overview

This repository contains a reproducible, single-notebook Google Colab pipeline (`Whole_Building_AI_IoT_Retrofit.ipynb`) that evaluates whole-building AI-IoT retrofit strategies by coupling **measured machine learning validation** with **full-year physical thermal simulation (EnergyPlus)**, **Deep Reinforcement Learning (PPO)**, and **Multi-Objective Optimization (NSGA-II)**.

### Key Results Summary
* **Measured Demand Baseline (LBNL Building 59 — GPU XGBoost):** `R² = 0.8249`, `MAE = 4.62 kWh`, `RMSE = 6.28 kWh` across `3,631` held-out hours.
* **Multivariate Sensor Anomaly Detection (PyTorch VAE):** Isolated real operational faults in Rooftop Unit 2 (`RTU-002`, peak mean reconstruction error `20.61` on Oct 14, 2020).
* **Full-Year Physical Simulation (18-Zone DOE Medium Office, 4,982.19 m², Surat TMYx Weather, 52,560 steps):**
  * **Tier 2 (`Occupancy + CO₂ + ToD DR, cost_first`) — Pareto-Optimal (Best NPV & Comfort):** `-30.9%` energy savings, 10-year NPV of **₹30.58M**, `800.2` comfort-degree-hours/yr, `CFPG = 0.465 yrs`.
  * **Tier 1 (`Smart Scheduling`) — Pareto-Optimal (Lowest Carbon & Fastest Payback):** `-29.7%` energy savings, `-3,826 tCO₂e` net 10-year carbon, `0.20 yr` (~2.4 mo) financial payback, `CFPG = 0.183 yrs`.
  * **Tier 3 (`PPO RL`) — Filtered Out by NSGA-II:** Achieved `-51.3%` raw energy reduction but exceeded the `1,200 deg-hrs/yr` comfort constraint (`7,927.8 deg-hrs`) due to short-horizon winter training (`5,120` steps).

---

## 📂 Repository Structure

```text
├── README.md                                  # Project documentation & setup guide
├── Whole_Building_AI_IoT_Retrofit.ipynb       # Complete end-to-end Google Colab pipeline
└── outputs/                                   # (Generated at runtime in Colab)
    ├── energyplus_retrofit_simulation_summary.csv
    ├── physical_financial_carbon_scorecard.csv
    ├── nsga2_pareto_retrofit_configurations.csv
    ├── nsga2_pareto_objectives.csv
    └── run_provenance.json
