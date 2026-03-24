# RecruitIQ — Smart Resume Screening System

An AI-powered resume screening and candidate ranking tool built with vanilla HTML/CSS/JS and the Claude API.

---

## Features

- **Job Description input** — paste any JD to define the role requirements
- **Multi-candidate resumes** — tabbed interface to manage multiple candidates
- **File upload** — load resumes from `.txt` or text-based `.pdf` files
- **Claude AI analysis** — each resume is scored against the JD using NLP
- **Ranked results** — candidates sorted by match score with expandable cards
- **Per-candidate breakdown:**
  - Match score (0–100) and tier (Excellent / Strong / Moderate / Weak)
  - ✅ Matched skills, ❌ Missing skills, ➕ Additional skills
  - 💪 Key strengths and ⚠️ Concerns
  - 📝 AI narrative assessment

---

## Project Structure

```
recruitiq/
├── index.html          # Main HTML entry point
├── css/
│   └── style.css       # All styles (dark industrial theme)
├── js/
│   ├── data.js         # Demo job description and candidate resumes
│   ├── api.js          # Claude API integration
│   ├── ui.js           # DOM rendering and UI helpers
│   └── app.js          # App state, tab management, main flow
└── README.md
```

---

## Setup & Usage

### 1. Open in a browser
This is a pure frontend project — just open `index.html` in any modern browser. No build step required.

> **Note:** Due to browser CORS policies, when opened as a local `file://` URL, the Anthropic API calls will be blocked. Use one of the options below to run it properly.

### 2. Run with a local HTTP server

**Using Python:**
```bash
cd recruitiq
python3 -m http.server 8080
# Then open http://localhost:8080
```

**Using Node.js (npx):**
```bash
cd recruitiq
npx serve .
# Then open http://localhost:3000
```

**Using VS Code:**
Install the "Live Server" extension, right-click `index.html` → "Open with Live Server".

---

## API Key

This project uses the Anthropic API via the Claude claude.ai proxy — **no API key configuration is needed** when running inside Claude.ai artifacts.

If deploying independently, you would need to add your API key to the request headers in `js/api.js`:

```js
headers: {
  "Content-Type": "application/json",
  "x-api-key": "YOUR_API_KEY_HERE",
  "anthropic-version": "2023-06-01"
}
```

> ⚠️ Never expose API keys in client-side code in production. Use a backend proxy instead.

---

## Tech Stack

| Layer     | Technology                        |
|-----------|-----------------------------------|
| Frontend  | Vanilla HTML5, CSS3, JavaScript   |
| Fonts     | Syne (display), Space Mono (body) |
| AI Model  | Claude Sonnet 4 (Anthropic API)   |
| NLP       | Handled by Claude (prompt-based)  |
| Hosting   | Any static file server            |

---

## How the AI Scoring Works

Each resume is sent to Claude along with the job description in a structured prompt. Claude returns a JSON object containing:

- `score` — integer 0–100 representing overall fit
- `tier` — categorical rating (Excellent / Strong / Moderate / Weak)
- `matchedSkills` — skills in the resume that match the JD
- `missingSkills` — skills required by JD but absent from resume
- `otherSkills` — additional skills not mentioned in JD
- `strengths` — candidate's key advantages for the role
- `concerns` — potential gaps or red flags
- `summary` — narrative 2–3 sentence assessment

---

## Extending the Project

Ideas for further development:

- **Backend (Flask/Django):** Add a Python backend to handle PDF parsing via `pdfplumber` or `PyMuPDF`
- **Database:** Store past screenings in PostgreSQL or SQLite
- **Export:** Add CSV/PDF export of candidate rankings
- **Batch upload:** Support bulk resume uploads via ZIP
- **Authentication:** Add login to save and manage job postings
- **React rewrite:** Migrate to React + TypeScript for larger teams

---

## License

MIT — free to use and modify.
