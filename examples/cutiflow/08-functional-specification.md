# Functional specification — CutiFlow

| Field | Value |
| --- | --- |
| Document ID | FSD-CUTIFLOW-001 |
| Version | 1.1 |
| Status | Baselined for build |
| Document owner | Sari Wulandari, Business Analyst |
| Companion BRD | BRD-CUTIFLOW-001 version 1.1 |
| Date | 28 October 2026 |

## Version history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| 1.0 | 22 October 2026 | Sari Wulandari | First build baseline, without half days. |
| 1.1 | 28 October 2026 | Sari Wulandari | CR-001. FR-16 added. No change to the approval diamonds. |

## 1. Purpose

This specification describes what CutiFlow does for the Operations pilot. It implements the BRD. It does not reopen scope. Behaviour that is not traced to a `BRQ-` or a `BR-` is called out as a design choice and is limited to section 3 (the resubmit path) and section 8 (email as the channel).

The process shape is [diagrams/cutiflow-leave-approval.bpmn](../../diagrams/cutiflow-leave-approval.bpmn). Use cases [UC-01](07-use-cases.md) and [UC-02](07-use-cases.md) are the narrative form of that file.

## 2. Actors and permissions

A supervisor is also an employee. HR Admin is a role on the person, granted through a Google group or an equivalent flag that Fajar controls. The nightly CSV sets department, supervisor, and hire date. It does not grant HR Admin.

| Action | Employee | Supervisor of that employee | HR Admin |
| --- | --- | --- | --- |
| Sign in with a company Google account | Yes | Yes | Yes |
| See own annual balance | Yes | Yes | Yes |
| See another person's balance | No | No | Yes |
| Create and submit own request | Yes | Yes | Yes |
| Decide a Submitted request | No | Direct reports only | No |
| Decide a Pending HR request | No | No | Yes |
| See department calendar (name, dates, type, half day) | Own department | Own department | All departments |
| See sick-leave reason and attachment | Own requests | No | Yes |
| Edit holidays, blackouts, adjustments, cuti bersama | No | No | Yes |
| Export the monthly CSV | No | No | Yes |
| Cancel own future Approved request | Yes, under BR-10 | No, not for other people | No, except by adjustment |

"No" means the server responds as if the record is not available. Hiding a button is not sufficient (NFR-05).

## 3. Status model

| From | Event | To | Who | Side effect |
| --- | --- | --- | --- | --- |
| (none) | Save | Draft | Employee | No notification |
| Draft | Submit, checks passed | Submitted | Employee | Email supervisor. Balance unchanged. |
| Draft | Submit, checks failed | Draft | Employee | Show the failed rule. No notification. |
| Submitted | Approve, BR-06 does not apply | Approved | Supervisor | Apply BR-02. Update calendar. Email employee. |
| Submitted | Approve, BR-06 applies | Pending HR | Supervisor | Balance unchanged. Email HR. |
| Submitted | Reject | Rejected | Supervisor | Comment required. Balance unchanged. Email employee. |
| Submitted | Return | Returned | Supervisor | Comment required. Email employee. |
| Pending HR | Approve | Approved | HR Admin | Apply BR-02. Update calendar. Email employee. |
| Pending HR | Reject | Rejected | HR Admin | Comment required. Balance unchanged. Email employee. |
| Pending HR | Return | Returned | HR Admin | Comment required. Email employee. |
| Returned | Resubmit, checks passed | Submitted | Employee | Email supervisor again. Previous approval steps are kept as history and do not count as a decision on the new submission. |
| Approved | Cancel, BR-10 allows | Cancelled | Employee | Restore BR-02 deduction if any. Remove calendar entry. |
| Draft | Discard | (deleted) | Employee | No audit beyond the deletion event. |

Design choice, not a business rule from the workshop: a request returned by HR resubmits to the supervisor rather than straight back to HR. Retno accepted this in the BRD 1.0 review because the alternative needs a second queue concept. It is testable in TC-10's shape and in UC-01 extension 6a.

There is no status for "waiting because the supervisor is away". The request stays Submitted. That is GAP-07, accepted for the pilot.

## 4. Process

The BPMN file is the source for sequence. This specification does not redraw it. Gateway "HR needed?" is true exactly when BR-06 is true. Gateway "Valid?" is true exactly when the submit checks in FR-05 pass.

## 5. Functional requirements

### Access

| ID | Statement | MoSCoW | Source |
| --- | --- | --- | --- |
| FR-01 | The system shall create a session only for a company Google account that matches an active employee, and shall reject every other sign-in. | Must | C-02's companion constraint from Fajar, decision D7 |

