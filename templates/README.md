# Templates

Blank documents. Copy one file into your project and delete the guidance blockquotes before you send it to a sponsor.

The [CutiFlow example](../examples/cutiflow/README.md) is the same set, filled in for a fictional Indonesian SME. Read that when a heading is unclear.

| Template | Use it when | Skip it when |
| --- | --- | --- |
| [Interview guide](interview-guide.md) | You are about to sit with one person who does the work | You already have notes and only need to record a decision |
| [Meeting notes](meeting-notes.md) | A workshop or decision meeting needs a record the same day | You are drafting requirements rather than recording what was said |
| [Gap analysis](gap-analysis.md) | You can describe today and the target, and you need to show what is missing | The problem is already agreed and you are writing the build contract |
| [Business requirements (BRD)](brd.md) | A sponsor must agree the problem, scope, outcomes, and business rules | The audience is the developer who needs screen and data behaviour |
| [Change request](change-request.md) | Someone wants to alter an agreed requirement | You are still discovering scope and nothing has been baselined |
| [User story](user-story.md) | You are slicing behaviour for delivery and acceptance | The rule is a one-line policy with no actor and no exception |
| [Use case](use-case.md) | One flow has several actors, returns, or failures that a story would hide | A single Given/When/Then already covers it |
| [Functional specification](functional-specification.md) | Design or build needs permissions, statuses, fields, and calculations | You only need the sponsor's yes on outcomes |
| [UAT test plan](uat-test-plan.md) | Business users will accept or reject a release | You are writing developer unit tests |
| [UAT test cases (CSV)](uat-test-cases.csv) | Testers need executable steps in a sheet | You only need the entry and exit criteria |
| [Traceability matrix (CSV)](requirements-traceability-matrix.csv) | You must show that every in-scope requirement has a story and a test | The change is a typo in a document |

## Suggested order

1. Interview guide and meeting notes, while the words are still the user's.
2. Gap analysis, once you can see today and the target side by side.
3. BRD, to baseline problem, scope, and business rules.
4. BPMN for the process you are about to specify. See the [BPMN cheat sheet](../guides/bpmn-cheat-sheet.md).
5. User stories and, for the few flows that need them, use cases.
6. Functional specification.
7. Traceability matrix, filled as you go, not the night before UAT.
8. UAT plan and test cases.
9. Change request from the moment scope is baselined.

Not every effort needs every file. A two-week internal fix often needs a change request, three stories, and a handful of test cases. A new system, which is what the example is, needs the full set.

## Identifiers

Keep one scheme for the whole effort. The example uses:

| Prefix | Meaning | Example |
| --- | --- | --- |
| `BRQ-` | Business requirement, an outcome the sponsor wants | `BRQ-01` |
| `BR-` | Business rule, a decision the business has already made | `BR-04` |
| `FR-` | Functional requirement, observable system behaviour | `FR-05` |
| `NFR-` | Non-functional requirement | `NFR-03` |
| `US-` | User story | `US-02` |
| `UC-` | Use case | `UC-01` |
| `TC-` | UAT test case | `TC-04` |
| `CR-` | Change request | `CR-001` |
| `GAP-` | Gap row | `GAP-03` |
| `SH-` | Stakeholder | `SH-02` |

MoSCoW values are `Must`, `Should`, `Could`, and `Won't`. The [MoSCoW guide](../guides/moscow-prioritisation.md) is the working definition used here. `Won't` means "not this release", and it stays on the list so it is not rediscovered every week.

## CSV files

Open the CSV files in a spreadsheet. The first row is the header. Do not rename columns if other people have formulas against them. The UAT plan explains the test-case columns. The traceability header is the contract:

`requirement_id` is the thing being traced. `requirement_type` is `Business`, `Functional`, `Non-functional`, or `Business rule`. Repeat IDs inside a cell separated by a space, for example `US-02 US-04`. Leave a cell empty rather than writing `n/a` when the link does not exist yet, so a filter for blanks still finds the holes.
