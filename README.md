# 🏠 California Housing Price Classification System

A full-stack **machine learning application** for classifying California housing prices into **LOW, MEDIUM, and HIGH** categories.  
This project demonstrates the **end-to-end ML lifecycle** — from data normalization and modeling to deployment using **FastAPI, Streamlit, Docker, and MLflow**.

---

## 📌 Project Overview

This project was developed as part of **EAS 503 – Final Project** under the guidance of **Prof. Mohammad Zia**.

### Key Capabilities
- Normalized relational database (3NF) using SQLite
- Feature engineering and stratified train/test split
- Multiple ML classification models with evaluation
- Best-performing **XGBoost classifier**
- REST API using **FastAPI**
- Interactive UI using **Streamlit**
- Containerized deployment using **Docker Compose**

---

## 🧠 Machine Learning Task

**Problem Type:** Multi-class Classification  
**Target Variable:** `price_class`  
**Classes:**
- `LOW`
- `MEDIUM`
- `HIGH`

---

## 📊 Best Model Performance

**Final Selected Model:** XGBoost Classifier

| Metric | Score |
|------|------|
| Accuracy | **82%** |
| Macro F1-score | **0.82** |

### Classification Report
          precision    recall  f1-score   support

    HIGH       0.89      0.84      0.86
     LOW       0.84      0.88      0.86
  MEDIUM       0.74      0.75      0.75

accuracy                           0.82



---

## 🗂️ Project Structure
housing_app_fall25_Siddy/
│
├── api/ # FastAPI backend
│ ├── app.py # Prediction API
│ └── Dockerfile
│
├── streamlit/ # Streamlit frontend
│ ├── app.py # UI
│ └── Dockerfile
│
├── notebooks/ # Jupyter notebooks
│ ├── 01_database_setup.ipynb
│ ├── 02_data_exploration.ipynb
│ ├── 03_modeling.ipynb
│ └── 04_model_evaluation.ipynb
│
├── data/
│ ├── housing.db # Normalized SQLite DB
│ └── data_schema.json # UI schema
│
├── models/
│ ├── final_xgb_classifier.pkl
│ └── label_encoder.pkl
│
├── docker-compose.yml
├── requirements.txt
└── README.md


---

## 🛠️ Installation

### Prerequisites
- Docker
- Docker Compose
- Git

---

### Clone Repository
```bash
git clone https://github.com/sidharth0909/Mkzia_Siddy.git
cd housing_app_fall25_Siddy
```

---

## ▶️ Running the Application (Local)

Start the full application using Docker:
```bash
docker compose up -d
```
Access the Services
Streamlit UI: http://localhost:8501
FastAPI Docs: http://localhost:8000/docs
Health Check: http://localhost:8000/health

## API USAGE
```bash
POST /predict
```

---


## 🖥️ Streamlit UI

The Streamlit app:
Automatically loads feature ranges from data_schema.json
Allows real-time prediction via the FastAPI backend
Displays predicted price class clearly

---


## 🧰 Technologies Used
Python
Scikit-learn
XGBoost
LightGBM
FastAPI
Streamlit
SQLite
Docker & Docker Compose
MLflow
Pandas & NumPy

---


## 🧑‍🏫 Academic Requirements Covered

✔ Database normalization (3NF)
✔ SQL JOIN queries
✔ Stratified train/test split
✔ Data profiling & correlation analysis
✔ 16 ML experiments (with & without PCA)
✔ MLflow logging
✔ Model persistence
✔ API + UI
✔ Docker deployment

---


## 🤝 Contributing

Pull requests are welcome.
For major changes, please open an issue first to discuss what you would like to change.

---


## 📄 License

This project is intended for academic use as part of EAS 503.
Reuse is permitted with proper attribution.

---


## 👤 Author

Sidharth Saholiya
University at Buffalo
EAS 503 – Fall 2025
Guided by Prof. Mohammad Zia
