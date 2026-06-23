<div align="center">

# 🛠️ AI-Based Predictive Maintenance and Suggestion System for CNC Machines

**An intelligent system that predicts CNC machine failures before they happen and recommends maintenance actions, powered by supervised Machine Learning.**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-0066CC?style=for-the-badge&logo=xgboost&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)

[![GitHub stars](https://img.shields.io/github/stars/Khyathi-Priya/AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection?style=flat&color=6C63FF)](https://github.com/Khyathi-Priya/AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/Khyathi-Priya/AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection?style=flat&color=6C63FF)](https://github.com/Khyathi-Priya/AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection/network)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat)](LICENSE)

</div>

---

## 📌 Overview

Unplanned downtime in manufacturing is costly and disruptive. This project builds an **AI-driven predictive maintenance system** that:

- 📡 Takes real-time CNC machine parameters as input (temperature, torque, speed, tool wear)
- 🤖 Predicts the probability of failure using a trained **XGBoost classifier**
- 🧠 Identifies the likely **reasons for failure** based on sensor patterns
- 🛠️ Recommends specific **maintenance actions** to prevent breakdown
- 📊 Displays results on an interactive **Streamlit dashboard**

> Built and benchmarked using the **AI4I 2020 Predictive Maintenance Dataset** — a real-world industrial sensor dataset for failure classification.

---

## 📸 Screenshots

### 🖥️ Input Parameters for healthy manchine
![App Input Form](pictures/Screenshot%202026-06-19%20153315.png)

### ✅ Healthy Machine Prediction
![No Failure Predicted](pictures/Screenshot%202026-06-19%20153801.png)

### Health status
![Healthy machine](pictures/Screenshot%202026-06-19%20153837.png)

### Suggestions
![suggestions](pictures/Screenshot%202026-06-19%20153846.png)

### 🖥️ Input Parameters for Unhealthy manchine
![Unhealthy](pictures/Screenshot%202026-06-19%20153949.png)

### ⚠️ Failure Risk Prediction
![Failure Predicted](pictures/Screenshot%202026-06-19%20154007.png)

### Health status
![Unhealthy machine](pictures/Screenshot%202026-06-19%20154027.png)

### 🧠 Failure Reasons & Maintenance Suggestions
![Failure Reasons and Suggestions](pictures/Screenshot%202026-06-19%20154038.png)

### 📊 Model Accuracy Comparison
![Model Accuracy Comparison](pictures/Screenshot%202026-06-19%20154017.png)

### 📋 Detailed Model Comparison Table
![Model Comparison Table](pictures/Screenshot%202026-06-19%20154007.png)

---

## 🧠 System Architecture

```
Machine Sensor Inputs
(Type, Temperature, Torque, Speed, Tool Wear)
        ↓
Feature Engineering Layer
        ↓
ML Model — XGBoost Classifier
        ↓
Prediction Output (Healthy / Failure Risk %)
        ↓
Rule-Based Reasoning Engine
        ↓
Failure Reason Identification → Maintenance Suggestion
        ↓
Streamlit Dashboard + Health Visualization
```

---

## 📂 Dataset — AI4I 2020

The **AI4I 2020 Predictive Maintenance Dataset** contains labeled sensor readings from industrial machines representing both healthy operation and various failure conditions.

> ⚠️ **Note:** Download the dataset directly from Kaggle if not already included in the repo:
>
> [![Kaggle](https://img.shields.io/badge/Download%20Dataset-Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)](https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020)
>
> After downloading, place the CSV file in the project root directory before running.

| Class | Description |
|---|---|
| Healthy (0) | Machine operating normally |
| Failure Risk (1) | Machine showing signs of impending failure |

---

## 🔍 Features Used

The model analyzes the following machine parameters:

| Feature Category | Features |
|---|---|
| Machine Info | Machine Type (L / M / H) |
| Temperature | Air Temperature (K), Process Temperature (K) |
| Mechanical Load | Rotational Speed (rpm), Torque (Nm) |
| Wear Indicator | Tool Wear (min) |

---

## 🤖 ML Model — XGBoost Classifier

The core prediction engine is an **XGBoost Classifier**, selected after benchmarking against 9 other supervised models.

### Why XGBoost?
- Highest overall Accuracy (98.9%) and ROC-AUC (0.964) among all tested models
- Handles imbalanced failure/healthy classes effectively
- Fast inference suitable for a real-time dashboard
- Robust to noise in sensor readings

### Models Compared

- Logistic Regression
- Decision Tree
- Random Forest
- K-Nearest Neighbors (KNN)
- Support Vector Machine (SVM)
- Naive Bayes
- AdaBoost
- Gradient Boosting
- **XGBoost** ✅ (Best Model)
- LightGBM

### Approach: Implement All, Then Pick the Best

Rather than assuming one algorithm upfront, **all 10 supervised classification models were implemented and trained on the same preprocessed dataset**, then evaluated side-by-side on Accuracy, Precision, Recall, F1 Score, and ROC-AUC. **XGBoost came out on top** across the key metrics and was carried forward as the model powering the live app.

### Training Pipeline (`model.py`)

```
Raw CSV Data (AI4I 2020)
        ↓
Data Preprocessing
  → Drop irrelevant columns (UDI, Product ID)
  → Encode categorical features (Machine Type)
  → Scale numerical features
        ↓
Train/Test Split (80/20)
        ↓
Implement & Train All 10 Classification Models
        ↓
Evaluate & Compare (Accuracy, Precision, Recall, F1, ROC-AUC)
        ↓
Best Model Identified — XGBoost
        ↓
XGBoost Used for Live Predictions in app.py
```

### How Predictions Work

At inference time (`app.py`):
1. User enters machine parameters via the Streamlit form
2. The input feature vector is preprocessed the same way as during training
3. The trained XGBoost model outputs a failure probability score
4. If failure risk is high, the reasoning engine flags the likely causes and suggests maintenance steps

> 📌 **To retrain the model**, run `model.py` after placing the AI4I 2020 dataset CSV in the project root. This re-runs the full comparison across all 10 models and refits the best one (XGBoost) for use in the app.

---

## 🧠 Failure Reasoning & Maintenance Engine

When a failure is predicted, the system explains **why** and **what to do about it**:

```
IF prediction == "Failure Risk":
    → Identify contributing factors
        (High Tool Wear / High Process Temp / High Rotational Speed)
    → Generate Failure Reasons
    → Generate Maintenance Suggestions
ELSE:
    → Mark as Healthy
    → Suggest routine preventive maintenance
```

### Example Outputs

| Condition | Output |
|---|---|
| 🟢 Healthy | "Continue routine preventive maintenance." |
| 🔴 Failure Risk | "Replace cutting tool", "Check coolant circulation system", "Reduce machine operating speed" |

---

## 🌐 Streamlit Dashboard (`app.py`)

The interactive dashboard provides:

- ✅ Live machine parameter input form
- ✅ Real-time failure prediction with probability %
- ✅ Machine health status pie chart (Healthy vs Failure Risk)
- ✅ Failure reason breakdown
- ✅ Maintenance action suggestions

---

## ⚙️ Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/Khyathi-Priya/AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection.git
cd AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Download the Dataset
Download from [Kaggle](https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020) and place the CSV file in the project root.

### 4. Train & Compare the Models *(implements all 10 models, including XGBoost)*
```bash
jupyter notebook model.py
```

### 5. Run the Application
```bash
streamlit run app.py
```

---

## 📁 Project Structure

```
AI-based-Predictive-Maintenance-System-for-Machine-Failure-Detection/
│
├── app.py                    # Streamlit dashboard
├── model.py     # Model training & comparison notebook (all 10 models)
├── requirements.txt          # Python dependencies
└── images/                   # Screenshots
```

---

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core language |
| Scikit-learn | Classical ML models & preprocessing |
| XGBoost / LightGBM | Gradient boosting models |
| Pandas & NumPy | Data loading & feature processing |
| Matplotlib | Visualization |
| Streamlit | Interactive real-time dashboard |

---

## 🚀 Future Enhancements

- [ ] Real-time IoT sensor data integration
- [ ] Multi-class failure type prediction (instead of binary)
- [ ] Cloud deployment on AWS / Azure / Streamlit Cloud
- [ ] Automated maintenance scheduling & ticket creation
- [ ] Model retraining pipeline for continuous learning
- [ ] SHAP-based explainability for failure predictions

---

## 👩‍💻 Author

**Khyathi Priya**
B.Tech — Computer Science Engineering (AI & ML)

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/Khyathi-Priya)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/khyathipriya/)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
