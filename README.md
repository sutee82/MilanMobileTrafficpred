# Milan Mobile Traffic Prediction

## Description

This project aims to predict mobile traffic in Milan using various machine learning regression models. The project is structured as a series of Jupyter notebooks, covering all aspect from data preprocessing to model training and evaluation.

## Project Structure

The project is organized into the following Jupyter notebooks:

1.  `01_Data_preprocessing.ipynb`: Handles the initial data loading, cleaning, and preprocessing steps necessary for model training.
2.  `02_KNN_regression.ipynb`: Implements and evaluates a K-Nearest Neighbors (KNN) regression model for traffic prediction.
3.  `03_RandomForrest_modelling.ipynb`: Implements and evaluates a Random Forest regression model.
4.  `04_XBOOST_modeling.ipynb`: Implements and evaluates an XGBoost regression model.

## Dataset

The dataset used in this project is a multi-source collection of urban life in the city of Milan and the Province of Trentino, Italy.

### Source

The dataset was curated and made available by:

Barlacchi, G., De Nadai, M., Larcher, R. et al. A multi-source dataset of urban life in the city of Milan and the Province of Trentino. *Sci Data* **2**, 150055 (2015). https://doi.org/10.1038/sdata.2015.55

It can be accessed through [nature.com](https://www.nature.com/articles/sdata201555).

### Time Period

The data spans a 2-month period from **November 1, 2013**, to **December 31, 2013**, with observations recorded every **10 minutes**.

### Data Components

The dataset is comprised of the following components:

#### 1. Call Detail Records (CDRs)

Provided by the **Semantics and Knowledge Innovation Lab (SKIL) of Telecom Italia**, the CDRs capture telecommunication activity. A record is generated for each of the following events:
* **Received SMS:** A user receives a text message.
* **Sent SMS:** A user sends a text message.
* **Incoming Call:** A user receives a phone call.
* **Outgoing Call:** A user makes a phone call.

#### 2. Precipitation Data

This includes meteorological information about precipitation in the covered area. The data is structured with the following features:
* **Area Covered:** The percentage of the geographical area experiencing precipitation.
* **Type:** The nature of the precipitation, categorized as `none`, `snow`, or `rain`.
* **Strength:** The intensity of the precipitation, rated on a scale from 0 to 3.

#### 3. National Holidays

To account for public holidays that may influence urban activity, a list of national holidays for the Milan region during the observation period has been generated and included.

## Performed data preprocessing to reduce dataset:
* Transformed millisecond timestamps into a standard datetime format, localized to 'Europe/Rome'.
* Only kept the middle 2500 square grid for processing (dropped 75% of the data) 
* Sums up SMS, call, and internet traffic activities based on unique 'Square ID' and time intervals as not interested in country code 
* Merges 'SMS-in'/'SMS-out' into a single 'SMS activity' and 'Call-in'/'Call-out' into 'Call activity' as not interested in direction of the activity
* Drops original, more granular SMS and call columns after combination.
* Results are a clean aggregated DataFrame suitable for further analysis and model training.

***



# Feature Engineering and Data Transformation

## Methodology

I performed extensive **feature engineering** and **data transformation** to prepare the dataset. The primary logic is encapsulated in two main Python functions: `comprehensive_data_transformation` for creating and modifying features, and `plot_transformation_effects` for visualizing the impact of these changes.

My `comprehensive_data_transformation` function takes the raw data and applies the following enhancements:

### 1. Temporal Feature Engineering
- **Cyclical Time Features**: I converted the `Time_Numeric` (hour of the day) into `hour_sin` and `hour_cos` features. This helps the model understand the cyclical nature of time (e.g., that 23:00 is as close to 00:00 as 01:00 is).
- **Time Periods**: I binned the `Time_Numeric` into categorical periods: `Night`, `Morning`, `Afternoon`, and `Evening`.
- **Day-of-Week Features**: From the `Date` column, I extracted the day of the week, created a binary `is_weekend` flag, and also generated `day_of_week_sin` and `day_of_week_cos` features to capture the weekly cycle.

### 2. Grid Square Feature Engineering
- **Grid Density**: I created a `grid_density` feature, which counts the occurrences of each `Milan_Grid_Square_ID`. This acts as a proxy for how active or important a particular grid cell is.
- **Average Grid Activity**: For each grid square, I calculated its average `SMS activity`, `Call activity`, and `Internet traffic activity` across the entire dataset, creating new features like `grid_avg_sms`.
- **Spatial Coordinates**: I derived `grid_x` and `grid_y` coordinates from the `Milan_Grid_Square_ID`, assuming a consistent numerical pattern (e.g., ID `5012` is treated as row `50`, column `12`).

### 3. Target Variable Transformations
- **Skewness Correction**: I checked the skewness of my target variables (`SMS activity`, `Call activity`, `Internet traffic activity`).
- **Applying Transformations**: For any target with a high absolute skewness (> 1.0), I applied three standard transformations to help normalize its distribution:
  - **Log Transformation**: `np.log1p` to handle potential zero values.
  - **Box-Cox Transformation**: A power transform that finds the best exponent to stabilize variance.
  - **Square Root Transformation**.

### 4. Interaction Features
- I created new features by combining existing ones to capture more complex relationships. Examples include:
  - `time_x_weekend`: The interaction between the hour of the day and whether it's a weekend.
  - `grid_density_x_time`: The interaction between a grid's density and the hour.
  - `sms_call_ratio`: The ratio of SMS to call activity.

## Models Used

The following machine learning models are explored in this project:
### GPU-Accelerated KNN Regression ⚡️

* **Model Training & Prediction**: A **K-Nearest Neighbors (KNN)** regressor is trained on **GPU-accelerated** data. Using **GridSearchCV**, the best number of neighbors was found to be 5. The final model then makes predictions on the test set.

* **Performance Evaluation**: The predictions are moved back to the **CPU** to calculate the overall **Mean Squared Error (MSE)** and **R-squared (R²)** scores, which evaluate the model's accuracy.

* **Detailed Analysis**: The model's performance is also assessed individually for each of the three target variables: '**SMS**', '**Call**', and '**Internet**' activity.

### XGBoost Regression  🤖

* **Data Preparation**: The script first separates the features and target variables, splits them into training and testing sets, and scales the features using `StandardScaler` to ensure model stability and improve performance.

* **Multi-Target Model Setup**: It defines an **XGBoost regressor** as the base model. Because the goal is to predict several target variables at once, this regressor is wrapped in scikit-learn's **`MultiOutputRegressor`**, which trains a separate XGBoost model for each target column.

* **Hyperparameter Tuning**: The script uses **`GridSearchCV`** to systematically test different combinations of hyperparameters (like the number of trees, tree depth, and learning rate). This process automates the search for the most effective model configuration, using 3-fold cross-validation to prevent overfitting.

* **Prediction with the Best Model**: After the grid search identifies the best-performing hyperparameters, it uses this optimal model to make predictions on the held-out test data.

* **Detailed Performance Evaluation**: Finally, the script evaluates the model's accuracy. It iterates through each target variable and calculates two key metrics:
    * **R-squared (R²)**: Measures how much of the variance in the target is explained by the model.
### Random Forest Multi-Target Regression 🌳

* **Data Preparation**: The script selects features and targets, fills any missing values with zero, splits the data into training and testing sets, and finally standardizes the features using `StandardScaler`.

* **Model Training**: A **Random Forest Regressor**, configured with specific hyperparameters (e.g., 200 trees, max depth of 15), is created. This model is then wrapped in a **`MultiOutputRegressor`** to enable it to predict multiple target variables at once.

* **Prediction & Evaluation**: The trained model makes predictions on the test data. The script then evaluates performance by calculating the **Mean Squared Error (MSE)**, **Root Mean Squared Error (RMSE)**, and **R-squared (R²)** for each individual target.

* **Execution & Output**: The entire process is encapsulated in a function that is called to train the model and return the final model, performance results, the scaler, and all data splits.

Of course. Here is the raw markdown code for the previous response.

Markdown

### Model Performance Conclusion

While all three models performed well, **XGBoost** is the superior choice, delivering the best combination of predictive accuracy and training efficiency.

### Model Comparison

* **XGBoost (Winner)** 🏆
    It achieved the lowest error rates across all categories and top-tier R² scores. Its fast, low-resource training makes it the most practical solution.
    * **SMS activity**: R² **0.9708**, RMSE **0.0509**
    * **Call activity**: R² **0.9579**, RMSE **0.0815**
    * **Internet traffic**: R² **0.9399**, RMSE **0.1064**

***

* **Random Forest**
    This model produced the highest R² scores, making it extremely accurate. However, its high error rates (RMSE) compared to XGBoost and its slow, resource-intensive training process make it a less optimal choice.
    * **SMS activity**: R² **0.9765**, RMSE **0.2031**
    * **Call activity**: R² **0.9702**, RMSE **0.2399**
    * **Internet traffic**: R² **0.9699**, RMSE **0.2291**

***

* **K-Nearest Neighbors (KNN)**
    A solid performer with good R² scores, but its accuracy and error rates were not competitive with the other two models.
    * **SMS activity**: R² **0.9010**, MSE **0.1737**
    * **Call activity**: R² **0.9565**, MSE **0.0841**
    * **Internet traffic**: R² **0.9065**, MSE **0.1630**

***

### Recommendation

For this project, **XGBoost is the recommended model**. It provides the most accurate predictions (especially considering its significantly lower RMSE values) while being the fastest and most efficient model to train.
