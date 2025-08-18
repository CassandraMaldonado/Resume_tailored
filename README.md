# Agentic Resume & Interview Prep Flow

A small weekend project where I use CrewAI flows and LLM agents to help me tailor my resume to a specific job posting and prep talking points for my first interview. Just me trying to speed up job applications and learn agents in the process.

I was manually: reading job posts, matching them to my skills, editing my resume and then jotting quick interview talking points. This repo automates the boring parts:

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

* **CrewAI Flows** chain steps with state. Each step calls an **Agent** with a clear role:

  * *Job Researcher* → extracts normalized requirements.
  * *Profile Analyst* → match & gap analysis.
  * *Resume Strategist* → outline, keywords, and targeted rewrites.
  * *Resume Writer* → ATS‑friendly Markdown resume.
  * *Interview Coach* → talking points + STAR cues.
* **Structured outputs** via Pydantic models so results are predictable.
* **LLM selection** is pluggable with LiteLLM; set `MODEL` and the right API key env var.

---

## Inputs & Outputs

**Inputs**

* `--resume` path to PDF/DOCX/TXT (required)
* One of: `--job path/to/txt` or `--job-text "...full JD..."`

**Outputs (JSON keys)**

* `requirements`: normalized skills/responsibilities/keywords
* `match_report`: coverage scores, gaps, suggested positioning
* `resume_outline`: section order, keywords, bullets to rewrite
* `resume_markdown`: ATS-oriented resume in Markdown
* `talking_points`: 4–8 bullets for recruiter screen + 2–3 STAR stories

---

## Swap LLMs quickly

```bash
export MODEL="anthropic/claude-3-5-sonnet-20240620"
export ANTHROPIC_API_KEY=...
python mckinsey_interview_flow.py --resume ... --job ...
```

Other examples: `gemini/gemini-1.5-pro`, `groq/llama3-70b-8192`, `ollama/llama3` (if running locally). Temperature is set low for extraction steps and slightly higher for writing.

---

## Notes on ATS + tone

* The resume writer keeps formatting simple: section headers, bullets, and clean keyword placement. You can paste the Markdown into your own template.
* I keep bullets concrete: numbers, scope, stacks, and outcomes.
* Talking points read like how I’d speak in a 15‑minute screen.

---

## Roadmap (things I might add later)

* Cover letter auto‑draft from the same outline
* A small STAR story library I can reuse
* LinkedIn scraping tool (for company/team context)
* Metric verifier (light heuristics to sanity check numbers)
* Export to PDF/Docx automatically

---

## FAQ

**Is this only for McKinsey?**  No — works for any posting. I just used a consulting‑style prompt style because it forces clear requirements → evidence mapping.

**Does it replace editing?**  No. It drafts fast; I still do a 5‑minute polish.

**Private data?**  Your resume text is processed by whichever model you configure. For sensitive content, use a local model or a provider/company you trust.

---

## Disclaimer

Not affiliated with McKinsey. This is a personal project to practice agentic workflows and speed up my own applications.

---

## License

MIT — feel free to fork/use.
