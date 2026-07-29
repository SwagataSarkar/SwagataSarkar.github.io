# Resume Tailoring Suggestions

The resume is what actually gets ranked by an ATS and skimmed first by a human — the cover
letter is secondary. A fit assessment that only produces a cover letter is diagnosing a
problem and then handing back a document that barely moves the needle on it. This section
is where the skill earns the "ATS system" framing for real: it turns the requirement-table
gaps into specific, actionable edits to the resume itself.

## The hard rule

Every suggestion must be a **rephrasing or resurfacing of something the candidate actually
did**, never an addition of something they didn't. This is not optional or a matter of
degree — inventing a skill, a metric, or a scope of ownership the resume doesn't support is
disqualifying, full stop, the same way it would be for the cover letter. The three moves
available are:

1. **Mirror the JD's exact terminology** where the resume already describes the same
   underlying work in different words. If the JD says "platform resilience" three times and
   the resume says "system reliability" for what's clearly the same category of work,
   suggest the JD's phrasing — same fact, ATS-legible language.
2. **Surface buried-but-relevant content.** If a bullet three jobs back, or a sub-clause
   inside an unrelated bullet, actually demonstrates something the JD asks for, suggest
   pulling it into its own visible line or moving it higher — it's currently invisible to
   both a keyword scan and a 6-second human skim, and it doesn't need to become anything
   other than what it already says.
3. **Tighten a vague bullet into something an ATS keyword-matches on.** "Led cross-team
   initiative" carries no matchable keywords; if the resume elsewhere establishes what that
   initiative actually was (a technology, a domain, a scale), suggest folding that specific
   detail into the bullet itself.

What's explicitly **not** allowed: adding a skill, tool, certification, or years of
experience that isn't demonstrated anywhere in the parsed resume text; inflating a title;
upgrading "contributed to" into "led"; or padding a bullet with the JD's keywords in a way
that isn't actually true of the work described. If a JD requirement is genuinely absent from
the resume, say so plainly as a real gap — don't manufacture a workaround.

## How to generate suggestions

Work directly from the requirement-by-requirement match table already built in Step 4 of
the main workflow:

- For every row marked **Missing**: check `extracted_text` again specifically for that
  requirement's keywords/concepts before concluding it's a hard gap. If there's genuinely
  nothing there, leave it as a real gap — don't force a suggestion. If there IS
  relevant-but-unlabeled content, reclassify it as an opportunity to surface, not a true
  gap, and say so (this can even upgrade the row's Match rating in the final table).
- For every row marked **Partial**: this is usually the richest source of suggestions — the
  underlying experience exists but isn't phrased or positioned to be legible to an ATS scan
  or a fast human read. Suggest the specific rewording or repositioning.
- For rows marked **Strong**: usually no suggestion needed, but if the resume's phrasing is
  meaningfully different from the JD's terminology for the same concept, a quick keyword-
  alignment suggestion is still worth including — this is pure ATS-legibility, not a content
  change.

## Output format

```
### Resume tailoring suggestions

| JD requirement | Current resume phrasing | Suggested edit | Why |
|---|---|---|---|
| [requirement] | "[exact or close-paraphrase of what's there now]" | "[specific suggested rewording/repositioning]" | [1 sentence: mirrors JD terminology / surfaces buried content / tightens vague language] |
```

Only include rows where there's an actual actionable edit — don't manufacture a suggestion
for every single requirement just to fill the table. If a requirement is a genuine gap with
nothing to surface, note it once in prose below the table rather than forcing an empty or
padded row: "No suggestion for [requirement] — this is a genuine gap, not a
phrasing/visibility issue."

After the table, offer to apply these edits directly: ask whether the user wants a revised
resume `.docx` generated with these specific changes applied, in addition to or instead of
the cover letter. If they say yes, apply only the suggestions from this table — don't take
the opportunity to rewrite anything else, restyle the document, or make additional changes
beyond what was already shown and agreed to. Keep the same structure and formatting the
original resume used (informed by the `inspect_resume.py` structural scan from Step 1), and
re-run `inspect_resume.py` on the output before presenting it, so any ATS formatting issues
already flagged in the original aren't accidentally reintroduced in the revised version.
