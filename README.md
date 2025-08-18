# Agentic Resume and Interview Prep Flow

> A small weekend project where I use CrewAI “flows” + LLM agents to help me tailor my resume to a specific job posting and prep talking points for the first interview. Not homework — just me trying to speed up job applications and learn agents in the process.

---

## Why I built this

I was manually: reading job posts, matching them to my skills, editing my resume, and then jotting quick interview talking points. Repeating that for every role is slow. This repo automates the boring parts:

* Extract the **real** requirements from a posting
* Map them to **my skills/experience**
* Propose a **resume strategy** (order, bullets, keywords)
* Generate an **ATS‑friendly resume draft** (Markdown)
* Produce **talking points + 2–3 STAR stories** for the intro call

I’m a data science student, so I designed it to be simple, reproducible, and easy to swap LLM providers.

---

## What it does (end‑to‑end flow)

**Flow stages** (CrewAI Flows):

1. **Learn job requirements** → parse a job description and normalize skills/responsibilities.
2. **Match to my profile** → rate coverage, surface gaps, propose quick wins.
3. **Resume strategy** → section order, keywords, bullets to rewrite.
4. **Write tailored resume** → ATS‑friendly Markdown output.
5. **Interview prep** → concise talking points + STAR stories I can actually say.

Outputs are returned as structured JSON + a Markdown resume body.

---

## Quickstart

```bash
# 1) Install
pip install "crewai>=0.103.0" crewai-tools litellm pydantic python-dotenv pypdf docx2txt

# 2) Choose an LLM (via LiteLLM routing)
export MODEL="gpt-4o-mini"      # or anthropic/claude-3-5-sonnet, gemini/gemini-1.5-pro, groq/llama3-70b-8192, etc.
export OPENAI_API_KEY=sk-...
# (use ANTHROPIC_API_KEY / GOOGLE_API_KEY / GROQ_API_KEY / etc. for other providers)

# 3) Run (resume from file + job posting from file or inline text)
python mckinsey_interview_flow.py \
  --resume ~/Documents/My_Resume.pdf \
  --job job_posting.txt
# or
python mckinsey_interview_flow.py \
  --resume ~/Documents/My_Resume.docx \
  --job-text "Paste the full job description here..."
```

**Where do I put my resume?**

* Easiest: just pass `--resume path/to/file.pdf|.docx|.txt`.
* The script extracts text from PDF/DOCX/TXT (uses `pypdf` and `docx2txt`). If a PDF has columns, converting to `.docx` or copying into `.txt` gives cleaner text.

**Save outputs to files**

* The script prints JSON + Markdown to stdout. I usually pipe the resume to a file:

  ```bash
  python mckinsey_interview_flow.py --resume My_Resume.pdf --job job.txt \
    > run_out.json
  # then copy the Markdown resume part into a file: resume_tailored.md
  ```

---

## Project structure

```
.
├── mckinsey_interview_flow.py   # the flow + agents + CLI
├── README.md                    # this file
└── requirements.txt             # optional; versions as above
```

---

## How it works (under the hood)

* **CrewAI Flows** chain steps with state. Each step calls an **Agent** with

