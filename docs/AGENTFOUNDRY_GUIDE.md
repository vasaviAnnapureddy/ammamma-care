# Ammamma Care: full path from setup to submission

6 Nov 2026. 
Every step is tagged CHECKED (with source) or NOT CHECKED. If a button looks different from what is written here, trust the screen and tell Claude.

## 0. Truth box (read first)
- Your laptop already has git 2.51, Node 24.15 and npm 11.12, and your git name is set. CHECKED on your laptop, 6 Nov.
- `E:\ammamma-care` is not a git repo yet. CHECKED.
- AgentFoundry's AI (SMART-CODE) writes code. The wiki says AgentFoundry can only READ GitHub for now, so you push with git commands from section 3. CHECKED on wiki.agentfoundry.me/connect/github.
- The AI inside YOUR app (it reads notes and prescription photos) is separate. Plan: Google Gemini API, Flash model, free tier. Exact model names and limits change often. NOT CHECKED today. Check them in AI Studio on the day, and test with one real call in Phase 2.
- PRIVACY: Google's free tier may use what you send to improve its products. NOT CHECKED today, so read the terms in AI Studio before you send anything. Until then: send no names to the AI, and use only DEMO residents or photos with the name covered.
- 15 working features in 8 nights is possible but risky. If Phase 5 is late, drop the 3 stretch features (marked S).

## 1. The 15 features
1. AI caseworker: reads a staff note (Telugu or English), suggests profile updates, drafts Form 1 letter, Prajavani petition, Elderline script. Rules check money facts.
2. AI photo reader: prescription or report photo -> medicine list and doctor notes. Staff must tick "correct".
3. Interview mode: the 15 questions in docs/INTAKE_15.md + 5 staff questions. Telugu first, English, Hindi. Big buttons, auto-save, "missed questions" list.
4. Many homes: each home has its own space and a 4-digit PIN. A demo home with fake residents and no PIN, for judges.
5. Resident cards "1 - Sarojini": colour, next step, days waiting.
6. Card page: profile, dated notes, health, bills, "this month vs last month".
7. Eligibility engine: Eligible / Not eligible / Check locally, with the reason (lib/schemes.json).
8. Document gap planner: which document blocks what, plus the doorstep fix.
9. Priority score: who needs help first, with reasons.
10. Proof trail: date, office, acknowledgement number, reply.
11. Escalation ladder: reminder after X days, next free channel, message drafted.
12. Places: nearest Jan Aushadhi Kendras for the home's PIN, LVPEI@Home with "what to say on the call".
13. Home problem finder + impact page (totals only, no names).
14. Downloads: one card as PDF, all cards as Excel.
15. S: Monthly wellbeing check with trends; S: fund-need cards for donors; S: booking tracker.

## 2. Tonight: setup (Phase 1, Fri 6 Nov)

### 2a. GitHub repo (5 min, you do it)
1. Open github.com and sign in as vasaviAnnapureddy.
2. Top right **+** -> **New repository**.
3. Repository name: `ammamma-care`. Choose **Public**.
4. Leave "Add a README" OFF. Under license choose **MIT License**.
5. Click **Create repository**. Keep this page open.

### 2b. Free accounts (15 min, you do it)
- Vercel: vercel.com -> **Sign Up** -> Hobby -> **Continue with GitHub**.
- Neon: neon.tech -> **Sign up** -> with GitHub -> create a project named `ammamma-care`. Pick the region closest to India in the list (NOT CHECKED which ones are shown). Copy the **connection string**.
- Google AI Studio: aistudio.google.com -> sign in -> **Get API key** -> create a key.
- SECRET RULE: the Neon string and the AI key go only in a file called `.env.local` on your laptop. Never paste them in chat, never on GitHub.

### 2c. AgentFoundry (20 min, CHECKED on wiki "first 10 minutes")
1. agentfoundry.me -> **Download v0.1.61 for Windows**. Run the setup file (the wiki calls it `CodeNow-Setup.exe`, the old name).
2. First screen -> **Sign up** -> your email.
3. Click **+** at the top next to the tabs -> pick `E:\ammamma-care` -> **Open**.
4. Bottom tab row -> **SMART-CODE**. Type `hello, are you ready?` and press **Ctrl+Enter**.
5. **Connections** tab -> **GitHub** -> allow only the `ammamma-care` repo.

