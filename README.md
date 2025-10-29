# Fleet-Management

# 🚀 Fleet Manager: Fuel Consumption Prediction Model

This repository contains the training script and data schema for a machine learning model that predicts fuel consumption for vehicle routes.

The model is trained on historical data (`routes_distance.csv`) and saved as a single file (`fleet_model.pkl`). This saved model is intended to be loaded by other applications (like an optimization system or API) to forecast costs for new, unseen routes.

---

## 📦 Model Details

* **Model Type:** Random Forest Regressor (`sklearn.ensemble.RandomForestRegressor`)
* **Purpose:** To predict a continuous numerical value (regression).
* **Target Variable:** `Fuel_Consumption_L` (Fuel consumed in liters)
* **Input Features:**
    * `Distance_KM` (Type: Numerical)
    * `Weather_Impact` (Type: Categorical)

---

## ⚙️ How It Works: The Training Pipeline

The `train_and_save.py` script builds and trains a `scikit-learn` **Pipeline**. This pipeline automatically handles all required pre-processing and then trains the model.

1.  **Data Loading:** Loads the `routes_distance.csv` file into a pandas DataFrame.
2.  **Preprocessing (`ColumnTransformer`):**
    * **Numerical Features:** `Distance_KM` is passed through without changes.
    * **Categorical Features:** `Weather_Impact` is transformed using a `OneHotEncoder`. This converts text labels (e.g., 'Low', 'Medium') into numerical columns.
3.  **Model Training:**
    * The pre-processed data is fed into a `RandomForestRegressor` (with 100 estimators).
    * The model learns the complex patterns between distance, weather, and fuel usage.
4.  **Serialization (Saving):**
    * The entire pipeline (pre-processor + trained model) is saved as a single file, `fleet_model.pkl`, using `joblib`.

---

## 🛠️ How to Re-Train the Model

Follow these steps to train a new version of the model on updated data.

### 1. Requirements
Ensure you have the required Python libraries installed:

```bash
pip install pandas scikit-learn joblib
```
### 2. Data Preparation
Place your historical route data in the root of this folder.

File Name: routes_distance.csv

Required Columns: Your CSV must contain the following columns:

Distance_KM

Weather_Impact

Fuel_Consumption_L

### 3. Run the Training Script
Execute the script from your terminal:

```bash
python train_and_save.py
```
### 4. Output
After running, you will see this output, and a new file will be created:

Starting model training...
Model trained successfully.
Model saved successfully as fleet_model.pkl!
This fleet_model.pkl file is your complete, pre-trained model, ready for use in your main application.
