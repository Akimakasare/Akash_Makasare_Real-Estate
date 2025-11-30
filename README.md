**India Housing Investment & Price Predictor**

**Project Overview**
This project implements an end-to-end Machine Learning solution for the Indian housing market. It involves data preprocessing, training two types of ML models (Classification and Regression), tracking the experiments using MLflow, and deploying the results in an interactive web application using Streamlit.

**Key Objectives:**

Classification: Predict whether a property is a "Good Investment" (proxied by High Public Transport Accessibility).
Regression: Predict the "Estimated Price after 5 Years" (proxied by the current Price in Lakhs).
MLflow Integration: Track model performance, parameters, and log model artifacts for governance.
Streamlit Deployment: Provide a user-friendly interface for making predictions and visualizing data insights.

**Project Structure**
The project consists of three main phases, executed across two primary Python scripts:
ML Development & MLflow Tracking (Steps 1-4)

Streamlit Application (Step 5)

Prerequisites

To run this project, you need a Python environment (e.g., Anaconda, Google Colab, or a virtual environment) and the following libraries:

# Core dependencies
pip install pandas numpy scikit-learn

# MLflow and Visualization dependencies
pip install mlflow plotly pyngrok

# Web application framework
pip install streamlit


**Data**

The project uses the India_housing_prices (Akash Makasare).csv file. Please ensure this file is placed in the root directory of your project where the scripts are executed.

Step-by-Step Execution Guide

Phase 1: Model Training and MLflow Tracking

This phase handles data cleaning, feature engineering, model training (using Random Forest as the final model), and logging everything to a local MLflow tracking server.

Action: Run the full combined Python script (Steps 1-4) in your Jupyter Notebook or Colab environment.

Phase 2: Streamlit Application Deployment

The Streamlit application provides the user interface for predictions and visualization. It relies on the models logged in the MLflow Registry during Phase 1.

File: streamlit_app.py

1. Save the Streamlit Script

Ensure the provided streamlit_app.py code is saved locally.

2. Run the App Locally (Recommended)

If running in a local terminal, execute:

streamlit run streamlit_app.py


3. Run the App in Google Colab (Using ngrok)

If you are running the project in Google Colab, use the following code in a new cell to launch the app and generate a public URL:

from pyngrok import ngrok
import subprocess
import os
import time

# Kill any existing ngrok tunnels
ngrok.kill()

# Define the Streamlit command
command = ["streamlit", "run", "streamlit_app.py", "--server.port", "8501", "--browser.serverAddress", "localhost"]

# Start the Streamlit process in the background
process = subprocess.Popen(command)
time.sleep(5) # Give the server a moment to start

# Open a tunnel to the Streamlit port (8501)
try:
    public_url = ngrok.connect(8501)
    print(f"Streamlit App is running at: {public_url}")
except Exception as e:
    print(f"Error opening ngrok tunnel: {e}")


MLflow Management

All experiments are logged under the experiment name Housing_Price_Prediction_EDA.

Viewing the MLflow UI

To view the logged runs, compare metrics, and inspect the registered models locally or in Colab, run the following command in a separate terminal or Colab cell:

# Run this command in a terminal where 'mlruns' directory is present
# The MLflow UI provides an overview of all your tracked experiments.
!mlflow ui --port 5000 


If running in Colab, use the pyngrok tunnel code provided in the previous steps to expose port 5000 and view the UI in your browser.

Note: This project uses Random Forest models for logging, as they provide interpretable Feature Importance scores for the Streamlit visualizations.
