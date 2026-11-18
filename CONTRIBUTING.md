# Contributing

This repository is a set of templates and one worked example. Changes should stay useful to a business analyst who copies a file into a real project.

## What helps

- Fix a template heading, prompt, or example that would mislead a reader.
- Add a worked row to a CSV only when the new row traces to an existing requirement in the CutiFlow example.
- Keep the primary language English. A short Bahasa Indonesia note is welcome when the term would otherwise be translated badly (`cuti`, `izin`, `cuti bersama`).

## What to leave out

- A second fictional case. One complete example is easier to maintain than two half-finished ones.
- Tool-specific process engines, Jira field maps, or Confluence macros. The templates are plain Markdown and CSV on purpose.
- Real client material. PT Aruna Karya and CutiFlow are fictional.

## Checks

```bash
npm ci
npm run lint
```

The Docs workflow also checks links. Relative links must point at files that exist.

## Identifier changes

If you rename `BR-01`, `FR-01`, `US-01`, `UC-01`, or `TC-01` in the example, update the BRD, the functional specification, the stories, the use cases, both CSV files, and the diagrams page in the same change. The point of the example is that those IDs meet.
