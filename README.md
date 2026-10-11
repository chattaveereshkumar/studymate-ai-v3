# StudyMate AI V3

Responsive React + TypeScript study workspace starter with Supabase authentication and owner-scoped database policies.

## Included
- Sign up, sign in, sign out, password-reset request (Supabase Auth)
- Student profile: name, college, course, year, semester, hours/day, preferred time
- Subject add/delete and progress/priority
- Exam add/delete and exam-aware scheduling
- Seven-day deterministic study planner; manual/completed tasks survive regeneration
- Manual tasks and completion tracking
- Focus timer and session logging
- Dashboard and progress summaries
- AI tutor interface wired to a secure Supabase Edge Function starter
- SQL schema with Row Level Security for profiles, subjects, exams, sessions, tasks, quiz attempts
- Planner unit tests

## Important honest status
This is a complete project starter, not yet a deployed production service. You must configure Supabase, run the schema, and deploy the AI function before accounts/cloud storage/real AI work. Tasks are currently stored in browser localStorage (scoped by signed-in user in that browser); migrate them to the `study_tasks` table for cross-device sync. AI quiz generation, reminders/notifications, real streak history, calendar sync, and end-to-end production testing remain to be implemented before calling V3 feature-complete.

## Run
1. Install Node.js 20+.
2. Extract the ZIP and open this folder in VS Code.
3. Run `npm install`.
4. Copy `.env.example` to `.env.local`.
5. Set `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` from your Supabase project.
6. Run all of `supabase/schema.sql` in the Supabase SQL Editor.
7. Run `npm run dev` and open the URL Vite prints.

Test/build: `npm test` then `npm run build`.

## Enable AI tutor
Deploy with Supabase CLI: `supabase functions deploy ai-tutor`.
Set server secrets: `supabase secrets set OPENAI_API_KEY=YOUR_KEY` and optionally `supabase secrets set OPENAI_MODEL=gpt-4.1-mini`. Do not put provider keys in `.env.local` or browser code. The function currently needs a production review, rate limiting, and provider usage controls before public use.

## Deployment
Deploy frontend to Vercel, Netlify, or Cloudflare Pages; set the two `VITE_SUPABASE_*` variables in hosting settings and configure Supabase Auth redirect URLs. Never commit `.env.local`, a service-role key, or an AI provider key.

## Structure
- `src/App.tsx` — application screens and interactions
- `src/lib/planner.ts` — transparent deterministic planner
- `src/lib/planner.test.ts` — planner tests
- `src/lib/supabase.ts` — safe browser client setup
- `supabase/schema.sql` — tables and Row Level Security
- `supabase/functions/ai-tutor/index.ts` — server-side AI function starter
