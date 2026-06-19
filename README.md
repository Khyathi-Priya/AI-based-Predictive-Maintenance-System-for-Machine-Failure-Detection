# AI-Based Predictive Maintenance System

## Overview
This project is an AI-powered Predictive Maintenance System developed using Machine Learning and Streamlit. The system analyzes machine operating parameters and predicts potential machine failures before they occur, helping reduce downtime and maintenance costs.

## Features
- Machine failure prediction using Machine Learning
- Interactive Streamlit dashboard
- Real-time user input and prediction
- Machine health monitoring
- Data-driven maintenance support
- Performance comparison of multiple ML algorithms

## Technologies Used
- Python
- Streamlit
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- LightGBM
- Matplotlib

## Project Structure

```text
├── app.py              # Streamlit frontend
├── model.py            # Machine learning backend
├── dataset.csv         # Dataset used for training
├── requirements.txt    # Project dependencies
└── README.md
```

## Machine Learning Models Used
- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier
- Gradient Boosting Classifier
- AdaBoost Classifier
- K-Nearest Neighbors (KNN)
- Support Vector Machine (SVM)
- Gaussian Naive Bayes
- XGBoost Classifier
- LightGBM Classifier

## Installation

Clone the repository:

```bash
git clone <repository-url>
cd ai-based-predictive-maintenance
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the application:

```bash
streamlit run app.py
```

## Application Workflow

1. User enters machine parameters.
2. Input data is processed by the predictive maintenance model.
3. The trained machine learning model predicts machine condition.
4. Results are displayed through an interactive Streamlit dashboard.
5. Visualizations help users understand machine health status.

## Objective

The objective of this project is to develop an intelligent maintenance system capable of predicting machine failures in advance, enabling proactive maintenance and improving operational efficiency.

## Author

Developed as an AI-Based Predictive Maintenance Project.
