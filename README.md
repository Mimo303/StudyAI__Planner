<div align="center">

```
 ⬡  StudyAI
```

# BCA Smart Study Planner

**AI-powered exam preparation for BCA students.**  
Enter your subjects. Get a complete, prioritised, day-by-day study plan — in under a minute.

<br/>

![HTML](https://img.shields.io/badge/HTML-Single%20File-f0c040?style=flat-square&logo=html5&logoColor=black)
![AI](https://img.shields.io/badge/AI-LLaMA%203.3%2070B-34d4ae?style=flat-square)
![Groq](https://img.shields.io/badge/API-Groq%20%28Free%29-ffffff?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-f0c040?style=flat-square)

</div>

---

## What it does

Most students stare at a list of 6 subjects two weeks before exams and have no idea where to start.

StudyAI solves that. You tell it your subjects, exam dates, and how hard each one feels to you. It calculates a **priority score** for every subject using gap days and difficulty, then calls a real AI model to generate a complete preparation plan — strategies, daily hours, and a day-by-day schedule all the way to your last exam.

No guesswork. No overwhelm. Just open the file and follow the plan.

---

## How it works

There are two layers of intelligence working together.

**Layer 1 — Your own priority algorithm**

Before any AI is called, a mathematical formula ranks your subjects:

```
priority = difficulty_weight ÷ gap_days

Hard = 3   Medium = 2   Easy = 1
```

A Hard subject with 7 days left scores `3 ÷ 7 = 0.43`.  
An Easy subject with 20 days left scores `1 ÷ 20 = 0.05`.  
The Hard one goes to the top. Every time. No bias.

Gap days are calculated smartly — not just "days from today" but the actual window between consecutive exams. So if your first exam is in 10 days and your second is 2 days after that, the second subject only gets 2 days of gap, not 12.

**Layer 2 — Groq API (LLaMA 3.3 70B)**

Once the priorities are computed, a structured prompt is sent to Groq's API. The model receives all your subject data, scores, and rankings — and returns:

- Subject-specific study strategies
- Realistic daily hour recommendations  
- A complete day-by-day schedule until your last exam
- Revision tips and motivational advice
- Which subject to start first and which can wait

The response comes back as clean JSON and is rendered instantly across 5 screens.

---

## The 5-screen flow

```
[ Add Subjects ] → [ Set Difficulty ] → [ AI Analysis ] → [ Smart Summary ] → [ Day Schedule ]
       ↓                   ↓                   ↓                  ↓                  ↓
  Name + date        Easy/Medium/Hard     Priority calc       Priority cards      Full calendar
  per subject        per subject          + Groq API call     Strategies/Tips     Day by day plan
```

---

## Features

- **Priority ranking** — mathematical score tells you exactly what to study first
- **AI study strategies** — personalised 2–3 sentence advice per subject
- **Day-wise schedule** — every day covered from today to your last exam
- **Plan history** — all plans auto-saved to localStorage, accessible anytime via "My Plans"
- **PDF download** — clean printable report with full plan
- **Text download** — plain `.txt` file of your entire schedule
- **API key memory** — enter once, remembered forever (or embed it for others)
- **Zero install** — one `.html` file, opens in any browser

---

## Getting started

### Step 1 — Get a free Groq API key

Go to [console.groq.com](https://console.groq.com) → Sign up (free, no card) → API Keys → Create Key

Your key looks like: `gsk_xxxxxxxxxxxxxxxxxxxxxxxxxxxx`

### Step 2 — Open the file correctly

> ⚠️ **Do not double-click the file.** Browsers block API calls from `file://` URLs.  
> You need to serve it over `http://` — here are two ways:

**Option A — VS Code Live Server** *(recommended)*
1. Install the **Live Server** extension in VS Code (by Ritwick Dey)
2. Right-click `StudyAI_v3_Final.html` → **Open with Live Server**
3. Browser opens at `http://127.0.0.1:5500` ✓

**Option B — Python**
```bash
python -m http.server 8000
# then open: http://localhost:8000/StudyAI_v3_Final.html
```

### Step 3 — Use the app

1. Paste your Groq API key in the bar at the top (saved automatically after first entry)
2. Add your subjects and exam dates on Screen 1
3. Rate each subject Easy / Medium / Hard on Screen 2
4. Hit Continue — the AI analyses everything and builds your plan
5. View priority summary on Screen 4 and full day schedule on Screen 5
6. Download as PDF or Text, or come back later via **My Plans**

---

## Sharing with others

If you want to share the file so others can use it **without needing their own API key**, open the HTML file and find this line near the top of the `<script>` section:

```js
const EMBEDDED_KEY = '';
```

Paste your key:

```js
const EMBEDDED_KEY = 'gsk_your_key_here';
```

Save and share that file. Anyone who opens it gets full access — no key required on their end. The API key bar disappears and a green confirmation banner appears instead.

---

## Tech stack

| Layer | What |
|---|---|
| UI | HTML5 + CSS3 (single file, no framework) |
| Logic | Vanilla JavaScript — priority algorithm + rendering |
| AI model | LLaMA 3.3 70B via Groq API |
| Storage | Browser localStorage — plans + API key |
| Fonts | Syne (display) + DM Sans (body) via Google Fonts |

---

## Project structure

```
StudyAI_v3_Final.html   ← entire app in one file
│
├── <style>             CSS — dark gold theme, animations, 5-screen layout
├── HTML screens        Screen 1–5 + history panel + modals
└── <script>
    ├── Key management  Embedded key or localStorage fallback
    ├── Priority algo   Sort → gap calc → weight → score → rank
    ├── Groq API call   fetch() to api.groq.com with structured prompt
    ├── Renderers       buildSummary(), buildSchedule()
    ├── History         savePlan(), loadPlan(), deletePlan() via localStorage
    └── Downloads       downloadPDF() — print dialog  |  downloadText() — .txt blob
```

---

## The priority formula explained

```
Subject A:  Hard (3)   ÷  8 days gap  =  0.375   ← study this FIRST
Subject B:  Medium (2) ÷  6 days gap  =  0.333
Subject C:  Easy (1)   ÷  7 days gap  =  0.143   ← this can wait
```

The formula naturally surfaces what matters most. A hard subject with a short window always outranks an easy subject with lots of time. Difficulty alone doesn't win — it has to be weighed against how much time you actually have before that exam.

---

## Common issues

| Problem | Cause | Fix |
|---|---|---|
| `NetworkError when fetching` | Opened via `file://` | Use Live Server or Python server |
| API key not working | Wrong key or expired | Re-generate at console.groq.com |
| Plan won't generate | Missing subject name or past date | Fill all fields with future dates |
| Model error | Model name changed | Check Groq docs for current model ID |

---

## Built for

BCA students across India preparing for semester exams. Works equally well for any student with multiple subjects and fixed exam dates.

---

<div align="center">

Made with focus. Powered by [Groq](https://groq.com) · [LLaMA 3.3](https://ai.meta.com/llama/)

</div>
