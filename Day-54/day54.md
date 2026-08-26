Day 54 — AI Career Copilot

Milestone 3: Skill Gap Report + Prep Plan (Gemini Integration)

Project: AI Career Copilot
Day: 54
Focus: Gemini-powered resume analysis and personalized preparation plan

1. Day 54 Objective

The goal of Day 54 is to begin the first real AI-powered feature of AI Career Copilot.

The feature takes a resume already saved in Supabase, sends it to Google's Gemini API, compares it against a fixed Software Engineer Intern skill framework, and produces:

Candidate strengths

Skill gaps

Priority levels

A personalized preparation plan

Core flow:

Resume → Skill Gaps → Preparation Plan

2. Previous Milestones Completed

Milestone 1 — Authentication ✅

Implemented and tested:

Login

Signup

Logout

Protected routes

Authentication state

Dashboard access

The dashboard successfully displayed the logged-in user's email.

Milestone 2 — Resume Upload + Save ✅

Implemented:

PDF resume upload

PDF text extraction using pdfjs-dist

Paste-text fallback

Saving resumes to Supabase

Linking each resume to the authenticated user_id

Recording source_type as pdf or paste

The Supabase resumes table was verified successfully and showed saved PDF and paste records.

3. Day 54 — Milestone 3

Skill Gap Report + Prep Plan

The backend will provide:

POST /api/analyze-resume

The endpoint will:

Authenticate the user.

Receive a resume_id.

Fetch the resume from Supabase.

Verify resume ownership.

Build the Gemini prompt.

Send the resume to Gemini.

Parse Gemini's structured JSON.

Save the result to skill_reports.

Return strengths, gaps, and prep plan to the frontend.

4. Skill Framework

Gemini evaluates the resume against:

Data Structures & Algorithms

OOP Fundamentals

System Design Basics

Databases / SQL

Version Control / Git

Web Fundamentals

Problem Solving / Communication

5. Backend Files

backend/lib/supabaseAdmin.js

Creates the Supabase admin client using:

SUPABASE_URL
SUPABASE_SERVICE_ROLE_KEY

backend/lib/geminiClient.js

Responsible for:

Gemini client initialization

Calling Gemini

Reading the model response

Parsing JSON responses

Configured model:

gemini-2.0-flash

backend/prompts/skillGapPrompt.js

Builds the prompt for resume evaluation.

Expected response:

{
  "strengths": [],
  "gaps": [],
  "prep_plan": []
}

Each gap contains:

{
  "topic": "",
  "why": "",
  "priority": ""
}

Each prep item contains:

{
  "topic": "",
  "action": "",
  "priority": ""
}

Allowed priorities:

high
medium
low

The prompt requires 2–5 strengths, 2–5 gaps, one preparation action per gap, and no invented strengths.

backend/middleware/verifyAuth.js

Protects API routes using:

Authorization: Bearer <token>

Invalid or missing tokens return 401.

backend/routes/analyzeResume.js

Creates:

POST /api/analyze-resume

It fetches the resume, verifies ownership, calls Gemini, validates the response, saves the report, and returns the generated data.

backend/index.js

Updated to:

Load environment variables

Enable CORS

Parse JSON

Keep the health-check route

Protect /api routes

Mount the analysis router

Health check:

GET http://localhost:5000/

Expected:

{
  "message": "AI Career Copilot backend is running"
}

6. Frontend Files

frontend/src/analysis/SkillGapReport.jsx

Displays:

Strengths

Skill gaps

Gap topics

Gap reasons

Priority levels

frontend/src/analysis/PrepPlan.jsx

Displays the personalized preparation plan and sorts items:

High → Medium → Low

Each item shows:

Priority

Topic

Concrete study action

7. Gemini SDK Setup

Run inside backend:

cd backend
npm install @google/generative-ai

Then restart the backend:

node index.js

Expected:

Backend running on http://localhost:5000

