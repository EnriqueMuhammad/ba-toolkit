# Gap analysis — leave requests at PT Aruna Karya

| Field | Value |
| --- | --- |
| Document owner | Sari Wulandari, Business Analyst |
| Sponsors | Retno Ayu, HR Manager |
| Version | 1.1 |
| Date | 28 October 2026 |
| Evidence window | Interview with Retno on 8 October 2026, observation of Putri Lestari on 13 October 2026, workshop on 14 October 2026, workbook `Saldo_Cuti_2026.xlsx` received 16 October 2026 |
| Target | An Operations employee can request leave, a supervisor can decide with the team calendar in view, and the annual balance updates when the request is approved, without HR retyping chats. |

Version 1.1 adds GAP-09 after [CR-001](05-change-request-cr-001.md). The earlier rows are unchanged.

## Context

About 95 employees request leave on WhatsApp. Two HR staff keep the balance in a spreadsheet, updated on Friday from whatever chats were forwarded. The August overlap in Operations is the incident the sponsor keeps citing. The workbook received on 16 October has 95 data rows, a remaining-days formula, and no column for leave type, approver, or attachment. Yellow highlight is Putri's private signal for "check this".

## Summary

| Priority | Count | Meaning for this release |
| --- | --- | --- |
| Must close | 7 | GAP-01 through GAP-06 and GAP-08. GAP-09 joined them when CR-001 was accepted. |
| Should close | 1 | GAP-07, the absent approver. Not in the pilot. |
| Later | 0 | Nothing sits in a vague later pile. Refused items are in the BRD as Won't. |
| Not a gap | 3 | Listed below so they are not redesigned. |

## Gaps

| ID | Area | Current state | Evidence | Target state | Gap | Impact if left | Recommendation | MoSCoW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| GAP-01 | Request record | The request is a chat message. HR sees it only when someone forwards it. | Putri entered five forwards and two verbal mentions on 13 October. One forward had no approval in the captured text. | Every request that HR is expected to know about has a status, a requester, and the decision. | There is no queue and no single record. | Approved leave is missing from the sheet, or is typed in without an approver. | A request with statuses, not a new chat group. | Must |
| GAP-02 | Balance visibility | Employees ask HR because the sheet is private and a week behind. | Retno, 8 October. The workbook is an HR file, not a shared employee view. | An employee can see their own entitled, used, and remaining annual days. | No self-service balance. | The "several a day" questions continue, and Thursday's number is still last Friday's number. | Show the balance from the same ledger that approval updates. | Must |
| GAP-03 | Day count | Putri counts weekdays on her fingers. There is no holiday list in the workbook. | Observation, 13 October. Retno was unsure holidays are always excluded. | Working days exclude weekends, public holidays, and cuti bersama dates that HR has published. | The calendar and the counter are not the same thing. | Balance disputes the first time a request touches a holiday. | HR-maintained calendar, used by the calculator, with one worked example in the specification. | Must |
| GAP-04 | Team overlap | A supervisor approves from memory. The Operations group chat is an incomplete picture. | August incident, Dimas, workshop. | Before approving, the supervisor can see approved leave for their own department. | No department calendar tied to approved requests. | Two people on the same client are out, and the client finds out first. | A department calendar of approved leave. Not a company-wide feed of reasons. | Must |
| GAP-05 | Sick-leave documents | Photos of doctor's notes sit in WhatsApp, including a group that also carries client files. | Retno, 8 October. Dimas, workshop, on the Operations group. | The file is attached to the request and is not visible to the supervisor. | There is no access boundary. | Medical information in a chat history. This is worse than the spreadsheet problem. | Attachment on the request, HR and employee only. | Must |
| GAP-06 | Handoff to payroll | Payroll asks HR who was off. HR answers from the sheet and from memory. | Retno, workshop decision D6. | Payroll receives a monthly file of approved leave. Payroll still calculates money. | No agreed extract. | The Friday retyping is partly replaced by a month-end retyping. | CSV export. Not a payroll integration. | Must |
| GAP-07 | Approver is away | Another manager replies in the chat. That person may not be the assigned supervisor. | Retno, interview. Workshop decision D8. | A named substitute can decide, or the request waits somewhere HR can see. | The pilot chooses the second half only. The queue will be visible. A substitute will not. | Requests sit while a supervisor travels. HR can see them and chase. The chat workaround remains tempting. | Accept for the pilot. First Should in the following release. | Should |
| GAP-08 | Audit | A correction overwrites the cell. Yellow highlight is the only history. | Workbook structure. Putri's highlight, observed 13 October. | Each status change and each balance adjustment stores actor, timestamp, and comment. | No history. | HR cannot explain a balance, which is the dispute they already have. | Audit events, including adjustments. | Must |
| GAP-09 | Half day | Consultants take Friday afternoon off and describe it as a full day, or they do not record it. | Dimas, 21 October, in CR-001. Not observed in the 13 October session. | An annual request can be morning or afternoon and deduct 0.5. | The baseline from 14 October had no half day, so the side channel would have remained for that case. | Operations keeps a private arrangement outside CutiFlow and the balance is a fiction by half a day at a time. | Accept CR-001. Half days are annual leave only. | Must |

## Already acceptable

| Area | Why it is acceptable | Evidence |
| --- | --- | --- |
| Google accounts | Every employee already has a Workspace account. A new password directory would be a project of its own. | Fajar, workshop, decision D7. |
| The entitlement number | 12 working days after 12 months is already how HR advises people. The gap is visibility and consistent counting, not the number. Confirmation against the regulation is still open (Q1). | Retno, interview and workshop. |
| Payroll calculation | Payroll already calculates unpaid leave and does not want this project inside those formulas. | Retno, decision D6. |

## Implications

- The Must rows are a request ledger, a balance, a calendar, a department view, a privacy boundary on sick leave, a CSV, and an audit trail. That is the pilot. It is not an HR suite.
- GAP-07 is a known hole. The mitigation during the pilot is a queue HR can see, plus Dimas's instruction that Operations annual leave does not get an "ok" on WhatsApp. If supervisors are away more than the pilot can tolerate, GAP-07 is promoted by a change request, not by a developer adding a delegate field.
- GAP-09 changed the baseline after it was written. The BRD version moves to 1.1 in the same change as this row.

## Trace

| Gap | Business requirement |
| --- | --- |
| GAP-01 | BRQ-02 |
| GAP-02 | BRQ-01 |
| GAP-03 | BRQ-05 |
| GAP-04 | BRQ-03 |
| GAP-05 | BRQ-06 |
| GAP-06 | BRQ-07 |
| GAP-07 | Not baselined. Should, next release. |
| GAP-08 | BRQ-02 |
| GAP-09 | BRQ-01, via CR-001, rule BR-05 |
