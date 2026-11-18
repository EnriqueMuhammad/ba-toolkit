# Use case — UC-[nn] [name]

## How to use this template

Use a use case when a flow has more than one actor or more than one way to finish, and a user story's scenarios would hide the path. Do not write a use case for every story. The CutiFlow example writes four use cases and eleven stories.

Number the main success scenario. Extensions refer to the step they branch from (`4a`). The extension either returns to a step or ends the use case.

> **Guidance.** Delete this block before you baseline the use case. Write steps as actor actions and system responses, alternating. Do not put business-rule prose inside a step. Point at the rule ID.

| Field | Value |
| --- | --- |
| ID | UC-[nn] |
| Name | [verb plus object] |
| Level | User goal |
| Primary actor | [role] |
| Supporting actors | [roles, including the system if it does something the user waits for] |
| Trigger | [the event that starts the use case] |
| Preconditions | [what is already true] |
| Postconditions on success | [what is true that was not true before] |
| Postconditions on failure | [what must be unchanged] |
| Priority | Must |
| Source | [story IDs and rule IDs] |

## Stakeholders and interests

| Stakeholder | Interest |
| --- | --- |
| [role] | [what they need this use case to protect] |

## Main success scenario

1. [Primary actor does something.]
2. [System responds.]
3. [Next actor acts.]
4. [System completes the goal.]

## Extensions

| Step | Condition | Handling |
| --- | --- | --- |
| 2a | [condition, in the actor's language] | [what happens]. The use case [returns to step n / ends]. |
| 3a | [another condition] | [handling] |

## Special requirements

- [A constraint that applies to this flow only, such as a privacy limit or a timing rule. Link `NFR-` or `BR-` IDs.]

## Frequency

[How often this happens at the volumes you were given. Say the source. Do not invent a peak figure.]

## Open issues

| ID | Issue | Owner |
| --- | --- | --- |
| [none, or a real question] | | |
