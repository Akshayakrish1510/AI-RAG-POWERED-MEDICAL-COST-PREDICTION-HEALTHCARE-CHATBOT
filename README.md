# 🏥 AI & RAG Powered Medical Cost Prediction & Healthcare Assistant

**Portfolio-grade AI application combining explainable XGBoost regression, RAG, vector search, LLMs, FastAPI and Streamlit.**

> **Healthcare safety:** This project is an educational software demonstration. It does not diagnose conditions, prescribe treatment, or provide a guaranteed medical/insurance quote.

## 🚀 What makes this version stronger

- **XGBoost regression** for medical-cost prediction
- **SHAP explanations** for individual predictions
- **Empirical prediction range** based on held-out residuals
- **RAG pipeline** with ChromaDB and sentence-transformer embeddings
- **Source-aware LLM responses**
- **FastAPI REST API** with validation and Swagger docs
- **Streamlit dashboard**
- **PostgreSQL-ready SQLAlchemy persistence layer**
- **Automated tests**
- **Docker support**
- **GitHub Actions CI**
- Clear distinction between U.S. insurance charges and Indian healthcare pricing

## 🧠 Architecture

```text
                         ┌────────────────────┐
                         │    Streamlit UI    │
                         └─────────┬──────────┘
                                   │
                  ┌────────────────┴────────────────┐
                  │                                 │
          Cost Prediction                       RAG Assistant
                  │                                 │
              XGBoost                         Embeddings
                  │                                 │
                SHAP                           ChromaDB
                  │                                 │
           Prediction + Range                 Retrieved Docs
                  │                                 │
                  │                              Groq LLM
                  │                                 │
                  └──────────────┬──────────────────┘
                                 │
                              FastAPI
                                 │
                         PostgreSQL-ready
                           persistence
```

## 🛠️ Technology

| Layer | Technology |
|---|---|
| Language | Python |
| ML | XGBoost, scikit-learn |
| Explainability | SHAP |
| RAG | LangChain |
| Embeddings | Sentence Transformers |
| Vector DB | ChromaDB |
| LLM | Groq |
| API | FastAPI + Pydantic |
| UI | Streamlit |
| Database | SQLAlchemy / PostgreSQL-ready |
| Testing | Pytest |
| Deployment | Docker |
| CI/CD | GitHub Actions |

XGBoost supports TreeSHAP-based model explanations, and current XGBoost documentation also documents GPU acceleration for training and SHAP workloads. citeturn0search3turn0search4

## 📂 Project Structure

```text
ai-medical-cost-rag/
├── app/
│   ├── main.py
│   ├── predictor.py
│   ├── rag_pipeline.py
│   └── database.py
├── data/
│   ├── demo_insurance.csv
│   └── medical_documents/
├── docs/
│   └── API.md
├── frontend/
│   └── streamlit_app.py
├── models/
├── scripts/
│   └── train_model.py
├── tests/
├── .github/workflows/ci.yml
├── Dockerfile
├── requirements.txt
└── README.md
```

## ⚙️ Run Locally

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

FastAPI's documentation recommends testing applications and pinning versions when preparing a reproducible deployment, which is why this project includes tests and a controlled dependency setup. citeturn0search1

## 🔬 ML Pipeline

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

## 🔎 RAG Pipeline

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

These are **model contributions**, not medical causal claims.

## 💬 RAG Example

Question:

> What factors can affect an insurance medical cost estimate?

The application retrieves relevant documents from ChromaDB and sends only the retrieved context to the LLM, producing an answer with the filenames used as sources.

## 🧪 Tests

Run:

```bash
pytest -q
```

GitHub Actions automatically runs the test suite on pushes and pull requests.

## 🐳 Docker

```bash
docker build -t ai-medical-cost-rag .
docker run -p 8000:8000 ai-medical-cost-rag
```

## 📈 Future Improvements

- Real healthcare cost dataset with appropriate geographic relevance
- Calibration and formal prediction intervals
- RAG evaluation: retrieval recall, groundedness and answer faithfulness
- PostgreSQL logging for predictions/chat sessions
- Authentication and role-based access
- PDF ingestion with page-level citations
- Redis caching
- Async inference
- Monitoring and observability
- Cloud deployment
- Multilingual healthcare information support
- Model/data versioning

## ⚠️ Dataset Limitation

The commonly used Medical Cost Personal Dataset represents **U.S. insurance charges**. It should not be presented as a model of Indian hospital prices.

The repository's included `demo_insurance.csv` is synthetic so that the project can run immediately. Replace it with a properly licensed dataset for serious experimentation.

## 👩‍💻 Portfolio Skills

**Python · Machine Learning · XGBoost · SHAP · NLP · LLMs · RAG · LangChain · ChromaDB · FastAPI · REST APIs · Streamlit · SQLAlchemy · PostgreSQL · Docker · GitHub Actions · Testing**
