# Agentic Resume & Interview Prep Flow

A small weekend project where I use CrewAI flows and LLM agents to help me tailor my resume to a specific job posting and prep talking points for my first interview. Just me trying to speed up job applications and learn agents in the process.

I was manually reading job posts, matching them to my skills, editing my resume and then jotting quick interview talking points. This repo automates the boring parts:

- It extracts the real requirements from a job posting url.
- Maps them to my skills and experience.
- Proposes a resume strategy with special keywords.
- Generates an ATS‑friendly updated resume markdown.
- Produces talking points and 2–3 experience stories for the intro call.

I’m a data science student, so I designed it to be simple, reproducible and easy to swap LLM providers.

## What I did

**CrewAI Flow stages:**

1. **Learns job requirements** -> it parses a job description and normalizes my skills and responsibilities.
2. **Matches the job description to my profile** -> rate coverage, surface gaps and proposes changes.
3. **Resume strategy** -> section order, keywords and bullets to rewrite.
4. **Writes a tailored resume** -> ATS‑friendly Markdown output.
5. **Interview prep** -> concises talking points + STAR stories I can actually say during the interview. 

Outputs are returned as structured JSON + a Markdown resume body.

**Where to put your resume?**

The script extracts text from PDF/DOCX/TXT. If a PDF has columns, converting to `.docx` or copying into `.txt` to givee a cleaner text.

## How it works

* **CrewAI Flows** chain steps with state. Each step calls an **Agent** with a clear role:

  * *Job Researcher* -> extracts normalized requirements.
  * *Profile Analyst* -> matches and gap analysis.
  * *Resume Strategist* -> outline, keywords and targeted rewrites.
  * *Resume Writer* -> ATS‑friendly Markdown resume.
  * *Interview Coach* -> talking points + STAR cues.
* **LLM selection** is pluggable with LiteLLM; set `MODEL` and the right API key env var.

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

## Notes on ATS + tone

* The resume writer keeps formatting simple: section headers, bullets, and clean keyword placement. You can paste the Markdown into your own template.
* I keep bullets concrete: numbers, scope, stacks, and outcomes.
* Talking points read like how I’d speak in a 15‑minute screen.

--