### 2d. Connect the folder to GitHub (PowerShell, you run it)
Open PowerShell (Start -> type PowerShell -> Enter). Run one line at a time:
```
cd E:\ammamma-care
git init
git branch -M main
git remote add origin https://github.com/vasaviAnnapureddy/ammamma-care.git
git pull origin main
git add .
git commit -m "Start Ammamma Care: plan and notes"
git push -u origin main
```
- `git pull` brings down the LICENSE file GitHub made. If a browser window asks you to sign in to GitHub, sign in there yourself.
- Done when: github.com/vasaviAnnapureddy/ammamma-care shows DECISIONS.md and docs.

## 3. How every phase works (the same loop each night)
1. In AgentFoundry, open the **SMART-CODE** tab. Paste that phase's prompt (section 4). Press **Ctrl+Enter**.
2. It must explain the files first. Read, then reply `ok, create them`.
3. Run the app: in AgentFoundry's terminal, or in PowerShell inside `E:\ammamma-care`, type `npm run dev`. Open http://localhost:3000 in Chrome. To stop it, press **Ctrl+C** in that terminal.
4. Check "Done when". If it fails, paste ONLY the red error lines to SMART-CODE.
5. Save to GitHub:
```
git add .
git commit -m "Phase N: <what>"
git push
```
6. Before the FIRST push, check that `.gitignore` has `.env.local` in it. If not, stop and ask.

## 4. Phases and the prompt to paste

| Phase | Date | Prompt to paste in SMART-CODE | Done when |
|---|---|---|---|
| 1 | Fri 6 | Read DECISIONS.md, docs/PHASES.md, docs/INTAKE_15.md. Create a Next.js app with TypeScript and Tailwind in this folder. Add a .gitignore that blocks .env*, node_modules and any real data. Explain every file before you create it. | localhost:3000 opens |
| 2 | Sat 7 | Add Prisma with Neon Postgres (connection string in .env.local). Tables: Home, Resident, Answer, Note, Event, Medicine, Place. Seed a Demo Home with 10 fake residents. Add one test API route that calls the Gemini Flash API with "say hello in Telugu". Explain first. | Fake residents show; the AI replies in Telugu |
| 3 | Sun 8 | Build interview mode from docs/INTAKE_15.md: one question per screen, big buttons, Telugu / English / Hindi switch, "not sure" and "ask later", a note box, auto-save each answer, and a "missed questions" list. Explain first. | One fake resident filled on the phone |
| 4 | Mon 9 | Build resident cards ("1 - Sarojini") and a card page with notes, health, bills, this month vs last month. Add a 4-digit PIN per home; the Demo Home needs no PIN. Explain first. Then help me deploy to Vercel. | Live link works on a phone. Fill Form 2 (section 5) |
| 5 | Tue 10 | Add lib/schemes.json from docs/mega_prompt_v2_text.txt and docs/mega_prompt_v2_tables.txt, an eligibility engine with 3 outcomes and reasons, a document gap planner, and a priority score with reasons. Add tests for age limits. Explain first. | Each card shows top scheme, blocker, priority |
| 6 | Wed 11 | Add the AI caseworker: staff note -> suggested profile updates (staff approves) + drafted letters. Add photo upload: prescription -> medicine list (staff ticks correct). Never send names to the AI. Never give medical advice. Explain first. | A note becomes a draft letter; a photo becomes a medicine list |
| 7 | Thu 12 | Add proof trail and escalation ladder, places (Jan Aushadhi Kendras for the home PIN, LVPEI@Home call script), home problem finder, impact page with totals only, PDF card and Excel download. Explain first. | Excel opens; impact page shows totals |
| 8 | Fri 13 | Help me write README.md (what, why, how to run, how AgentFoundry was used), check every feature, and fix bugs only. No new features. | Everything works on the live link |

