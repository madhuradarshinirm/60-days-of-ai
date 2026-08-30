# Implementation Blueprint — AI Career & Interview Copilot
### Days 2–10 | AB Talks 60-Day Claude AI Challenge — 10-Day Capstone

**This document is the single source of truth for building this project.** Each day below is written so a fresh AI conversation can pick it up with no prior context and continue building without redesigning or re-planning. Paste the relevant day's section (plus "Handoff Notes from previous day") into a new chat to continue.

**Locked decisions from Day 1 (do not re-litigate these):**
- Product: AI Career & Interview Copilot for **Software Engineer Intern** candidates only (single role, v1.0)
- Core loop: **Resume Upload → Skill Gap Report → Personalized Prep Plan → Mock Technical Interview → AI Feedback**
- Interview questions: **conceptual CS + coding-review (no code execution)**, selected **semi-dynamically** from a tagged question bank based on identified gaps
- Feedback format: **score + 3-4 structured points** (strengths + improvements)
- Resume input: **PDF upload + plain text paste fallback**
- Accounts: **yes**, via a managed auth/database provider (free tier)
- Out of scope for v1.0: HR/behavioral practice, code execution, multi-role support, fully dynamic question generation, DOCX parsing, payments
- Deliverable on Day 10: live deployed app + README/case study + demo video
- Builder profile: beginner/intermediate, solo, ~3-4 hrs/day, has deployed full apps before, has an LLM API key ready

---

## Day 2 — Technical Design & System Architecture ✅ COMPLETED

### 🎯 Objective
Finalize the tech stack and produce the complete technical design: architecture, database schema, API contract, UI wireframes, and project structure — no code written yet.

### ✅ Final Locked Stack (confirmed Day 2, AI provider updated Day 3)
| Layer | Choice |
|---|---|
| Frontend | React (Vite) |
| Backend | Node.js + Express |
| Database | Supabase (Postgres) |
| Auth | Supabase Auth (email/password) |
| AI | **Google Gemini API** (switched from Anthropic Claude API on Day 3 — free tier requirement) |
| Frontend Hosting | Vercel |
| Backend Hosting | Render (free Web Service) |

### 📦 Deliverables produced Day 2 (all in `docs/`)
- `ARCHITECTURE.md`, `SCHEMA.md`, `API.md`, `UI-WIREFRAMES.md`, `PROJECT-STRUCTURE.md`

### ➡️ Handoff notes for Day 3
Design complete. Day 3 begins actual project scaffolding, Supabase project creation, and foundation code — no design decisions remain open except AI provider (resolved Day 3, see below).

---

## Day 3 — Project Setup & Foundation ✅ COMPLETED

### 🎯 Objective
Build the project's technical foundation: dev environment configured, both `frontend/` and `backend/` scaffolded and running, Supabase project live with schema deployed, environment variables wired, and basic routing/navigation/auth scaffold in place. No full feature logic yet — that starts Day 4.

### 📖 What I'll learn
Scaffolding a two-service (frontend + backend) JavaScript project from scratch; connecting a managed backend-as-a-service (Supabase); structuring environment variables safely; setting up client-side routing.

### 🛠 Features to build
None — foundation only, per plan. A "Hello World" level app that runs, not a working product yet.

