# recruiter-ops

> **AI-powered talent acquisition & screening system** built on Claude Code.
> Forked from [santifer/career-ops](https://github.com/santifer/career-ops) — reframed for the **Recruiter / Talent Acquisition** perspective.

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](VERSION)
[![Claude Code](https://img.shields.io/badge/built%20with-Claude%20Code-blueviolet)](https://claude.ai/code)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🎯 What Is This?

The original `career-ops` was designed to help **job seekers** automate their job search using AI. This fork **flips the perspective** — it's rebuilt for **Recruiters, HR Specialists, and Talent Acquisition professionals** who want to:

- Screen and evaluate candidate resumes at scale with AI
- Match JD requirements against candidate profiles automatically
- Generate structured interview question sets per role
- Track candidate pipeline status via a Go dashboard
- Batch-process candidate pools and produce sourcing reports
- Export candidate evaluation PDFs for hiring managers

---

## 🗂️ Repository Structure

```
recruiter-ops/
├── modes/               # 14 AI skill modes (recruiter-adapted)
│   ├── 01-jd-parser          # Parse JD into structured requirements
│   ├── 02-resume-screener    # Score resumes against JD criteria
│   ├── 03-interview-gen      # Generate behavioral & technical questions
│   ├── 04-culture-fit        # Culture alignment analysis
│   ├── 05-comp-benchmarker   # Salary & market benchmarking
│   ├── 06-sourcing-strategy  # Boolean search & sourcing plan
│   ├── 07-offer-letter       # Draft offer letter templates
│   ├── 08-rejection-writer   # Empathetic rejection messaging
│   ├── 09-diversity-audit    # DE&I language & pipeline audit
│   ├── 10-ref-check          # Reference check question generator
│   ├── 11-onboarding-brief   # Post-hire onboarding handoff brief
│   ├── 12-headcount-plan     # Headcount planning & workforce analysis
│   ├── 13-jd-writer          # JD writing from scratch or template
│   └── 14-pipeline-report    # Weekly pipeline status report
│
├── dashboard/           # Go-based hiring pipeline dashboard
├── batch/               # Batch candidate screening scripts
├── templates/           # JD templates, evaluation rubrics, email templates
├── jds/                 # Job description inputs (drop .txt or .md files here)
├── data/                # Candidate data & pipeline tracker (CSV/JSON)
├── output/              # Generated reports & evaluation PDFs
├── reports/             # Weekly summaries & sourcing reports
├── interview-prep/      # Interview kit generation output
├── docs/                # Documentation
│
├── CLAUDE.md            # Claude Code configuration & skill definitions
├── generate-pdf.mjs     # PDF export for candidate evaluations
├── batch-screen.mjs     # Batch resume screening runner
├── pipeline-sync.mjs    # Pipeline status sync & dedup
└── package.json
```

---

## 🔄 Perspective Flip: job-seeker → recruiter

| Original (career-ops) | This Fork (recruiter-ops) |
|---|---|
| Write tailored cover letters | Screen & score candidate cover letters |
| Optimize my resume for ATS | Evaluate candidate resumes vs. JD ATS criteria |
| Research company culture | Assess candidate culture alignment |
| Generate interview answers | Generate interview question banks |
| Track my application status | Track candidate pipeline stages |
| Salary negotiation tips | Comp benchmarking & offer calibration |
| Follow-up email templates | Rejection & offer communication templates |
| Interview prep coach | Structured interview kit generator |

---

## ⚡ Quick Start

### Prerequisites

- [Claude Code](https://claude.ai/code) — required for AI skill execution
- Node.js ≥ 18
- Go ≥ 1.21 (for the dashboard)

### Setup

```bash
git clone https://github.com/glen200392/career-ops.git recruiter-ops
cd recruiter-ops
npm install
```

### Run a Resume Screening

1. Drop a JD into `jds/` as `role-name.md`
2. Drop candidate resumes into `data/candidates/`
3. Run Claude Code with mode `02-resume-screener`:

```bash
# In Claude Code terminal
/mode 02-resume-screener
> Screen all candidates in data/candidates/ against jds/senior-engineer.md
```

4. Outputs saved to `output/screening-results-[date].json`
5. Generate PDF report:

```bash
node generate-pdf.mjs --input output/screening-results-today.json
```

### Launch the Pipeline Dashboard

```bash
cd dashboard
go run main.go
# Opens at http://localhost:8080
```

---

## 🧠 14 Skill Modes for Recruiters

All modes are invoked inside **Claude Code** using `/mode <name>`.

| # | Mode | Recruiter Use Case |
|---|---|---|
| 01 | `jd-parser` | Extract must-have skills, nice-to-haves, seniority level from any JD |
| 02 | `resume-screener` | Score & rank candidates vs. JD with justification |
| 03 | `interview-gen` | Build structured interview kits (behavioral + technical) |
| 04 | `culture-fit` | Assess cultural alignment from resume signals |
| 05 | `comp-benchmarker` | Pull market salary ranges, equity benchmarks |
| 06 | `sourcing-strategy` | Generate LinkedIn Boolean strings, target company lists |
| 07 | `offer-letter` | Draft localized, compliant offer letters |
| 08 | `rejection-writer` | Generate empathetic, brand-safe rejection emails |
| 09 | `diversity-audit` | Flag biased JD language, check pipeline diversity |
| 10 | `ref-check` | Generate role-specific reference check questions |
| 11 | `onboarding-brief` | Create hiring manager handoff brief post-offer |
| 12 | `headcount-plan` | Model headcount scenarios with skill gap analysis |
| 13 | `jd-writer` | Write JDs from scratch or improve existing ones |
| 14 | `pipeline-report` | Automate weekly pipeline summary with conversion metrics |

---

## 📊 Pipeline Dashboard

The Go dashboard provides a real-time view of your hiring pipeline:

- **Stages tracked**: Sourced → Screened → Interview → Offer → Hired / Rejected
- **Metrics**: Time-to-hire, stage conversion rates, offer acceptance rate
- **Filters**: By role, department, recruiter, date range
- **Export**: CSV export for ATS integration

---

## 📁 Working with JD Files

Drop any job description into `jds/` as plain text or Markdown. Example format:

```markdown
# Senior Software Engineer — Platform Team

## About the Role
...

## Requirements
- 5+ years backend development
- Strong TypeScript/Node.js
...

## Nice to Have
- Experience with Kubernetes
...
```

The `jd-parser` mode will extract structured criteria automatically.

---

## 🔧 Batch Processing

Screen an entire candidate pool in one command:

```bash
node batch-screen.mjs \
  --jd jds/product-manager.md \
  --candidates data/candidates/ \
  --output output/ \
  --top 10
```

Outputs a ranked shortlist with score breakdowns and AI reasoning.

---

## 🏗️ Adapting for Your Organization

1. **Edit `CLAUDE.md`** — customize skill definitions, scoring rubrics, company values
2. **Add JD templates** in `templates/` for your most common roles
3. **Configure pipeline stages** in `config/pipeline.json` to match your ATS
4. **Set evaluation weights** in `config/screening-weights.json` (skills, experience, culture)

---

## 🤝 HR Tech Stack Integration

This system is designed to complement (not replace) your ATS. Outputs are structured for easy import into:

- **Greenhouse** — JSON candidate exports
- **Workday** — CSV pipeline imports
- **Lever** — Structured feedback notes
- **Custom HRIS** — via standardized `DATA_CONTRACT.md` schema

See [`DATA_CONTRACT.md`](DATA_CONTRACT.md) for the candidate data schema.

---

## 📜 Original Project

This fork is based on **[santifer/career-ops](https://github.com/santifer/career-ops)** — an excellent AI-powered job search system. The core Claude Code architecture, dashboard, and PDF generation pipeline are preserved. All skill modes have been reframed from candidate to recruiter perspective.

---

## 🧑‍💼 Maintainer

**Tsung Lun Ho** | Digital Transformation Office, Tai Sheng Group

Focused on AI adoption in HR and Talent Acquisition workflows.

---

## License

[MIT](LICENSE) — see original project for attribution requirements.
