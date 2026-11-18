# User stories — CutiFlow pilot

Baseline: BRD-CUTIFLOW-001 version 1.1. The single-story blank is [templates/user-story.md](../../templates/user-story.md). The criteria follow the [acceptance criteria guide](../../guides/acceptance-criteria.md).

Fixtures used below, unless a scenario changes them:

- Today is Wednesday 18 November 2026, Asia/Jakarta.
- Raka Putra, E-0142, Operations, hired 2 March 2024, supervisor Dimas Pratama. Annual balance 2026: entitled 12, used 4, remaining 8.
- Wulan Sari, E-0208, Finance, hired 2019, supervisor Budi Santoso. Remaining annual balance 10.
- Retno Ayu is HR Admin. The 2026 holiday calendar includes Thursday 25 December 2026 as a public holiday. Finance blackout includes 24, 28, 29, 30, and 31 December 2026, which are the last five working days of the quarter once 25 December and the weekend are removed.

## US-01 See my annual balance

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-01 |

**As an** employee, **I want** to see my annual-leave balance, **so that** I can decide whether to request leave without asking HR.

| Rule | What this story has to respect |
| --- | --- |
| BR-01 | A colleague with less than 12 months' service sees a remaining balance of 0, not a pro-rata invention. |
| BR-02 | The number is the approved ledger, not a draft. |

```gherkin
Feature: Annual balance

  Scenario: An eligible employee sees the ledger
    Given Raka has entitled 12, used 4, and remaining 8 for 2026
    When Raka opens his balance
    Then he sees entitled 12, used 4, and remaining 8
    And he does not see Wulan's balance

  Scenario: Someone still in their first year sees zero annual leave
    Given today is 18 November 2026
    And Sinta joined on 1 March 2026, which is under 12 months
    When Sinta opens her balance
    Then entitled and remaining annual days are 0
```

Trace: BRQ-01, FR-02, TC-01.

## US-02 Submit annual leave

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-02, BRQ-04, BR-01, BR-04, BR-08 |

**As an** employee, **I want** to submit annual leave for a range of dates, **so that** my supervisor has a request to decide and my balance is not spent by a draft.

| Rule | What this story has to respect |
| --- | --- |
| BR-04 | Notice is three working days, with the example date in the rule. |
| BR-08 | Overlap with an open request is a refusal, not a second approval. |
| BR-09 | Finance blackout is tested here because the requester feels it at submit time. |

```gherkin
Feature: Submit annual leave

  Scenario: Two working days are accepted and waiting on the supervisor
    Given Raka has 8 annual days remaining
    When Raka submits annual leave for 8 December 2026 through 9 December 2026
    Then the request status is Submitted
    And the working-day count is 2
    And Dimas is notified
    And Raka's remaining balance is still 8

  Scenario: Eleven working days are refused
    Given Raka has 8 annual days remaining
    When Raka submits annual leave for 1 December 2026 through 15 December 2026
    Then submission is refused for insufficient annual balance
    And the request remains Draft
    And the remaining balance is still 8

  Scenario: Next-day annual leave is too soon
    Given today is Wednesday 18 November 2026
    When Raka submits annual leave starting Thursday 19 November 2026
    Then submission is refused under BR-04
    And the earliest start date shown is Monday 23 November 2026

  Scenario: A date already approved cannot be requested again
    Given Raka already has Approved annual leave on 8 December 2026 and 9 December 2026
    When Raka submits annual leave for 9 December 2026
    Then submission is refused because the date overlaps an approved request
    And the existing request is unchanged

  Scenario: Finance cannot book the quarter-end blackout
    Given Wulan is in Finance
    And the Finance blackout includes 28 December 2026 and 29 December 2026
    When Wulan submits annual leave for those two dates
    Then submission is refused because the dates are in a blackout
```

Out of scope: half days (US-11), sick leave (US-03), the supervisor's decision (US-04).

Trace: BRQ-02, BRQ-04, UC-01, FR-03, FR-04, FR-05, FR-06, TC-02, TC-03, TC-04, TC-11, TC-12, TC-21.

## US-03 Submit sick leave without exposing the file

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-06, BR-03, BR-11 |

**As an** employee, **I want** to submit sick leave with a doctor's note when I am out for more than a day, **so that** HR has the document and my supervisor does not receive the file.

