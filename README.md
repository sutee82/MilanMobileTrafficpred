# Milan Mobile Traffic Prediction

## Description

This project aims to predict mobile traffic in Milan using various machine learning regression models. The project is structured as a series of Jupyter notebooks, each focusing on a specific part of the data science pipeline, from data preprocessing to model training and evaluation.

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

***



## Feature engineering 


## Models Used

The following machine learning models are explored in this project:
*   GPU accelerated (CuML) K-Nearest Neighbors (KNN) Regression
*   GPU accelerated (CuML) Random Forest Regression
*   XGBoost Regression

## How to Run

1.  Ensure you have Python and Jupyter Notebook installed.
2.  Clone the repository.
3.  Install the necessary dependencies (e.g., pandas, scikit-learn, xgboost, matplotlib, seaborn). You might find these listed at the beginning of each notebook.
    ```bash
    pip install pandas scikit-learn xgboost matplotlib seaborn jupyter
    ```
4.  Run the Jupyter notebooks 
