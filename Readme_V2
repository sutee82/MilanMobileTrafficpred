# Milan Mobile Traffic Prediction

### Description

This project aims to predict mobile traffic in Milan using various machine learning regression models. The project is structured as a series of Jupyter notebooks, covering all aspects from data preprocessing to model training and evaluation.

### Project Structure

The project is organized into the following Jupyter notebooks:
* `01_Data_preprocessing.ipynb`: Handles the initial data loading, cleaning, and preprocessing steps.
* `02_KNN_regression.ipynb`: Implements and evaluates a K-Nearest Neighbors (KNN) regression model.
* `03_RandomForest_modelling.ipynb`: Implements and evaluates a Random Forest regression model.
* `04_XGBOOST_modeling.ipynb`: Implements and evaluates an XGBoost regression model.

---

### Dataset

The dataset used in this project is a multi-source collection of urban life in the city of Milan and the Province of Trentino, Italy.

* **Source**: Barlacchi, G., De Nadai, M., Larcher, R. et al. *A multi-source dataset of urban life in the city of Milan and the Province of Trentino*. Sci Data 2, 150055 (2015).
* **Time Period**: November 1, 2013, to December 31, 2013 (2 months).
* **Data Components**:
    1.  **Call Detail Records (CDRs)**: Aggregated SMS, call, and internet activity, recorded every 10 minutes.
    2.  **Meteorological Data**: Information on precipitation type (none, snow, rain) and intensity.
    3.  **National Holidays**: A list of public holidays for the Milan region.

---

### Data Preprocessing & Feature Engineering

#### Initial Processing
To prepare the data for analysis, several preprocessing steps were performed:
* Timestamps were converted to a standard `datetime` format localized to 'Europe/Rome'.
* To focus on the most active urban core and improve computational efficiency, the dataset was filtered to the central 2500 grid squares.
* The direction of communication was not relevant to predicting traffic volume, so `SMS-in`/`SMS-out` and `Call-in`/`Call-out` were merged into single `SMS activity` and `Call activity` features.

#### Feature Engineering
To help the models better understand temporal and spatial patterns, several new features were engineered:
* **Temporal Features**: Cyclical features (`hour_sin`, `day_of_week_cos`) were created to handle the cyclical nature of daily and weekly patterns. Categorical time periods (e.g., `Morning`, `Evening`) and an `is_weekend` flag were also generated.
* **Spatial Features**: Grid coordinates (`grid_x`, `grid_y`) were derived from the Grid ID. A `grid_density` feature was created to represent the overall activity level of each grid square.
* **Target Variable Transformation**: To normalize their distributions and improve model performance, target variables (`SMS`, `Call`, `Internet`) were transformed using log, Box-Cox, or square root transformations based on their skewness.

---

### Model Performance Conclusion

All three models demonstrated strong predictive capabilities, but **XGBoost emerged as the superior model**. It delivered the best combination of high accuracy (R²) and low prediction error (RMSE), making it the most reliable and efficient choice.

#### Model Comparison

Here is a comparison of the best-performing models, evaluated on the test set.

* **XGBoost (Winner) 🏆**
    * This model is the clear winner. It achieved excellent R² scores while maintaining the **lowest Root Mean Squared Error (RMSE)** across all targets. This indicates it not only explains the data well but also has the smallest average prediction error.
    * **SMS activity**: R² **0.9210**, RMSE **0.1420**
    * **Call activity**: R² **0.9626**, RMSE **0.0738**
    * **Internet traffic**: R² **0.9470**, RMSE **0.0923**

* **Random Forest 🌳**
    * The Random Forest model also produced high R² scores, proving to be a powerful predictor. However, its RMSE was slightly higher than XGBoost's, suggesting a marginally larger prediction error. Combined with its significantly slower training time, it is a less optimal choice.
    * **SMS activity**: R² **0.9765**, RMSE **0.2031**
    * **Call activity**: R² **0.9702**, RMSE **0.2399**
    * **Internet traffic**: R² **0.9699**, RMSE **0.2291**

* **K-Nearest Neighbors (KNN) ⚡️**
    * KNN served as a solid baseline but was not competitive with the more advanced ensemble models. It had the lowest R² scores and the highest RMSE, making it the least accurate of the three.
    * **SMS activity**: R² **0.9010**, RMSE **0.4168**
    * **Call activity**: R² **0.9565**, RMSE **0.2900**
    * **Internet traffic**: R² **0.9065**, RMSE **0.4037**

#### Final Recommendation

**XGBoost is the recommended model** for this mobile traffic prediction task. It provides the most accurate and reliable predictions by balancing an excellent fit (high R²) with the lowest prediction error (low RMSE), all while being computationally efficient.
