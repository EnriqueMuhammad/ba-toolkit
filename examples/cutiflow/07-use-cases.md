# Use cases — CutiFlow pilot

Four use cases cover the flows where a story would hide a branch. The other stories stand on their acceptance criteria alone. The blank is [templates/use-case.md](../../templates/use-case.md). The picture of UC-01 and UC-02 together is the [approval diagram](../../diagrams/README.md).

## UC-01 Submit a leave request

| Field | Value |
| --- | --- |
| Level | User goal |
| Primary actor | Employee |
| Supporting actors | CutiFlow |
| Trigger | The employee needs leave and opens a new request. |
| Preconditions | The employee is signed in. The holiday calendar for the year has been published. The employee's hire date, department, and supervisor are on file. |
| Postconditions on success | A request is Submitted. The supervisor has been notified. The balance is unchanged. |
| Postconditions on failure | The request is Draft or does not exist. Nobody was notified. The balance is unchanged. |
| Priority | Must |
| Source | US-02, US-03, US-10, US-11, BR-03, BR-04, BR-05, BR-08, BR-09 |

### Stakeholders and interests

| Stakeholder | Interest |
| --- | --- |
| Employee | The request is either waiting on the right person, or it explains why it was not submitted. |
| Supervisor | They are not notified of drafts and invalid requests. |
| HR | A sick-leave file is present when BR-03 requires it, and is not emailed to the supervisor. |

### Main success scenario

1. The employee opens a new request and chooses a type, the dates, and, for annual leave, an optional half day.
2. CutiFlow shows the working-day count using BR-07 and, for a half day, BR-05.
3. The employee enters a reason and, when they have one, attaches a file.
4. The employee submits.
5. CutiFlow checks BR-01, BR-03, BR-04, BR-05, BR-08, and BR-09.
6. CutiFlow sets the status to Submitted, stores the audit event (BR-12), and notifies the supervisor.

### Extensions

| Step | Condition | Handling |
| --- | --- | --- |
| 2a | The range contains no working days. | CutiFlow shows that the count is 0 and does not offer submit. The use case ends. |
| 4a | The employee saves instead of submitting. | The status is Draft. The supervisor is not notified. The use case ends. |
| 5a | A check fails. | The request stays Draft. CutiFlow names the rule that failed. The balance does not change. The use case ends. |
| 6a | The employee is resubmitting a Returned request (US-10). | The previous decision comment stays visible. The status becomes Submitted. Any earlier approval step is not reused. The use case ends at step 6. |

### Special requirements

- BR-11. The submit confirmation to the supervisor does not include the sick-leave reason or the file.
- NFR-05. The checks in step 5 run on the server. Hiding the button is not the control.

### Frequency

Putri's estimate, not a count: 8 to 15 requests a week across the company, higher before cuti bersama. The pilot is one department of 18 people, so the pilot volume is a fraction of that. Source: interview 8 October 2026.

## UC-02 Decide a leave request

| Field | Value |
| --- | --- |
| Level | User goal |
| Primary actor | Supervisor, then HR Admin only when BR-06 says so |
| Supporting actors | CutiFlow, Employee |
| Trigger | A request is Submitted, or a supervisor approval has moved it to Pending HR. |
| Preconditions | The decider is the employee's supervisor, or is HR Admin for a Pending HR request. |
| Postconditions on success | The request is Approved. BR-02 has been applied. The department calendar shows it. The employee has been notified. |
| Postconditions on failure | The request is Rejected or Returned. The balance is unchanged. The employee has been notified with the comment. |
| Priority | Must |
| Source | US-04, US-05, BR-02, BR-06, BR-12 |

### Stakeholders and interests

| Stakeholder | Interest |
| --- | --- |
| Supervisor | They can see the department calendar before they commit. |
| HR Admin | Long, unpaid, and special leave cannot become approved without them. |
| Employee | A rejection or a return says why. |

### Main success scenario

1. The supervisor opens a Submitted request for a direct report and the department calendar.
2. The supervisor approves and enters a comment.
3. CutiFlow evaluates BR-06.
4. BR-06 does not require HR. CutiFlow sets Approved, applies BR-02, updates the calendar, writes the audit event, and notifies the employee.

### Extensions

