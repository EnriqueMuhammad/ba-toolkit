# Gap analysis — [process or product name]

## How to use this template

A gap is the difference between a current fact and a target you are willing to fund. It is not a list of complaints, and it is not a solution design.

Write the current state from evidence: a shadowing note, a spreadsheet, a ticket count. Write the target state as an outcome, not as a screen. The recommendation can name a feature. The gap itself should still make sense if that feature is rejected.

> **Guidance.** Delete this block before you circulate the analysis. One row per gap. Split a row that contains two different fixes.

| Field | Value |
| --- | --- |
| Document owner | [name, role] |
| Sponsors | [names] |
| Version | [0.1 draft] |
| Date | [YYYY-MM-DD] |
| Evidence window | [what you looked at, and when] |
| Target | [the future state in one sentence] |

## Context

[Two or three sentences. What process, which people, why now.]

## Summary

| Priority | Count | Meaning for this release |
| --- | --- | --- |
| Must close | [n] | The release does not solve the problem without these |
| Should close | [n] | Close them if they do not push a Must out |
| Later | [n] | Recorded so they are not mistaken for oversights |
| Not a gap | [n] | Already acceptable. Left here so nobody "fixes" them |

## Gaps

| ID | Area | Current state | Evidence | Target state | Gap | Impact if left | Recommendation | MoSCoW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GAP-01 | [area] | [what happens today, one or two sentences] | [file, observation, or quote] | [what should be true] | [what is missing, not the product name] | [who feels it, and how often] | [the response you recommend] | Must |

## Already acceptable

List things you looked at and do not propose to change. This is how a gap analysis stays trusted.

| Area | Why it is acceptable | Evidence |
| --- | --- | --- |
| [area] | [reason] | [source] |

## Implications

- [What the Must rows do to scope, roles, or data.]
- [What you are explicitly not solving, and the risk you are accepting.]

## Trace

When a recommendation is accepted, give it a business requirement ID and point the row at the BRD. Rejected recommendations stay in this document with the reason, so the next workshop does not reopen them by accident.