### 📝 Step-by-step implementation plan (as executed today)
1. Verified environment: Node v22.19.0, npm 10.9.3, Git 2.50.1 — all healthy.
2. Scaffolded frontend: `npm create vite@latest frontend -- --template react`, then `npm install`.
3. Scaffolded backend: `mkdir backend && cd backend && npm init -y`, then `npm install express cors dotenv @supabase/supabase-js`.
4. Installed remaining frontend dependencies: `npm install react-router-dom @supabase/supabase-js pdfjs-dist`.
5. Created Supabase project (`ai-career-copilot`, South Asia/Mumbai region, Free tier).
6. Ran full schema SQL from `SCHEMA.md` in Supabase SQL Editor — created all 5 tables (`resumes`, `skill_reports`, `questions`, `interview_sessions`, `interview_answers`) with RLS policies. Verified in Table Editor.
7. Confirmed Email/Password auth provider enabled in Supabase Auth settings.
8. Retrieved API credentials (Publishable key, Secret key, Project URL) from Supabase → Settings → API Keys.
9. **Decision point:** discovered Anthropic Claude API account had $0 credits. Switched AI provider to **Google Gemini API** (free tier) to satisfy PRD's free-tier requirement. Updated `ARCHITECTURE.md`, `PROJECT-STRUCTURE.md`, `API.md`, and this Blueprint accordingly (see change log in `ARCHITECTURE.md`).
10. Created `frontend/.env` (`VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, `VITE_API_BASE_URL`) and `backend/.env` (`SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`, `GEMINI_API_KEY`, `PORT`).

### 📂 Files and folders created today
```
ai-career-copilot/
├── frontend/                  (Vite React scaffold, dependencies installed)
│   ├── .env                   (gitignored)
├── backend/                   (Express scaffold, dependencies installed)
│   ├── .env                   (gitignored)
├── docs/                      (Day 1-2 deliverables to be organized here)
```
Remaining foundation code (routing, layout, auth scaffold, Supabase clients, API client) to be created in the rest of today's session per `PROJECT-STRUCTURE.md`.

### 🔗 APIs, libraries, services, or tools integrated
- Supabase (Auth + Postgres) — live, free tier
- Google Gemini API — free tier (replaces Claude API)
- react-router-dom, pdfjs-dist, @supabase/supabase-js (frontend)
- express, cors, dotenv, @supabase/supabase-js (backend)

### 🧪 Testing tasks
- Confirmed `npm install` completed with 0 vulnerabilities on both frontend and backend.
- Confirmed all 5 Supabase tables exist via Table Editor.
- Confirmed Email auth provider shows "Enabled."

### 🐞 Common issues and debugging tips
- **AI provider swap mid-project:** handled cleanly because `ARCHITECTURE.md` always treated the LLM as a single wrapped client — no schema or API contract changes needed, only the client wrapper file and env variable name.
- **Supabase's newer key naming** ("Publishable key" / "Secret key") replaces the older "anon key" / "service_role key" terms found in some Supabase docs/tutorials — they are functionally equivalent.

### ✅ End-of-day checklist
- [x] Environment verified (Node, npm, Git)
- [x] Frontend scaffolded and dependencies installed
- [x] Backend scaffolded and dependencies installed
- [x] Supabase project created, schema deployed, RLS policies active
- [x] Email/password auth enabled
- [x] Environment variables configured in both `.env` files
- [x] AI provider decision resolved (Gemini) and documented
- [ ] Foundation code (routing, layout, auth scaffold) — in progress, see chat
- [ ] Hello World verified running — pending
- [ ] Committed and pushed to GitHub — pending

### 📸 Expected project state and screenshots to capture
- Terminal output for each scaffold/install step
- Supabase Table Editor showing all 5 tables
- Supabase Auth Providers showing Email enabled
- Running Hello World app in browser (pending)

### ➡️ Handoff notes for Day 4
**AI provider is Google Gemini, not Claude — use `GEMINI_API_KEY` and Gemini's API format for all AI calls from today onward.** Foundation (routing, layout, Supabase clients, auth scaffold) is in place by end of Day 3. Day 4 now covers a combined scope: (1) finish wiring **working** signup/login/logout and resume upload+save logic — originally planned as a standalone Day 3 — plus (2) the Skill Gap Report + Prep Plan AI integration using Gemini. If time is tight, prioritize (1) and (2)'s core loop; defer AI prompt-quality polish to Day 7's polish pass rather than over-iterating today.

---

## Day 4 — Auth + Resume Input (Working Logic) + Skill Gap Report & Prep Plan (AI Integration)

*Note: this day's scope was expanded on Day 3 — it now includes finishing the working authentication and resume-input logic (originally planned as a standalone Day 3) in addition to the original AI integration work, since Day 2 was used entirely for design. See Day 3's handoff notes above.*

### 🎯 Objective
Part A: Finish wiring **working** signup/login/logout and resume upload+save logic on top of today's (Day 3's) foundation scaffold. Part B: Send the saved resume text to the LLM (Gemini), generate a structured Skill Gap Report and Prep Plan, and display both clearly in the UI.

### 📖 What I'll learn
Wiring a managed auth flow into a React UI; handling file uploads and PDF text extraction; prompt engineering for structured, reliable JSON output from an LLM; designing a UI around AI-generated content that must feel personalized and trustworthy.

### 🛠 Features to build
**Part A — Auth + Resume Input:**
- Working signup / login / logout (build on Day 3's `useAuth` scaffold)
- Protected route enforcement (build on Day 3's `ProtectedRoute` scaffold)
- Resume upload (PDF, using `pdfjs-dist`) with text extraction
- Resume paste-text fallback
- Save extracted resume text to the `resumes` table, linked to the logged-in user

**Part B — AI Integration:**
- "Analyze My Resume" action that calls the Gemini API
- Skill Gap Report display (strengths vs. gaps)
- Personalized Prep Plan display (prioritized topic list)
- Save both to the database, linked to the user and resume

### 📝 Step-by-step implementation plan

**Part A:**
1. Build `SignUp.jsx` and `Login.jsx` forms using `supabase.auth.signUp()` and `supabase.auth.signInWithPassword()`, using the `useAuth` hook created Day 3.
2. Confirm the `ProtectedRoute` wrapper (Day 3 scaffold) correctly redirects unauthenticated users.
3. Build `ResumeUpload.jsx`: a file input accepting `.pdf`, plus a "Paste your resume text instead" textarea toggle.
4. Use `pdfjs-dist` to extract text client-side from the uploaded PDF.
5. On submit, save extracted/pasted resume text to the `resumes` table (RLS-protected, per `SCHEMA.md`) linked to `user_id`.
6. Show a simple confirmation state ("Resume received") after successful save.

**Part B:**
7. Define the **SDE Intern skill framework** as a fixed reference list fed into the prompt — e.g. Data Structures & Algorithms, OOP fundamentals, System Design basics, Databases/SQL, Version Control/Git, Web Fundamentals, Problem Solving/Communication.
8. Write the Gemini prompt instructing the model to: read the resume text, compare against the skill framework, and return **strict JSON**: `{ strengths: [...], gaps: [{ topic, why, priority }], prep_plan: [{ topic, action, priority }] }`.
9. Build the backend endpoint `POST /api/analyze-resume` (per `API.md`): fetches resume text, calls the Gemini API via `geminiClient.js`, parses the JSON response, saves it to `skill_reports`.
10. Build `SkillGapReport.jsx` and `PrepPlan.jsx` to render the results clearly.
11. Add a loading state while the AI call is in progress, and error handling for malformed/failed responses (retry-once pattern per `ARCHITECTURE.md`).

### 📂 Files and folders to create or modify
```
frontend/src/
├── auth/
│   ├── SignUp.jsx
│   ├── Login.jsx
├── resume/
│   ├── ResumeUpload.jsx
│   ├── resumeParser.js
├── analysis/
│   ├── SkillGapReport.jsx
│   ├── PrepPlan.jsx
backend/
├── routes/
│   ├── analyzeResume.js
├── prompts/
│   ├── skillGapPrompt.js
├── lib/
│   ├── geminiClient.js
```

### 🔗 APIs, libraries, services, or tools to integrate
- `@supabase/supabase-js` (auth + database calls)
- `pdfjs-dist` (PDF text extraction)
- Google Gemini API
- Supabase (`resumes` and `skill_reports` tables)

### 🧪 Testing tasks
- Sign up a new test account, confirm it appears in Supabase Auth dashboard.
- Log out and log back in successfully.
- Upload a real PDF resume, confirm extracted text looks correct (spot check).
- Use paste fallback, confirm it saves identically.
- Confirm an unauthenticated user is redirected away from protected screens.
- Run the analysis on 3-4 different real/sample resumes and check output quality and consistency.
- Confirm malformed JSON from Gemini is caught and doesn't crash the UI.
- Confirm results save correctly and reload correctly if the user revisits the page.

### 🐞 Common issues and debugging tips
- **PDF extraction returns garbled text:** common with multi-column resumes — this is exactly why the paste fallback exists; don't over-invest time perfecting PDF parsing.
- **Supabase RLS blocking inserts:** confirm policies from `SCHEMA.md` are active (verified Day 3) — if inserts fail, double check `auth.uid() = user_id` matches.
- **Gemini returns JSON wrapped in markdown fences:** strip these before `JSON.parse()`, or instruct the model explicitly to return raw JSON only.
- **Report feels generic, not personalized:** verify the actual resume text is being interpolated into the prompt, not a placeholder.

### ✅ End-of-day checklist
- [x] Signup/login/logout working end-to-end
- [x] Protected routes enforced
- [x] PDF upload extracts and saves text; paste fallback works identically
- [x] Resume analysis produces valid structured JSON reliably (verified working, real personalized output confirmed)
- [x] Skill Gap Report and Prep Plan render clearly and persist correctly
- [x] Error states handled gracefully throughout (caught and correctly reported both a 404 routing bug and a 502 Gemini model error during testing)

### 🐞 Issues encountered and resolved today
1. **404 on `/analyze-resume`:** `apiClient.js`'s base URL didn't include the `/api` prefix used when mounting routes in `backend/index.js`. Fixed by calling `apiPost('/api/analyze-resume', ...)`.
2. **502 — Gemini model deprecated:** `gemini-2.0-flash` returned `404 Not Found` from Google's API — the model was retired. Google's own error message specified the replacement. Fixed by updating `backend/lib/geminiClient.js` to use `gemini-3.6-flash`.

### 📸 Expected project state and screenshots to capture
- Screenshot of signup form and successful account creation
- Screenshot of resume upload screen with a real resume uploaded
- Screenshot of a completed Skill Gap Report and Prep Plan for a real test resume ✅ captured
- Screenshot of the relevant Supabase table rows (`resumes`, `skill_reports`) ✅ captured

### ➡️ Handoff notes for next day
Auth, resume storage, and AI-driven Skill Gap Report + Prep Plan are all working and persisted, verified against a real resume. **Note the AI model in use is `gemini-3.6-flash`, not `gemini-2.0-flash`** — if the model is deprecated again in the future, check Google's error message for the current recommended replacement. Day 5 builds the tagged question bank and the logic that selects mock interview questions based on the gaps identified today.

---

## Day 5 — Interview Question Bank + Semi-Dynamic Selection Logic

### 🎯 Objective
Build the tagged question bank (conceptual + coding-review questions) and the logic that selects relevant questions based on the user's identified skill gaps.

### 📖 What I'll learn
Structuring reusable content data; writing selection/filtering logic that connects two features (Skill Gap Report → Interview) into one coherent product loop.

### 🛠 Features to build
- Static, tagged question bank (stored as JSON or a database table)
- Question selection logic (filter/prioritize by matching gap topics)
- Interview session initialization (creates a set of questions for the user to answer)

### 📝 Step-by-step implementation plan
1. Build the question bank content: aim for **25-40 questions total**, tagged by topic (matching the Day 4 skill framework: DSA, OOP, System Design basics, Databases/SQL, Git, Web Fundamentals). Mix conceptual questions (~60%) and coding-review questions (~40%, e.g. "Write a function to X, then explain your approach").
2. Store the bank either as a static JSON file (`questionBank.json`) bundled with the app, or as a Supabase table `questions` (id, topic, type, prompt, difficulty) — a table is preferable since it lets you edit content without redeploying.
3. Write the **selection logic**: given the user's `gaps` array (with priorities) from `skill_reports`, select ~6-8 questions total, weighted toward higher-priority gap topics, with at least 1 question from a topic the user is strong in (to build confidence and demonstrate range).
4. Create an `interview_sessions` table: `id, user_id, skill_report_id, question_ids (array), created_at, status`.
5. Build the "Start Mock Interview" action: runs the selection logic, creates a session row, and navigates the user into the interview flow (built tomorrow).

### 📂 Files and folders to create or modify
```
backend/
├── data/
│   ├── questionBank.json          (or migrate to Supabase table)
├── routes/
│   ├── startInterview.js
├── logic/
│   ├── selectQuestions.js
```

### 🔗 APIs, libraries, services, or tools to integrate
- Supabase (new `questions` and `interview_sessions` tables, or bundled JSON)

### 🧪 Testing tasks
- Confirm selection logic returns different question sets for different gap profiles (test with 2-3 varied skill reports).
- Confirm no duplicate questions within a single session.
- Confirm a session row is created correctly with the right `question_ids`.

### 🐞 Common issues and debugging tips
- **Selection logic always returns the same questions:** check that gap priority/topic matching is actually reading the real `gaps_json`, not falling back to a default.
- **Question bank too thin in one topic:** if a topic has too few tagged questions, selection will feel repetitive across users — pad thin topics before moving on.

### ✅ End-of-day checklist
- [x] Question bank has 25-40 tagged questions covering all skill-framework topics (30 questions, all 7 topics)
- [x] Selection logic reliably weights toward gap topics
- [x] `interview_sessions` created correctly with selected question IDs (verified 3 test sessions, each with 7 question UUIDs)
- [x] Manually verified output feels personalized (question topics matched each test profile's gap areas)

### 🐞 Issues encountered and resolved today
- **SQL Editor failed on a single 30-row INSERT** (backend error, likely a statement size/timeout limit on this project tier). Fixed by splitting into 4 smaller batches (3, 9, 9, 9 rows).
- **Duplicate rows from re-running batches across multiple open SQL Editor tabs** — table showed 66 rows instead of 30. Fixed with a `DELETE ... WHERE id NOT IN (SELECT MIN(id) ... GROUP BY ...)` de-duplication query, verified back down to exactly 30.

### 📸 Expected project state and screenshots to capture
- Screenshot of the question bank data (Supabase table view) ✅ captured
- Screenshot/log of selection logic output for a sample skill report ✅ captured (`interview_sessions` table + browser console)

### ➡️ Handoff notes for next day
Question selection is working and tied to each user's gaps. `interview_sessions` holds the question set for a session (currently created via the Analysis screen's "Start Mock Interview" button, which for now just logs the result and shows an alert — no dedicated interview-taking UI yet). Day 6 builds the actual interview UI — presenting questions one at a time, capturing answers, and sending each answer to the LLM (Gemini, using model `gemini-3.6-flash`) for feedback.

---

## Day 6 — Mock Interview Flow + AI Feedback

### 🎯 Objective
Build the interview-taking experience: present questions one at a time, capture the user's answer, and generate structured AI feedback (score + strengths + improvements) per answer.

### 📖 What I'll learn
Building multi-step interactive flows in React; prompt engineering for evaluative (not just generative) AI tasks; designing UI for AI feedback that feels credible and useful.

### 🛠 Features to build
- Interview question-by-question UI (progress indicator, one question at a time)
- Answer input (textarea for both conceptual and coding-review questions)
- AI feedback generation per answer (score + 3-4 structured points)
- Session summary screen at the end

### 📝 Step-by-step implementation plan
1. Build `InterviewSession.jsx`: loads the session's question set, shows one question at a time with a progress bar ("Question 3 of 7").
2. Build the answer textarea with a "Submit Answer" button.
3. Write the **feedback prompt**: given the question, the question type (conceptual/coding-review), and the user's answer, instruct the LLM to return strict JSON: `{ score: 1-10, strengths: [...max 3], improvements: [...max 3] }`. Keep the prompt strict about staying within moderate detail (per PRD scope) — not a full model answer.
4. Build `POST /api/evaluate-answer` endpoint that calls the LLM and returns parsed feedback.
5. Create an `interview_answers` table: `id, session_id, question_id, user_answer, score, strengths_json, improvements_json, created_at`.
6. After each answer's feedback is shown, let the user proceed to the next question.
7. Build `SessionSummary.jsx`: shown after the last question — average score, list of all questions with their individual scores, link back to the dashboard.

### 📂 Files and folders to create or modify
```
frontend/src/
├── interview/
│   ├── InterviewSession.jsx
│   ├── QuestionCard.jsx
│   ├── FeedbackCard.jsx
│   ├── SessionSummary.jsx
backend/
├── routes/
│   ├── evaluateAnswer.js
├── prompts/
│   ├── feedbackPrompt.js
```

### 🔗 APIs, libraries, services, or tools to integrate
- Your LLM provider's API
- Supabase (`interview_answers` table)

### 🧪 Testing tasks
- Complete a full mock interview session end-to-end (all questions, all feedback).
- Test with a deliberately weak/short answer and a strong/detailed answer — confirm scores and feedback genuinely differ.
- Confirm session summary correctly aggregates all answers and scores.
- Refresh mid-session and confirm behavior is sensible (either resumes or clearly restarts — decide and be consistent).

### 🐞 Common issues and debugging tips
- **Feedback feels generic/copy-pasted across answers:** verify the actual `user_answer` text is reaching the prompt, not a stale value.
- **Score inconsistency (same answer scores very differently on reruns):** add a bit more structure/rubric guidance to the prompt (e.g. "score 8-10 = correct and well-explained, 5-7 = correct but underexplained, below 5 = incorrect or missing key ideas").
- **UI feels slow between questions:** make sure the loading state clearly communicates "AI is reviewing your answer" so it doesn't look frozen.

### ✅ End-of-day checklist
- [x] Full interview session completes end-to-end without errors (verified full 7-question run)
- [x] Feedback is structured, specific, and varies meaningfully by answer quality
- [x] Session summary displays and aggregates correctly (6.9/10 average, matched Supabase's stored 6.857... rounded correctly)
- [x] All answers and scores persist to the database (7 rows in `interview_answers`, session marked `completed` with correct `average_score`)

### 🐞 Issues encountered and resolved today
- **Missing `/interview-summary` route:** planned as part of Milestone 3 but the full interview run (built and tested in Milestone 2) reached it before that milestone's route was added, producing a blank page with a "No routes matched" console error. Expected sequencing gap, not a bug — resolved by completing Milestone 3 (`SessionSummary.jsx` + route registration) as planned.

### 📸 Expected project state and screenshots to capture
- Screenshot of a question card mid-interview ✅ captured (via earlier milestone testing)
- Screenshot of an AI feedback card after answering ✅ captured
- Screenshot of the final session summary screen ✅ captured, cross-verified against Supabase

### ➡️ Handoff notes for next day
The full core product loop now works locally end-to-end: signup → resume → gap report/prep plan → mock interview (7 questions, real Gemini feedback) → summary with accurate average score. Day 7 focuses on polish, the saved-history feature (dashboard showing past reports/sessions), and getting the app ready to deploy.

---

## Day 7 — Saved History Dashboard + UI Polish

### 🎯 Objective
Build the dashboard that lets logged-in users revisit past prep plans and interview attempts, and polish the overall UI/UX so the product feels cohesive, not like disconnected screens.

### 📖 What I'll learn
Designing a simple dashboard/history view backed by relational data; UI polish techniques that meaningfully increase perceived product quality without much extra time investment.

### 🛠 Features to build
- Dashboard/home screen listing past skill reports and interview sessions
- Navigation between all screens (dashboard, upload, report, interview, summary)
- Visual polish pass (consistent spacing, colors, loading/empty states)

### 📝 Step-by-step implementation plan
1. Build `Dashboard.jsx`: on login, query `skill_reports` and `interview_sessions` for the current user, list them chronologically with key info (date, average score, quick links).
2. Add "Start New Analysis" and "View Report" / "Retake Interview" actions from the dashboard.
3. Add a persistent navigation bar (logo/name, Dashboard, Logout) across all screens.
4. Do a full pass on visual consistency: consistent color palette, spacing, button styles, font sizes across every screen built Days 3-6.
5. Add empty states (e.g. "No reports yet — upload your resume to get started") and loading skeletons where missing.
6. Test the entire flow as a brand-new user from scratch, then again as a returning user with history.

### 📂 Files and folders to create or modify
```
frontend/src/
├── dashboard/
│   ├── Dashboard.jsx
├── layout/
│   ├── NavBar.jsx
│   ├── EmptyState.jsx
├── styles/
│   ├── theme.css (or equivalent, consolidating colors/spacing)
```

### 🔗 APIs, libraries, services, or tools to integrate
- No new services — this is consolidation and UI work using what's already integrated

### 🧪 Testing tasks
- New user flow: signup → dashboard (empty) → full loop → dashboard (populated).
- Returning user flow: log in → see history → open an old report → retake interview.
- Check the app on a smaller browser window/mobile width for obvious layout breaks.

### 🐞 Common issues and debugging tips
- **Dashboard queries slow or return wrong user's data:** double check RLS policies and that queries filter by `user_id` explicitly, not relying on RLS alone during development.
- **Inconsistent styling across screens:** this is the day to fix it — resist adding new features today, this is a polish-only day.

### ✅ End-of-day checklist
- [x] Dashboard shows accurate history for the logged-in user only (verified: 3 real reports, dates, gaps, scores)
- [x] Navigation works consistently across all screens (verified across Dashboard, Resume Upload, Analysis, Interview, Summary)
- [x] Empty and loading states exist everywhere data is fetched (shared `EmptyState.jsx` component)
- [x] Full new-user and returning-user flows tested manually, no dead ends
- [x] Global visual consistency pass applied (shared `theme.css` — colors, spacing, typography, buttons, inputs, focus states)

### 🐞 Issues encountered and resolved today
- **Dashboard heading overlapped with long email addresses** — caught during Milestone 1 testing, fixed in Milestone 2 by splitting "Welcome back" and the email onto separate lines with `word-break`.

### 📸 Expected project state and screenshots to capture
- Screenshot of the dashboard with history populated ✅ captured
- Screenshot showing consistent nav/branding across 3 different screens (Dashboard, Resume Upload, Interview Summary) ✅ captured

### ➡️ Handoff notes for next day
The app is now feature-complete and polished, running correctly on localhost with a consistent visual theme applied across every screen. Day 8 is entirely about deployment: getting the frontend, backend, and environment variables live and working in production.

---

## Day 8 — Testing, Debugging & Production Optimization ✅ COMPLETED

*Note: this day was reordered on Day 8 itself — originally the Blueprint scheduled Deployment for Day 8 and this QA pass for later. We swapped the order so the app is hardened before going live rather than after. Day 9 is now Deployment; Day 10 remains final QA + submission (lighter now, since most hardening happened today).*

### 🎯 Objective
Perform a full QA, security, and production-readiness review of the application built Days 3-7, and fix every real issue found before deploying.

### 📖 What I'll learn
Systematic pre-launch QA practices; the difference between `beforeunload` (tab close/refresh) and browser Back/Forward navigation, and why they require different handling in a single-page app; defensive patterns like error boundaries and catch-all routes.

### 🛠 Issues found and fixed
**Backend hardening:**
- Deduplicated Gemini retry logic into a single shared `callGeminiForJson` helper (was previously copy-pasted in two route files)
- Added startup validation — the server now fails fast with a clear message if `GEMINI_API_KEY` is missing, instead of failing cryptically mid-request
- Added missing database indexes on foreign key columns (`user_id`, `session_id`) across `resumes`, `skill_reports`, `interview_sessions`, `interview_answers`

**Frontend robustness:**
- Added a catch-all 404 route (`NotFound.jsx`) — previously a mistyped/missing URL rendered a blank page
- Added a React Error Boundary — previously any unexpected render error blanked the entire app with no recovery path
- Fixed accessibility: form `<label>` elements now properly associated with inputs via `htmlFor`/`id`; error messages use `role="alert"`
- Added a client-side 3000-character limit (matching the backend's existing limit) with a live counter on interview answers, so users get feedback before submitting instead of after
- Removed a leftover debug `console.log`

**Unsaved-progress navigation warning (the main debugging effort of the day):**
- First attempt used only `beforeunload` — confirmed via testing that this does **not** fire on browser Back/Forward, since React Router intercepts Back as a client-side navigation, not a real page unload
- Second attempt added a `popstate` listener with a manual `history.pushState` guard — this caused a *worse* bug: mixing native history manipulation with React Router's internal state tracking caused `location.state` to be lost on Back, breaking the interview session entirely
- **Final fix:** made `sessionStorage` the source of truth for the active interview session (not React Router's `location.state`), so the session survives regardless of history-stack manipulation. The `popstate` guard now works correctly: Cancel keeps the user on their in-progress question with their typed answer intact; confirming takes them to the Dashboard and clears the stored session.
- Visually verified working via screenshot, including the Cancel/Stay path

### 📂 Files created, modified, or deleted
```
backend/
├── lib/geminiClient.js          (modified — startup validation, shared retry helper)
├── routes/analyzeResume.js       (modified — uses shared helper)
├── routes/evaluateAnswer.js      (modified — uses shared helper)

frontend/src/
├── layout/
│   ├── NotFound.jsx              (new)
│   ├── ErrorBoundary.jsx         (new)
├── App.jsx                       (modified — catch-all route, ErrorBoundary wrapper)
├── auth/
│   ├── Login.jsx                 (modified — accessible labels)
│   ├── SignUp.jsx                (modified — accessible labels)
├── interview/
│   ├── QuestionCard.jsx          (modified — character limit + counter, accessible label)
│   ├── InterviewSession.jsx      (modified — sessionStorage-based navigation guard)
```
Plus a one-time SQL migration adding 4 indexes (run directly in Supabase, not a tracked file).

### 🔗 APIs, libraries, services, or tools used
None new — this was entirely refactoring and hardening of existing integrations (Supabase, Gemini).

### 🧪 Testing tasks completed
- Backend restart verified clean after refactor; resume analysis and answer feedback re-tested and confirmed unchanged in behavior
- 404 page tested with a nonsense URL
- Character limit tested at the 3000-char boundary
- Leave-interview warning tested three times across two debugging iterations, final version visually verified via screenshot including both Cancel and Confirm paths
- Full regression: complete 7-question interview run (via in-app buttons, no shortcuts) confirmed working end-to-end after all changes

### 🐞 Common issues and debugging tips (for future reference)
- **`beforeunload` does not catch browser Back/Forward in a React Router SPA.** Use a `popstate` listener for that case instead.
- **Do not rely on React Router's `location.state` surviving manual `history.pushState`/`popstate` manipulation.** If you need data to survive arbitrary history changes, store it in `sessionStorage` and treat that as the source of truth.

### ✅ End-of-day checklist
- [x] All 9 real issues identified in the QA review fixed and verified
- [x] Full regression test passed after all changes
- [x] No known blocking bugs remain
- [x] CORS restriction and rate limiting explicitly deferred and documented (not forgotten) — CORS to be fixed during tomorrow's deployment

### 📸 Expected project state and screenshots to capture
- Screenshot of the 404 page
- Screenshot of the leave-interview confirm dialog (Cancel and Confirm paths) ✅ captured
- Screenshot of a completed full interview run through the Summary screen ✅ captured

### ➡️ Handoff notes for next day
The application is fully hardened and regression-tested on localhost. Day 9 (originally Day 8 in the Blueprint) is deployment: get the frontend on Vercel, backend on Render, configure environment variables and Supabase redirect URLs, and **restrict CORS to the real production frontend domain** (currently open to all origins, acceptable for localhost dev only).

---

## Day 9 — Deployment

### 🎯 Objective
Deploy the complete application to a live, publicly accessible URL, with all environment variables and services (Supabase, Gemini API) working correctly in production.

### 📖 What I'll learn
Production environment variable management; debugging the gap between "works on localhost" and "works in production."

### 🛠 Features to build
None new — this day is entirely deployment and production verification of everything already built and hardened on Day 8.

### 📝 Step-by-step implementation plan
1. Push the final, polished, hardened codebase to GitHub.
2. Connect Vercel to the GitHub repo for the frontend; connect Render for the backend (per `ARCHITECTURE.md`'s locked stack decision).
3. Configure build settings (usually auto-detected for a Vite app).
4. Add all environment variables into each host's dashboard — **never commit these**.
5. **Restrict backend CORS to the actual deployed frontend domain** (flagged as a Day 8 known-gap — must not go live with CORS open to all origins).
6. In Supabase, add the production URL to Auth's allowed redirect URLs / site URL settings.
7. Trigger the deploy, then test the entire core loop on the live URL exactly as a new user would.
8. Fix any production-only bugs and redeploy.

### 📂 Files and folders to create or modify
```
backend/index.js                 (update CORS configuration for production)
frontend/vite.config.js          (verify build settings if needed)
```

### 🔗 APIs, libraries, services, or tools to integrate
- Vercel (frontend hosting)
- Render (backend hosting)
- Supabase Auth production URL configuration

### 🧪 Testing tasks
- Full core loop test on the live URL: signup → resume → report → plan → interview → feedback → summary → dashboard history.
- Test in an incognito/private browser window to rule out cached localhost sessions.
- Test signup/login specifically, since this is the most common production-only failure point.
- Re-verify the leave-interview warning and 404 page work identically in production.

### 🐞 Common issues and debugging tips
- **"Works locally, breaks in production":** almost always environment variables not set in the host dashboard, or Supabase redirect URL not updated.
- **CORS errors in production only:** confirm the backend's CORS allowed-origins list includes the exact deployed frontend URL (including https://, no trailing slash mismatch).
- **Auth redirect loops:** check Supabase Auth site URL settings match your actual deployed domain exactly.

### ✅ End-of-day checklist
- [ ] App is live at a public URL
- [ ] CORS restricted to the production frontend domain only
- [ ] Full core loop tested and working on the live URL, in an incognito window
- [ ] Signup/login confirmed working in production
- [ ] No console errors on any core screen in production

### 📸 Expected project state and screenshots to capture
- Screenshot of the live URL in the browser address bar with the app loaded
- Screenshot of a completed live signup
- Screenshot of a completed live interview feedback screen

### ➡️ Handoff notes for next day
The product is fully deployed and functioning end-to-end in production. Day 10 focuses on final live-site QA, the README/case study, demo video, and submission.

---

## Day 10 — README, Demo Video, Final QA & Submission

### 🎯 Objective
Produce a polished README/case study, record a demo video, do one final live-site QA pass, and formally submit the completed capstone.

### 📖 What I'll learn
Communicating a technical project clearly to a time-constrained reader; systematic final QA under time pressure without introducing new risk.

### 🛠 Features to build
None — documentation, presentation, and bug fixes only. No new features today, by design.

### 📝 Step-by-step implementation plan
1. Write `README.md` in the repo root: Problem, Solution (with screenshots), Core Features, Tech Stack, Architecture, Live Demo link, How to Run Locally, What's Out of Scope / Future Work.
2. Add 3-5 real screenshots from the live deployed app into the README.
3. Write a short case study section: the problem, the key product decision you're proud of (e.g. semi-dynamic question selection tying gaps to practice, or the sessionStorage navigation-guard fix from Day 8), and one thing you'd do differently with more time.
4. Record a 2-4 minute demo video walking through the live product; upload and link it in the README.
5. Run the **full core loop** on the live URL once more, in a fresh incognito window, as a first-time user.
6. Test edge cases: a very short/sparse resume, an empty interview answer, rapid double-clicking submit buttons, logout mid-flow.
7. Prioritize any found bugs: **P0 (breaks the core loop) → P1 (visible but doesn't block) → P2 (nice-to-fix, skip if time-constrained)**. Fix only P0 and P1, then re-run the full core loop test after any fix.
8. Final proofread of the README — links, screenshots, typos.
9. Submit per the AB Talks 60-Day Claude AI Challenge submission instructions (repo link, live link, video link, README).
10. Optional: a short personal retrospective — what worked, what you'd scope differently next time.

### 📂 Files and folders to create or modify
```
README.md
docs/
├── case-study.md   (optional, can also fold into README)
├── screenshots/
```

### 🔗 APIs, libraries, services, or tools to integrate
None new — free OS-native screen recording tool only.

### 🧪 Testing tasks
- Full core loop, fresh incognito window, start to finish.
- Edge cases: empty inputs, very long inputs, rapid clicking, logout mid-flow.
- Re-verify the leave-interview warning and 404 page work identically in production (carried over from Day 8/9).
- Click every link in the README; watch the demo video fully through once.

### 🐞 Common issues and debugging tips
- **Tempted to add "just one more feature":** don't — risk tolerance should be near zero today; a working, polished v1.0 beats a broken v1.1.
- **A fix for one bug breaks something else:** always retest the full loop after any change.
- **Screenshots go stale** if the UI changes after taking them — take final screenshots only after all fixes are deployed.

### ✅ End-of-day checklist
- [ ] README complete with screenshots, live link, and tech stack
- [ ] Case study section written
- [ ] Demo video recorded and uploaded
- [ ] Full core loop verified working on live URL, fresh incognito session
- [ ] All P0 and P1 bugs (if any) fixed and retested
- [ ] Submission completed per challenge instructions

### 📸 Expected project state and screenshots to capture
- Screenshot of the finished README rendered on GitHub
- Final screenshot of the deployed dashboard
- Screenshot of the submitted entry/confirmation (if applicable)

### ➡️ Handoff notes
Capstone complete. Project is deployed, documented, demoed, and submitted. Any remaining P2 issues or the excluded v1.0 features (HR interview practice, code execution, multi-role support, dynamic question generation, server-side rate limiting) are documented as future work in the README — a clear, honest scope story is itself a strength in review.
