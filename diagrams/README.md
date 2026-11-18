# Diagrams — CutiFlow leave approval

Three views of one process. The decisions are the same. The layout is not, because a README, a modelling tool, and a Markdown file do not want the same canvas.

| File | Open it with | Layout |
| --- | --- | --- |
| [cutiflow-leave-approval.png](cutiflow-leave-approval.png) | Any browser. This is the preview below. | Columns, so the picture stays readable on a page |
| [cutiflow-leave-approval.svg](cutiflow-leave-approval.svg) | A browser or a vector editor | Same drawing as the PNG |
| [cutiflow-leave-approval.drawio](cutiflow-leave-approval.drawio) | [diagrams.net](https://app.diagrams.net/) or the Draw.io VS Code integration | Same column layout as the poster, editable |
| [cutiflow-leave-approval.bpmn](cutiflow-leave-approval.bpmn) | [bpmn.io](https://bpmn.io/) or [Camunda Modeler](https://camunda.com/download/modeler/) | Left to right, which is the easier editing direction |

The `.bpmn` file is a documentation model. `isExecutable` is false. The gateway labels are the business choices. They are not engine expressions to deploy.

Rules the pictures assume, in full in the [BRD](../examples/cutiflow/04-brd.md):

- **Valid?** fails when the notice period, the balance, the overlap, the blackout, or the sick-leave attachment rule fails. The request goes back to the employee.
- **Return** is the supervisor sending it back for changes. The amber line on the poster runs around the edge of the pool and re-enters **Revise request**, then validation runs again.
- **HR needed?** is yes when working days are greater than 3, or the type is unpaid or special ([BR-06](../examples/cutiflow/04-brd.md)).
- **Approved** updates the annual balance only for annual leave and cuti bersama. The employee is told on every decision. Those two facts are captions, not extra tasks, because every outcome would otherwise repeat the same box.

## Poster

![CutiFlow leave request to approval, with lanes for the employee, the system, the supervisor, and HR](cutiflow-leave-approval.png)

## Flowchart

```mermaid
flowchart TD
  start([Leave needed]) --> submit[Submit leave request]
  submit --> validate[Validate request]
  revise[Revise request] --> validate
  validate --> valid{Valid?}
  valid -->|No| revise
  valid -->|Yes| review[Review request]
  review --> decision{Supervisor decision}
  decision -->|Reject| rejected([Rejected])
  decision -->|Return| revise
  decision -->|Approve| hrNeeded{HR needed?}
  hrNeeded -->|No| post[Update balance and calendar]
  hrNeeded -->|Yes| hr[HR review]
  hr --> hrDecision{HR decision}
  hrDecision -->|Reject| rejected
  hrDecision -->|Approve| post
  post --> approved([Approved])
```

## Sequence

The employee is notified on every final decision. That return message is one arrow here so the chart stays readable. The functional specification lists the emails.

```mermaid
sequenceDiagram
  actor Employee
  participant CutiFlow
  actor Supervisor
  actor HR
  Employee->>CutiFlow: Submit leave request
  CutiFlow->>CutiFlow: Validate balance, notice, overlap, blackout, attachment
  alt Invalid
    CutiFlow-->>Employee: Show the failed rule and keep Draft
  else Valid
    CutiFlow->>Supervisor: Request is Submitted
    alt Reject or return
      Supervisor->>CutiFlow: Reject or return, with a comment
      CutiFlow-->>Employee: Decision, balance unchanged
    else Approve, HR not required
      Supervisor->>CutiFlow: Approve
      CutiFlow->>CutiFlow: Deduct balance if the type requires it
      CutiFlow-->>Employee: Approved
    else Approve, HR required
      Supervisor->>CutiFlow: Approve
      CutiFlow->>HR: Request is Pending HR
      HR->>CutiFlow: Approve or reject
      CutiFlow-->>Employee: Final decision
    end
  end
```

## Data

Holidays are reference data used by the day-count. They are not a child of a request, so they are not drawn as a relationship. A request stores the working-day result, not a copy of the calendar.

```mermaid
erDiagram
  DEPARTMENT ||--o{ EMPLOYEE : employs
  EMPLOYEE ||--o{ EMPLOYEE : supervises
  EMPLOYEE ||--o{ LEAVE_BALANCE : holds
  EMPLOYEE ||--o{ LEAVE_REQUEST : submits
  LEAVE_TYPE ||--o{ LEAVE_REQUEST : classifies
  LEAVE_REQUEST ||--o{ APPROVAL_STEP : records
  EMPLOYEE ||--o{ APPROVAL_STEP : decides
  LEAVE_REQUEST ||--o{ ATTACHMENT : may_include
  DEPARTMENT ||--o{ BLACKOUT : restricts
  EMPLOYEE {
    string id
    string name
    date hire_date
    string department
  }
  LEAVE_BALANCE {
    int year
    decimal entitled_days
    decimal used_days
    decimal adjustment_days
  }
  LEAVE_REQUEST {
    date start_date
    date end_date
    string half_day
    decimal working_days
    string status
  }
  APPROVAL_STEP {
    string decision
    string comment
    datetime decided_at
  }
  ATTACHMENT {
    string filename
    string visible_to
  }
  BLACKOUT {
    date start_date
    date end_date
    string leave_type
  }
  LEAVE_TYPE {
    string code
    boolean deducts_annual_balance
  }
```

Field meanings and the remaining-balance formula are in the [functional specification](../examples/cutiflow/08-functional-specification.md). The [BPMN cheat sheet](../guides/bpmn-cheat-sheet.md) explains the symbols and why this diagram refuses a parallel gateway.
