 # Milan Mobile Traffic Prediction

## NON-TECHNICAL EXPLANATION OF YOUR PROJECT

This forecasting tool predicts mobile phone usage—including calls, texts, and internet data—across different areas of Milan. Its primary purpose is to assist network operators in anticipating demand spikes, enabling them to allocate resources efficiently and prevent service disruptions such as dropped calls or slow data speeds. This ensures a more reliable experience for customers. The tool also serves as a valuable resource for urban planners who study mobility patterns within the city.

## DATA

The project utilizes a multi-source dataset documenting urban life in Milan, Italy, from November 1, 2013, to December 31, 2013. The data combines aggregated Call Detail Records (CDRs) for SMS, calls, and internet activity, along with meteorological data and a list of national holidays. The dataset was filtered to focus on the central 2500 grid squares of the city.

**Citation:** Barlacchi, G., De Nadai, M., Larcher, R. et al. A multi-source dataset of urban life in the city of Milan and the Province of Trentino. *Sci Data* 2, 150055 (2015).

## MODEL

The project evaluated three different regression models to predict mobile traffic: K-Nearest Neighbors (KNN), Random Forest, and XGBoost. These models were chosen to compare a baseline algorithm (KNN) with more advanced and powerful ensemble methods (Random Forest and XGBoost), which are well-suited for handling complex, non-linear patterns in time-series data.

## HYPERPARAMETER OPTIMSATION

For all models the Gridsearch was used for Hyperparameter optimization. This was done using a limited dataset due to hight computational requirements for 2 out of the three models (KNN and Random Forest).

## RESULTS

A comparison of the three models showed that while all were strong predictors, **XGBoost was the superior model**. It delivered the best combination of high accuracy (R²) and low prediction error (RMSE), making it the most reliable and efficient choice for this forecasting task.

### Model Comparison

Below is a performance summary for each model on the test set:

**XGBoost (Winner) 🏆**
This model achieved the best balance of high R² scores and the lowest Root Mean Squared Error (RMSE), indicating the smallest average prediction error.
* **SMS activity**: R² 0.9210, RMSE 0.1420
* **Call activity**: R² 0.9626, RMSE 0.0738
* **Internet traffic**: R² 0.9470, RMSE 0.0923

**Random Forest 🌳**
This model produced high R² scores but had slightly higher prediction errors (RMSE) and a significantly slower training time than XGBoost.
* **SMS activity**: R² 0.9765, RMSE 0.2031
* **Call activity**: R² 0.9702, RMSE 0.2399
* **Internet traffic**: R² 0.9699, RMSE 0.2291

**K-Nearest Neighbors (KNN) ⚡️**
KNN served as a solid baseline but was the least accurate model, with the lowest R² scores and the highest RMSE.
* **SMS activity**: R² 0.9010, RMSE 0.4168
* **Call activity**: R² 0.9565, RMSE 0.2900
* **Internet traffic**: R² 0.9065, RMSE 0.4037

### Final Recommendation

**XGBoost is the recommended model** for this mobile traffic prediction task. It provides the most accurate and reliable predictions by balancing an excellent fit (high R²) with the lowest prediction error (low RMSE), all while being computationally efficient.
