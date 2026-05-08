AI-Powered Interview Preparation Platform
1. Project Title
InterviewAI — AI-Powered Interview Preparation Platform

3. Project Description
InterviewAI is a full-stack GenAI platform that helps job seekers prepare for interviews by analyzing their resume and target job description. Users can upload their resume, paste a job description, and receive AI-generated technical, behavioral, and role-specific interview questions with suggested answers. The platform also tracks interview preparation history and provides performance insights through an analytics dashboard.

3. Tech Stack
Frontend: React, TypeScript, Tailwind CSS
Backend: FastAPI, Python
Database: PostgreSQL
Authentication: JWT
AI/LLM: OpenAI API, LangChain
File Processing: PyMuPDF / pdfplumber
Deployment: Docker, Render/AWS, Vercel
Version Control: Git, GitHub

4. Core Features
User Authentication

Users can register, log in, and securely access their dashboard using JWT-based authentication.

Resume Upload

Users upload a PDF resume. The backend extracts resume text and stores it for AI analysis.

Job Description Matching

Users paste a job description, and the system compares it with the resume to identify skill gaps, matching skills, and role alignment.

AI-Generated Interview Questions

The platform generates:

Technical questions
Behavioral questions
Scenario-based questions
Role-specific questions
AI-Generated Answers

For each question, the system provides a strong sample answer using the user’s resume experience.

Interview History

Users can view past interview sessions, job descriptions, generated questions, and answers.

Analytics Dashboard

Dashboard shows:

Total interviews prepared
Skill match percentage
Common missing skills
Number of technical vs behavioral questions
Preparation progress
5. GitHub Repository Structure
interviewai-platform/
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── database.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   ├── auth.py
│   │   ├── config.py
│   │   │
│   │   ├── routers/
│   │   │   ├── auth_routes.py
│   │   │   ├── resume_routes.py
│   │   │   ├── interview_routes.py
│   │   │   └── analytics_routes.py
│   │   │
│   │   ├── services/
│   │   │   ├── resume_parser.py
│   │   │   ├── ai_service.py
│   │   │   ├── jd_matcher.py
│   │   │   └── analytics_service.py
│   │   │
│   │   └── utils/
│   │       └── security.py
│   │
│   ├── requirements.txt
│   ├── Dockerfile
│   └── .env.example
│
├── frontend/
│   ├── src/
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   ├── api/
│   │   │   └── axios.ts
│   │   ├── pages/
│   │   │   ├── Login.tsx
│   │   │   ├── Register.tsx
│   │   │   ├── Dashboard.tsx
│   │   │   ├── UploadResume.tsx
│   │   │   ├── InterviewPrep.tsx
│   │   │   └── History.tsx
│   │   ├── components/
│   │   │   ├── Navbar.tsx
│   │   │   ├── QuestionCard.tsx
│   │   │   ├── SkillMatchCard.tsx
│   │   │   └── AnalyticsChart.tsx
│   │   └── styles/
│   │       └── index.css
│   │
│   ├── package.json
│   ├── tailwind.config.js
│   └── Dockerfile
│
├── docker-compose.yml
├── README.md
├── architecture.png
└── screenshots/
6. Database Tables
users
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(150) UNIQUE NOT NULL,
    password_hash TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
resumes
CREATE TABLE resumes (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    file_name VARCHAR(255),
    extracted_text TEXT,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
interview_sessions
CREATE TABLE interview_sessions (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    resume_id INT REFERENCES resumes(id),
    job_title VARCHAR(150),
    company_name VARCHAR(150),
    job_description TEXT,
    skill_match_score FLOAT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
interview_questions
CREATE TABLE interview_questions (
    id SERIAL PRIMARY KEY,
    session_id INT REFERENCES interview_sessions(id),
    question_type VARCHAR(50),
    question TEXT,
    sample_answer TEXT
);
7. Backend API Endpoints
Auth APIs
POST /auth/register
POST /auth/login
GET  /auth/me
Resume APIs
POST /resume/upload
GET  /resume/list
GET  /resume/{resume_id}
Interview APIs
POST /interview/generate
GET  /interview/history
GET  /interview/{session_id}
Analytics APIs
GET /analytics/summary
GET /analytics/skills
8. AI Prompt Used in Backend
You are an expert technical interviewer and career coach.

Analyze the candidate resume and job description.

Generate:
1. 10 technical interview questions
2. 5 behavioral interview questions
3. 5 scenario-based interview questions
4. Strong sample answers using the candidate's resume
5. Missing skills from the job description
6. Resume-to-job match percentage

Candidate Resume:
{resume_text}

Job Description:
{job_description}

Return the response in structured JSON format.
9. Main Backend Flow
User logs in
↓
Uploads resume PDF
↓
Backend extracts resume text
↓
User pastes job description
↓
System compares resume with JD
↓
OpenAI/LangChain generates questions and answers
↓
Results are stored in PostgreSQL
↓
Frontend displays interview questions, answers, and analytics
10. README.md Content for GitHub
# InterviewAI — AI-Powered Interview Preparation Platform

InterviewAI is a full-stack GenAI application that helps job seekers prepare for interviews by analyzing their resume and a target job description. The platform generates AI-powered technical, behavioral, and scenario-based interview questions with strong sample answers.

## Features

- User authentication using JWT
- Resume PDF upload and text extraction
- Job description analysis
- AI-generated interview questions
- AI-generated sample answers
- Resume-to-job skill matching
- Interview history tracking
- Analytics dashboard

## Tech Stack

Frontend:
- React
- TypeScript
- Tailwind CSS

Backend:
- FastAPI
- Python
- PostgreSQL
- SQLAlchemy
- JWT Authentication

AI:
- OpenAI API
- LangChain
- Prompt Engineering

Deployment:
- Docker
- Vercel
- Render / AWS

## Architecture

User → React Frontend → FastAPI Backend → PostgreSQL  
FastAPI → Resume Parser → LangChain/OpenAI → Interview Output

## How to Run Locally

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
Frontend
cd frontend
npm install
npm run dev
Environment Variables

Create .env file:

DATABASE_URL=postgresql://username:password@localhost:5432/interviewai
OPENAI_API_KEY=your_openai_api_key
JWT_SECRET_KEY=your_secret_key
Future Improvements
Voice-based mock interviews
Resume ATS scoring
LinkedIn profile analysis
Interview performance scoring
Video interview practice
Multi-language support

System Workflow:
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/2a64b9e4-d9b5-412f-8633-cd4a91bdd3d6" />

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/352dc752-ffd3-4b24-bbf7-0a1cb6b74ec0" />

