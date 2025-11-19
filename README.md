# ASHRAE-Energy-Prediction
Kaggle ASHRAE Energy Prediction with end-to-end preprocessing, feature engineering, and site-based ML models.

## Overview

This is a project called **ASHRAE Energy Prediction** from Kaggle. The goal is to predict the energy usage (`meter_reading`) of buildings across multiple sites, based on metadata and weather data.  

The dataset is large, messy, real-world data with missing values, skewed distributions, outliers, and features that require different treatments. It was a perfect playground for doing some data cleaning, feature engineering, and building predictive modeling.  

---

## Motivation

I chose this project because it was challenging enough to apply my knowledge of regression problems while also learning new techniques and methods. Once again, I realized how important it is to study and understand the data before building models. In this project, the better preprocessing and feature engineering I did, the better my models performed.  

---

## Dataset

The dataset contains:  

- **Building metadata:** Information about each building (size, year built, primary use, etc.). Separate files for train and test.  
- **Weather data:** Site-specific weather features like temperature, wind, and cloud coverage. Separate files for train and test.  
- **Meter readings:** Energy consumption for each building at hourly timestamps (only in train file).  

There are shared columns between these files that are used to merge them (site_id, building_id, and timestamp)

**Challenges in the dataset:**

- Time alignment issues between building and weather data.  
- Missing values in weather and building features requiring different imputation methods.  
- Skewed distributions in the target variable.  
- Outliers and unrealistic sensor readings.  
- High cardinality features (building_id) and cyclic features (wind_direction, hour, etc.).

---

## Key Steps / Methods

I went through every step in this project in detail in my notebooks, explaining the reasoning behind each method and step. Here’s a summary:  

**Data Cleaning & Preprocessing**  
- Handling missing values (median imputation, forward/backward fill, time-based interpolation)  
- Removing unrealistic sensor values and extreme spikes  

**Feature Engineering**  
- Converting timestamps into meaningful features (`hour`, `day`, `month`) with cyclical encoding  
- Encoding categorical features  
- Creating additional features  

**Target Transformation**  
- Applied `log1p` transformation to handle heavy skewness in the target variable (`meter_reading`)  
- Compared with Yeo-Johnson power transform for validation  

**Model Selection & Tuning**  
- Tested tree-based models: RandomForest, XGBoost, LightGBM, CatBoost  
- Used site-specific models for better predictions  
- Hyperparameter tuning via `RandomizedSearchCV`  

**Final Model**  
- Trained final models on all training data per site  
- Saved models using `joblib`  
- Generated predictions on the test dataset  

---

## Notebooks

The project is divided into three notebooks:  

1. **`exploration_1.ipynb`** — Data exploration, baseline models, and initial feature analysis. This notebook was my first draft, explaining every step and why I chose it. At the end, I learned a lot but wasn’t completely satisfied with the results.  
2. **`exploration_2.ipynb`** — Advanced preprocessing, feature engineering, and site-based models.  
3. **`final_model.ipynb`** — Final models applied to the full training and test sets. This notebook trains on the complete dataset and generates predictions. Steps are mostly the same as in `exploration_2.ipynb`.  

---

## How to Reproduce Results

To reproduce the final predictions for the ASHRAE Energy Prediction project, follow these steps:

1. **Get the necessary files from this repository:**  
   - `best_models_per_site.pkl` — best models per site from `exploration_2.ipynb`  
   - `best_params_per_site.pkl` — best hyperparameters per site from `exploration_2.ipynb`  

2. **Run `final_model.ipynb`:**  
   - This notebook trains the final site-specific models on the full training data using the provided best models and hyperparameters.  
   - Predictions for the test dataset are generated and saved automatically.  

**Note:** You do not need to run `exploration_2.ipynb` to reproduce the final predictions, unless you want to explore or retrain the subset models yourself.

---

## Important

- This project was mostly done by me without the use of AI. The only section where I used AI was to get ideas on handling errors that I could not solve myself, outliers, memory issues, and cyclical features.  

---

## Lessons Learned

Through this project, I learned how critical it is to do thorough data exploration and preprocessing for building strong models. I explored and cleaned a messy real-world dataset, used advance feature engineering for better model performance, and built site-specific models. I also made sure each step was well-documented and reproducible, which helped me get reliable results.
