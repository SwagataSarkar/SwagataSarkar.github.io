# job-fit-check

A [Claude Skill](https://www.anthropic.com/news/skills) that evaluates a resume against a
specific job posting the way a rigorous ATS + human recruiter screen actually would —
then helps close the gaps it finds, instead of just reporting them.

## Why

Most "check my resume against this job" tools do one of two things: a shallow keyword
count, or a vague "you seem like a great fit!" pep talk. Neither is very useful, and
neither addresses the thing that actually decides whether a resume gets a callback: **the
resume itself**, not the cover letter. Cover letters get skimmed for a few seconds if
they're opened at all — the resume is what gets parsed and ranked.

This skill is built around that reality:

- **Score the substance, not the title.** Two roles titled "Senior Product Manager" can be
  completely different jobs. The skill reads the actual responsibilities and required
  experience in the posting, not just the label on it.
- **Check whether the file will even survive parsing.** A resume can be a perfect content
  match and still get auto-rejected because it's built as a two-column table an ATS reads
  out of order. This skill actually opens the file and inspects its structure.
- **Turn gaps into edits, not just a diagnosis.** For every requirement the resume only
  partially matches, the skill suggests a specific, traceable rewording or repositioning —
  never a fabrication. If the underlying experience isn't there, it says so plainly instead
  of manufacturing a workaround.

## What it does

Given a **resume (PDF or DOCX)** and a **job posting URL**, it produces:

1. **A structural ATS-parsing scan** of the resume file itself — tables used for layout,
   text boxes, header/footer-only contact info, multi-column layouts that scramble reading
   order, non-extractable ("scanned image") PDFs, missing standard section headers,
   non-standard fonts.
2. **A requirement-by-requirement match table** — every real requirement in the JD mapped
   to specific evidence in the resume, or the specific reason it's missing.
3. **A scope/level analysis** that checks the posting's actual responsibilities against the
   resume's demonstrated scope, independent of what the job title says (a "Senior" role
   asking for 3 years of narrow execution work is flagged as a scope mismatch even though
   the title alone wouldn't catch it).
4. **An overall match score out of 10**, with the specific 2-3 things pulling it down
   spelled out in plain language.
5. **Traceable resume tailoring suggestions** — mirroring the JD's terminology where the
   resume already describes the same work differently, surfacing buried-but-relevant
   experience, tightening vague bullets into keyword-matchable ones. Every suggestion is a
   rephrasing of something the candidate actually did, never an addition.
6. On request: a **tailored cover letter** (Word `.docx`), a **LinkedIn InMail** draft, and
   a **revised resume** applying the accepted suggestions — re-scanned for ATS formatting
   risk before it's handed back.

The recommendation always comes first, with everything else underneath it as supporting
evidence. And regardless of whether the verdict is GO or NO-GO, the skill always asks
before drafting anything — the scorecard is information for the candidate's decision, not
a gate that makes the decision for them.

## Example output shape

```
## Fit Assessment: Staff Product Manager at [Company]

### Recommendation: GO WITH CAVEATS
Strong on scale and seniority; held back by one real domain gap.

### Overall match score: 8/10
...

### ATS formatting check
⚠️ 1 table detected in the document body — may cause parsing issues
✅ No header/footer-only contact info
✅ Text is fully extractable

### Requirement-by-requirement match
| JD requirement | Match | Evidence / gap |
|---|---|---|
| 7+ years PM experience incl. AI-native products | Strong | ... |
| Experience in [specific domain] | Partial | Adjacent experience in X, not direct |

### Resume tailoring suggestions
| JD requirement | Current phrasing | Suggested edit | Why |
|---|---|---|---|
| "platform resilience" | "system reliability" | "platform resilience" | mirrors JD terminology, same underlying work |

### Why not higher
...

**Next step:** Want a revised resume applying these suggestions, a tailored cover letter,
both, or want to skip this one?
```

## Installation

1. Download [`job-fit-check.skill`](./job-fit-check.skill) from this repo (or clone the
   `job-fit-check/` folder directly if you're using it outside claude.ai).
2. In [claude.ai](https://claude.ai), open the file and click **Save skill** to install it
   to your account. In Claude Code or the Claude Developer Platform, place the
   `job-fit-check/` folder under your skills directory.

## Usage

Upload a resume (PDF or DOCX) and share a job posting URL in the same message, then ask
something like:

- "Check my fit for this role: [job posting URL]"
- "What's my ATS match score for this job?"
- "Am I qualified for this position, and does my resume have any formatting issues?"

The skill will ask, once and briefly, whether you have any hard constraints (visa
sponsorship, location, IC vs. management track) it should screen for — answer or skip, and
it moves straight into the assessment.

## How it works

```
job-fit-check/
├── SKILL.md                              # Workflow: parse → scan → fetch JD → score → present → tailor → draft
├── scripts/
│   └── inspect_resume.py                 # Opens the resume file and inspects its actual
│                                          # structure (tables, text boxes, headers/footers,
│                                          # multi-column layout, extractable text, fonts)
└── references/
    ├── fit-scorecard-format.md           # Scoring methodology and output template
    ├── ats-formatting-checklist.md       # ATS-parsing risk reference for the scan
    ├── resume-tailoring.md               # Rules and format for tailoring suggestions
    └── outreach-style.md                 # Cover letter / InMail structure and style
```

`inspect_resume.py` is a real structural parser — for `.docx` it uses `python-docx` to
check for tables, headers/footers, embedded text boxes, images, and fonts; for `.pdf` it
uses `pdfplumber` to check for extractable text, embedded images, and a layout heuristic
that flags likely multi-column resumes. It's not judging content or wording — it's
answering "would an ATS parser choke on this file," the same question a real ATS asks
before a human ever sees the resume.

## Honesty by design

Every fact used in scoring, the cover letter, the InMail, and the resume tailoring
suggestions has to trace back to something actually present in the parsed resume text. The
skill is explicitly instructed never to invent a skill, inflate a title, round up years of
experience, or upgrade "contributed to" into "led." If a job requirement is a genuine gap,
the skill says so plainly rather than manufacturing a workaround — the goal is an honest
read, not a flattering one.

## Limitations

- LinkedIn job postings often don't render via automated fetch — paste the job title,
  company, and description text instead, or the skill will try to find the same posting on
  the company's Greenhouse/Lever page.
- The ATS formatting scan checks file structure, not visual design — a resume can pass the
  scan and still be poorly laid out, or vice versa in edge cases.
- This is a diagnostic and drafting aid, not a guarantee of ATS outcomes — different ATS
  platforms parse differently, and the match score is a heuristic, not a certified result.

## Built with

[Claude](https://claude.ai) — including using its own [Skills](https://www.anthropic.com/news/skills)
system to build and package this skill.