Stretch (only if Phase 7 is done on time): wellbeing trends, fund-need cards, booking tracker.

## 5. GitHub submission form ("Form 2")
Open: github.com/karlmehta/code-for-a-billion/issues/new?template=submission.yml (CHECKED, from codeforindia.org).
- Title: `[Submission] Ammamma Care: AI case manager for old age homes`
- Team / Project name: `Ammamma Care`
- Team members: `Vasavi Annapureddy (@vasaviAnnapureddy)`
- Problem statement: 2 to 5 sentences on elders who lose pensions and care because no one owns their case.
- What you built: the features + "built in AgentFoundry with SMART-CODE".
- GitHub repository URL: `https://github.com/vasaviAnnapureddy/ammamma-care`
- Demo URL: your Vercel link (later add the video link too).
- Scale & severity: use numbers with sources (judged 50%).
- Deployment & impact data: only real totals, no names. If none yet, say so honestly.
- Track: **Health**. Contact email: it will be PUBLIC, so choose which one.
- Tick the 3 boxes only when they are true.
- File it on Mon 9 after the live link works. Edit it on Fri 13 with real numbers and the video.

## 6. Video (Fri 13)
2 to 3 minutes: the problem (20 s), interview mode (30 s), a card (30 s), AI note -> letter (30 s), proof and escalation (20 s), impact totals (20 s). Use the Demo Home only.

## 7. Things only you can do
- All logins, keys and the GitHub sign-in pop-up.
- The home visit, consent from each resident, the home's PIN code.
- Calls: IPPB 155299, LVPEI 7032666437 (is Miyapur inside 25 km?), HelpAge (check the number).
- Approving every file in AgentFoundry.

## 8. Exact steps: Vercel, Neon, AI Studio (added 6 Nov after Vasavi hit the Vercel screen)

### Vercel: NOT now. Do it in Phase 4.
- Why: the repo has only docs, no app yet. Deploying now gives an empty or failed site.
- Now: close the "New Project" page. Do not pick "Pro Trial" or "Pro". Do not create a Team (Teams are paid).
- Your existing free account (the one running radhe-crm.vercel.app) can hold more projects. Radhe stays as it is.
- In Phase 4:
  1. Open https://vercel.com/new
  2. Next to `vasaviAnnapureddy/ammamma-care` click **Import**.
  3. In the team / scope dropdown pick your PERSONAL account (the one Radhe is under, marked Hobby). NOT CHECKED: the exact label, it is usually your name + "projects".
  4. Project Name: `ammamma-care`. Framework: Next.js (auto).
  5. Open **Environment Variables**, add `DATABASE_URL` and `GEMINI_API_KEY` (values from .env.local).
  6. Click **Deploy**. Your link: ammamma-care.vercel.app (or similar if taken).

### Neon (do tonight, 5 min)
1. Open https://console.neon.tech and sign in (GitHub is fine; use the same account as Radhe if Radhe used Neon).
2. Click **New Project**.
3. Name: `ammamma-care`. Postgres version: leave default.
4. Region: pick the one closest to India in the list (Singapore or Mumbai if shown).
5. Click **Create project**.
6. On the dashboard click **Connect**. Copy the connection string (starts with `postgresql://`).
7. Keep it in Notepad for now. In Phase 2 it goes into `.env.local` as `DATABASE_URL=...`. Never in chat or GitHub.
- Free: a new project on the free plan costs nothing (free plan allows many projects, CHECKED in ac-3).

### Google AI Studio (do tonight, 3 min)
Why: this key is for YOUR app's AI (reads staff notes and prescription photos). AgentFoundry's SMART-CODE only writes code; it is not inside your app.
1. Open https://aistudio.google.com/apikey and sign in with Google.
2. Click **Create API key**. If asked, create a new project for it.
3. Copy the key (starts with `AIza`). Keep it in Notepad.
4. In Phase 2 it goes into `.env.local` as `GEMINI_API_KEY=...`.
5. Before real resident data: read the free-tier terms on that page (privacy, NOT CHECKED).
