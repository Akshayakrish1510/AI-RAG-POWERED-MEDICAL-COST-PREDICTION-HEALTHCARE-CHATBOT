AI & RAG Powered Medical Cost Prediction & Healthcare Assistant

-XGBoost regression for medical-cost prediction
-SHAP explanations for individual predictions
-RAG pipeline with ChromaDB and sentence-transformer embeddings
-Source-aware LLM responses
-FastAPI REST API with validation and Swagger docs
-Streamlit dashboard
-PostgreSQL-ready SQLAlchemy persistence layer
-Automated tests
-Docker support
-GitHub Actions CI
-Clear distinction between U.S. insurance charges and Indian healthcare pricing


Technology

Language - Python 
ML - XGBoost, scikit-learn 
Explainability - SHAP 
RAG - LangChain 
Embeddings - Sentence Transformers 
Vector DB - ChromaDB 
LLM - Groq 
API - FastAPI + Pydantic 
UI - Streamlit 
Database - SQLAlchemy / PostgreSQL-ready 
Testing - Pytest 
Deployment - Docker 
CI/CD - GitHub Actions 

Run Locally

### 1. Create environment

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

### 2. Install

```bash
pip install -r requirements.txt
```

### 3. Train

```bash
python scripts/train_model.py
```

This creates:

```text
models/medical_cost_xgboost.joblib
models/metrics.json
```

### 4. Build the vector store

```bash
python -c "from app.rag_pipeline import build_vector_store; build_vector_store()"
```

### 5. Configure Groq

Copy `.env.example` to `.env` and provide your API key.

### 6. Launch Streamlit

```bash
streamlit run frontend/streamlit_app.py
```

### 7. Launch FastAPI

```bash
uvicorn app.main:app --reload
```

Then open:

```text
http://127.0.0.1:8000/docs
```

ML Pipeline

```text
Dataset
   ↓
Train/Test Split
   ↓
Preprocessing
   ↓
XGBoost Regression
   ↓
MAE / RMSE / R²
   ↓
Residual Analysis
   ↓
Prediction + Empirical Range
   ↓
SHAP Explanation
```

RAG Pipeline

```text
Medical Documents
       ↓
Chunk / Index
       ↓
Sentence Transformers
       ↓
ChromaDB
       ↓
Similarity Search
       ↓
Relevant Context
       ↓
Groq LLM
       ↓
Answer + Sources
```

## 📊 Prediction Output

The API returns:

```json
{
  "prediction": 12450.21,
  "lower_bound": 10820.50,
  "upper_bound": 14079.92,
  "mae": 1234.56,
  "r2": 0.86
}
```

The lower/upper values are an empirical residual-based range for this portfolio experiment. They are **not** a statistical confidence interval and should not be interpreted as an actual hospital or insurer quote.

## 🔍 Explainability

The `/explain` endpoint uses SHAP to identify which transformed input features contributed most to an individual model prediction.

Example:

```text
smoker_yes     → positive contribution
bmi            → positive contribution
age            → positive contribution
children       → smaller contribution
```

