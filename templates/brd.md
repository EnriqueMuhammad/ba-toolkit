# Business requirements — [project name]

## How to use this template

The BRD is the sponsor's document. It records the problem, the outcomes, the scope, and the business rules. It does not specify screens, field lengths, or APIs. Those belong in the [functional specification](functional-specification.md).

Write requirements as outcomes a business person can accept or reject. "The employee can see remaining annual leave without asking HR" is a business requirement. "The system shall display a balance card on the home page" is a functional one.

> **Guidance.** Delete this section, including this blockquote, before you send the document for approval. Replace bracketed text. Do not leave a requirement that contains the word "support" or "manage" unless the next sentence says what the person can do.

| Field | Value |
| --- | --- |
| Document ID | BRD-[project]-[nnn] |
| Version | 0.1 |
| Status | Draft |
| Document owner | [BA name] |
| Business owner | [sponsor name and role] |
| Date | [YYYY-MM-DD] |
| Related documents | [gap analysis, workshop notes] |

## Version history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| 0.1 | [date] | [name] | First draft for review |

## 1. Executive summary

[Five to eight lines. What is wrong today, what will be true after this release, and what is deliberately not included. A sponsor who reads only this section should be able to tell you if you have the wrong project.]

## 2. Objectives and how we will know

An objective without a measure is a slogan. Name the baseline, the target, and where the number will come from. If you cannot measure it yet, say what you will start counting at go-live.

| ID | Objective | Measure | Baseline | Target | Source |
| --- | --- | --- | --- | --- | --- |
| OBJ-01 | [outcome] | [metric] | [today's number or "not recorded"] | [number and by when] | [report, sample, or log] |

## 3. Background

[How the work is done today, in the user's words. Name the tools, including the informal ones. Link the gap analysis rather than pasting it.]

## 4. Scope

### In scope

- [Capability, stated as something a person can do]

### Out of scope

- [Item, and the reason it is out. "Later" is weaker than "payroll already calculates this, and this release only hands payroll a file."]

### Later, already requested

Items people asked for that you are not doing now. This list is what stops them returning as surprises.

| Item | Why it waits | Where it is tracked |
| --- | --- | --- |
| [item] | [reason] | [backlog or CR] |

## 5. Stakeholders

| ID | Name | Role | Interest in this project | Responsibility |
| --- | --- | --- | --- | --- |
| SH-01 | [name] | [role] | [what they need to be true] | [approve, provide data, operate, or use] |

## 6. Business requirements

Each statement should be true or false after go-live, without looking at the software design.

| ID | Requirement | MoSCoW | Rationale | Source |
| --- | --- | --- | --- | --- |
| BRQ-01 | [The person] can [outcome] without [the workaround they use today]. | Must | [why it matters] | [workshop, interview, policy] |

## 7. Business rules

A business rule is a decision the business has made, whether or not a system enforces it. Write the rule so two analysts would apply it the same way. Put examples in a second sentence when a date or a count could be read two ways.

| ID | Rule | Applies to | Source | Confirmed by |
| --- | --- | --- | --- | --- |
| BR-01 | [Rule, including the exception in the same row if the exception is part of the rule.] | [leave type, department, or "all"] | [policy section or "workshop, not yet in the policy"] | [name, or "unconfirmed"] |

## 8. Assumptions, dependencies, constraints

| ID | Type | Statement | If this is wrong |
| --- | --- | --- | --- |
| A-01 | Assumption | [statement] | [what you will have to reopen] |
| D-01 | Dependency | [statement] | [what slips] |
| C-01 | Constraint | [statement] | [what you cannot choose] |

## 9. Risks

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- | --- |
| R-01 | [risk] | Low / Medium / High | Low / Medium / High | [what you are doing now, not a hope] | [name] |

## 10. Cost and benefit, only what you can stand behind

State the comparison and the assumption. A range is more honest than a false precise total. If you have not estimated build cost, say so and do not invent one.

| Item | Figure | Assumption |
| --- | --- | --- |
| [Benefit or cost] | [range or qualitative] | [what would change the figure] |

## 11. Approval

Approval means the approver accepts the scope and the rules as the baseline. Changes after signature go through a change request.

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Business owner | [name] | Pending | |
| [Other approver] | [name] | Pending | |
