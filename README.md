# JobQuest-AI

## PROJECT TITLE

JobQuest AI: An AI-powered job search platform that parses resumes, scores job fit semantically, and auto-generates tailored cover letters using RAG.

## Problem / Why this exists
Job seekers waste time manually tailoring resumes and cover letters for every application, and generic ATS tools use simple keyword matching instead of understanding actual fit."'
This shows you can think about why, not just how.


## Features
- Resume parsing via Claude API
- Semantic ATS scoring (cosine similarity, not keyword matching)
- RAG-powered tailored cover letter generation
- Kanban application tracker
- Gmail auto-classification of application status
- Google Calendar sync for interviews
- AI interview prep (question bank, STAR points, feedback)


## Tech stack
- Frontend: React
- Backend: Node.js / Express
- Database: PostgreSQL + Prisma
- AI: Claude API, embeddings (OpenAI/Voyage), pgvector for RAG
- Integrations: Gmail API, Google Calendar API


# Setup / installation instructions
- git clone ...
- npm install
- cp .env.example .env   (list required env vars)
- npm run dev
