# Fit Scorecard Format

The goal is to reproduce what a rigorous ATS + human recruiter screen would actually tell a
candidate — not a vibes-based "Strong/Moderate/Weak," and not a level check that just
pattern-matches the job title against the resume's most recent title. Two roles both titled
"Senior Product Manager" can be completely different jobs; score the actual substance, using
only what's demonstrated in the resume.

**Lead with the recommendation, then the score, then show the work that backs it up.** The
user wants the bottom line first and the reasoning as support underneath, not a table they
have to read through before finding out what you think. And regardless of what the
recommendation says — even a clear NO-GO — always end by asking whether they want to
proceed with the cover letter anyway. The scorecard is information for their decision, not a
gate that makes the decision for them; they may have context the scorecard can't see (a
referral, willingness to stretch, wanting the practice), so the call is always theirs.

## Step A: Extract the JD's real requirements

Pull out, verbatim where possible:
- Every required and preferred qualification (years of experience, specific skills, tools,
  domains).
- The stated years-of-experience bar.
- Scope signals in the responsibilities section — these matter more than the title:
  - **Senior/Staff-level scope**: owns strategy end-to-end, sets direction with minimal
    oversight, works across multiple teams/orgs, influences without authority, architects
    net-new systems, mentors others, represents the org to leadership.
  - **Junior/mid-level scope**: executes a plan set by someone else, works within a single
    well-defined team, "supports" or "assists," limited cross-functional scope.
- Whether the role is individual-contributor or has direct reports — read the actual
  "what you'll do" list rather than trusting the title alone; "Manager," "leads a team of
  X," "hires and develops," "manages performance" are people-management signals regardless
  of how the title reads, and conversely titles like "Lead" or "Head of" sometimes just
  mean seniority branding on an IC role.

## Step B: User-specified constraints (if any)

Before scoring, ask the user (once, briefly) whether there are any hard constraints this
role needs to clear before it's worth scoring at all — for example visa sponsorship needs,
location/remote requirements, or IC-vs-management preference. Not everyone has these; if the
user says no or doesn't answer, skip this step and move straight to scoring — don't block
the assessment on it.

If constraints are given, check them against the posting and note status (✅ / ❌ / ⚠️
Unconfirmed) for each. A failure here should weigh heavily on the recommendation but
shouldn't stop the process — still run the full requirement match below so the user has the
complete picture, and always close by asking whether they want to proceed anyway.

## Step C: Requirement-by-requirement match

A table mapping each real JD requirement (from Step A) to the specific evidence in the
resume, or the specific gap if there isn't any.

```
| JD requirement | Match | Evidence / gap |
|---|---|---|
| [verbatim or close paraphrase of requirement] | Strong / Partial / Missing | [specific line/experience from the resume that satisfies it, OR the specific reason it doesn't — e.g. "No experience found with X; closest adjacent experience is Y, which covers Z but not the core ask"] |
```

Do this for every meaningfully distinct requirement — typically 5-10 rows. Don't compress
multiple requirements into one row just to save space; each gap should be individually
visible and explained, not folded into a vague overall impression.

## Step D: Scope and level analysis

Assess whether the role's actual scope (from Step A) matches the candidate's demonstrated
scope in the resume — total years of experience, the size/ambiguity of initiatives they've
owned, whether they've led cross-functional or cross-team work, whether they've built
something from scratch versus maintained an existing system.

State one of:
- **Matches their level** — scope and seniority language align with what the resume
  demonstrates.
- **Titled below their level but scope fits** — title inflation/deflation happens; call it
  out as a non-issue if the actual responsibilities line up.
- **Titled at their level but scope is junior** — e.g. posting says "Senior" but asks for
  3-4 years of experience and describes narrow execution-only work. Flag this explicitly:
  applying could mean being over-qualified and mis-leveled even though the title looks
  right, and the role may not offer the ownership the candidate is used to.
- **Role-track mismatch** (IC vs. management) — already reflected in Step B if the user
  specified a preference; note it here too for completeness even if they didn't.

## Step E: Overall match score

Score 1-10, and don't hide the arithmetic — briefly state what's pulling the score up or
down.
- **9-10**: Nearly every requirement is a Strong match, scope aligns, no meaningful gaps.
- **7-8**: Most requirements Strong, one or two Partial, scope aligns or is a minor
  mismatch.
- **5-6**: Real mix of Strong/Partial/Missing, or a clear scope mismatch even if skills are
  fine.
- **3-4**: Multiple Missing requirements, or the role is a stretch across several
  dimensions at once.
- **1-2**: Fundamentally the wrong role for reasons beyond a stated constraint (rare — a
  constraint failure is usually the dominant driver at this end of the scale).

A constraint failure and a low requirement-match score are two separate things — a role can
score 8/10 on substance and still be a bad idea purely because of a constraint like location.
Keep these distinct in the writeup rather than conflating "doesn't fit" reasons.

## Full output template

```
## Fit Assessment: [Job Title] at [Company]

### Recommendation: [GO / GO WITH CAVEATS / NO-GO]
[1-2 sentences on the single biggest driver of this call.]

### Overall match score: [X]/10
[1-2 sentences on what's driving the score up or down]

### ATS formatting check
[See references/ats-formatting-checklist.md — group by severity, or state "no structural
ATS risks detected" if the scan came back clean]

### Constraints (if specified)
[table, only if the user gave any — otherwise omit this section entirely]

### Requirement-by-requirement match
[table from Step C]

### Resume tailoring suggestions
[table — see references/resume-tailoring.md for methodology; note any genuine gaps below the table in prose]

### Scope and level analysis
[Step D verdict + 2-3 sentence explanation]

### Why not higher (if score < 9)
[Plainly list the specific gaps pulling the score down — pull directly from the
Missing/Partial rows in the requirement table and any scope mismatch. This should read like
what a recruiter would actually say if being honest about why the screen wasn't perfect,
not a repeat of the table in prose form — synthesize the 2-3 things that matter most.]

**Next step:** Want a revised resume applying these suggestions, a tailored cover letter,
both, or want to skip this one?
```

The "Next step" question is always the closing line, worded the same way regardless of the
recommendation above it — don't soften it into an implicit "obviously skip this" for a
NO-GO, and don't skip asking for a clear GO either. Always ask.
