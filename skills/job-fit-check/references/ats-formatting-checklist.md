# ATS Formatting Checklist

This is the reasoning behind `scripts/inspect_resume.py`'s flags, plus the handful of
things the script can't detect structurally and need a read-through instead. The point of
this whole section is separate from content fit — a resume can be a perfect content match
for a job and still get auto-rejected before a human ever sees it, purely because of how
it's built as a file. That's a different failure mode from "not qualified," and it deserves
its own section in the output rather than being folded into the content scoring.

## What the script catches automatically

Run `scripts/inspect_resume.py <path>` on the uploaded resume first — it inspects the
file's actual internal structure (not just what it looks like visually) and returns JSON
with `extracted_text` and a `flags` list, each with a `severity` (critical / high / medium /
low), an `issue`, and a `detail` explaining the ATS-parsing mechanism behind it. Common
findings:

- **Tables used for layout** — many ATS parsers read tables cell-by-cell out of order or
  skip them, scrambling a two-column skills grid or a table-based header.
- **Header/footer content** — a lot of parsers ignore document headers and footers
  entirely; contact info placed only there can vanish completely.
- **Text boxes / floating shapes** — content inside a text box is often invisible to
  parsers even though it displays fine visually.
- **Images/icons carrying information** — a phone-icon glyph next to a number with no
  "Phone:" label means the number has no textual context once icons are stripped.
- **Multi-column layouts (PDF)** — a narrow sidebar next to a wider body column commonly
  gets read left-to-right straight across the page, splicing sidebar text into the middle
  of unrelated sentences.
- **No extractable text at all (PDF)** — the file is a scanned image or an image export;
  this is a critical, disqualifying issue since almost no ATS will OCR an uploaded resume.
- **Non-standard fonts** — decorative fonts can fail to embed or convert cleanly to plain
  text.
- **Missing standard section headers** — Experience / Education / Skills (or close
  synonyms) are what most parsers pattern-match on to segment the document; a creative
  label like "My Journey" instead of "Experience" risks that whole section not being
  correctly bucketed.
- **Unusual bullet glyphs** — decorative bullets occasionally convert to garbled
  characters.

## What to additionally eyeball in the extracted text

The script tells you the structure; read the `extracted_text` output for a few things it
can't judge on its own:

- **Date consistency** — wildly inconsistent date formats across entries (e.g. "Jan 2020,"
  "1/2021," "2022–Present" all in the same resume) can confuse date-parsing logic that
  some ATS use to compute total years of experience.
- **Contact info actually present in the extracted text** — confirm name, email, and phone
  number all appear as plain text in `extracted_text`, not just visually on the page (this
  cross-checks the header/footer and image flags above).
- **File name** — if you know it (the person may mention it), a generic name like
  `resume.pdf` or `Document1.docx` isn't a parsing risk but is worth a one-line nudge —
  many recruiters and ATS displays show the filename, and `FirstLast_Resume.pdf` reads
  better.

## How to present this in the output

Group findings by severity, critical/high first, and always explain the *mechanism* (why
an ATS would choke on it), not just "this is bad practice" — that's what makes the flag
actionable rather than a stylistic opinion. If there are zero flags, say so explicitly
("no structural ATS risks detected") rather than omitting the section, since a clean scan
result is itself useful information.
