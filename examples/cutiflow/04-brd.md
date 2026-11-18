# Business requirements — CutiFlow

| Field | Value |
| --- | --- |
| Document ID | BRD-CUTIFLOW-001 |
| Version | 1.1 |
| Status | Baselined for build |
| Document owner | Sari Wulandari, Business Analyst |
| Business owner | Retno Ayu, HR Manager |
| Date | 28 October 2026 |
| Related documents | [Workshop notes](01-meeting-notes-workshop.md), [interview](02-interview-notes-hr.md), [gap analysis](03-gap-analysis.md), [CR-001](05-change-request-cr-001.md) |

## Version history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| 0.9 | 21 October 2026 | Sari Wulandari | Issued for comment after the workshop. Half days excluded, following decision D9. |
| 1.0 | 22 October 2026 | Sari Wulandari | Comments from Retno and Dimas applied. Still no half days. |
| 1.1 | 28 October 2026 | Sari Wulandari | CR-001 accepted. BR-05 added. Half-day annual leave is in the pilot. |

## 1. Executive summary

Operations staff at PT Aruna Karya ask their supervisor for leave on WhatsApp. HR retypes whatever was forwarded into a spreadsheet, usually on Friday. Employees cannot see their balance, two people on the same team have been out at once without either approver knowing, and photographs of doctor's notes sit in chat.

CutiFlow is an internal web application for a four-week Operations pilot. An employee can see their annual balance and submit a request. The supervisor decides with the department calendar in view. HR decides as well when the request is long, unpaid, or special. Approved annual leave and cuti bersama change the balance the same day. Payroll receives a monthly file and does not receive a new payroll system.

This release does not calculate pay, does not replace attendance, and does not provide a native mobile app. A substitute approver, for when the supervisor is travelling, is deliberately not in the pilot.

## 2. Objectives and how we will know

| ID | Objective | Measure | Baseline | Target | Source |
| --- | --- | --- | --- | --- | --- |
| OBJ-01 | Annual leave in the pilot is requested in CutiFlow | Share of Operations annual-leave requests made in CutiFlow during the first 30 days of the pilot | Not recorded. The current channel is WhatsApp. | At least 90 percent | CutiFlow request log, plus a tally Retno keeps of any WhatsApp annual-leave requests that still arrive from Operations |
| OBJ-02 | Supervisors decide while the request is still useful | Median time from Submitted to a supervisor decision, in the second two weeks of the pilot | Not recorded | At most one working day | Timestamps in CutiFlow |
| OBJ-03 | Friday stops being a retyping job | Time Putri spends updating leave balances on Friday | About three hours, timed by Retno on two Fridays in September 2026, including chasing chats | Under 30 minutes of adjustments and exceptions, timed the same way on two Fridays in the pilot | Retno's timing notes |
| OBJ-04 | A supervisor does not discover an overlap after the fact | Approved Operations overlaps during the pilot that were not visible on the department calendar before the second approval | One known incident, August 2026 | Zero | HR incident note, reviewed at the end of the pilot |

OBJ-03 is a timed sample, not a time-and-motion study. If the pilot changes the way Putri works, the number is still worth having. It is not precise enough to support a rupiah saving, and this document does not claim one.

## 3. Background

The process as corrected in the workshop is the one in the [interview notes](02-interview-notes-hr.md) and the 13 October observation. The gaps worth funding are listed in the [gap analysis](03-gap-analysis.md). This section does not repeat them.

PT Aruna Karya has about 95 employees and an HR team of two. There is no HRIS. There is Google Workspace. Those two facts are why the pilot can use single sign-on and a manager file, and why it must not assume an employee master will appear from somewhere else.

## 4. Scope

### In scope

- An employee sees their own annual-leave balance and their own requests.
- An employee submits annual, sick, special, or unpaid leave, including a half day of annual leave.
- The system counts working days from a holiday calendar HR maintains.
- The supervisor approves, rejects, or returns a request, with the department calendar visible.
- HR approves, rejects, or returns a request when the rules require a second decision.
- Approved annual leave and cuti bersama update the balance. Cancellation of a future approved request puts the days back.
- HR records holidays, blackout dates, balance adjustments, and cuti bersama.
- HR exports a month of approved leave to CSV.
- The interface is Bahasa Indonesia by default, and English is available.
- Sign-in uses the company Google account.

### Out of scope

- Calculating pay, including the money value of unpaid leave. Payroll keeps that. This release hands them a file.
- A native mobile application. A phone browser is acceptable to the pilot sponsor.
- Clock-in, attendance, overtime, and recruitment.
- WhatsApp or Slack notifications.
- More than one legal entity, or a manager hierarchy that is not "this person's supervisor".

### Later, already requested

| Item | Why it waits | Where it is tracked |
| --- | --- | --- |
| Substitute approver when the supervisor is away | Real, and the pilot volume does not justify the extra role. HR can see the queue and chase. | GAP-07, decision D8. Should, next release. |
| A reminder when a request has been waiting a working day | Useful, and not required for the record to be correct. | Should, not yet a story. |
| WhatsApp notification | Email is enough. A second channel is a second product. | Could. Not scheduled. |

