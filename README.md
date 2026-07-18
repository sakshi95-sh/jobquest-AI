# JobQuest AI
 
An AI-powered job search platform that parses resumes, scores job fit semantically using RAG, and auto-generates tailored cover letters — instead of relying on generic keyword matching.
 
<!-- Add live demo link + screenshot/GIF here once deployed (Phase 7) -->
**Live demo:** _coming soon_
 
---
 
## Why this exists
 
Job seekers waste hours manually tailoring resumes and cover letters for every application, while most ATS tools only do shallow keyword matching that misses real fit. JobQuest AI uses retrieval-augmented generation (RAG) to understand the *meaning* behind a resume and a job description, not just overlapping words — so scoring and cover letters are grounded in what actually matters for that specific role.
 
---
 
## Features
 
- **Resume parsing** — structured extraction from an uploaded resume via the Claude API
- **Semantic ATS scoring** — cosine similarity between resume and job description embeddings, not keyword matching
- **RAG-powered cover letter generation** — retrieves the most relevant resume chunks for a given job description, then generates a tailored cover letter
- **Kanban application tracker** — drag-and-drop board across application stages (Applied, Interviewing, Offer, Rejected)
- **Gmail auto-classification** — reads application-status emails and updates the tracker automatically
- **Google Calendar sync** — automatically adds interview dates to your calendar
- **AI interview prep** — categorized question bank, STAR talking-point generator, and mock-answer feedback
---
 
## Tech stack
 
| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | Node.js / Express |
| Database | PostgreSQL + Prisma |
| AI / LLM | Claude API (Anthropic) |
| Embeddings | OpenAI / Voyage AI |
| Vector search | pgvector (PostgreSQL extension) |
| Integrations | Gmail API, Google Calendar API |
 
---
 
## Architecture
 
```
┌─────────────┐      ┌──────────────────┐      ┌────────────────────┐
│   React     │ ───▶ │  Node/Express API  │ ───▶ │   PostgreSQL +     │
│  Frontend   │ ◀─── │   (Backend)         │ ◀─── │   pgvector          │
└─────────────┘      └──────────────────┘      └────────────────────┘
                              │
                              ├──▶ Claude API (parsing, cover letters, interview prep)
                              ├──▶ Embedding API (resume + job description vectors)
                              ├──▶ Gmail API (status email classification)
                              └──▶ Google Calendar API (interview sync)
```
 
**How RAG fits in:** when a job description is pasted, it's converted into an embedding, compared against the user's stored resume-chunk embeddings via cosine similarity, and the most relevant chunks are retrieved and passed to Claude to generate a tailored cover letter and match score.
 
---
 
## Database schema
 
**`users`**
| Field | Type | Notes |
|---|---|---|
| user_id | PK | |
| email | string | required, unique |
| password_hash | string | never stored as plain text |
| preferred_role | string | optional |
| resume | text | base resume, uploaded once |
 
**`applications`**
| Field | Type | Notes |
|---|---|---|
| application_id | PK | |
| user_id | FK → users | |
| company_name | string | |
| role_applied_for | string | |
| job_description | text | user-pasted |
| apply_date | date | |
| status | enum | Applied / Interviewing / Offer / Rejected |
| match_score | float | from semantic ATS scoring |
| cover_letter | text | nullable — not every application needs one |
 
---
 
## Getting started
 
```bash
git clone <repo-url>
cd jobquest-ai
npm install
 
# copy and fill in environment variables
cp .env.example .env
```
 
**Required environment variables:**
```
DATABASE_URL=
CLAUDE_API_KEY=
EMBEDDING_API_KEY=
GMAIL_CLIENT_ID=
GMAIL_CLIENT_SECRET=
GOOGLE_CALENDAR_CLIENT_ID=
GOOGLE_CALENDAR_CLIENT_SECRET=
```
 
```bash
npm run dev
```
 
---
 
## What I'd improve with more time
 
- Real job-board search (LinkedIn/Indeed integration) instead of manual paste-in
- Caching embeddings to avoid redundant API calls
- Versioned resumes instead of a single stored resume
- More robust email classification (currently rule-based on top of Gmail parsing)
---
 
## Author
 
Sakshi - https://www.linkedin.com/in/imsakshish/

 
