# 🎯 TalentLens v3 — AI Hiring Suite

> **Score resumes. Rank candidates. Conduct AI-powered speech interviews. Generate recruiter-grade reports.**  
> All in one unified Streamlit application powered by Groq's LLaMA 3.3 70B.

---

## ✨ What Is TalentLens?

TalentLens v3 is an end-to-end AI hiring assistant built for recruiters and hiring managers. It eliminates manual resume screening and generic interview processes by combining:

- **Intelligent resume parsing** — extracts skills, projects, internships, education automatically
- **JD-based candidate scoring** — ranks candidates with customizable scoring weights
- **Speech-primary AI interview** — asks questions aloud, captures your spoken answers live, 60-second timer per question
- **Recruiter-grade evaluation reports** — STAR method detection, green/red flags, hire confidence %, per-question breakdowns

---

## 🖥️ Screenshots

| Score & Compare | Interview Report |
|---|---|
| Radar charts per candidate, ranked leaderboard | Overall score, skill bars, green/red flags, per-question analysis |

---

## 🔄 End-to-End Workflow

```
Tab 1: Define Role          →  Generate or paste a Job Description
                                  ↓ Tech stack auto-extracted from JD
Tab 2: Upload Resumes       →  Upload PDF/DOCX resumes (bulk supported)
                                  ↓ AI parses all resumes simultaneously
Tab 3: Score & Compare      →  AI scores and ranks all candidates
                                  ↓ Top candidate auto-loaded for interview
Tab 4: AI Interview         →  Speech-primary interview (60s per question)
                                  ↓ 7 personalized questions generated from JD + resume
Tab 5: Interview Report     →  Recruiter-grade report with hire recommendation
Tab 6: Final Report         →  Comparison matrix + downloadable hiring report
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9 or higher
- A free **Groq API key** from [console.groq.com](https://console.groq.com)
- A modern browser with microphone and camera access (for AI Interview)

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/talentlens-v3.git
cd talentlens-v3
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set Your API Key

Open `streamlit_app.py` and replace the placeholder on line ~27:

```python
GROQ_API_KEY = "your_groq_api_key_here"   # ← Replace with your actual key
```

> ⚠️ **Security Note:** The API key is stored only in the backend Python file and is never exposed in the UI. For production deployments, use environment variables or Streamlit secrets instead (see [Deployment](#-deployment) section below).

### 4. Run the App

```bash
streamlit run streamlit_app.py
```

The app opens at `http://localhost:8501` by default.

---

## 📦 Requirements

```
streamlit>=1.35.0
groq
pypdf
python-docx
numpy
plotly
```

Install all at once:

```bash
pip install streamlit groq pypdf python-docx numpy plotly
```

---

## 🗂️ Tab-by-Tab Guide

### 📋 Tab 1 — Job Description

**Two ways to get a JD:**

**Option A — AI Generate:**
1. Type a one-line role description (e.g. *"Python developer, 2+ years, FastAPI, AWS"*)
2. Click **⚡ Generate Job Description**
3. AI writes a full professional JD and **auto-extracts the tech stack** from it

**Option B — Paste Your Own:**
1. Paste an existing JD into the text box
2. Click **Use This JD**
3. Click **🔍 Extract Tech Stack from JD** to auto-detect technologies

The extracted tech stack is shown as tags and is automatically passed to the AI Interview generator.

---

### 📂 Tab 2 — Upload Resumes

1. Drag and drop one or more **PDF or DOCX** resume files
2. Click **🤖 Parse All Resumes with AI**
3. Each resume is parsed for: name, email, phone, experience, skills, technologies, education, certifications, internships, and projects
4. View parsed profiles in expandable cards

> **Tip:** Always complete Tab 1 before parsing resumes so the JD context is available.

---

### 🏆 Tab 3 — Score & Compare

**Scoring Weights** (set in the sidebar, must total 100%):

| Dimension | Default | Range |
|---|---|---|
| Skills | 30% | 10–60% |
| Experience | 30% | 10–60% |
| Education | 20% | 5–40% |
| Culture Fit | 20% | 5–40% |

1. Adjust weights in the sidebar to match your hiring priorities
2. Click **⚡ Score All Candidates**
3. View **radar charts** per candidate and a **ranked leaderboard**
4. Expand any candidate for a full score breakdown, strengths, gaps, and verdict

The **#1 ranked candidate is automatically pre-loaded** into the AI Interview tab — no re-upload needed.

---

### 🎤 Tab 4 — AI Interview

**How the interview works:**

