# Day 53 – Project Setup & Foundation

## Capstone Project

### AI Career & Interview Copilot

Day 53 focused on setting up the technical foundation of the AI Career & Interview Copilot capstone project.

## Today's Objective

The goal was to move from product planning and system design into the actual development environment by setting up the frontend, backend, database, authentication, environment configuration, and AI integration foundation.

## Tech Stack

- React + Vite
- Node.js + Express
- Supabase PostgreSQL
- Supabase Authentication
- Google Gemini API
- React Router
- PDF.js
- Vercel for frontend deployment
- Render for backend deployment

## Work Completed

### 1. Development Environment

Verified the development environment:

- Node.js v22.19.0
- npm v10.9.3
- Git v2.50.1

### 2. Frontend Setup

Created the React + Vite frontend application.

Installed:

- React
- Vite
- React Router DOM
- Supabase JavaScript client
- PDF.js

### 3. Backend Setup

Created the Node.js + Express backend.

Installed:

- Express
- CORS
- dotenv
- Supabase JavaScript client
- Google Gemini SDK

### 4. Supabase Setup

Created the `ai-career-copilot` Supabase project using the free tier.

Created and verified the following database tables:

- `resumes`
- `skill_reports`
- `questions`
- `interview_sessions`
- `interview_answers`

Row Level Security policies were also configured according to the approved database design.

### 5. Authentication

Enabled Supabase Email/Password authentication for the application.

### 6. Environment Configuration

Created separate environment files for the frontend and backend.

The frontend contains the Supabase project URL, publishable key, and backend API URL.

The backend contains the Supabase URL, Supabase secret key, Gemini API key, and server port.

Sensitive credentials are stored locally and are not committed to GitHub.

### 7. AI Provider Update

The original architecture planned to use the Anthropic Claude API.

However, Anthropic API access required paid credits, while the project has a free-tier requirement. Therefore, the AI provider was intentionally changed to Google Gemini.

The architecture and project documentation were updated to reflect this change.

The rest of the AI interaction design, API contracts, database schema, and application scope remain unchanged.

### 8. Gemini Integration Foundation

Installed the Google Gemini SDK and created the initial Gemini client foundation for future AI-powered features.

## Key Learning

Today I learned how to convert a product and system design into a working development foundation.

I also learned the importance of keeping API credentials in environment variables and protecting sensitive keys from being committed to GitHub.

Another important learning was that an AI provider can be replaced without redesigning the entire application when the architecture uses a dedicated AI client layer.

## Important Security Practices

- API keys are stored in `.env` files.
- Supabase secret credentials remain backend-only.
- Gemini API keys remain backend-only.
- `.env` files are excluded from Git tracking.
- Secret keys are never committed to GitHub.

## Day 53 Outcome

The project development environment and core foundation are ready for feature implementation.

The frontend and backend applications have been scaffolded, Supabase has been configured, authentication has been enabled, the database has been created, and the Gemini integration foundation has been prepared.

## Next Step

Day 54 will focus on implementing the first major product features, including authentication, resume handling, PDF parsing, and the Skill Gap Report functionality.

## Status

**Day 53 – Completed ✅**
