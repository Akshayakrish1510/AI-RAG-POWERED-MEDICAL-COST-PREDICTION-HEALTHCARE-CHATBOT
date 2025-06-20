 Medical-Price-prediction
        This project predicts the "healthcare costs of individuals" using machine learning models trained on demographic and health-related features. It aims to help users anticipate and manage their medical expenses proactively—especially in an era of rising healthcare     demand and cost.

 1. Project Highlights

 Predicts medical charges using patient data
 Built-in evaluation metrics (R², RMSE, MAE)
 Uses models like Random Forest and XGBoost
 Interactive Streamlit dashboard to explore high-cost predictions
 Outputs predictions and saves filtered results (e.g., ₹50,000+)

2.  Dataset

Here I used the public "insurance.csv" dataset which includes:
a) age – age of the person
b) sex – gender
c) bmi – body mass index
d) children – number of children
e) smoker – whether the person smokes
f) region – location
g) charges – actual medical expenses (target variable)

 3.Technologies Used

 Category-------------------Tools & Libraries                              
      |                       |     
 Programming -------------- Python                                          
 Data Analysis ------------ pandas, numpy                                   
 ML Models ---------------- scikit-learn, xgboost                          
 Visualization ------------ matplotlib, seaborn                             
 Web App (UI) ------------- Streamlit                                       

4. ML Models Used

Random Forest Regressor (primary model)
XGBoost Regressor (optional advanced model)
Evaluation Metrics: R² Score, RMSE, MAE

5. How to Run

Setup Environment

'terminal' >
pip install -r requirements.txt