## 5. Stakeholders

| ID | Name | Role | Interest in this project | Responsibility |
| --- | --- | --- | --- | --- |
| SH-01 | Retno Ayu | HR Manager | Friday retyping and balance questions stop, without a new daily chore and without medical files in chat | Business owner. Decides rules, MoSCoW, and UAT. |
| SH-02 | Dimas Pratama | Head of Operations | His team can be off without two people disappearing from the same client | Pilot sponsor. Tells Operations that WhatsApp is no longer an approval. |
| SH-03 | Budi Santoso | Finance Supervisor | Quarter-end blackout still holds | Confirms blackout dates each quarter. |
| SH-04 | Fajar Nugroho | IT | A system he can sign in with Workspace and hand over without a new identity store | Staging, SSO, and the nightly manager file. |
| SH-05 | Employees | Requesters | They can know their balance and the status of a request | Use the pilot as instructed. |
| SH-06 | Putri Lestari | HR officer | She stops guessing which chat is the real approval | Operates adjustments, the calendar, and the export. |

## 6. Business requirements

| ID | Requirement | MoSCoW | Rationale | Source |
| --- | --- | --- | --- | --- |
| BRQ-01 | An employee can see their remaining annual leave without asking HR. | Must | This is the question HR answers several times a day. | GAP-02, interview 8 October |
| BRQ-02 | A leave request and its decision are recorded with the requester, the approver, the time, and the comment. | Must | A forwarded chat is not a record. Yellow highlight is not history. | GAP-01, GAP-08, decision D1 |
| BRQ-03 | A supervisor can see approved leave in their own department before they approve another request. | Must | The August overlap is the incident the sponsor will use to judge the pilot. | GAP-04, OBJ-04 |
| BRQ-04 | The annual balance changes on the day an annual request or cuti bersama becomes approved, and changes back if that request is cancelled under the rules. | Must | A balance that waits for Friday is the current system. | GAP-02, BR-02 |
| BRQ-05 | HR can publish public holidays and cuti bersama once, and day counts use that calendar. | Must | Finger-counting across a holiday will fail the first UAT that includes one. | GAP-03 |
| BRQ-06 | The reason and the file for sick leave are limited to the employee and HR. | Must | The current workaround stores medical photos in chat. Shipping that again would be a step backwards. | GAP-05, decision D4 |
| BRQ-07 | HR can export approved leave for a month without retyping it for payroll. | Must | Otherwise the Friday chore moves to month-end. | GAP-06, decision D6 |

## 7. Business rules

These are company decisions for the pilot. Assumption A-01 applies to every row that quotes a number of days. Two analysts should get the same answer from the examples.

| ID | Rule | Applies to | Source | Confirmed by |
| --- | --- | --- | --- | --- |
| BR-01 | Annual entitlement is 12 working days in a calendar year after 12 continuous months of service. Before that, the annual balance is 0. Unpaid leave may still be requested. | Annual balance | Workshop, Retno. Not yet matched to the written regulation. | Unconfirmed against the regulation. Open question Q1. |
| BR-02 | Only annual leave and cuti bersama deduct the annual balance. Sick, special, and unpaid leave do not. The balance changes only when the request becomes Approved, and is restored only when an Approved request becomes Cancelled. | All types | Workshop | Retno, 14 October |
| BR-03 | Sick leave of more than one working day cannot be submitted without an attachment. One working day can. | Sick | Workshop. Currently a habit. | Unconfirmed against the regulation. Q1. |
| BR-04 | Annual leave must start at least three working days after the submission date. Count the next working day as day 1. Example: submitted Wednesday 18 November 2026, the earliest start is Monday 23 November 2026. Sick leave and bereavement may start on the submission date or up to two working days before it. Other special leave is not exempt. | Annual, sick, bereavement | Workshop, worked example added in this BRD so the count is unambiguous | Retno, 22 October, on the example |
| BR-05 | A half day is annual leave for a single working day, morning or afternoon, and it deducts 0.5. It is refused on a weekend or published holiday. | Annual | CR-001 | Retno, 22 October |
| BR-06 | After the supervisor approves, HR must also approve when working days are greater than 3, or the type is unpaid, or the type is special. Otherwise the supervisor's approval is final. A half day is 0.5 and does not go to HR on duration alone. | All types | Decision D3 | Retno, 14 October |
| BR-07 | Weekends, public holidays, and published cuti bersama dates are not counted as requested leave days and are not deducted by the request. Cuti bersama is deducted by the HR action in BR-13, not by an employee request that happens to touch those dates. | Day count | Workshop | Retno, 14 October |
| BR-08 | A new request is refused when any of its dates overlap a request of the same employee in status Submitted, Returned, Pending HR, or Approved. Draft, Rejected, and Cancelled do not block. | All types | Specification of "you cannot be off twice". Not controversial in the workshop. Stated here so it is testable. | Retno, 22 October |
| BR-09 | An employee in Finance cannot submit annual leave that overlaps a blackout HR has configured. The default blackout is the last five working days of each quarter. HR may edit the dates. The rule does not apply to sick leave or bereavement. | Finance, annual | Decision D5 | Budi, 14 October |
| BR-10 | The employee who owns an Approved request may cancel it only when the start date is at least one working day in the future. The balance is restored if BR-02 had deducted it. | Cancellation | Agreed with Retno during BRD 1.0 review, so the pilot has a way back from a mistake | Retno, 22 October |
| BR-11 | Sick-leave reason text and attachments are visible to the requesting employee and to HR Admin. Supervisors see the type and the dates only. | Sick | Decision D4 | Retno and Dimas, 14 October |
| BR-12 | Every status change and every balance adjustment stores the actor, the timestamp in Asia/Jakarta, and a comment. A balance adjustment cannot be saved without a comment. | Audit | GAP-08 | Retno, 14 October |
| BR-13 | HR creates cuti bersama as Approved leave for employees who are eligible under BR-01. Employees do not submit it. It deducts the annual balance once. Running it again for the same dates and the same person does not deduct twice. | Cuti bersama | Workshop | Retno, 14 October |