| Rule | What this story has to respect |
| --- | --- |
| BR-02 | Sick leave does not deduct annual balance. |
| BR-03 | More than one working day requires an attachment before submit. |
| BR-11 | The supervisor's view has type and dates only. |

```gherkin
Feature: Sick leave

  Scenario: Two sick days without a file cannot be submitted
    When Raka submits sick leave for 18 November 2026 and 19 November 2026 with no attachment
    Then submission is refused
    And no approver is notified

  Scenario: Two sick days with a file do not change the annual balance
    Given Raka has 8 annual days remaining
    When Raka submits sick leave for 18 November 2026 and 19 November 2026 with an attachment named catatan-dokter.pdf
    Then the status is Submitted
    And the remaining annual balance is still 8

  Scenario: The supervisor does not receive the file
    Given the sick-leave request in the previous scenario is Submitted
    When Dimas opens that request
    Then he sees type Sick and the dates
    And he does not see the reason text or catatan-dokter.pdf
```

Trace: BRQ-06, UC-01, FR-05, FR-12, TC-05, TC-06, TC-15.

## US-04 Supervisor decides

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-02, BRQ-03 |

**As a** supervisor, **I want** to approve, reject, or return a direct report's request while I can see my department's approved leave, **so that** the decision is recorded and I do not double-book the team.

```gherkin
Feature: Supervisor decision

  Scenario: Approval of two annual days becomes final
    Given Raka's request for 8 December 2026 and 9 December 2026 is Submitted
    And those dates do not overlap other approved Operations leave
    When Dimas approves with the comment "Covered by Sinta"
    Then the status is Approved
    And Raka's remaining balance is 6
    And Raka is emailed the comment

  Scenario: Rejection keeps the balance
    Given Raka's request for 8 December 2026 and 9 December 2026 is Submitted
    And his remaining balance is 8
    When Dimas rejects with the comment "Client workshop that week"
    Then the status is Rejected
    And the remaining balance is still 8
    And Dimas cannot reject without a comment

  Scenario: A supervisor cannot decide for someone else's team
    Given Wulan's request is Submitted and her supervisor is Budi
    When Dimas opens his approval queue
    Then Wulan's request is not in the queue
```

Trace: BRQ-02, BRQ-03, UC-02, FR-07, FR-09, FR-10, TC-02, TC-09.

## US-05 HR second approval

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BR-06 |

**As an** HR admin, **I want** long, unpaid, and special leave to wait for HR after the supervisor has approved, **so that** those requests are not final just because a supervisor said yes.

```gherkin
Feature: HR second approval

  Scenario: Four working days are not final at the supervisor's approval
    Given Raka has 8 annual days remaining
    And Raka submitted annual leave for 8 December 2026 through 11 December 2026, which is 4 working days
    When Dimas approves
    Then the status is Pending HR and not Approved
    And the remaining balance is still 8
    And Retno is notified

  Scenario: HR rejection does not deduct
    Given that request is Pending HR
    When Retno rejects with the comment "Too close to the client go-live"
    Then the status is Rejected
    And the remaining balance is still 8

  Scenario: Unpaid leave goes to HR even when it is one day
    Given Raka submitted unpaid leave for 8 December 2026, which is 1 working day
    When Dimas approves
    Then the status is Pending HR
```

Trace: BR-06, UC-02, FR-08, TC-07, TC-08, TC-20.

## US-06 Department calendar

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-03, BR-11 |

**As a** supervisor, **I want** to see approved leave for my department, **so that** I can spot an overlap before I approve.

```gherkin
Feature: Department calendar

  Scenario: Approved leave appears for the same department only
    Given Raka's annual leave on 8 December 2026 and 9 December 2026 is Approved
    When Dimas opens the Operations calendar
    Then he sees Raka on those dates with type Annual
    And he does not see Finance leave

  Scenario: A draft does not appear
    Given Raka has a Draft request for 15 December 2026
    When Dimas opens the Operations calendar
    Then 15 December 2026 does not show Raka
```

Trace: BRQ-03, FR-09, FR-12, TC-18.

## US-07 Cancel a future approved request

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BR-10, BR-02 |

