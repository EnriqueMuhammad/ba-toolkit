# UAT test plan — [project name]

## How to use this template

UAT answers one question: does this release do what the business agreed, in the hands of the people who will live with it? It is not a dump of developer test cases, and it is not a place to invent new requirements. A failed case is either a defect or a wrong case. Decide which, in writing.

Executable steps live in [uat-test-cases.csv](uat-test-cases.csv). This plan says why you are testing, who tests, when you start, and when you are allowed to finish.

> **Guidance.** Delete this block before you issue the plan. Entry criteria that are already false on the day you write the plan are wishes. Change the date or change the criteria.

| Field | Value |
| --- | --- |
| Release | [name] |
| Plan owner | [name] |
| Business owner | [name] |
| Version | 0.1 |
| Date | [YYYY-MM-DD] |
| Requirements baseline | [BRD and FSD versions] |
| Test case sheet | [uat-test-cases.csv] |

## 1. Objective

[What decision this UAT supports. Usually: go live for a named group, or do not.]

## 2. Scope

### In this UAT

- [Must stories or requirement IDs]

### Not in this UAT

- [Won't and Could items, and any Must item you are explicitly deferring, with the reason]

## 3. Environment and data

| Item | Detail |
| --- | --- |
| Environment | [staging URL or "to be provided"] |
| Build | [how you will know which build you tested] |
| Accounts | [roles, and that they are not production accounts] |
| Calendar and reference data | [what must be loaded first] |
| Date used as "today" | [if the rules depend on the current date, fix it and say so] |

Do not test with real medical files or real identity numbers. Use labelled fixtures.

## 4. Roles

| Role | People | Responsibility |
| --- | --- | --- |
| Business owner | [name] | Accepts or rejects the release |
| Tester | [names] | Executes cases in their real role |
| BA | [name] | Maintains cases, triages "defect versus wrong case" |
| Support | [name] | Unblocks access and data. Does not "fix" the expected result during a test |

## 5. Entry criteria

All of these are true before the first case is executed:

- [ ] The requirements baseline named above is the one that was built.
- [ ] Every in-scope Must requirement has at least one test case, or a written reason why it is checked by review instead.
- [ ] The environment, accounts, and reference data above are ready.
- [ ] Testers have a one-hour walkthrough of the cases, not of the whole project history.

## 6. Exit criteria

- [ ] Every in-scope test case is Passed, or Failed with an accepted waiver.
- [ ] No open defect of severity 1 or 2 against the baseline.
- [ ] The business owner has signed section 10.

A waived failure names the case, the reason, and who accepted the risk.

## 7. Severity

| Severity | Meaning | Example shape |
| --- | --- | --- |
| 1 | The user cannot complete a Must flow, or data that should be protected is exposed. No workaround that the business will actually use. | Approval cannot be recorded. A sick-leave file is visible to the wrong role. |
| 2 | A Must rule gives the wrong result, and a workaround exists but costs someone real time on every occurrence. | Balance deducts the wrong number of days. |
| 3 | A Should item, or a Must item with a workaround the business accepts for this release. | Wording, sort order, a report column. |
| 4 | Cosmetic, no effect on the decision or the record. | Alignment, a label. |

Severity is about the baseline, not about how embarrassed the team is.

## 8. Running the test

- Execute the CSV in the order the plan names, because later cases may depend on earlier data.
- Write the actual result in the sheet. "As expected" is not a result.
- Failures become defects with the case ID on them. Do not edit the expected result to match the software during the cycle. If the expected result was wrong, the BA raises that as a case defect and the business owner agrees before the expected result changes.
- Retest on a named build.

## 9. Schedule

| When | What | Who |
| --- | --- | --- |
| [date] | Entry review | [names] |
| [dates] | Execution | [names] |
| [date] | Defect triage | [names] |
| [date] | Exit decision | [business owner] |

## 10. Sign-off

| Role | Name | Decision | Date | Notes |
| --- | --- | --- | --- | --- |
| Business owner | | Accept / Accept with waivers / Reject | | |
| [Operational owner] | | | | |

## Test case columns

The CSV header is fixed:

| Column | What to put in it |
| --- | --- |
| `test_case_id` | `TC-` plus a number. Never reuse a retired ID. |
| `title` | The situation, not the click. |
| `requirement_ids` | `FR-`, `BRQ-`, `BR-`, or `NFR-` IDs, separated by spaces. |
| `user_story_ids` | `US-` IDs, separated by spaces. |
| `priority` | Must cases are the exit criteria. Should cases are run if time remains. |
| `preconditions` | State of the account and the data before step 1. |
| `test_data` | Names, dates, and amounts. |
| `steps` | Numbered actions. One action per number. |
| `expected_result` | What the tester can observe, including what must not change. |
| `actual_result` | Blank until execution. |
| `status` | `Not run`, `Passed`, `Failed`, or `Waived`. |
| `tester` | Blank until execution. |
| `date_executed` | Blank until execution. |
| `defect_id` | Blank unless a defect was raised. |