Marriage and bereavement durations, as stated in the workshop and held as configuration rather than as law: marriage three working days, bereavement of an immediate family member two working days. Open question Q1.

## 8. Assumptions, dependencies, constraints

| ID | Type | Statement | If this is wrong |
| --- | --- | --- | --- |
| A-01 | Assumption | Day-count entitlements and the sick-note threshold are company policy captured in the workshop. Counsel has not reviewed them. They must be configurable. | The numbers change by configuration. The shape of the rules does not. If counsel forbids a rule, that is a change request. |
| A-02 | Assumption | Every pilot employee has a company Google account they can use on a desk or a phone browser. | The pilot list shrinks to people who have accounts, or SSO is the wrong sign-in. Fajar says this assumption holds. |
| A-03 | Assumption | HR can maintain a CSV of employee, department, supervisor, and hire date, and IT can load it nightly. There is no HRIS API. | A manual user screen is required before go-live. That is a change request, not a silent addition. |
| A-04 | Assumption | On the pilot's first Monday, Operations supervisors stop approving annual leave on WhatsApp. Sick-leave photos have a one-week grace. | OBJ-01 fails. The software can still be correct. The adoption risk is R-01. |
| D-01 | Dependency | Staging uses Google SSO before UAT starts. | UAT moves. Fajar owns the dependency. |
| D-02 | Dependency | The 2026 holiday list and any remaining cuti bersama dates are in the system before day-count UAT. | Day-count cases are blocked. Retno owns the list. |
| C-01 | Constraint | HR is two people. The pilot must not add a daily retyping job. | A design that needs Putri to re-enter approvals is out of scope even if it is easier to build. |
| C-02 | Constraint | Bahasa Indonesia is the default language of the interface. | An English-only pilot is not acceptable to Retno. |
| C-03 | Constraint | "Today" and stored timestamps use Asia/Jakarta. | Notice-period tests become arguments about midnight. |

## 9. Risks

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- | --- |
| R-01 | Supervisors keep approving on WhatsApp, so the ledger is not the truth. | Medium | High | Dimas tells Operations the channel has changed. During the pilot HR will not adjust a balance from a chat screenshot. Requests go through CutiFlow or they are not approved leave. | Dimas |
| R-02 | The holiday list arrives too late to test the calculator. | Medium | Medium | UAT entry criteria require the calendar to be loaded. The dependency is D-02. | Retno |
| R-03 | Sick-leave files are copied to a shared drive "for convenience" and the privacy rule is bypassed outside the product. | Medium | High | BRQ-06 and BR-11 are Must. TC-15 is a severity 1 case. HR will not accept a shared folder as the file store. | Retno |
| R-04 | Special-leave durations in the configuration are wrong once Retno checks the regulation. | Medium | Low | The durations are configuration. Changing a number is not a code change. Q1 tracks the check. | Retno |
| R-05 | A travelling supervisor stalls the queue, and the team returns to chat. | Medium | Medium | HR can see Submitted requests. GAP-07 is the next release if the pilot shows the stall is common. | Retno |

## 10. Cost and benefit, only what this project can stand behind

| Item | Figure | Assumption |
| --- | --- | --- |
| HR Friday effort | About three hours today, target under 30 minutes | Retno's timing of two Fridays, repeated during the pilot. This is not a salary saving calculation. |
| Balance questions | "Several a day", uncounted | If Operations stops asking, the pilot has worked even if other departments still call HR. |
| Build and run cost | Not estimated in this document | IT has not issued an estimate. Inventing one would make the approval look more precise than it is. |
| Payroll effort | A monthly file replaces a conversation. The size of that saving was not measured. | Payroll did not attend the workshop. Do not quote a payroll saving. |

## 11. Approval

Version 1.1 is the build baseline. Anything that changes a rule or a Must after this signature is a change request.

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Business owner | Retno Ayu | Approved version 1.1 | 28 October 2026 |
| Pilot sponsor | Dimas Pratama | Approved version 1.1, including CR-001 | 28 October 2026 |
| IT, for the constraints | Fajar Nugroho | Accepted the SSO and CSV constraints. This is not a build estimate. | 28 October 2026 |
