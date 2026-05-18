# AgentAI888 — Affiliate Platform & Revvy Revenue Agent

The complete AgentAI888 affiliate ecosystem by **The Alleges Group Inc.** — a
marketing landing page, a full affiliate dashboard, and **Revvy**, an AI Revenue
Agent that helps each affiliate prospect, pitch, and close.

---

## What's in this repo

```
agentai888-repo/
├── frontend/
│   ├── index.html                  Marketing landing page
│   ├── dashboard.html               Affiliate dashboard + Revvy
│   └── agentai888-complete.html     Both pages merged into one file
└── backend/
    ├── main.py                      FastAPI service (Revvy's backend)
    ├── requirements.txt             Python dependencies
    ├── schema.sql                   Supabase database tables
    ├── .env.example                 Environment variable template
    └── README.md                    Backend-specific setup guide
```

---

## The two pieces

### 1. Frontend — three self-contained HTML files

Each file is a complete app: HTML, CSS, and JavaScript in one file, no build step.

| File | What it is |
|------|-----------|
| `index.html` | Public marketing/landing page that recruits affiliates |
| `dashboard.html` | The affiliate portal — login, AI agent marketplace, commissions, team, AI Promo Studio, and the **Revvy Revenue Agent** |
| `agentai888-complete.html` | Landing page + dashboard combined into a single file (uses an internal iframe to switch views) |

**You deploy one of two ways — pick one:**

- **Two-file:** deploy `index.html` and `dashboard.html` together in the same
  folder. `index.html` is the homepage; its buttons link to `dashboard.html`.
- **Single-file:** deploy only `agentai888-complete.html` (rename it
  `index.html`). Everything is in one file — nothing else to upload.

> Note on the single file: it switches between landing and dashboard internally.
> Open it from a real host or by double-clicking the downloaded file — some
> sandboxed in-app previews block its internal navigation.

### 2. Backend — the Revvy Revenue Agent service

A FastAPI service that gives Revvy live capabilities. **The dashboard works
without it** (Revvy runs in demo mode); the backend turns on the real features:

- **AI proxy** — Revvy's chat, Blueprint, and prospectus generation, with the
  Anthropic API key kept server-side (never exposed to the browser).
- **Lead storage** — every Leak & Fix Blueprint auto-saves the prospect as a lead.
- **Prospectus storage** — generated prospectuses save to the affiliate's account.
- **Twilio voice + SMS** — Revvy can call or text a prospect from your number.

Full backend setup is in [`backend/README.md`](backend/README.md).

---

## Quick start

### Run the frontend
No build needed. Either:
- Double-click `frontend/index.html`, **or**
- Serve the `frontend/` folder with any static host.

The dashboard runs in **Demo Mode** out of the box — no configuration required.

### Run the backend (optional, for live Revvy)
```bash
cd backend
pip install -r requirements.txt
cp .env.example .env        # fill in real values
uvicorn main:app --reload --port 8000
```
Then open the dashboard, click **⚙ Setup**, and paste your backend URL into the
**Revvy Backend** field.

---

## Deployment

### Frontend → Netlify (or any static host)
1. Choose your approach (two-file or single-file, see above).
2. Drag the file(s) onto [Netlify Drop](https://app.netlify.com/drop).
3. Make sure your homepage file is named `index.html`.

### Backend → Railway / Render / Fly.io
1. Push this repo to GitHub.
2. Create a new project from the repo, root directory `backend/`.
3. Start command: `uvicorn main:app --host 0.0.0.0 --port $PORT`
4. Add the environment variables from `backend/.env.example`.

See [`backend/README.md`](backend/README.md) for the full walkthrough, including
Supabase and Twilio setup.

---

## Configuration

All configuration is done through the dashboard's **⚙ Setup** panel — no code
edits needed:

| Field | Purpose |
|-------|---------|
| Supabase URL + anon key | Affiliate accounts, commissions, team data |
| Anthropic API key | Direct AI fallback (optional if backend is used) |
| Revvy Backend URL | Powers live Revvy — AI, lead/prospectus saving, Twilio |

Leave fields blank to run in Demo Mode.

---

## Tech stack

- **Frontend:** single-file HTML + CSS + vanilla JavaScript; Supabase JS client;
  Chart.js; dark enterprise design system
- **Backend:** Python · FastAPI · httpx · Uvicorn
- **Data:** Supabase (PostgreSQL)
- **Integrations:** Anthropic API, Twilio (voice + SMS)

---

## Security notes

- API keys and tokens belong on the **backend** (environment variables), never
  committed to the repo. `.env` is gitignored; only `.env.example` is tracked.
- In production, set the backend's `ALLOWED_ORIGINS` to your real domain instead
  of `*`.
- For outbound calling/texting at scale, follow Twilio's compliance rules
  (consent, calling hours, opt-out handling).

---

## License

Proprietary — © The Alleges Group Inc. All rights reserved.

## Credits

Built for **AgentAI888** by **The Alleges Group Inc.**, Houston, TX.
