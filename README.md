# MediVise 💊

**MediVise** is a full-stack clinical decision-support platform that reads handwritten or printed prescriptions, extracts the prescribed drugs using OCR + fuzzy matching, and predicts drug-drug interaction risk using a trained machine learning model — helping patients, doctors, pharmacists, and researchers catch dangerous medication combinations before they cause harm.

## ✨ Features

- **Prescription Upload & OCR** — Upload a photo of a prescription; MediVise extracts text via OCR and identifies drug names using fuzzy string matching.
- **ML-Powered Interaction Analysis** — A trained classification model (XGBoost) predicts the severity of interactions between drug pairs, with SHAP-based explainability showing the key contributing factors.
- **Risk Reporting** — Get an overall risk rating (Low / Moderate / High), suggested alternative medications, and food-drug interaction warnings.
- **PDF Clinical Reports** — Generate a downloadable PDF summary of medications, risks, and recommendations.
- **Role-Based Dashboards** — Separate portals and permissions for:
  - **Patients** — upload prescriptions, view analysis, track status, download reports
  - **Doctors** — create/manage prescriptions, review patient history, approve medications
  - **Pharmacists** — review a queue of pending prescriptions, view high-risk alerts, approve/flag/discard
  - **Researchers** — aggregate statistics and visualizations across all analyzed prescriptions
  - **Admins** — manage users, drugs database, and system settings
- **Session-Based Authentication** — Secure login/signup with hashed passwords and role-based access control.

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, AngularJS, jQuery |
| Backend API | Node.js, Express, MongoDB (Mongoose), express-session |
| ML Service | Python, FastAPI, scikit-learn, XGBoost, SHAP |
| OCR & NLP | Custom OCR + fuzzy drug-name extraction pipeline |
| Reporting | PDFKit |

## 📁 Project Structure

```
Medivise-main/
├── backend/          # Express API server (auth, prescriptions, role routes)
│   ├── server.js
│   ├── go.js             # Auth, patient, admin, researcher routes
│   ├── doctorRoutes.js
│   └── pharmacistRoutes.js
├── frontend/         # Static multi-role frontend (AngularJS)
│   ├── index.html
│   ├── patient/
│   ├── doctor/
│   ├── pharmacist/
│   ├── researcher/
│   └── admin/
└── ml-model/         # Python ML microservice
    ├── api.py             # FastAPI service exposing /analyze
    ├── main.py            # OCR -> extraction -> prediction pipeline
    ├── train_model.py     # Model training script
    ├── ocr.py / ocr_runner.py
    ├── drug_extraction.py
    ├── text_processing.py
    └── predict.py
```

## 🚀 Getting Started

### Prerequisites
- Node.js and npm
- Python 3.9+
- MongoDB running locally (`mongodb://127.0.0.1:27017`)

### 1. Backend (Node.js API)
```bash
cd backend
npm install
node server.js
```
Server runs on `http://localhost:5000`.

### 2. ML Service (Python/FastAPI)
```bash
cd ml-model
pip install -r requirements.txt
uvicorn api:app --reload --port 8000
```
ML service runs on `http://127.0.0.1:8000`.

### 3. Frontend
The frontend is served as static files by the Express backend — once the backend is running, visit `http://localhost:5000` in your browser.

## 🔌 API Overview

| Route Prefix | Description |
|---|---|
| `/go/*` | Auth (signup/login/logout), patient actions, admin management, researcher analytics |
| `/api/doctor/*` | Doctor prescription creation, review, and approval |
| `/pharmacist/*` | Pharmacist queue, alerts, decisions, stats |
| `POST /analyze` (ML service, port 8000) | Runs the interaction model on a drug pair |

## ⚠️ Disclaimer
MediVise is a prototype for educational/research purposes. It is **not** a substitute for professional medical advice. Always consult a licensed healthcare provider before making medication decisions.

## 📄 License
Add a license of your choice (e.g., MIT) here.