1. The top-scored candidate's resume is auto-loaded (or upload a different one)
2. Click **🎤 Start AI Interview**
3. AI generates **7 personalized questions** based on the resume + JD:
   - 2 × Project questions (from the candidate's own projects)
   - 2 × Technical questions (from the JD's tech stack)
   - 2 × Behavioral STAR-format questions
   - 1 × Career/Resume question
4. Each question is **read aloud** by the AI automatically
5. Your **spoken answer is captured live** as a transcript
6. A **60-second countdown timer** per question — auto-submits when it hits zero
7. You can optionally click **✏️ Edit Answer** to correct your spoken response
8. Click **✓ Submit & Next Question** to proceed, or **Skip →** to skip

**Browser Requirements for Interview:**
- Microphone access (required for speech capture)
- Camera access (optional — mic-only mode available if camera is blocked)
- Speech Recognition API support (Chrome/Edge recommended; Firefox may have limited support)

---

### 📊 Tab 5 — Interview Report

Generated automatically after all 7 questions are answered. The report includes:

| Section | Details |
|---|---|
| **Header** | Candidate name, date, hire recommendation |
| **Key Metrics** | Overall score /100, Hire confidence %, Communication /100, Technical /100 |
| **Skill Scores** | Communication, Technical, Confidence, Clarity — each with progress bar |
| **Executive Summary** | AI-written paragraph summarizing the candidate's performance |
| **Green Flags** | Positive signals detected in answers |
| **Red Flags** | Concerns or gaps identified |
| **Per-Question Analysis** | Score, depth (shallow/adequate/strong), specificity, STAR detection, feedback |
| **Final Verdict** | Recommendation + confidence percentage |

**Score Integrity Rules:**
- Questions with no answer, skipped responses, or answers under 5 words are **hard-scored at 0**
- Top-level scores are scaled proportionally to how many questions were actually answered
- The AI **cannot infer scores from the resume** — only actual spoken/typed answers count

Download the report as a **JSON file** for records or further processing.

---

### 📑 Tab 6 — Final Report

A summary dashboard across all scored candidates:

- **Metrics row:** Total evaluated, Recommended count, Consider count, Not Recommended, Average score, Top pick name
- **Comparison matrix:** Side-by-side score breakdown for all candidates (Overall, Skills, Experience, Education, Culture Fit, Projects, Internships, Verdict)
- **Downloadable .txt report:** Full text summary of all candidate rankings, strengths, gaps, and verdicts

---

## ⚙️ Configuration

### Sidebar Controls

| Control | Description |
|---|---|
| **AI Connected** | Shows connection status (green = OK) |
| **Scoring Weights** | Adjust Skills / Experience / Education / Culture Fit percentages |
| **Session Stats** | Live count of parsed and scored resumes |
| **Candidates List** | Names of all uploaded candidates |
| **🗑️ Reset Everything** | Clears all session data and starts fresh |

### Scoring Weight Rules
- All four weights must add up to **exactly 100%**
- The sidebar shows a warning if the total is off
- Scoring is disabled until weights are valid

---

## 🔐 Security & Deployment

### Local Development
The API key is hardcoded in `streamlit_app.py`. This is fine for local use but **do not push the key to a public repository.**

Add `streamlit_app.py` to `.gitignore` or use the approach below for any shared/deployed environment.

### Production — Use Streamlit Secrets

1. Create `.streamlit/secrets.toml`:
```toml
GROQ_API_KEY = "gsk_your_actual_key_here"
```

2. Update `streamlit_app.py`:
```python
GROQ_API_KEY = st.secrets["GROQ_API_KEY"]
```

3. On Streamlit Community Cloud, add the secret via the dashboard under **App Settings → Secrets**.

### Production — Use Environment Variables

```bash
export GROQ_API_KEY="gsk_your_actual_key_here"
```

```python
import os
GROQ_API_KEY = os.environ.get("GROQ_API_KEY", "")
```

---

## 🧠 AI Model Details

| Component | Model | Provider |
|---|---|---|
| JD Generation | LLaMA 3.3 70B Versatile | Groq |
| Tech Stack Extraction | LLaMA 3.3 70B Versatile | Groq |
| Resume Parsing | LLaMA 3.3 70B Versatile | Groq |
| Candidate Scoring | LLaMA 3.3 70B Versatile | Groq |
| Interview Question Generation | LLaMA 3.3 70B Versatile | Groq |
| Interview Evaluation Report | LLaMA 3.3 70B Versatile | Groq |
| Speech Recognition | Web Speech API | Browser-native |
| Text-to-Speech (question reading) | Web Speech API | Browser-native |

Groq's free tier provides generous rate limits. If you hit a rate limit (`429`), the app automatically waits and retries up to 3 times.

---

## 📁 Project Structure

```
talentlens-v3/
│
├── streamlit_app.py          # Main application (all-in-one)
├── requirements.txt          # Python dependencies
├── README.md                 # This file
│
└── .streamlit/
    └── secrets.toml          # (Optional) API key for deployment
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend Framework | Streamlit |
| AI / LLM | Groq API — LLaMA 3.3 70B |
| Speech Recognition | Web Speech API (browser-native) |
| Text-to-Speech | Web Speech Synthesis API |
| Charts | Plotly (radar charts) |
| PDF Parsing | pypdf |
| DOCX Parsing | python-docx |
| Data | NumPy |
| Styling | Custom CSS (Sora + JetBrains Mono fonts) |

---

## ❓ Troubleshooting

| Problem | Solution |
|---|---|
| ❌ AI not connected | Check that `GROQ_API_KEY` is correct and your Groq account is active |
| Speech not captured | Allow microphone access in your browser; use Chrome or Edge for best compatibility |
| Questions score 0 even with answers | Make sure you submit before the 60s timer expires, or use Edit Answer to type your response |
| Resume parsing shows empty fields | Ensure the PDF is text-based (not a scanned image); try converting to DOCX |
| Rate limit errors | Groq free tier has per-minute limits; the app auto-retries; wait a moment between bulk operations |
| Camera blocked warning | Camera is optional; mic-only mode works fine for the interview |

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 👤 Author

Built with ❤️ using Streamlit + Groq.  
For questions or feedback, open a GitHub issue.

---

*TalentLens v3 · AI Hiring Suite · Resume Evaluator + Speech Interview · Groq LLaMA 3.3*