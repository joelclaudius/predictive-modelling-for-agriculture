# Crop Prediction Model

This project involves the development of a machine learning model to predict the most suitable crop to plant based on soil properties. The model is built using logistic regression and trained on a dataset of soil measurements.

## Project Overview

The objective of this project is to create a predictive model that helps farmers decide which crop to plant based on the soil's Nitrogen (`N`), Phosphorus (`P`), Potassium (`K`), and pH levels. The model is evaluated based on its F1 score, and the best-performing feature is identified.

## Files in This Repository

- **`soil_measures.csv`**: The dataset containing the soil properties and the corresponding crop labels.
- **`crop_prediction.ipynb`**: The Jupyter Notebook containing the code for data loading, preprocessing, model training, evaluation, and selection of the best feature.
- **`app.py`**: The Flask application that serves as a backend API for predicting the crop based on soil properties.
- **`logistic_regression_K.pkl`**: The serialized logistic regression model trained on the `K` feature, which produced the best F1 score.
- **`requirements.txt`**: The Python dependencies required to run this project.
- **`README.md`**: This file, which provides an overview of the project.

## Dataset

The dataset (`soil_measures.csv`) contains the following columns:

- **`N`**: Nitrogen level in the soil.
- **`P`**: Phosphorus level in the soil.
- **`K`**: Potassium level in the soil.
- **`ph`**: pH level of the soil.
- **`crop`**: The crop type suitable for planting given the soil properties.

## Model Training

In the Jupyter Notebook:

1. **Data Loading**: The dataset is loaded using `pandas`.
2. **Data Preprocessing**: The data is split into features (`N`, `P`, `K`, `ph`) and the target variable (`crop`). Missing values are checked (though none are handled here since there are no missing values).
3. **Model Training**: Logistic regression models are trained on each individual feature to identify the best-performing one.
4. **Evaluation**: Each model is evaluated using the weighted F1 score, and the feature with the highest score is selected as the best predictor.
5. **Model Saving**: The best model (using the `K` feature) is saved using `joblib`.

## Flask API

The `app.py` file contains a Flask application that serves as a backend API:

- **`/` (GET)**: A welcome route to test the API.
- **`/predict` (POST)**: Accepts JSON data containing the soil properties (`N`, `P`, `K`, `ph`) and returns the predicted crop based on the trained logistic regression model.

### Example Request

```bash
curl -X POST http://localhost:5000/predict -H "Content-Type: application/json" -d '{"N": 90, "P": 40, "K": 70, "ph": 6.5}'
```
