# Functional specification — [project name]

## How to use this template

The functional specification tells a designer or developer what the system does. It implements the [BRD](brd.md). It does not reopen the business case. If a behaviour is not implied by a business requirement or a business rule, it does not belong here until someone accepts a [change request](change-request.md).

Write "the system shall" statements that a tester can fail. "The system shall be user friendly" is not a functional requirement. Put quality targets in the non-functional section and make them checkable.

> **Guidance.** Delete this block before baseline. Every `FR-` traces to a `BRQ-` or a `BR-`. If it does not, it is a design preference and should be labelled as one.

| Field | Value |
| --- | --- |
| Document ID | FSD-[project]-[nnn] |
| Version | 0.1 |
| Status | Draft |
| Document owner | [BA name] |
| Companion BRD | [ID and version] |
| Date | [YYYY-MM-DD] |

## Version history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| 0.1 | [date] | [name] | First draft |

## 1. Purpose

[What this specification covers, and the BRD version it implements.]

## 2. Actors and permissions

| Action | [Actor A] | [Actor B] | [Actor C] |
| --- | --- | --- | --- |
| [action] | Yes | No | Yes |

Call out anything an actor must not see, not only what they can do. Privacy bugs come from the cells left blank.

## 3. Status model

Name the statuses and the only transitions you allow. A diagram is welcome. A table is enough.

| From | Event | To | Who | Side effect |
| --- | --- | --- | --- | --- |
| [status] | [event] | [status] | [actor] | [notification, balance, or none] |

## 4. Process

Link the BPMN file and name the steps this specification covers. Do not redraw a drifting copy of the diagram in words if the file is the source.

## 5. Functional requirements

| ID | Statement | MoSCoW | Source |
| --- | --- | --- | --- |
| FR-01 | The system shall [observable behaviour], when [condition]. | Must | [BRQ-nn, BR-nn] |

Group the rows if you have more than about fifteen: access, capture, validation, decision, recording, notification, administration. The IDs stay stable when you regroup.

## 6. Data the behaviour depends on

Specify meaning, not a physical database. If a column has a rule, the rule is here or in the BRD, not only in a developer's head.

| Entity | Field | Meaning | Rule |
| --- | --- | --- | --- |
| [entity] | [field] | [what it is] | [BR-nn or "free text, optional"] |

## 7. Calculation and validation

Write calculations in sentences a tester can execute by hand. Include the timezone, the calendar, and one numeric example.

| ID | Rule | Example |
| --- | --- | --- |
| [FR or BR] | [calculation] | [inputs and the result] |

## 8. Notifications and records

| Event | Who is told | Channel | What is stored |
| --- | --- | --- | --- |
| [event] | [role] | [email, in app, none] | [audit fields] |

## 9. Non-functional requirements

| ID | Statement | How we will check |
| --- | --- | --- |
| NFR-01 | [checkable statement] | [test, report, or review] |

## 10. Reporting and integration

| Need | Consumer | Format | Frequency |
| --- | --- | --- | --- |
| [need] | [who] | [CSV, screen, API] | [when] |

## 11. Out of scope

Repeat the BRD exclusions that a developer would otherwise "just add". This section is allowed to be dull.

## 12. Open issues

| ID | Issue | Owner | Needed before |
| --- | --- | --- | --- |
| OI-01 | [issue] | [name] | [build / UAT / go-live] |