**As an** employee, **I want** to cancel annual leave I no longer need, **so that** the days return to my balance and the team calendar.

```gherkin
Feature: Cancel approved leave

  Scenario: A December booking cancelled in November restores the balance
    Given today is 18 November 2026
    And Raka has Approved annual leave for 8 December 2026 and 9 December 2026
    And his remaining balance is 6
    When Raka cancels that request
    Then the status is Cancelled
    And his remaining balance is 8
    And those dates no longer show him on the Operations calendar

  Scenario: Leave that has already started cannot be cancelled by the employee
    Given today is 8 December 2026
    And Raka has Approved annual leave for 8 December 2026 and 9 December 2026
    When Raka tries to cancel it
    Then the request stays Approved
    And the balance is unchanged
```

Trace: BR-10, UC-03, FR-11, TC-14.

## US-08 HR keeps the calendar, the blackout, and the ledger

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-05, BR-09, BR-12, BR-13 |

**As an** HR admin, **I want** to publish holidays, blackout dates, balance adjustments, and cuti bersama, **so that** the calculator and the balance match what HR has actually decided.

```gherkin
Feature: HR reference data and adjustments

  Scenario: An adjustment without a comment is refused
    When Retno tries to add 1 day to Raka's 2026 balance with an empty comment
    Then the adjustment is not saved
    And the remaining balance is unchanged

  Scenario: Cuti bersama deducts once
    Given Raka is eligible under BR-01 and has 8 days remaining
    When Retno runs cuti bersama for 20 March 2026 and 23 March 2026 for Operations
    Then Raka has an Approved cuti bersama request for those dates
    And his remaining balance is 6
    When Retno runs the same dates again
    Then the balance stays 6
```

20 March 2026 is a Friday and 23 March 2026 is a Monday. They are fixture dates for the pilot data, not a claim about the official cuti bersama calendar.

Trace: BRQ-05, UC-04, FR-13, FR-15, TC-16, TC-19.

## US-09 Monthly export

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-07 |

**As an** HR admin, **I want** a CSV of approved leave for a month, **so that** payroll does not wait for me to retype it.

```gherkin
Feature: Monthly export

  Scenario: The file contains approved leave and skips drafts
    Given Raka has Approved annual leave on 8 December 2026 and 9 December 2026
    And Raka has a Draft request on 15 December 2026
    When Retno exports December 2026
    Then the file has a row for Raka on 8 December 2026 and 9 December 2026
    And it has no row for 15 December 2026
```

Trace: BRQ-07, FR-14, TC-17.

## US-10 Revise a returned request

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | BRQ-02 |

**As an** employee, **I want** to fix a request my supervisor returned, **so that** I do not have to abandon it and start an unexplained second draft.

```gherkin
Feature: Returned requests

  Scenario: Resubmitting a corrected request starts again with the supervisor
    Given Dimas returned Raka's request with the comment "Move it off the workshop week"
    When Raka changes the dates to 15 December 2026 and 16 December 2026 and resubmits
    Then the status is Submitted
    And Dimas is notified again
    And the approval cycle does not remember a previous HR decision, because there was none
```

A request returned by HR also resubmits to the supervisor, not straight back to HR. That is a v1 choice, recorded in the functional specification, so a returned long request is re-checked from the start.

Trace: UC-01, FR-06, FR-07, TC-10.

## US-11 Half-day annual leave

| Field | Value |
| --- | --- |
| MoSCoW | Must |
| Release | Operations pilot |
| Source | CR-001, BR-05 |

**As an** employee, **I want** to take a morning or an afternoon of annual leave, **so that** a Friday afternoon is recorded as half a day instead of disappearing into chat.

```gherkin
Feature: Half-day annual leave

  Scenario: Friday afternoon deducts half a day
    Given Raka has 8 annual days remaining
    When Raka submits annual leave for the afternoon of 11 December 2026
    Then the working-day count is 0.5
    And the status is Submitted
    When Dimas approves
    Then the status is Approved
    And the remaining balance is 7.5
    And the Operations calendar shows Raka as afternoon only

  Scenario: A half day cannot be sick leave
    When Raka submits sick leave for the morning of 18 November 2026
    Then the half-day choice is not available
```

Trace: BR-05, CR-001, UC-01, FR-16, TC-13.
