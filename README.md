# 🏠 California Housing Price Classification App  
**EAS 503 – Final Project (Fall 2025)**  

**Student:** Sidharth Saholiya  
**Instructor:** Mohammad Zia  
**Course:** EAS 503 – Data Science  

---

## 📌 Project Overview

This project is a **full end-to-end machine learning system** that classifies California housing blocks into **price categories**:

- **LOW**
- **MEDIUM**
- **HIGH**

The application covers the **entire ML lifecycle**:
- Database normalization (3NF)
- Data exploration & profiling
- Feature preprocessing pipelines
- Multiple ML experiments with cross-validation
- Model selection using **macro F1-score**
- Model deployment using **FastAPI**
- User interface using **Streamlit**
- Containerized deployment using **Docker Compose**

---

## 🎯 Problem Formulation

Instead of predicting an exact house price (regression), the problem is converted into a **multi-class classification task**.

This approach:
- Simplifies interpretation
- Handles capped values better
- Enables balanced evaluation using F1-score

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
│ ├── data_schema.json # UI schema
│
├── models/
│ ├── final_xgb_classifier.pkl
│ └── label_encoder.pkl
│
├── docker-compose.yml
├── requirements.txt
└── README.md

## 🗄️ Database Design (3NF)

The raw dataset was normalized into **Third Normal Form (3NF)**.

### Tables
- `block`
- `block_housing_stats`
- `ocean_proximity`
- `price_class`

### Example SQL JOIN

```sql
SELECT
    b.longitude,
    b.latitude,
    s.housing_median_age,
    s.total_rooms,
    s.total_bedrooms,
    s.population,
    s.households,
    s.median_income,
    op.name AS ocean_proximity,
    pc.label AS price_class
FROM block b
JOIN block_housing_stats s ON b.block_id = s.block_id
JOIN ocean_proximity op ON op.ocean_proximity_id = b.ocean_proximity_id
JOIN price_class pc ON pc.price_class_id = s.price_class_id;
✔ No redundancy
✔ Referential integrity
✔ Efficient querying

📊 Exploratory Data Analysis (EDA)
Key Observations
Target classes are perfectly balanced

Strong correlation between:

median_income and price class

Geographic location and price

Missing values present in total_bedrooms

Capped values in housing_median_age

Tools Used
Pandas

Correlation matrix

ydata-profiling

Distribution plots

🔄 Train / Test Split
A stratified split was used to preserve class balance.

matlab
Copy code
Train:
LOW       ~33.35%
MEDIUM    ~33.32%
HIGH      ~33.33%

Test:
LOW       ~33.36%
MEDIUM    ~33.31%
HIGH      ~33.33%
🧪 Machine Learning Experiments
Preprocessing Pipeline
SimpleImputer (median)

StandardScaler

OneHotEncoder

ColumnTransformer

Models Evaluated
Model	Test F1 (Macro)
Logistic Regression	0.72
Ridge Classifier	0.68
Gradient Boosting	0.78
XGBoost (Final)	0.82
LightGBM	0.81

🏆 Final Model – XGBoost
Performance
yaml
Copy code
Accuracy: 0.82
Macro F1: 0.82
Classification Report
java
Copy code
HIGH    F1 = 0.86
LOW     F1 = 0.86
MEDIUM  F1 = 0.75
✔ Best generalization
✔ Balanced precision & recall
✔ Robust to feature scaling

💾 Model Persistence
Saved using joblib:

final_xgb_classifier.pkl

label_encoder.pkl

🚀 FastAPI Backend
Endpoints
POST /predict

GET /health

Example Request
json
Copy code
{
  "instances": [
    {
      "longitude": -118.49,
      "latitude": 34.26,
      "housing_median_age": 29,
      "total_rooms": 2127,
      "total_bedrooms": 435,
      "population": 1166,
      "households": 409,
      "median_income": 3.53,
      "ocean_proximity": "NEAR BAY"
    }
  ]
}
Example Response
json
Copy code
{
  "predictions": ["HIGH"]
}
🖥️ Streamlit Frontend
Dynamic form generation from data_schema.json

Validated inputs

Real-time predictions

Access locally:

arduino
Copy code
http://localhost:8501
🐳 Docker Deployment
Run Locally
bash
Copy code
docker compose up -d
Services
Service	Port
FastAPI	8000
Streamlit	8501

☁️ Cloud Deployment
The same Docker Compose setup runs on:

DigitalOcean

AWS EC2

Any Linux VM with Docker

No code changes required.

📤 How to Push This Project to GitHub (STEP-BY-STEP)
1️⃣ Go inside the project folder
bash
Copy code
cd housing_app_fall25_Siddy
2️⃣ Initialize Git (if needed)
bash
Copy code
git init
3️⃣ Add your fork as remote (check first)
bash
Copy code
git remote -v
If not present:

bash
Copy code
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
4️⃣ Add files
bash
Copy code
git add .
5️⃣ Commit changes
bash
Copy code
git commit -m "Final EAS 503 Housing Price Classification Project"
6️⃣ Push to GitHub
bash
Copy code
git branch -M main
git push -u origin main
🎤 Presentation (12–15 Minutes)
Topics covered:

Problem formulation

Database normalization

EDA insights

Modeling experiments

Final model selection

Deployment architecture

Live demo

✅ Grading Rubric Coverage
✔ Database normalization (3NF)
✔ SQL JOIN queries
✔ Stratified split
✔ EDA & profiling
✔ 16+ ML experiments
✔ MLflow logging
✔ Model persistence
✔ FastAPI deployment
✔ Streamlit UI
✔ Docker Compose
✔ Cloud-ready setup

👤 Author
Sidharth Saholiya
MS Data Science – University at Buffalo
