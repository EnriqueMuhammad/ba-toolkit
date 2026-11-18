# Writing acceptance criteria

Acceptance criteria say how you will know a story is done. They are not a restatement of the story in the future tense, and they are not a test script for every click. The [user story template](../templates/user-story.md) has a place for them. The [CutiFlow stories](../examples/cutiflow/06-user-stories.md) are the worked version.

## A criterion is testable when

- A person who was not in the workshop can set up the `Given` from the text.
- The `When` is one action.
- The `Then` is something they can observe, including a value that must stay the same.
- Two reasonable testers would agree on pass or fail.

"The page is intuitive" fails all four. "Raka, with 8 days remaining, submits 11 working days of annual leave and sees the refusal `Insufficient annual balance`, and the remaining balance is still 8" passes.

## Shape

```gherkin
Scenario: The rule has a name that says what is being protected
  Given a concrete state
  And a second fact, only if it changes the result
  When the actor does one thing
  Then the outcome is visible
  And something that must not happen did not happen
```

Write at least three scenarios for any story that enforces a rule:

1. The main success, with numbers.
2. The rule firing (refusal, extra approver, or a deduction).
3. The recovery or the explicit non-effect (balance unchanged, file still hidden, status still draft).

A story with only a happy path will be built as a happy path.

## Use the business rule, do not rewrite it

Bad:

```gherkin
Then the system calculates the days in a smart way
```

Better, pointing at the rule and showing one application of it:

```gherkin
Given today is Wednesday 18 November 2026
When Raka submits annual leave starting Thursday 19 November 2026
Then the request is refused because BR-04 requires three working days' notice
And the earliest accepted start date shown is Monday 23 November 2026
```

The calculation lives once, in the BRD or the functional specification. The scenario proves this story uses it. If you copy the full algorithm into every story, the copies will diverge the first time the rule changes.

## Smells, and the fix

| Smell | Why it hurts | Fix |
| --- | --- | --- |
| Several `When` steps | You are writing a script, and the failure point is ambiguous | One action. Put setup in `Given`. |
| UI choreography ("click the blue button") | The criterion breaks when the control moves, and it never stated the rule | Name the action ("submits the request"), not the widget |
| Adjectives: quick, easy, flexible, robust | Nobody can fail the test | A number, a role, or a refusal message |
| "The system should allow the user to..." | That is a requirement headline, not a scenario | A case with data |
| No negative case | Invalid requests will be saved | A scenario where the save must not happen |
| Hidden data ("a valid employee") | The tester invents a different employee | Name the fixture |
| Criteria that belong to another story | The story never finishes | Move them and link the ID |

## Worked rewrite

Loose:

> The supervisor can approve leave and the employee is notified appropriately. Long leave is handled.

Tight enough to test, and still not a script:

```gherkin
Scenario: Four working days of annual leave is not final until HR approves
  Given Raka has 8 annual days remaining
  And Raka submitted 8 to 11 December 2026, which is 4 working days
  And Dimas has approved it
  When Retno opens the HR queue
  Then the request is Pending HR and not Approved
  And Raka's remaining balance is still 8
```

The notification can be its own scenario. "Appropriately" has been replaced by a status and an unchanged balance, which is what the business rule (`BR-02`, `BR-06`) actually protects. See [US-05](../examples/cutiflow/06-user-stories.md).

## Checklist before you call the story ready

- [ ] Fixtures are named, or the criterion says "any employee who...".
- [ ] Dates that depend on "today" name the date.
- [ ] At least one `Then` would fail if the business rule were coded backwards.
- [ ] You have said what does not change.
- [ ] You have not specified colour, pixel position, or database tables.
- [ ] The scenario title tells you which rule failed when the test goes red.

## Where the detail goes instead

| Kind of detail | Home |
| --- | --- |
| The full day-count algorithm and its example | Functional specification |
| The policy number (12 days, 3 days' notice) | Business rule in the BRD |
| Click-by-click execution | UAT test case CSV |
| A flow with several actors and returns | Use case |
