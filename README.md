# EV Smart Power Management System

Multi-output regression model for predicting real-time power allocation across EV subsystems, benchmarked against a rule-based Battery Management System (BMS) baseline.

## Overview

Modern EVs rely on rule-based logic to distribute battery power across propulsion, auxiliary, and infotainment subsystems. This project replaces that static approach with a data-driven model that learns power allocation patterns from real driving behavior — improving prediction accuracy while also estimating remaining vehicle range.

## Problem Statement

Given a vehicle's driving state (speed, acceleration, terrain, auxiliary load, etc.), predict:
1. **Propulsion power (P1)**
2. **Auxiliary power (P2)**
3. **Infotainment power (P3)**
4. **Remaining range**

...simultaneously, as a multi-output regression problem.

## Dataset

- **Training:** NEV (New Energy Vehicle) Energy Management Dataset — 4,806 rows after cleaning
- **Validation:** Real-world BMW i3 driving-cycle data — 70 trips, ~789K rows
- Dataset sources are not redistributed in this repo due to size/licensing; see `data/README.md` for access details

## Methodology

- **Model:** Multi-output Random Forest Regression
- **Key design decisions:**
  - Dropped the *Battery Degradation* feature due to high multicollinearity with State of Charge (SOC)
  - Ruled out LSTM/sequence models — the training data lacked temporal continuity needed for meaningful sequence learning
  - Reframed the problem from classification to multi-output regression for continuous, real-valued power allocation across subsystems
  - Added remaining range as a fourth model output, extending beyond the original 3-subsystem scope

## Results

Benchmarked against a rule-based BMS baseline, the model achieved a significant reduction in Mean Absolute Error (MAE) across all power allocation outputs — demonstrating that learned, data-driven allocation outperforms static rule-based logic on real driving-cycle data.

*(See `images/` for prediction vs. actual plots and MAE comparison charts.)


## Tech Stack

- Python (pandas, NumPy, scikit-learn)
- Matplotlib / Seaborn for visualization
- Jupyter Notebook

