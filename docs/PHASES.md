# Ammamma Care: 15 features and 10 phases (v2, late-night plan)

> REPLACED on 6 Nov by docs/AGENTFOUNDRY_GUIDE.md version 3 (8 phases, 6 to 13 Nov). Kept only for history.

Rewritten 4 Nov 2026 after Vasavi asked for a bigger project. Replaces the first version.
Built only inside AgentFoundry. Facts: docs/notes/notes.md ac-1 to ac-5.

## Honest score check (GUESS, not a fact)
Judges score 4 x 25 (JUDGING.md, CHECKED). Feature count is NOT a criterion. More features only help "Quality", and only if they work.

| Criterion | If we do this plan well | If we have no field data |
|---|---|---|
| Size (25) | 17 to 21. 149M Indians 60+, 22.6% get a pension (v2 doc, LASI; not re-checked) | same |
| Severity (25) | 15 to 20. Lost pension, blindness from untreated cataract | same |
| Quality (25) | 18 to 22 if all 15 work. About 10 if many are half-broken | same |
| Proven impact (25) | 12 to 18 with 40 residents screened and applications with acknowledgement numbers | 0 to 5 |
| Total | about 62 to 81 | about 45 to 60 |

Nobody can know the real score. The 3 close entries have 0 real users (CHECKED, ac-3), so real data is the biggest lever.

## My earlier mistake
I put the AI caseworker in the "only if time is left" list. This is an AGENTIC-AI hackathon with a "Best Use of AgentFoundry Agents" award (CHECKED, ac-1). The AI agent must be core. Fixed below as feature 1.

## The 15 features (all connected)
1. **AI caseworker agent**: reads a caretaker note (English or Telugu), updates the profile, drafts Form 1 letter / Prajavani petition / Elderline script, plans next steps. Rules check every money fact; AI never decides eligibility.
2. **Layered interview** (about 15 data points per resident in 10 modules: basics, documents, money, pension history, health, medicines, eyes and ears, mobility, mood and loneliness, family and wishes). One question per screen, auto-save, "missed questions" list.
3. **Resident cards** "1 - Sarojini": colour, next step, days waiting, "This month" box, Telugu + English.
4. **Life timeline** per resident: every visit, call, document, reply.
5. **Eligibility engine**: Eligible / Not eligible / Check locally, with the reason, for every scheme in schemes.json.
6. **Document gap planner**: which document blocks what, and the doorstep fix.
7. **Proof trail**: date, office, acknowledgement number, officer name, reply.
8. **Escalation ladder**: reminder after X days, next free channel, message drafted.
9. **Home problem finder**: reads all residents and lists the home's biggest problems ("12 no bank account, 9 need eye check, 7 spend over Rs 500 a month on medicines").
10. **Priority score**: who needs help first, with reasons shown (no black box).
11. **Medicine tracker**: monthly cost, Jan Aushadhi price, nearest Kendras for the home's PIN, "call before going".
12. **Booking tracker**: LVPEI@Home group visit (suggested when 10+ need eye checks), IPPB doorstep visit, with reference numbers.
13. **Monthly wellbeing check**: mood, loneliness, falls, sleep, appetite. Shows trends per resident.
14. **Fund-need cards**: no names, rupee estimate, shareable image for donors. Consent only.
15. **Excel export + impact dashboard**: one resident or whole home; totals before and after.

Data: about 120 fields at first interview + every event, check and medicine after that. So each resident builds up hundreds of data points over time. No Aadhaar or bank numbers ever.

## Phases (late nights, about 4 hours a night)

| Phase | Date | Build | Done when |
|---|---|---|---|
| 1 | Wed 4 night | Setup: AgentFoundry, repo, Vercel, Neon. Printable intake sheet for tomorrow | Sheet printed or on phone |
| 2 | Thu 5 | **Home visit**: chairman questions, consent, interview residents on the sheet. Night: database + import from the sheet | Real answers saved in the PRIVATE database |
| 3 | Fri 6 | Interview mode (2) + cards (3). Demo deploy. **File Form 2** | Live link works on a phone |
| 4 | Sat 7 | Eligibility (5) + document gaps (6) + priority score (10) | Every card shows top scheme and blocker |
| 5 | Sun 8 | Timeline (4) + proof trail (7) + escalation (8) | Reminder appears after X days |
| 6 | Mon 9 | AI caseworker agent (1) | A note turns into a profile update + drafted letter |
| 7 | Tue 10 | Problem finder (9) + wellbeing (13) + medicines (11) | Home problem list shows real numbers |
| 8 | Wed 11 | Bookings (12) + fund cards (14) + Excel (15) + PIN lock for private pilot | Excel opens; real data only behind the lock |
| 9 | Thu 12 | Impact dashboard (15), test all 15 features, README | Every feature passes its check in TESTING.md |
| 10 | Fri 13 | Video 2 to 3 min, update Form 2 with numbers, submit | Submitted. 14 and 15 are buffer |

**Safety rule for the plan:** if Phase 5 is not done by Sun 8 night, features 12, 13, 14 move to "after the hackathon". Better 12 working than 15 broken.

## Truths about the visit tomorrow
- The app will not be ready by tomorrow. So tomorrow uses a sheet; the app imports it later.
- 15 questions take about 10 mins per resident (GUESS). Elders get tired. Do the money and documents modules first for everyone, the rest on later calls with staff.
- Consent first, for every resident.

## Your own tasks
- Logins: AgentFoundry, GitHub, Vercel, Neon.
- Tomorrow: chairman, consent, home's PIN and district, interviews.
- Calls: IPPB 155299, LVPEI 7032666437 (Miyapur inside 25 km?), HelpAge (check the number).
- Approve every file in AgentFoundry. Fill Form 2 on 6 Nov, edit on 12 Nov.
