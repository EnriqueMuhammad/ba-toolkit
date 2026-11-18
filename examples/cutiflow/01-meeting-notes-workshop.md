# Meeting notes — CutiFlow discovery workshop

| Field | Value |
| --- | --- |
| Date | 14 October 2026, Asia/Jakarta |
| Time | 09:00–10:30 |
| Place | Meeting room Melati, and a Meet link for Fajar |
| Facilitator | Sari Wulandari |
| Notes by | Sari Wulandari |
| Purpose | Agree the current process, the outcomes for a pilot, and the rules that a BRD may treat as decided |
| Related documents | [Interview notes](02-interview-notes-hr.md), gap analysis to follow |

## Attendees

| Name | Role | Present |
| --- | --- | --- |
| Retno Ayu | HR Manager, business owner | Yes |
| Dimas Pratama | Head of Operations | Yes |
| Budi Santoso | Finance Supervisor | Yes |
| Fajar Nugroho | IT | Yes, remote |
| Putri Lestari | HR officer | No. Observed on 13 October. Retno will confirm the notes with her. |
| Sari Wulandari | Business Analyst | Yes |

## Agenda

1. Correct the current process (15 minutes).
2. Two awkward cases: the August overlap, and a sick-leave photo (25 minutes).
3. Outcomes for a pilot (20 minutes).
4. MoSCoW and rules (20 minutes).
5. Decisions and actions (10 minutes).

The agenda is the one in the [gathering guide](../../guides/requirement-gathering.md). It held. The half-day question was parked.

## Discussion

### Current process

Sari played back the interview: WhatsApp to the supervisor, Friday spreadsheet, no reliable holiday list, sick-leave photos in chat. Dimas corrected one point. He does not always reply in the employee's private chat. For his team he often replies in the Operations group, so the rest of the team can see who is out. That group is also where client files are sometimes shared. Retno said that is an additional reason not to leave medical photos there.

Budi confirmed the Finance blackout is his rule, not a company-wide rule. He wants it to survive a new system. He accepted that HR should be able to edit the dates rather than hard-code "the last week", because the last week and the last five working days are not the same thing once holidays are removed. The room agreed the default is the last five working days of the quarter.

### August overlap

In August two Operations consultants on the same client were both off for three days. Each had an "ok" from a different chat. Dimas found out on the Monday. He wants to see his department's approved leave before he approves another request. He does not need to see the reason for sick leave. He needs the dates and the type.

### Sick leave

Retno wants a file attached for sick leave longer than one working day, visible to HR and the employee, not to the supervisor. Dimas agreed immediately. Nobody in the room could point to the clause in the company regulation. The rule is recorded as workshop policy pending Retno's confirmation against the regulation. See assumption A-01 in the BRD.

### What "long" means, and who approves

The room set the second approver as HR, after the supervisor, when the request is more than three working days, or the type is unpaid, or the type is special (marriage or bereavement of an immediate family member). Special-leave durations were stated by Retno as three working days for marriage and two for bereavement. She will confirm both figures. They are configurable. They are not a reading of the statute.

Cuti bersama stays an HR action. Employees do not request it. It deducts annual balance. The 2026 figure Putri already applied was four days. The system has to represent that kind of deduction with a reason, not as a silent edit.

### Pilot shape

Dimas offered Operations, 18 people, as the pilot. Retno will not run two processes for them: on the go-live Monday, Operations stops accepting annual leave on WhatsApp. A one-week grace for sick-leave photos was Dimas's request, so nobody hides an illness because the new form is unfamiliar. Retno accepted one week, not more.

Fajar said every employee already has a Google Workspace account. There is no HRIS to sync managers from. A CSV that HR owns, loaded nightly, is acceptable to him for the pilot. He was explicit that a native app is out.

### Half days

Dimas asked for Friday afternoons. The room was split, and the item was not required for Retno to sponsor the pilot. Parked. It came back as [CR-001](05-change-request-cr-001.md) on 21 October and was accepted. These notes are not edited to pretend it was decided here.

## Decisions

| ID | Decision | Owner |
| --- | --- | --- |
| D1 | The pilot is CutiFlow for Operations, 18 people, for four weeks. Success is described in the BRD measures, not as "users like it". | Retno |
| D2 | Leave types in the pilot: Annual, Sick, Special (marriage, bereavement), Unpaid, plus HR-created Cuti bersama. | Retno |
| D3 | Supervisor approves first. HR approves after that only when working days exceed 3, or the type is unpaid or special. | Retno |
| D4 | Sick-leave reason and attachments are visible to the employee and HR only. | Retno |
| D5 | Finance blackout is configurable, defaulting to the last five working days of each quarter, and applies to Finance annual leave. | Budi |
| D6 | The product exports a monthly CSV for payroll. It does not calculate pay. | Retno |
| D7 | Sign-in is Google Workspace. The UI default language is Bahasa Indonesia, with an English toggle. | Fajar |
| D8 | A substitute approver is not in the pilot. HR can see the queue. | Retno |
| D9 | Half-day leave is not in the baseline coming out of this workshop. | Retno |

## Open questions

| ID | Question | Who will answer | By when |
| --- | --- | --- | --- |
| Q1 | Do the company regulations match 12 days, the sick-note threshold, and the special-leave durations? | Retno | 28 October 2026 |
| Q2 | What are the remaining 2026 public holidays and any unused cuti bersama dates? | Retno | 17 October 2026 |
| Q3 | Which Google group, if any, should map to HR Admin? | Fajar | 21 October 2026 |

## Actions

| ID | Action | Owner | Due |
| --- | --- | --- | --- |
| A1 | Send `Saldo_Cuti_2026.xlsx` and the holiday list she has | Retno | 17 October 2026 |
| A2 | Confirm Workspace SSO can restrict HR Admin | Fajar | 21 October 2026 |
| A3 | Issue BRD 0.9 for comment | Sari | 21 October 2026 |
| A4 | Tell the Operations leads that a pilot is being specified, without promising a date | Dimas | 16 October 2026 |

## Parking lot

- Substitute approver while a supervisor is away. First `Should` after the pilot. Decision D8.
- Half-day annual leave. Reopened by CR-001, not by editing D9 out of existence.
- WhatsApp or Slack messages. Email is enough for the pilot.
- Clock-in, recruitment, and payroll formulas. Not this project.
