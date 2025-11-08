# HackPrinceton Judging — Lightweight Hackathon Scoring App

This project is a small, production-capable web application used for collecting and viewing hackathon judging scores. It's built as a Python/Flask backend that serves a single-page React frontend. The app demonstrates full-stack skills in building REST APIs, integrating a relational database, and packaging a static frontend for deployment.

## Elevator pitch (for recruiters)

An end-to-end hackathon judging platform: judges submit numeric scores for teams through a React SPA; the Flask API persists scores in PostgreSQL and exposes endpoints for retrieving scores and judges. The project is simple, robust, and easy to deploy — a good example of a full-stack engineer who can ship working features quickly and responsibly.

## Key technologies

- Backend: Python, Flask, Flask-CORS, Flask-SQLAlchemy (REST API)
- Database: PostgreSQL (local or via a `DATABASE_URL` env var)
- Frontend: React (source in `frontend/src`, production build in `static/` and `frontend/build/`)
- Tooling & deployment: npm, pip, Procfile (Heroku-style), `requirements.txt`, `runtime.txt`, dotenv for config
- Other: SQL migration/init helpers (`init_db.py`, `init_db.sql`), logging

## Notable files and structure

- `app.py` — Flask application that: serves the frontend static files, exposes REST endpoints under `/api/*`, and contains the SQLAlchemy `Score` model.
- `frontend/` — React source and build; the built static assets are included in `static/` for simple static serving.
- `init_db.py` / `init_db.sql` — helpers to initialize or inspect the DB schema.
- `requirements.txt` & `runtime.txt` — Python dependencies and runtime declaration for deployment.
- `Procfile` — simple declaration for process type (useful for Heroku-like deployment).

## Features / what it demonstrates

- REST API for CRUD-like operations (GET `/api/scores`, POST `/api/scores`, GET `/api/judges`)
- Persistent storage with SQLAlchemy models and PostgreSQL
- Data integrity: unique constraint on (judge, team) to avoid duplicate submissions
- Single-page React frontend bundled as static files and served by Flask for a zero-maintenance deploy
- Environment-driven configuration (dotenv, `DATABASE_URL`, `PORT`) to support local and cloud deployments
- Minimal but clear logging and error handling around DB operations

## Sample data model (brief)

Score model fields: id, judge (string), team (string), score (float). Unique constraint `unique_judge_team` ensures one score per judge-team pair.

## How to run locally (quick)

1. Create a Python virtual environment and install requirements:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

2. (Optional) Start a local Postgres instance and set `DATABASE_URL`, or rely on the default configured DB in `app.py`.

3. Initialize the database (if needed):

```bash
python init_db.py
# or run the SQL in init_db.sql against your Postgres instance
```

4. Build the frontend (if you change React source):

```bash
cd frontend
npm install
npm run build
cd ..
```

5. Run the Flask app:

```bash
export FLASK_APP=app.py
export DATABASE_URL="postgresql://..."   # if not using defaults
python app.py
```

The app will serve the frontend at `/` and the API at `/api/*` (default port 5001 unless `PORT` is set).

## What I worked on / what to look for in the code

- Clear, minimal REST endpoints in `app.py` showing pragmatic API design.
- SQLAlchemy model + unique constraint demonstrating attention to data correctness.
- Static serving of a React build plus CORS configuration for API compatibility.
- Simple logging and DB initialization flow.

## Next steps / possible improvements (small wins)

- Add authentication/authorization to protect endpoints.
- Add pagination and aggregation endpoints for leaderboard views.
- Add unit/integration tests for the API and model constraints.
- Add CI/CD pipeline (GitHub Actions) to run tests and build the frontend automatically.

---

If you'd like, I can also produce a condensed one-page bullet summary tailored to a specific role (Backend Engineer, Full-stack, DevOps), or add a short developer-focused CONTRIBUTING section with commands and env var examples.
