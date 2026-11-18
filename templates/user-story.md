# User story — US-[nn] [short title]

## How to use this template

One story, one user outcome. If the acceptance criteria need two unrelated actors who never meet in the same flow, you have two stories. Link the business rule IDs rather than restating the rule in different words.

The [acceptance criteria guide](../guides/acceptance-criteria.md) is the standard this template expects: concrete data, a failure case, and no hidden UI design.

> **Guidance.** Delete this block before you put the story on the wall. Keep the story, the rules, and the scenarios.

| Field | Value |
| --- | --- |
| ID | US-[nn] |
| Title | [short title] |
| Epic or process | [name] |
| MoSCoW | Must |
| Release | [release name] |
| Story owner | [BA or product owner] |
| Source | [BRQ, BR, CR, or workshop decision] |

## Story

**As a** [role, specific enough that a second role would not fit],
**I want** [capability],
**so that** [outcome the role cares about, not "so that the system is better"].

## Context

[Three to six lines. The situation, the rule that bites, and what is explicitly not part of this story.]

## Rules this story must not break

| Rule | What this story has to respect |
| --- | --- |
| BR-[nn] | [the part of the rule that shows up here] |

## Acceptance criteria

```gherkin
Feature: [story title]

  Scenario: [happy path, with a concrete case]
    Given [state, with names or numbers a tester can set up]
    And [another fact, if it changes the result]
    When [one action]
    Then [observable result]
    And [second observable result, if it is part of the same outcome]

  Scenario: [a rule fires]
    Given [state that should be rejected or redirected]
    When [the action]
    Then [the system refuses or routes]
    And [what does not change]

  Scenario: [the user can recover, or the story does not pretend the only outcome is success]
    Given [state]
    When [the action]
    Then [result]
```

## Out of scope for this story

- [Nearby behaviour that belongs in another story ID]

## Trace

| Business requirement | Use case | Functional requirement | Test case |
| --- | --- | --- | --- |
| [BRQ-nn] | [UC-nn or blank] | [FR-nn] | [TC-nn] |

## Ready checklist

- The role is a person, not "the system" and not "the user".
- The "so that" is an outcome, and it is not a restatement of the "I want".
- At least one scenario would fail if the relevant business rule were implemented backwards.
- A tester who was not in the workshop can set the data up from the scenario text.
- MoSCoW is a release decision, not a synonym for "important". See the [MoSCoW guide](../guides/moscow-prioritisation.md).
