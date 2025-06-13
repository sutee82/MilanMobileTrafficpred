# Milan Mobile Traffic Prediction

## Description

This project aims to predict mobile traffic in Milan using various machine learning regression models. The project is structured as a series of Jupyter notebooks, each focusing on a specific part of the data science pipeline, from data preprocessing to model training and evaluation.

## Project Structure

The project is organized into the following Jupyter notebooks:

1.  `01_Data_preprocessing.ipynb`: Handles the initial data loading, cleaning, and preprocessing steps necessary for model training.
2.  `02_KNN_regression.ipynb`: Implements and evaluates a K-Nearest Neighbors (KNN) regression model for traffic prediction.
3.  `03_RandomForrest_modelling.ipynb`: Implements and evaluates a Random Forest regression model.
4.  `04_XBOOST_modeling.ipynb`: Implements and evaluates an XGBoost regression model.

## Models Used

The following machine learning models are explored in this project:
*   K-Nearest Neighbors (KNN) Regression
*   Random Forest Regression
*   XGBoost Regression

## How to Run

1.  Ensure you have Python and Jupyter Notebook installed.
2.  Clone the repository.
3.  Install the necessary dependencies (e.g., pandas, scikit-learn, xgboost, matplotlib, seaborn). You might find these listed at the beginning of each notebook.
    ```bash
    pip install pandas scikit-learn xgboost matplotlib seaborn jupyter
    ```
4.  Run the Jupyter notebooks in sequential order, starting from `01_Data_preprocessing.ipynb`.
