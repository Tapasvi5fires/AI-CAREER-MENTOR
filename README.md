# 🧠 AI Career Mentor

### **AI-Powered Resume Intelligence & Career Recommendation System**

*A full-stack, production-grade multi-agent LLM system built by
**Tapasvi Panchagnula***

------------------------------------------------------------------------

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-green)
![Streamlit](https://img.shields.io/badge/Streamlit-Frontend-red)
![Gemini](https://img.shields.io/badge/Gemini-LLM-yellow)
![FAISS](https://img.shields.io/badge/FAISS-Vector%20DB-purple)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![Render](https://img.shields.io/badge/Render-Deployed-success)
![License](https://img.shields.io/badge/License-MIT-blue)

![Issues](https://img.shields.io/github/issues/Tapasvi5fires/AI-CAREER-MENTOR)
![Forks](https://img.shields.io/github/forks/Tapasvi5fires/AI-CAREER-MENTOR)
![Stars](https://img.shields.io/github/stars/Tapasvi5fires/AI-CAREER-MENTOR)
![Last
Commit](https://img.shields.io/github/last-commit/Tapasvi5fires/AI-CAREER-MENTOR)

------------------------------------------------------------------------

# 🔗 Live Applications

-   **Frontend:** https://ai-career-mentor-frontend-2u2q.onrender.com\
-   **Backend:** https://ai-career-mentor-backend-2u2q.onrender.com

------------------------------------------------------------------------

# ✨ Key Features

### 🔍 **1. Resume Intelligence Extraction (GeminiAgent)**

Extracts: - Technical skills\
- Soft skills\
- Experience summary\
- Education\
- Certifications\
- Career readiness level\
- Skill proficiency scores\
- Critical knowledge gaps

Produces a **structured JSON profile** used by other agents.

------------------------------------------------------------------------

### 🧠 **2. Deep Content Generation (DataEnrichmentAgent)**

Creates: - Multi-stage learning roadmap\
- Skill improvement plan\
- Domain-aligned career suggestions\
- Advanced ML/AI mini-project ideas\
- Capstone recommendations

High creativity + long-form reasoning (high tokens).

------------------------------------------------------------------------

### 📊 **3. Visualization-Ready Metrics**

Outputs include: - Skill Radar Scores\
- Gap Analysis\
- Domain Fit Level\
- Strength Matrix

------------------------------------------------------------------------

### 🔁 **4. Stable & Reliable System**

-   Automatic retry\
-   Exponential backoff\
-   Handles: 503 errors, timeouts, LLM rate limits

------------------------------------------------------------------------

# 🏗️ Architecture Overview

    User → Streamlit UI → FastAPI Backend → Agents → Final JSON → UI Visualization

------------------------------------------------------------------------

# 📂 Project Structure 

    AI-CAREER-MENTOR/
    │
    ├── app/
    │   ├── main.py
    │   ├── agents/
    │   │   ├── gemini_agent.py
    │   │   ├── enrichment_agent.py
    │   │   ├── mentor_agent.py
    │   └── services/
    │       ├── rag_service.py
    │
    ├── ui/
    │   ├── app.py
    │
    ├── start_backend.sh
    ├── start_frontend.sh
    ├── docker-compose.yml
    ├── requirements.txt

------------------------------------------------------------------------

# 🧩 Internal Working --- **Deep Technical Explanation**

## 1️⃣ Streamlit Frontend

Role: - Accepts resume text or file\
- Sends data to FastAPI via POST\
- Receives: - Profile JSON\
- Roadmaps\
- Skill scores\
- Project list\
- Displays visual charts and formatted content

File parsing in frontend ensures fast feedback for users.

------------------------------------------------------------------------

## 2️⃣ FastAPI Backend

All logic lives in `app/main.py`

Steps:

### **➤ Step 1 --- File Parsing**

-   `.pdf` → parsed using **PyMuPDF**
-   `.docx` → parsed using **python-docx**
-   Raw text → no preprocessing needed\
-   All converted to **clean plain text**

------------------------------------------------------------------------

### **➤ Step 2 --- Agent Orchestration**

#### 🧩 **GeminiAgent --- Core Extraction**

Defined in:\
`app/agents/gemini_agent.py`

Purpose:\
Produce structured, accurate resume intelligence.

Config: - Low temperature\
- High max tokens\
- Deterministic output

------------------------------------------------------------------------

#### 🧩 **DataEnrichmentAgent --- Deep Generation**

Defined in:\
`app/agents/enrichment_agent.py`

Purpose: - Generate detailed content\
- Long-form reasoning\
- Personalized learning LLM output

Config: - Higher temperature\
- Very high token limits

------------------------------------------------------------------------

#### 🧩 **MentorAgent --- Final Combiner**

Defined in:\
`app/agents/mentor_agent.py`

Combines: - GeminiAgent output\
- EnrichmentAgent output\
- RAG service results

Outputs one clean JSON dictionary:

    {
      "profile": ...,
      "skills": ...,
      "roadmap": ...,
      "projects": ...,
      "charts": ...
    }

------------------------------------------------------------------------

## 3️⃣ RAG Vector Search

Defined in:\
`app/services/rag_service.py`

Uses: - FAISS vector DB\
- Embedding models\
- Skill similarity search

Purpose: - Detect missing skills\
- Suggest role transitions

------------------------------------------------------------------------

## 4️⃣ Retry & Backoff Logic

All LLM calls have:

    wait → retry → wait longer → retry

This prevents LLM crash failures.

------------------------------------------------------------------------

# ▶️ Running Locally

## Start Backend:

    uvicorn app.main:app --reload --port 7311

## Start Frontend:

    streamlit run ui/app.py --server.port=7312

------------------------------------------------------------------------

# ☁️ Deployment (Render)

### Backend:

    uvicorn app.main:app --host 0.0.0.0 --port 10000

### Frontend:

    streamlit run ui/app.py --server.port=10000 --server.address=0.0.0.0

Environment Variables required:

    LLM_API_KEY
    BACKEND_URL
    VECTOR_DB_PATH
    JOB_API_KEY (optional)

------------------------------------------------------------------------

# 🔥 Why This Project Is Recruiter-Impressive

-   Real LLM engineering (multi-agent design)\
-   Backend + Frontend integration\
-   Resume parsing pipeline\
-   Production-level error handling\
-   RAG + FAISS\
-   Deployments + Docker + Render\
-   Clean architecture

This shows strong *full-stack AI engineering* capability.

------------------------------------------------------------------------

# ✨ Credits

Built with passion by **Tapasvi Panchagnula** ❤️