| Step | Condition | Handling |
| --- | --- | --- |
| 2a | The supervisor rejects. | A comment is required. Status becomes Rejected. The balance is unchanged. The employee is notified. The use case ends. |
| 2b | The supervisor returns the request. | A comment is required. Status becomes Returned. The employee may start UC-01 extension 6a. The use case ends. |
| 2c | The decider is not the supervisor of this employee and is not acting as HR on a Pending HR request. | CutiFlow does not offer a decision. The use case ends. |
| 4a | BR-06 requires HR. | Status becomes Pending HR. The balance is unchanged. HR is notified. The use case continues at step 5. |
| 5 | HR Admin opens the Pending HR request. | HR approves, rejects, or returns. Reject and return require a comment. |
| 5a | HR approves. | Same result as step 4. The use case ends. |
| 5b | HR rejects or returns. | Same handling as 2a or 2b. A return from HR also goes back to the employee, and a later resubmit starts again at the supervisor. The use case ends. |

### Special requirements

- The supervisor's screen for a sick-leave request does not include the reason or the attachment (BR-11). HR's screen does.

### Frequency

The same requests as UC-01, plus no extras. HR sees only the subset BR-06 selects. That subset was not counted in the spreadsheet, because the spreadsheet has no leave type. Do not invent a percentage.

## UC-03 Cancel approved leave

| Field | Value |
| --- | --- |
| Level | User goal |
| Primary actor | Employee |
| Supporting actors | CutiFlow |
| Trigger | The employee no longer needs an approved request. |
| Preconditions | The request is Approved and belongs to the employee. |
| Postconditions on success | The request is Cancelled. Any BR-02 deduction is restored. The calendar entry is gone. |
| Postconditions on failure | The request stays Approved and the balance is unchanged. |
| Priority | Must |
| Source | US-07, BR-10, BR-02 |

### Main success scenario

1. The employee opens their Approved request.
2. CutiFlow checks BR-10.
3. The employee confirms cancellation.
4. CutiFlow sets Cancelled, restores the balance if BR-02 had deducted it, removes the calendar entry, and writes the audit event.

### Extensions

| Step | Condition | Handling |
| --- | --- | --- |
| 2a | The start date is not at least one working day in the future. | CutiFlow refuses. The request stays Approved. Example: on Tuesday 8 December 2026, leave that starts that day cannot be cancelled here. The employee asks HR for an adjustment instead. The use case ends. |
| 3a | The request is cuti bersama created by HR. | The employee does not see cancel. HR reverses it with an adjustment if the business decision changes. The use case ends. |

### Frequency

Unknown. Putri described corrections, not a rate. The pilot will be the first count.

## UC-04 Apply cuti bersama

| Field | Value |
| --- | --- |
| Level | User goal |
| Primary actor | HR Admin |
| Supporting actors | CutiFlow |
| Trigger | HR has published cuti bersama dates and is ready to deduct them. |
| Preconditions | The dates are on the holiday calendar as cuti bersama. The employee list and hire dates are loaded. |
| Postconditions on success | Each eligible employee has one Approved cuti bersama request for those dates, and the balance is deducted once. |
| Postconditions on failure | No partial silent deduction. Either the run completes or it reports who was skipped and why. |
| Priority | Must |
| Source | US-08, BR-13, BR-01, BR-02 |

### Main success scenario

1. HR Admin selects one or more cuti bersama dates and a department, or the whole company.
2. CutiFlow lists eligible employees (BR-01) and skips anyone who already has an Approved cuti bersama request for those dates.
3. HR Admin confirms.
4. CutiFlow creates the Approved requests, deducts the working days once, and writes an audit event per employee with the comment "Cuti bersama" plus the year.

### Extensions

| Step | Condition | Handling |
| --- | --- | --- |
| 2a | An employee already has Approved annual leave on one of the dates. | CutiFlow lists the clash and does not deduct that person until HR resolves the overlap. The others may proceed. HR's choice is recorded. |
| 3a | HR cancels the run. | Nothing is written. The use case ends. |

### Frequency

A handful of dates a year, applied in one or two runs. Source: Retno's description of the 2026 deduction, interview 8 October.

## What is deliberately not a use case

US-01, US-06, and US-09 are queries. A use case would only repeat the scenario. US-11 is an extension of UC-01 step 1, via BR-05, and does not have its own goal-level flow.
