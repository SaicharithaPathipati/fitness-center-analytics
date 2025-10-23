# fitness-center-analytics
predict the calorie burn and segment the people according to their fitness


# Fitness Center Analytics — Personalized Training with ML

**Personalize workouts with machine learning to boost outcomes, retention, and membership growth.**  
K-Means segmentation + calorie-prediction models (Multiple Linear Regression, Random Forest) power individualized plans and coaching.

---

## 🚀 TL;DR
- **Outputs:** 3 actionable member segments + a calorie-prediction model with **R² ≈ 0.94** (MLR).  
- **Best regression model:** **Multiple Linear Regression** (accuracy + interpretability).  
- **Key levers:** **Session duration** and **intensity (Avg BPM / HR zones)**; **hydration** helps; **fat %** and **hydration-need ratio** reduce burn.  
- **Clustering quality:** K=3, mean silhouette ≈ **0.17**; **Ward.D2** linkage strongest (silhouette ≈ **0.24**).

---

## 🧩 Problem & Goals
**Problem.** The gym needs to understand what drives calorie expenditure and how to group members for tailored programs that improve engagement and outcomes.

**Goals.**
- **Business:** Personalize plans by segment to improve results, **retention**, and sign-ups.  
- **Analytical:** (1) Build meaningful member segments; (2) Predict **Calories_Burned** and explain the drivers.

---

## 📦 Data (overview)
- **Entities:** demographics (Age, Gender), body metrics (Weight, Height, BMI, Fat%), workout behavior (Workout_Type, Session_Duration, Workout_Frequency, Experience_Level), **heart-rate metrics** (Max/Avg/Resting BPM), **hydration** (Water_Intake), and **Calories_Burned**.  
- **Engineered features:** **BMI_Category, Weight/Height Ratio, Heart-Rate Range, Heart-Rate Reserve, Heart Intensity Ratio, Calories per kg, Workout Intensity Score, Hydration Need Ratio, Age Group**.  
- **Quality:** No missing values after prep and checks.

---

## 🛠️ Feature Engineering & Selection
- Built training-load features (**Workout Intensity Score**, HR ratios), efficiency (**Calories per kg**), and hydration indicators (**Hydration Need Ratio**).  
- For regression, retained predictors with |corr| ≥ 0.20 (e.g., **Session_Duration**, **Intensity**, **Experience_Level**, **Calories_per_kg**, **Workout_Frequency**, **Water_Intake**, **Avg_BPM**; negatives: **Hydration_Need_Ratio**, **Fat_%**, **HR_Reserve**).  
- De-emphasized/removed weak signals (e.g., **Age, Height, Weight, BMI raw**, **Resting/Max BPM** alone).

---

## 🔎 EDA — What drives calories?
- **Session Duration** → strongest positive driver.  
- **Intensity / Avg BPM / Intensity ratios** → higher sustained effort → more calories.  
- **Hydration** → positive (Water_Intake); **Hydration-Need Ratio** → negative (inefficient hydration vs time).  
- **Fat %** → negative; **Experience Level** → slight negative (efficiency effect).  

---

## 🤖 Modeling

### A) Segmentation (Unsupervised)
- **Algorithms:** **K-Means** and **Hierarchical** (Ward.D2).  
- **Normalization:** z-score (features on comparable scale).  
- **Model choice:** **K = 3** (elbow) with mean silhouette ≈ **0.17**; **Ward.D2** showed best cohesion (≈ **0.24**).

**Member segments (K = 3).**
1) **Active & Hydrated** — moderate-long sessions, good hydration, solid burn.  
2) **Beginners** — higher BMI, lower intensity/duration; need on-ramps & hydration nudges.  
3) **Experienced / Fitness-Oriented** — leaner, higher intensity (HIIT/Strength).

### B) Calorie Prediction (Supervised)
- **Models compared:** **Multiple Linear Regression (MLR)** and **Random Forest (RF)** on a **70/15/15** train/val/test split.  
- **MLR (selected):** **MAE ≈ 51.3**, **RMSE ≈ 63.97**, **R² ≈ 0.94**.  
- **RF (benchmark):** **MAE ≈ 51.99**, **RMSE ≈ 66.84**, **R² ≈ 0.93**.  
- **Why MLR?** Slightly better error + **explainability** → clearer coaching levers.

---

## 🧭 Operational Playbook
**For coaches & product:**
- **Personalize plans** with segment + model drivers: extend **structured session duration**, train in **HR zones**, and **hydrate smarter**.  
- **Beginner track:** gentle progression, habit building, hydration cues.  
- **Experienced track:** HIIT/Strength blocks, performance targets, recovery focus.  
- **App logic:** show predicted calories, segment tag, and weekly adjustments (duration/intensity/hydration).

---

## 📊 Results (at a glance)
- **R² ≈ 0.94** calorie model; robust yet interpretable.  
- **3 segments** map directly to differentiated programming and nudges.  
- Clear **levers** (duration, intensity, hydration) to drive outcomes and retention.