### Request and balance

| ID | Statement | MoSCoW | Source |
| --- | --- | --- | --- |
| FR-02 | The system shall show the signed-in employee their entitled, used, and remaining annual days for the selected calendar year, computed as entitled plus adjustments minus used. | Must | BRQ-01, BR-01 |
| FR-03 | The system shall let an employee save a draft without notifying anyone. | Must | UC-01 extension 4a |
| FR-04 | The system shall set working days to the count of dates from start to end inclusive that are not a Saturday, a Sunday, or a published holiday or cuti bersama date. | Must | BRQ-05, BR-07 |
| FR-05 | The system shall refuse submit, keep Draft, and leave the balance unchanged when the request violates BR-01, BR-03, BR-04, BR-08, or BR-09, or when working days are 0. | Must | Those rules |
| FR-06 | The system shall, on a successful submit, set Submitted, store the audit event, and email the supervisor. The email does not include a sick-leave reason or attachment. | Must | BRQ-02, BR-11 |
| FR-16 | The system shall let an employee mark an annual request as morning or afternoon of a single working day, store working days as 0.5, and refuse that mark on any other leave type or on a non-working day. | Must | BR-05, CR-001 |

### Decision

| ID | Statement | MoSCoW | Source |
| --- | --- | --- | --- |
| FR-07 | The system shall let the employee's supervisor approve, reject, or return a Submitted request. Reject and return require a comment. Any other person shall receive the same response as if the request did not exist. | Must | BRQ-02, UC-02 |
| FR-08 | The system shall move an approved Submitted request to Pending HR when BR-06 is true, and to Approved when BR-06 is false. HR Admin shall approve, reject, or return a Pending HR request. Reject and return require a comment. | Must | BR-06 |
| FR-09 | The system shall, when status becomes Approved, deduct annual balance only if the type is annual or cuti bersama, and shall show the leave on the department calendar including morning or afternoon when FR-16 applies. | Must | BR-02, BRQ-03, BRQ-04 |
| FR-10 | The system shall email the employee when the request becomes Approved, Rejected, or Returned, and the message shall include the latest comment. | Must | BRQ-02 |
| FR-11 | The system shall let the owning employee cancel an Approved request when BR-10 allows, restore any deduction made under FR-09, and remove the calendar entry. Cuti bersama created under FR-13 is not cancellable by the employee. | Must | BR-10, UC-03 |

### Privacy, administration, record

| ID | Statement | MoSCoW | Source |
| --- | --- | --- | --- |
| FR-12 | The system shall return sick-leave reason text and attachments only to the requesting employee and to HR Admin. | Must | BRQ-06, BR-11 |
| FR-13 | The system shall let HR Admin add and retire holiday dates, edit blackout periods per department and leave type, post a balance adjustment only with a comment, and run cuti bersama so that an eligible employee is deducted once for a given date. | Must | BR-09, BR-12, BR-13, BRQ-05 |
| FR-14 | The system shall export CSV of Approved leave that overlaps a chosen calendar month, one row per leave date, and shall omit every other status. | Must | BRQ-07 |
| FR-15 | The system shall store, for every status change and every balance adjustment, the actor, the timestamp in Asia/Jakarta, the from-status and to-status where relevant, and the comment. | Must | BR-12 |

## 6. Data the behaviour depends on

Physical tables are a design choice. The names below are the entities in the [ERD](../../diagrams/README.md). Meanings are not optional.

| Entity | Field | Meaning | Rule |
| --- | --- | --- | --- |
| Employee | hire_date | Start of continuous service | BR-01 |
| Employee | supervisor_id | The only person who may decide a Submitted request | FR-07 |
| Employee | department_id | Calendar and blackout scope | BR-09, FR-09 |
| Leave balance | entitled_days, used_days, adjustment_days | Components of the remaining figure | FR-02. Remaining is entitled + adjustment − used. |
| Leave request | type | Annual, sick, special, unpaid, or cuti bersama | Decision D2 |
| Leave request | half_day | Blank, morning, or afternoon | FR-16. Blank means full days. |
| Leave request | working_days | The FR-04 result, or 0.5 | Not typed in by the employee |
| Leave request | status | Section 3 | |
| Leave request | reason | Free text | Hidden for sick leave outside FR-12 |
| Approval step | decision, comment, decided_at | One row per decision, kept after a resubmit | FR-15 |
| Attachment | file, visibility | The doctor's note or other file | FR-12 |
| Holiday date | date, kind | Public holiday or cuti bersama | FR-04 excludes both |
| Blackout | department, type, start, end | A closed range | BR-09 |
| Audit event | actor, timestamp, comment | The history Putri does not have today | BR-12 |

