# Change request — CR-001 Half-day annual leave

| Field | Value |
| --- | --- |
| ID | CR-001 |
| Title | Half-day annual leave |
| Raised by | Dimas Pratama, Head of Operations |
| Date raised | 21 October 2026 |
| Status | Accepted |
| Decision by | Retno Ayu, HR Manager |
| Decision date | 22 October 2026 |
| Baseline affected | BRD 1.0, which had followed workshop decision D9 and excluded half days |

## 1. What is being asked

Operations consultants often take Friday afternoon off and work Saturday before a client workshop. Dimas wants an annual-leave request that covers one morning or one afternoon and deducts half a day. Example: Raka Putra requests the afternoon of Friday 11 December 2026. His annual balance falls by 0.5 when the request is approved. A half day cannot be sick leave, special leave, or unpaid leave in this request.

## 2. Why now

BRD 1.0 was in review. Dimas's point, which Sari agrees with, is that the pilot forbids WhatsApp approvals for annual leave. If Friday afternoon cannot be recorded, his team will keep a side channel and the balance will be wrong by half a day at a time. Waiting for a later release recreates the problem the pilot is meant to stop. This is the same case as GAP-09.

## 3. Options

| Option | Description | Effect on the baseline | Reason to prefer or reject |
| --- | --- | --- | --- |
| A. Do nothing | Full days only, as in workshop decision D9. | None. | Friday afternoons stay on WhatsApp. The pilot rule becomes something supervisors will break in the first week. |
| B. Half day, annual leave only | One date, morning or afternoon, deduct 0.5, and only on a working day. Supervisor approval follows the normal path. A half day is not more than three working days, so it does not go to HR under BR-06. | Adds BR-05. Touches the calculator, the form, the calendar label, and one UAT case. | Solves the case Dimas actually has. Does not invent hourly leave. |
| C. Any start and end time | The requester picks hours. The balance deducts a fraction of 8 hours. | New duration model, new overlap rules, and a different conversation with payroll about what a day is. | This is a time-attendance product. Fajar and Retno both refused it in the workshop when the mobile app came up. It is the wrong size for the trigger. |

Recommended option: B. It closes the side channel without redefining what a working day is.

## 4. Impact if the recommended option is accepted

| Area | Impact |
| --- | --- |
| Business rules | Add BR-05. BR-02 already says annual leave deducts the balance. Half a day is a quantity, not a new leave type. |
| Requirements and stories | BRQ-01 still holds. Add US-11 and FR-16. |
| Process | No new lane and no new approver. The submit task gains a half-day choice. The BPMN does not change, because the decision diamonds do not change. The functional specification does. |
| Data | `half_day` on the request: blank, morning, or afternoon. `working_days` may be 0.5. |
| Tests | Add TC-13. Adjust the calendar expectation so a half day is visible as morning or afternoon. |
| People | Employees gain one choice. HR does not gain a chore. Supervisors see the half day on the department calendar. |
| Time and cost | Small. One field, one branch in the day calculator, one label on the calendar. No new role and no new integration. IT had not issued a build estimate. This note does not invent one. |

## 5. Decision

| Decision | Conditions | Documents to update |
| --- | --- | --- |
| Accepted | Annual leave only. One date. Morning or afternoon. The date must be a working day. Working days become 0.5. Notice period BR-04 still applies. Half days do not go to HR solely because they are half days. | BRD to 1.1, gap analysis GAP-09, FSD, US-11, UC-01 extension, RTM, TC-13. Workshop decision D9 stays in the minutes as the historical no. |

## 6. Trace

The matrix rows for BR-05, FR-16, US-11, and TC-13 are the check that this acceptance actually landed. If those rows are missing, the change was agreed and not specified.
