# Worked example: CutiFlow at PT Aruna Karya

PT Aruna Karya is fictional. It is a Surabaya professional-services firm, about 95 people, that implements and trains software. Leave is requested on WhatsApp and the balance lives in a spreadsheet called `Saldo_Cuti_2026.xlsx`. This folder is the requirements set for **CutiFlow**, a small internal web application that replaces that habit for one pilot department.

The documents use the blank files in [templates](../../templates/README.md). Nothing here is a legal opinion about Indonesian employment law. Where a number looks like the statute, the BRD says it is company policy from a workshop and that counsel has not reviewed it.

> **Catatan.** `Cuti` di contoh ini memotong saldo hanya untuk cuti tahunan dan cuti bersama. `Cuti sakit`, `cuti khusus`, dan cuti di luar tanggungan tidak memotong saldo tahunan. Jangan gabungkan ketiganya jadi satu jenis "leave" tanpa bertanya ke HR.

## Cast

| ID | Person | Role in the example |
| --- | --- | --- |
| SH-01 | Retno Ayu | HR Manager. Business owner. Decides MoSCoW and signs UAT. |
| SH-02 | Dimas Pratama | Head of Operations. Pilot sponsor. Supervisor of the pilot team. |
| SH-03 | Budi Santoso | Finance Supervisor. Owns the quarter-end blackout. |
| SH-04 | Fajar Nugroho | IT. Google Workspace and the staging environment. |
| SH-05 | Employees | Requesters. |
| SH-06 | Putri Lestari | HR officer. Updates the spreadsheet every Friday. |
| | Sari Wulandari | Business analyst. Author of these documents, inside the fiction. |
| | Raka Putra (E-0142) | Operations consultant. Hire date 2 March 2024. Fixture for most test cases. |
| | Wulan Sari (E-0208) | Finance staff. Fixture for the blackout case. |

Raka's fixture balance for 2026, unless a case says otherwise: entitled 12, used 4, remaining 8. His supervisor is Dimas. The UAT plan fixes "today" as Wednesday 18 November 2026 so notice-period cases do not depend on the clock.

## Reading order

| Order | Document | What you should learn from it |
| --- | --- | --- |
| 1 | [HR interview and a short observation](02-interview-notes-hr.md) | How the spreadsheet and the chat actually work |
| 2 | [Workshop notes, 14 Oct 2026](01-meeting-notes-workshop.md) | The decisions the BRD is not allowed to contradict |
| 3 | [Gap analysis](03-gap-analysis.md) | What is missing, what is already fine, and what waits |
| 4 | [Business requirements](04-brd.md) | Problem, scope, measures, and the rules |
| 5 | [Change request CR-001](05-change-request-cr-001.md) | Half-day leave, accepted after the first baseline |
| 6 | [User stories](06-user-stories.md) | The release, sliced, with Gherkin |
| 7 | [Use cases](07-use-cases.md) | Submit, decide, cancel, and cuti bersama |
| 8 | [Functional specification](08-functional-specification.md) | Statuses, permissions, calculations, data |
| 9 | [Diagrams](../../diagrams/README.md) | The same approval flow as a poster, BPMN, and Mermaid |
| 10 | [UAT plan](09-uat-test-plan.md) and [test cases](uat-test-cases.csv) | How the business will accept the pilot |
| 11 | [Traceability matrix](requirements-traceability-matrix.csv) | The chain from requirement to test |

## Rules at a glance

The controlled wording is in the [BRD](04-brd.md). This index is only a map.

| ID | In one line |
| --- | --- |
| BR-01 | 12 annual working days after 12 months' service. None before that. |
| BR-02 | Only annual leave and cuti bersama deduct the annual balance, and only when the request becomes Approved. |
| BR-03 | Sick leave of more than one working day needs an attachment before it can be submitted. |
| BR-04 | Annual leave must start at least three working days after submission. Sick leave and bereavement may start today or up to two working days ago. |
| BR-05 | A half day is annual leave, one working day, morning or afternoon, and deducts 0.5. Added by CR-001. |
| BR-06 | HR approves after the supervisor when working days are more than 3, or the type is unpaid or special. |
| BR-07 | Weekends, public holidays, and cuti bersama dates are not counted as requested leave days. |
| BR-08 | Dates that overlap a Submitted, Returned, Pending HR, or Approved request are refused. |
| BR-09 | Finance cannot take annual leave on a configured blackout. The default is the last five working days of each quarter. |
| BR-10 | An employee may cancel an Approved request only when the start is at least one working day away. |
| BR-11 | Sick-leave reason and attachments are visible to the employee and HR only. |
| BR-12 | Status changes and balance adjustments store actor, Asia/Jakarta timestamp, and a comment. Adjustments require a comment. |
| BR-13 | HR creates cuti bersama as approved leave. Employees do not request it. |

## What the release is not

Payroll calculation, a native mobile app, clock-in, recruitment, WhatsApp notifications, and a standing substitute approver. The substitute approver is the first `Should` for the release after the pilot. It is written down so it does not look forgotten.
