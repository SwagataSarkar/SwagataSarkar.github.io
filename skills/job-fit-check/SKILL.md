---
name: job-fit-check
description: Evaluate a resume (PDF or DOCX) against a job posting URL like a rigorous ATS + recruiter screen — a requirement-by-requirement match against the JD's actual requirements (not keyword overlap), a scope/level check on real responsibilities vs. title, a scan of the resume for structural ATS-parsing risks (tables, text boxes, headers/footers, multi-column layouts, missing section headers, non-extractable PDF text), an overall match score out of 10, and traceable resume tailoring suggestions (mirroring JD terminology, surfacing buried-but-relevant experience) so the candidate can close gaps, not just learn about them. If it's a good fit (or the user says proceed anyway), drafts a cover letter as a Word .docx, a LinkedIn InMail, and can produce a revised resume applying accepted suggestions. Use whenever the user uploads a resume plus a job posting URL and asks for a fit check, match score, ATS check, or "am I qualified for this." Always run the fit assessment first, even if only the cover letter was requested.
---

# Job Fit Check

This skill reproduces what a rigorous ATS system plus a human recruiter screen would
actually tell a candidate about a specific job posting — not a vague "you seem
qualified," but a requirement-by-requirement breakdown, a check of whether the resume file
itself will even survive automated parsing, and a score that's traceable back to specific
evidence and gaps.

## Inputs

This skill needs two things: a **resume** (PDF or DOCX) and a **job posting URL**. If
either is missing, ask for it before proceeding — don't guess at resume content from
conversation context, and don't try to run an assessment against a resume you haven't
actually parsed.

## Workflow

### Step 1: Parse the resume and scan it for ATS formatting risk

Run `scripts/inspect_resume.py <path-to-resume>` on the uploaded file. This returns JSON
with the extracted text (`extracted_text`) and a list of structural `flags` — things like
tables used for layout, text boxes, header/footer-only contact info, multi-column PDF
layouts, non-extractable PDF text, missing standard section headers, and non-standard
fonts. Read `references/ats-formatting-checklist.md` for the reasoning behind each flag
type and for the couple of things worth eyeballing in the extracted text that the script
can't catch structurally (date-format consistency, whether contact info actually appears
as plain text, filename quality).

Use `extracted_text` as the source of truth for everything downstream — every claim in the
fit assessment and any drafted materials must trace back to what's actually in this text,
not to assumptions about what a resume "probably" contains.

### Step 2: Get the job posting

Fetch the URL with `web_fetch`. If it's a LinkedIn URL, it likely won't render — ask the
user to paste the job title, company, and description text instead, or try finding the
same posting on the company's Greenhouse/Lever page via web search. Read the full posting:
title, level signals, location/remote policy, required and preferred qualifications, team
description.

### Step 3: Ask about hard constraints (once, briefly, optional)

Before scoring, ask the user whether there are any hard constraints this role needs to
clear to be worth pursuing at all — common ones are visa sponsorship needs,
location/remote requirements, or IC-vs-management track preference. If they don't have any
or don't answer, skip straight to scoring — this is optional context, not a blocking
question.

### Step 4: Score fit like an ATS + human recruiter screen

Follow `references/fit-scorecard-format.md` Steps A through E in full: extract the JD's
real requirements and scope signals, check any stated constraints, build the
requirement-by-requirement match table against the parsed resume text, do the scope/level
analysis (based on actual responsibilities, not the title alone), and compute the overall
match score with a clear "why not higher" explanation.

Run this regardless of whether a stated constraint failed — the user gets the full picture
either way, and decides for themselves whether to proceed.

### Step 5: Present the assessment, leading with the recommendation

Follow the exact output ordering in `references/fit-scorecard-format.md`'s full template:
recommendation first, then the overall score, then the ATS formatting findings, then
constraints (if any were given), then the requirement table and scope analysis as
supporting detail underneath.

### Step 6: Generate resume tailoring suggestions

This runs automatically as part of the assessment — it's diagnostic, not a drafted
deliverable, so it doesn't wait for a go-ahead the way the cover letter does. Follow
`references/resume-tailoring.md`: work through the requirement table's Partial and Missing
rows and identify where the resume already contains relevant experience that's just
underemphasized or phrased differently from the JD's language, versus rows that are
genuine gaps with nothing to surface. Every suggestion must be a rephrasing or
resurfacing of something the candidate actually did — never an addition of something
that isn't in the parsed resume text. This is the same non-negotiable rule that governs
the cover letter, applied one level earlier in the process.

Present this as its own table right after the requirement-by-requirement match. Then close
with the same question every time, worded consistently regardless of the recommendation
above it: ask whether the user wants a revised resume applying these suggestions, a
tailored cover letter, both, or to skip this one entirely. A NO-GO doesn't end the process
automatically — they may have context the scorecard can't see, so the decision is always
theirs to make explicitly.

### Step 7: Draft outreach materials and/or revised resume (only after they say proceed)

Before drafting, scan the full work history in the parsed resume text for whichever
experience most directly matches this specific JD — don't default to just the most recent
1-2 roles if an earlier role is actually the stronger signal for this posting.

Depending on what the user asked for in Step 6, produce any combination of:

1. **Cover letter** — three paragraphs, no date line, clean standard formatting matching
   the resume's own font/style where reasonable. Always produce this as a distinct Word
   `.docx` file for this specific posting — use the `docx` skill
   (`/mnt/skills/public/docx/SKILL.md`) to build it, don't just hand back inline text. Save
   to `/mnt/user-data/outputs/CoverLetter_[Company]_[ShortRoleTitle].docx` — a distinct file
   per company/role so multiple applications never overwrite each other.
2. **LinkedIn InMail** — short, direct, addressed to the hiring manager or recruiter,
   following the InMail rules in `references/outreach-style.md`. Present this inline as
   text in the conversation — it's meant to be copy-pasted directly, not downloaded.
3. **Revised resume** — apply only the specific suggestions already shown and agreed to in
   Step 6, nothing beyond that scope. Use the `docx` skill to produce it, preserving the
   original resume's structure and formatting. Save to
   `/mnt/user-data/outputs/Resume_[Company]_[ShortRoleTitle].docx`. Before presenting it,
   re-run `scripts/inspect_resume.py` on the output to confirm no ATS formatting issues
   were reintroduced in the edit.

Present whichever files were produced with `present_files` when done.

Every claim in all materials must trace back to the resume's `extracted_text`. Double
check before presenting: no invented metrics, no inflated titles, no scope claims the
resume doesn't support.

## Notes on speed vs. thoroughness

Steps 1-6 (parse, scan, fetch, screen, score, present, tailor) should happen in one pass
once both inputs are available — that's the whole value of the tool, and the tailoring
suggestions are diagnostic output, not a drafted deliverable, so they don't wait for a
go-ahead either. Only Step 7 waits for explicit go-ahead, and that go-ahead is always asked
for explicitly, even after a NO-GO. If a PDF resume returns no extractable text at all, say
so immediately as a critical finding before attempting any content-based scoring — there's
no reliable resume content to score against in that case, and the formatting issue itself
is the most urgent thing to flag.
