# 🧠 AI Customer Sentiment Analysis Dashboard

A production-ready NLP pipeline that fine-tunes **DistilBERT** on customer feedback and serves predictions through a **FastAPI** REST API with a **Streamlit** real-time dashboard.

---

## ✨ Features

| Layer | Stack |
|---|---|
| Model | DistilBERT (fine-tuned, 3-class: Positive / Neutral / Negative) |
| API | FastAPI + Uvicorn |
| Dashboard | Streamlit + Plotly |
| Database | PostgreSQL via SQLAlchemy / asyncpg |
| Experiment tracking | Weights & Biases (W&B) |
| Notebooks | JupyterLab (EDA → Pre-processing → Training → Evaluation) |

---

## 📊 Model Performance

| Metric | Score |
|--------|-------|
| Accuracy | **100%** |
| Macro F1 | **1.0000** |
| Weighted F1 | **1.0000** |

> Trained on 5,000 synthetic customer feedback entries (website, app, email, social media, support tickets, surveys).  
> Train / Val / Test split: **70 / 15 / 15 %** (stratified).

---

## 🗂️ Project Structure

```
sentiment_dashboard/
├── data/                   # CSV splits (not tracked – see .gitignore)
│   └── .gitkeep
├── models/
│   └── sentiment_model/    # Model config & tokenizer configs (weights excluded)
│       ├── config.json
│       ├── label_config.json
│       ├── special_tokens_map.json
│       └── tokenizer_config.json
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_training.ipynb
│   └── 04_evaluation.ipynb
├── reports/
│   ├── confusion_matrix.png
│   ├── wordclouds.png
│   ├── evaluation_report.json
│   └── training_metrics.json
├── .env.example            # Copy to .env and fill in your secrets
├── requirements.txt
└── REPORT.md               # Detailed methodology & results
```

---

## 🚀 Quick Start

### 1 – Clone & install dependencies

```bash
git clone https://github.com/<your-username>/sentiment-dashboard.git
cd sentiment-dashboard/sentiment_dashboard
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate
pip install -r requirements.txt
```

### 2 – Configure environment

```bash
cp .env.example .env
# Edit .env with your DATABASE_URL, WANDB_API_KEY, etc.
```

### 3 – Download model weights

The fine-tuned weights (`model.safetensors`) are **not** stored in this repo due to size (~255 MB).  
Download them from the [Hugging Face Hub](https://huggingface.co/) or regenerate by running:

```bash
jupyter lab notebooks/03_training.ipynb
```

### 4 – Launch (Docker – recommended)

```bash
docker compose up --build
```

| Service | URL |
|---------|-----|
| REST API (Swagger) | http://localhost:8000/docs |
| Streamlit Dashboard | http://localhost:8501 |

---

## 🔬 Notebooks

| Notebook | Purpose |
|----------|---------|
| `01_eda.ipynb` | Exploratory Data Analysis – class balance, length distributions, word clouds |
| `02_preprocessing.ipynb` | HTML stripping, URL removal, lowercasing, train/val/test splits |
| `03_training.ipynb` | DistilBERT fine-tuning with Hugging Face Trainer + W&B logging |
| `04_evaluation.ipynb` | Confusion matrix, per-class metrics, error analysis |

---

## ⚙️ Environment Variables

Copy `.env.example` → `.env` and populate:

| Variable | Description |
|----------|-------------|
| `DATABASE_URL` | PostgreSQL connection string |
| `MODEL_PATH` | Local path to saved model directory |
| `HF_MODEL_NAME` | Base Hugging Face model name |
| `WANDB_PROJECT` | W&B project name |
| `WANDB_API_KEY` | Your W&B API key |
| `API_HOST` / `API_PORT` | FastAPI bind address |
| `DASHBOARD_API_URL` | Streamlit → API base URL |
| `LOG_LEVEL` | `INFO` / `DEBUG` / `WARNING` |
| `SENTRY_DSN` | Sentry error tracking DSN (optional) |

---

## 📈 Business Impact

- **Automated triage** – negative feedback auto-routed to support within seconds  
- **Trend monitoring** – daily dashboard detects product issues early  
- **Scale** – processes **1,000+ entries/minute** vs ~50 for manual review  

---

## 🧪 Running Tests

```bash
pytest --asyncio-mode=auto
```

---

## 📄 License

MIT
