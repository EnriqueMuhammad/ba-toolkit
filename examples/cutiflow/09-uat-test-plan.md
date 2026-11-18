# UAT test plan — CutiFlow Operations pilot

| Field | Value |
| --- | --- |
| Release | Operations pilot, build baseline BRD 1.1 and FSD 1.1 |
| Plan owner | Sari Wulandari, Business Analyst |
| Business owner | Retno Ayu, HR Manager |
| Version | 1.0 |
| Date | 11 November 2026 |
| Requirements baseline | [BRD](04-brd.md) 1.1 and [FSD](08-functional-specification.md) 1.1 |
| Test case sheet | [uat-test-cases.csv](uat-test-cases.csv) |

## 1. Objective

Retno decides whether Operations can stop accepting annual leave on WhatsApp. That decision is yes only if the Must cases pass on the named staging build and she has signed section 10. A pass is not a company-wide go-live.

## 2. Scope

### In this UAT

Every Must story US-01 through US-11, the rules those stories name, and the permission checks in TC-15 and TC-22. The sheet is TC-01 through TC-22.

### Not in this UAT

- Substitute approver (GAP-07). If a tester asks for it, it is a note, not a failed case.
- WhatsApp delivery, payroll calculation, the mobile app, clock-in.
- A load test. NFR-02 is one spot check in the entry review, not a case.
- Retention and uptime (NFR-03, NFR-04). IT confirms those in writing. They are not clicks.

## 3. Environment and data

| Item | Detail |
| --- | --- |
| Environment | Staging URL published by Fajar in the entry review. Not production. |
| Build | The git revision or build number shown in the footer, written on the sign-off line. |
| Accounts | Raka Putra (employee, Operations), Dimas Pratama (supervisor), Wulan Sari (employee, Finance), Budi Santoso (Finance supervisor), Retno Ayu (HR Admin), plus one Google account that is not an employee, for TC-22. |
| Calendar and reference data | 2026 holidays include 25 December 2026. Finance blackout includes 24, 28, 29, 30, and 31 December 2026. Departments, supervisors, and hire dates loaded from the fixture CSV. |
| Date used as "today" | Wednesday 18 November 2026. The staging clock is fixed to that date for the whole cycle so BR-04 and BR-10 do not move under the testers. |

No real doctor's notes. TC-05 and TC-06 use a file named `catatan-dokter.pdf` whose contents are the sentence "UAT fixture, not a medical document".

Each case in the CSV states its own starting balance. Testers reset Raka's balance to the precondition before the case, using an HR adjustment that quotes the case ID as the comment, or they use a fresh fixture load. Cases do not depend on leftovers from other cases.

## 4. Roles

| Role | People | Responsibility |
| --- | --- | --- |
| Business owner | Retno Ayu | Accepts or rejects the pilot |
| Tester | Raka Putra, Dimas Pratama, Wulan Sari, Budi Santoso, Putri Lestari | Execute the cases for their role. Putri runs the HR cases with Retno watching the first three. |
| BA | Sari Wulandari | Maintains the sheet. Decides, with Retno, whether a failure is a defect or a wrong case. |
| Support | Fajar Nugroho | Accounts, clock, and the build number. Does not change an expected result. |

## 5. Entry criteria

All of these are true before TC-01 is executed:

- [ ] Staging is the build named in section 3, and the footer shows that build.
- [ ] SSO works for the five business accounts, and the non-employee account is refused (this is TC-22, and it is also an entry check).
- [ ] Holiday calendar, Finance blackout, and the employee CSV match section 3.
- [ ] The balance page and Dimas's queue have been opened once on the office network. If either takes more than two seconds to become usable, NFR-02 is recorded as an open item. It does not block entry unless the page is unusable.
- [ ] Bahasa Indonesia is the default, and English can be selected (NFR-01). A missing translation on balance, submit, approve, or reject blocks entry.
- [ ] Testers have walked through the sheet for one hour. They have not been asked to re-read the BRD in that hour.

## 6. Exit criteria

- [ ] TC-01 through TC-22 are Passed, or Failed with a waiver Retno has signed in section 10.
- [ ] No open severity 1 or severity 2 defect against the 1.1 baseline.
- [ ] Retno has signed section 10.

Should-level ideas that surface during the week are written on a list for the next release. They are not failed cases.

## 7. Severity

| Severity | Meaning | Example in this pilot |
| --- | --- | --- |
| 1 | A Must flow cannot be completed, or sick-leave content is visible to a supervisor, or the balance changes when the rule says it must not. | TC-15 fails. TC-03 deducts the balance anyway. |
| 2 | A Must rule returns the wrong number or the wrong approver, and the only workaround is a spreadsheet. | Working days include 25 December. A four-day request never reaches HR. |
| 3 | A Should, or a Must with a workaround Retno will accept for four weeks. | English translation missing on a secondary label. Export column order wrong but the data is there. |
| 4 | No effect on the decision or the record. | Spacing, capitalisation of a heading. |

## 8. Running the test

- Reset data to the case precondition. Do not rely on the previous case.
- Write the actual result, including the balance and the status you saw. "As expected" is not a result.
- A failure becomes a defect with the `TC-` ID in the title. Do not edit the expected result during the cycle unless Sari and Retno agree the case was wrong. That agreement is a note on the row.
- Retest on a build number. Replace the number in section 3. Do not retest on "latest".

## 9. Schedule

| When | What | Who |
| --- | --- | --- |
| 21 November 2026 | Entry review | Sari, Fajar, Retno |
| 24–26 November 2026 | Execute TC-01 through TC-22 | Testers in section 4 |
| 27 November 2026 | Defect triage | Sari, Retno, Fajar |
| 28 November 2026 | Exit decision | Retno, with Dimas for the Operations adoption call |

## 10. Sign-off

| Role | Name | Decision | Date | Notes |
| --- | --- | --- | --- | --- |
| Business owner | Retno Ayu | Pending execution | | Build number: |
| Pilot sponsor | Dimas Pratama | Pending execution | | Adoption call only. He does not waive a severity 1. |

## Case index

Steps and expected results are in the CSV. This index is the coverage check.

| Case | Title | Priority |
| --- | --- | --- |
| TC-01 | Employee sees own balance, including a first-year zero | Must |
| TC-02 | Supervisor approval of two annual days deducts 2 | Must |
| TC-03 | Eleven working days are refused and do not deduct | Must |
| TC-04 | Annual leave on the next day is refused | Must |
| TC-05 | Two sick days without a file are refused | Must |
| TC-06 | Sick leave with a file does not deduct annual balance | Must |
| TC-07 | Four annual days stay Pending HR after the supervisor approves | Must |
| TC-08 | HR rejection leaves the balance unchanged | Must |
| TC-09 | Supervisor rejection requires a comment and does not deduct | Must |
| TC-10 | A returned request can be resubmitted to the supervisor | Must |
| TC-11 | An overlapping date is refused | Must |
| TC-12 | Finance blackout dates are refused | Must |
| TC-13 | Friday afternoon deducts 0.5 and shows on the calendar | Must |
| TC-14 | Cancelling future leave restores the balance | Must |
| TC-15 | The supervisor cannot see a sick-leave file | Must |
| TC-16 | A balance adjustment without a comment is refused | Must |
| TC-17 | December export includes approved dates and omits drafts | Must |
| TC-18 | The department calendar shows approved leave only, and not another department | Must |
| TC-19 | Cuti bersama deducts once | Must |
| TC-20 | One unpaid day still goes to HR | Must |
| TC-21 | The holiday calendar removes 25 December from the count | Must |
| TC-22 | A Google account that is not an employee cannot sign in | Must |
