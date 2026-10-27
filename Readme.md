# Snap2Solve

**Snap it. Report it. Fix it.**

Snap2Solve is an open-source tool that turns a photo of a civic problem into a ready-to-send complaint, then keeps pressure on until it is fixed. Built by Team Tech Astra for [Elite Coders CodeSprint 2026](https://unstop.com).

> **Status:** in development. The MVP is due on 15 November 2026. Items marked *(planned)* are not built yet.

## The problem

Reporting a garbage dump, pothole, broken streetlight or waterlogged road means finding the right department, finding its contact, and writing a formal complaint. Most people give up. Even when a complaint is filed, nobody follows up, and there is no public record of what was reported or fixed.

*Filing a complaint is easy. Getting it solved is hard. Snap2Solve fixes the second part.*

## Features

### MVP (target: 15 November 2026)
- **WhatsApp bot:** send a photo and your location to report an issue. A web app is available as a fallback.
- **AI issue detection:** a vision model classifies the issue (garbage, pothole, streetlight, waterlogging, and so on).
- **Complaint generator:** a formal complaint in Hindi or English with location, category and date.
- **Public map dashboard:** every report appears on an open map with category filters.
- **7-day auto-reminder:** if an issue is not marked fixed in 7 days, a reminder email goes to the authority.

### Roadmap *(planned)*
- **Auto-escalation chain:** JE, then ward officer, then commissioner, then an RTI draft.
- **Before/after verification:** when a fix is claimed, nearby users are asked to confirm with a photo.
- **Duplicate merging:** many reports of the same spot become one complaint with a "reported by N people" count.
- **Ward report card:** a public leaderboard of complaints solved per ward and how fast.
- **Hindi voice notes:** speak the complaint instead of typing it.
- **Municipal portal integration** and more regional languages.

## How it works

```
Photo + location (WhatsApp or web)
        |
        v
AI detects the issue type
        |
        v
Complaint drafted (Hindi / English)
        |
        v
Sent to the authority  ->  7-day clock starts
        |                         |
        v                         v
Appears on public map      Reminder email if not fixed
```

## Tech stack

| Part | Choice |
|---|---|
| Frontend | React / Next.js (mobile-first) |
| Backend | FastAPI (Python) or Node.js |
| AI | Vision-capable LLM API |
| Messaging | WhatsApp Cloud API (test number during development) |
| Maps | Leaflet + OpenStreetMap |
| Database | Supabase or SQLite |
| Reminders | Scheduler + SMTP email |
| Deployment | Vercel + Render / Railway |

*Update this table to match what the code actually uses.*

## Project structure

```
Snap2Solve_Codesprint/
├── frontend/          # web app and map dashboard
├── backend/           # API, complaint generation, reminder scheduler
├── bot/               # WhatsApp webhook handler
├── data/
│   └── cities/        # community-contributed city templates and contacts
├── docs/              # screenshots, architecture notes
├── .env.example       # required environment variables (no secrets)
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## Getting started

```bash
git clone https://github.com/pannapurna041-hash/Snap2Solve_Codesprint.git
cd Snap2Solve_Codesprint

# backend
cd backend
pip install -r requirements.txt
cp ../.env.example .env      # then fill in your keys
uvicorn main:app --reload

# frontend (in a new terminal)
cd frontend
npm install
npm run dev
```

*Adjust the commands once the code is in place.*

### Environment variables

| Variable | Purpose |
|---|---|
| `LLM_API_KEY` | vision and text model for categorisation and complaint drafting |
| `WHATSAPP_TOKEN` | WhatsApp Cloud API access token |
| `WHATSAPP_VERIFY_TOKEN` | webhook verification |
| `DATABASE_URL` | database connection |
| `SMTP_HOST`, `SMTP_USER`, `SMTP_PASS` | sending complaint and reminder emails |

Never commit real keys. Keep them in `.env`, which is listed in `.gitignore`.

## Adding your city

Snap2Solve is only as useful as its local data. To add a city, create a file in `data/cities/` and open a pull request:

```json
{
  "city": "Ghaziabad",
  "state": "Uttar Pradesh",
  "authorities": [
    {
      "category": "garbage",
      "department": "Municipal Corporation, Sanitation",
      "email": "example@example.gov.in",
      "escalation": ["Junior Engineer", "Ward Officer", "Commissioner"]
    }
  ]
}
```

Use only contact details that are publicly published by the authority, and include a source link in your pull request.

## Contributing

Contributions are welcome, especially city data, translations and bug fixes. See `CONTRIBUTING.md` for the workflow. Please open an issue before starting a large change.

## Privacy

Reports include a photo and location. Do not upload photos showing identifiable people, vehicle number plates or private property. We plan to blur faces and plates automatically *(planned)*.

## Team

**Tech Astra**, ABES Engineering College, Ghaziabad

- Anand Rai
- Aditya Kumar Khare
- Tejasvi Rana
- Annapurna

## Licence

Released under the [MIT Licence](LICENSE). *Replace with Apache-2.0 if you prefer, and keep the LICENSE file in sync.*