## 7. Calculation and validation

Timezone for "today" is Asia/Jakarta (C-03).

| ID | Rule | Example |
| --- | --- | --- |
| FR-04 | Count inclusive dates that are Mon–Fri and not on the holiday calendar. | 8 December 2026 through 11 December 2026 is Tuesday to Friday, no holiday in the fixture, so 4. |
| BR-04 | Next working day after submission is day 1. | Submitted Wednesday 18 November 2026. Thursday 19 is day 1, Friday 20 is day 2, Monday 23 is day 3. Earliest annual start is 23 November 2026. |
| FR-16 | A half day forces the range to one working day and sets the count to 0.5 before balance checks. | Afternoon of Friday 11 December 2026 deducts 0.5 on approval, not 1. |
| FR-02 | Remaining = entitled + adjustments − used. | Raka starts at 12 + 0 − 4 = 8. After the half day is approved, used is 4.5 and remaining is 7.5. |
| BR-13 | A second run for the same employee and date creates nothing and deducts nothing. | The US-08 scenario. |

Working-day example the UAT fixtures rely on: December 2026 in the fixture has one public holiday, Thursday 25 December. A request from 24 December through 31 December, if it were not blocked by the Finance blackout, would count 24, 28, 29, 30, and 31. That is five working days. 25 December is excluded, and 26–27 December are a weekend.

## 8. Notifications and records

| Event | Who is told | Channel | What is stored |
| --- | --- | --- | --- |
| Submitted | Supervisor | Email | Audit event, no sick-leave attachment |
| Pending HR | HR Admin group | Email | Audit event |
| Approved, Rejected, Returned | Employee | Email including the comment | Audit event and, for Approved, the balance and calendar change |
| Cancelled | None required for the pilot | The employee sees the new status | Audit event and the reversal |
| Adjustment or cuti bersama | None | The employee sees the balance | Audit event with a comment |

Email is the channel because decision D7's alternatives (WhatsApp, Slack) are Could or Won't. A product that only shows an in-app inbox would fail BRQ-02 for a supervisor who is not staring at CutiFlow. That is a design choice inside an agreed outcome.

## 9. Non-functional requirements

| ID | Statement | How we will check |
| --- | --- | --- |
| NFR-01 | The interface is Bahasa Indonesia by default and can be switched to English by the signed-in person. The choice persists for that person. | Review on staging with Raka's account, both labels for balance, submit, approve, and reject. |
| NFR-02 | The balance page and the supervisor queue are usable within 2 seconds on a 10 Mbps connection, with the 95-employee fixture loaded. | One timed check on staging from the office network during UAT entry. This is a spot check, not a load test. |
| NFR-03 | During the pilot, the service is aimed at 99.5 percent availability on weekdays 08:00–18:00 WIB, excluding a maintenance window IT announces at least one working day ahead. | IT's existing uptime check. This is a pilot target, not a penalty clause. |
| NFR-04 | Audit events and attachments are retained for five years. | Operations note from IT, confirmed before go-live. Not a UAT click-through. |
| NFR-05 | Every permission in section 2 is enforced on the server for a direct request, not only by hiding the control. | TC-15, plus a review that Dimas's session cannot fetch Wulan's approval by identifier. |

## 10. Reporting and integration

| Need | Consumer | Format | Frequency |
| --- | --- | --- | --- |
| Approved leave | Payroll, via HR | CSV from FR-14 | Monthly, and whenever HR asks |
| Employees, departments, supervisors, hire dates | CutiFlow | CSV loaded by IT | Nightly |
| Sign-in | Employees | Google Workspace | Each session |

There is no write-back to payroll and no HRIS.

CSV columns for FR-14, in this order: `employee_id`, `employee_name`, `department`, `leave_type`, `date`, `half_day`, `status`. `status` is always `Approved` in this file. `half_day` is blank, `morning`, or `afternoon`.

## 11. Out of scope

Repeated from the BRD so they are not built as helpful extras: pay calculation, native mobile app, clock-in, recruitment, WhatsApp or Slack, a standing substitute approver, multi-entity structures.

## 12. Open issues

| ID | Issue | Owner | Needed before |
| --- | --- | --- | --- |
| OI-01 | Confirm special-leave durations and the sick-note threshold against the company regulation. Numbers stay configurable meanwhile. | Retno | Go-live, not prototype |
| OI-02 | HR Admin Google group name. | Fajar | UAT entry |
| OI-03 | Privacy notice text on the sick-leave attachment field. | Retno | UAT entry |
