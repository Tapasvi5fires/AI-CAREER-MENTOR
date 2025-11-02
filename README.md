🧠 AI Career Mentor Application

This application is a full-stack career analysis tool built with a modular FastAPI backend and a user-friendly Streamlit frontend. It uses the Gemini API to analyze a user's resume, extract detailed skill and experience data, and generate personalized, high-quality career recommendations, roadmaps, and project ideas.

Frontend Access link :[https://ai-career-mentor-frontend-2u2q.onrender.com](https://ai-career-mentor-frontend-uxos.onrender.com)
Backend link : [https://ai-career-mentor-backend-2u2q.onrender.com](https://ai-career-mentor-backend-2u2q.onrender.com)

✨ Key Features

Robust Profile Extraction: Uses the GeminiAgent to extract core data (skills, interests, education, certifications, career level) into a structured JSON format.

Advanced Content Generation: The DataEnrichmentAgent performs a secondary, targeted LLM call to generate detailed, high-quality Learning Roadmaps and Advanced Mini-Projects.

Data Visualization Ready: Extracts crucial metrics like Skill Proficiency Scores and Critical Knowledge Gaps directly from the resume, ready for chart visualization in the frontend.

Resilience and Stability: Implements Exponential Backoff and Retry logic on all external API calls to overcome transient errors (like 503 Service Unavailable).

Flexible Input Handling: Supports analysis of pasted text or direct file upload of PDF and DOCX resumes.

🏗️ Architecture and Workflow

The application uses a clean Modular Agent Pattern to separate concerns:

Frontend (Streamlit): Sends user input (raw text or file content) to the FastAPI backend via a multipart/form-data POST request.

main.py (FastAPI): Receives the request, handles file parsing (PDF/DOCX), and orchestrates the agents.

GeminiAgent (Core Extraction): Makes the first LLM call (low temperature, high max tokens) to extract the primary data points and chart metrics (e.g., skill scores).

DataEnrichmentAgent (High-Quality Generation): Makes a second, targeted LLM call (higher temperature, huge max tokens) using the core profile data to generate verbose, detailed content (Roadmap/Projects).

MentorAgent (Orchestrator): Compiles the output from all sources (Gemini, Enrichment, RAG service) into a single, comprehensive dictionary before returning the final JSON response to the Streamlit frontend.

⚙️ Setup and Installation

Prerequisites

Python 3.10+

Gemini API Key: Obtain an API key from Google AI Studio.

Step 1: Clone and Set up Virtual Environment

# Clone the repository
git clone [YOUR_REPO_URL]
cd ai-career-mentor

# Create and activate a virtual environment
python -m venv venv
# On Windows:
.\venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate


Step 2: Install Dependencies

Install all necessary Python libraries, including FastAPI, Uvicorn, Streamlit, LLM SDKs, and file handling libraries.

pip install -r requirements.txt
# (Assuming your requirements.txt covers: fastapi uvicorn requests python-dotenv numpy sentence-transformers python-docx "python-multipart" "pyfpdf" "httpx")
# If you don't have a requirements.txt:
pip install fastapi uvicorn requests python-dotenv numpy sentence-transformers python-docx "python-multipart" "PyMuPDF" httpx



Step 3: Configure Secrets

Create a file named .env in the root directory of the project (or set Render environment variables) and add your keys.

Example (.env):

LLM_API_KEY="your_gemini_or_llm_api_key_here"
JOB_API_KEY="optional_job_api_key_for_external_job_search"
VECTOR_DB_PATH="./data/skills_index.faiss"

You can also use the provided `.env.example` as a template.

▶️ How to Run the Application Locally

You must start the backend (FastAPI) first, followed by the frontend (Streamlit).

1. Start the Backend API (FastAPI)

Run the backend server using Uvicorn. For local development this project uses port 7311
by default (see `run.txt`). Ensure your virtualenv is active, then:

uvicorn app.main:app --reload --port 7311

(The terminal should show: Uvicorn running on http://0.0.0.0:7311)

2. Start the Frontend (Streamlit)

In a separate terminal window (with the same virtual environment active), start the Streamlit application.
By default this repo used port 7312 for Streamlit locally (see `run.txt`). Run:

streamlit run ui/app.py --server.port=7312

Make sure BACKEND_URL in your environment points to the backend (default local: http://localhost:7311).

(The app will open automatically in your browser, typically at http://localhost:7312)

Deploying to Render (free tier)

We recommend creating two separate services on Render: one for the backend and one for the frontend.

Backend service (ai-career-mentor-backend)

- Service Name: ai-career-mentor-backend
- Environment / Runtime: Python 3.x
- Build Command: pip install -r requirements.txt
- Start Command: uvicorn app.main:app --host 0.0.0.0 --port 10000

Frontend service (ai-career-mentor-ui)

- Service Name: ai-career-mentor-ui
- Environment / Runtime: Python 3.x
- Build Command: pip install -r requirements.txt
- Start Command: streamlit run ui/app.py --server.port=10000 --server.address=0.0.0.0

Notes on Ports

- Render assigns public ports automatically; the service start commands above instruct the app to listen on port 10000 inside the container. Render will handle the external port mapping.

Environment Variables to add in Render dashboard (Service → Environment):

- LLM_API_KEY (required if you want LLM features)
- BACKEND_URL (required for the frontend service: set this to the backend's public Render URL after the backend is deployed)
- JOB_API_KEY (optional)
- VECTOR_DB_PATH (optional, if you deploy with a FAISS index)

Automatic linking

1. Create the backend service on Render using the settings above. Once the backend build finishes, copy the backend's public URL (for example: https://ai-career-mentor-backend.onrender.com).
2. Create the frontend service on Render. In the frontend service's Environment tab, add `BACKEND_URL` and set its value to the backend's public URL.

The Streamlit app reads `BACKEND_URL` from the environment and will call the deployed backend automatically.

If you want a single place that lists these Render settings (copy/paste friendly), see `render-services.md` in the repo.

Troubleshooting

500 Internal Server Error: If this happens, check the FastAPI terminal output. If the error is MAX_TOKENS, the LLM is overloaded, but the retry logic should handle it. If the error is structural, ensure all your agent files are saved correctly and the imports are accurate.

400 Bad Request: Check the frontend code to ensure it's sending the data as multipart/form-data.


ModuleNotFoundError: Ensure all packages listed in Step 2 are installed, especially python-docx and PyMuPDF.

