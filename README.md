# Career Navigator

An interactive careers explorer for the UK. It helps someone work out which careers fit them, understand what each one is actually like, see the exact route in, and (if they upload a CV) find the smartest move from where they are now.

It is built as a single self-contained HTML file. No server, no build step, no accounts. Open it in a browser and it runs.

> **Status: working prototype.** The product is functional end to end, but the data underneath it needs sourcing and citing before it should be treated as authoritative. See "Honesty and data provenance" below, and `ROADMAP.md`.

## What it does

The app has four tabs.

### 1. Find your match
- A 22-question questionnaire on a 0 to 5 agree/disagree scale. Every question is skippable, and blanks simply do not count.
- It reads two things at once: what you want from work (pay, security, work-life balance and so on) and how you are wired (the six RIASEC work-style dimensions used in vocational psychology).
- An optional MBTI type adds a personality-compatibility layer.
- You can skip the quiz and set priorities manually with sliders or one-tap persona presets instead.
- It ranks all 120 careers, shows why each one fits, and flags anything you rated important that it is weak on. Every result links straight to its full report.

### 2. Career report
For any career:
- Money shape: gross and take-home pay (through a UK 2026/27 income tax and National Insurance engine) and the shape of the earnings curve.
- A seven-axis profile radar and a salary sparkline.
- Strengths, weak spots, a "best if", and a verdict.
- Who it suits: a work-style profile, a derived MBTI-leaning type, and a compatibility score once you have set your type.
- A career progression slider: drag through five stages (entry to peak) to see earnings, lifestyle and typical role at each.
- The route in: numbered steps with indicative difficulty and cost per stage, plus alternative entry routes.
- A viability read tailored to your profile once you have taken the questionnaire.
- Links to UK sources (National Careers Service, Prospects) to read more.

### 3. Overlay and compare
- Select any set of careers and overlay their profiles on one radar, chart their salary curves together (gross or take-home), and read a side-by-side stats table. A filter box finds careers fast.

### 4. CV and pivot
- Paste your CV or upload a `.pdf`, `.docx` or `.txt`. Files are parsed in your browser; only the parser library is fetched from a CDN, never your CV.
- Scores CV quality on a transparent rubric, and detects your skills, education, experience and certifications.
- Rates your fit against any target career and gives an upskilling plan for the gaps.
- A pivot engine ranks the whole library two ways: where you would slot in now (the smallest jump) and what is worth a retrain (the best fit with what you want), each tagged short hop, moderate reskill or full retrain.
- All of this is fused with your questionnaire results once you have taken it.

## Honesty and data provenance

This is the load-bearing part of the project, and it is deliberately visible in the app under "About these numbers".

Two tiers of trust:
- The salary figures and the take-home tax engine are anchored in UK market and HMRC data. The tax engine is verified against gov.uk for England, 2026/27.
- The seven axis scores, and therefore every match and verdict, are structured judgement, not measured data. The future-proofing axis is a forecast about automation, not an observation.

Stated plainly, so the app never over-claims:
- Most of the 120 salary figures are currently triangulated estimates, not yet sourced from ONS. Fixing this is the first roadmap priority.
- The route maps are indicative of the typical path and vary by employer and by nation of the UK. Always check the relevant professional body before committing.
- MBTI is included because it is popular and engaging, but it is psychometrically weak. It is caveated in the app and paired with the RIASEC model, which is the actual standard.
- The CV analyser is a heuristic that reads keywords and structure, not meaning. It is a rough compass, not a recruiter.
- The external links are auto-generated UK searches, not curated per career yet.

## Running it

Open `career-navigator.html` in any modern browser. That is the whole thing.

To put it online, drag the file into Netlify, Vercel or Cloudflare Pages, or serve it from any static host.

CV file parsing (PDF and Word) needs an internet connection the first time, because it loads `pdf.js` and `mammoth.js` from a CDN. The `.txt` paste path works fully offline.

## Tech

- A single HTML file: HTML, CSS and vanilla JavaScript, no framework.
- Charts are hand-drawn inline SVG, with no chart library.
- Fonts: Saira Condensed, IBM Plex Sans and IBM Plex Mono (Google Fonts).
- CV parsing: `pdf.js` and `mammoth.js`, loaded on demand from cdnjs.
- No backend, no database, no accounts, no browser storage. All state lives in memory for the session.

## Data model

Each career record holds:
- `id`, `name`, `col` (colour)
- `ax`: seven axis scores from 0 to 10 (pay, future, secure, entry, speed, life, option)
- `sal`: a five-stage salary in thousands of pounds (entry, early, mid, senior, peak)
- `blurb`: a one-line summary
- `route`: summary, time, cost, three steps, and alternative routes

Two companion maps key off the same id:
- `W`: a six-value RIASEC work-style code, which drives the psychological profile, the MBTI derivation and work-style matching
- `TAGS`: skill domains, which drive CV-to-career matching

Everything else (psychological profiles, MBTI compatibility, viability, stage difficulty, links, the progression model) is derived from these. Adding a career is therefore a data task, not a code task, which is what lets the library scale.

## Known limitations

- Salary and axis data need independent sourcing and citation (see the roadmap).
- The model has not been validated against real career-satisfaction outcomes.
- Accessibility is limited: the SVG-heavy interface likely fails screen readers today.
- Legacy binary `.doc` files cannot be parsed in-browser. Save as `.docx` or PDF.
- No persistence: refreshing loses your results.

## Repository files

- `career-navigator.html` - the application
- `CLAUDE.md` - a working brief for continuing the project in Claude Code
- `README.md` - this file
- `ROADMAP.md` - the plan to take it from prototype to product

## Licence

To be decided.