8. Environment Variables

Required locally:

SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
GEMINI_API_KEY=your_gemini_api_key

These values must remain in .env.

Never commit or expose:

Supabase service-role key

Gemini API key

Other credentials

The project .gitignore protects environment files.

9. Testing Plan

Test 1 — Gemini SDK

cd backend
npm install @google/generative-ai

Confirm installation completes without errors.

Test 2 — Backend

node index.js

Confirm:

Backend running on http://localhost:5000

Test 3 — Health Check

Open:

http://localhost:5000/

Expected:

{
  "message": "AI Career Copilot backend is running"
}

Test 4 — Authentication Protection

Call the analysis endpoint without a Bearer token.

Expected:

401 Unauthorized

Test 5 — Resume Ownership

Attempt to analyze a resume belonging to another user.

Expected:

403 This resume does not belong to you

Test 6 — End-to-End Gemini Analysis

After the frontend connection is added:

Log in.

Select a saved resume.

Start analysis.

Send the authenticated request.

Gemini analyzes the resume.

Strengths are returned.

Gaps are returned.

Prep plan is returned.

Report is saved in Supabase.

10. Expected Application Flow

User
  ↓
Login / Signup
  ↓
Dashboard
  ↓
Upload or Paste Resume
  ↓
Save Resume in Supabase
  ↓
Select Resume
  ↓
Analyze Resume
  ↓
Backend Authentication
  ↓
Fetch Resume
  ↓
Gemini Analysis
  ↓
Skill Gap Report
  ↓
Personalized Prep Plan
  ↓
Save Report in Supabase

11. GitHub Security Lesson

During the Day 3 GitHub push, GitHub Push Protection detected secrets in the local commit and rejected the push.

The commit was reset before the secrets were accepted by the remote repository, and .gitignore was updated to protect environment files.

Current protection includes:

node_modules/
.env
.env.local
*.env
frontend/.env
backend/.env
dist/
build/
.DS_Store

This is an important security lesson: API keys and Supabase service-role credentials must never be committed to a repository.

12. Learning Outcomes

Day 54 covers:

Gemini API integration

Express API design

Bearer-token authentication

Supabase admin client

Resume ownership verification

Prompt engineering

Structured JSON generation

AI response parsing

Saving AI results to Supabase

React component composition

Priority-based UI

Environment-variable security

13. Day 54 Status

Feature

Status

Supabase Authentication

✅ Complete

Signup / Login

✅ Complete

Protected Routes

✅ Complete

Resume PDF Upload

✅ Complete

Resume Paste Fallback

✅ Complete

Resume Save to Supabase

✅ Verified

Gemini SDK Setup

🔄 In Progress

Gemini Backend Client

🔄 In Progress

Authentication Middleware

🔄 In Progress

/api/analyze-resume

🔄 In Progress

Skill Gap Report UI

🔄 In Progress

Prep Plan UI

🔄 In Progress

End-to-End AI Analysis

⏳ Pending

Final Day 54 Verification

⏳ Pending

14. Day 54 Deliverables

Gemini SDK installation

Gemini client

Supabase admin client

Authentication middleware

Resume analysis API

Skill-gap prompt

Skill Gap Report component

Prep Plan component

Updated backend server

Testing screenshots

Documentation

Git commit and push after verification

15. Next Step

Finish the connecting frontend piece that triggers:

POST /api/analyze-resume

and displays:

Skill Gap Report
+
Prep Plan

Then perform end-to-end verification, take the required screenshots, update the Day 54 documentation, and commit/push the verified work.

Day 54 Summary

Day 54 moves AI Career Copilot from a working authentication and resume-storage application toward its core AI functionality.

The application already supports authenticated users and saved resumes. This milestone adds the intelligence layer that transforms resume data into actionable career guidance using Gemini.

Core loop:

Resume → AI Skill Gap Analysis → Personalized Preparation Plan
