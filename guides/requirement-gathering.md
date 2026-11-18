# Requirement gathering

A short field guide. The [interview guide](../templates/interview-guide.md) is the script. The [meeting notes](../templates/meeting-notes.md) are the record. This page is how to choose the technique and how not to waste the room.

The [CutiFlow workshop](../examples/cutiflow/01-meeting-notes-workshop.md) and the [HR interview](../examples/cutiflow/02-interview-notes-hr.md) are the same techniques, filled in.

## Pick a technique for the question you have

| Technique | Use it when | It is the wrong tool when | It produces |
| --- | --- | --- | --- |
| One-to-one interview | You need the real steps, the exceptions, and the words one person uses | You need a decision between departments | Notes, candidate rules, a corrected process |
| Workshop | You need a shared picture or a priority call | You have not yet watched the work, so the room will invent a tidy process | Decisions, a scoped Must list, open questions with owners |
| Observation | People say "it depends" or you suspect the policy and the practice differ | The work is rare and nothing will happen while you are there | Evidence: timings, workarounds, the actual tool |
| Document and record analysis | A policy, a spreadsheet, or a sample of past requests already exists | The documents are aspirational and nobody follows them. Pair it with observation | Rules that are written, columns that are actually filled, volumes |
| Survey | You need a spread of opinion from many people and you already know the questions | You are still discovering what the questions are | Counts. Not the process |
| Prototype or worked example | People cannot react to a paragraph but can react to a form | You are using the picture to skip the rules | Corrections to fields, words, and order |

Use two techniques before you baseline a BRD. For CutiFlow that was an interview with the HR manager, then a read of the spreadsheet she sent, then a workshop with operations and finance. The workshop would have ratified a fictional process if the interview had not happened first.

## How to run a 90-minute workshop

This is the agenda the CutiFlow workshop used. Steal the shape, not the leave-specific questions.

| Minutes | What you do | What you do not do |
| --- | --- | --- |
| 0–10 | Purpose, decisions you need today, how the notes will be used | A tour of your template folder |
| 10–25 | Play back the current process in their words and let them correct it | Defend your diagram |
| 25–50 | Walk two awkward cases you brought with you. Force the rule, the exception, and who may grant it | Accept "we'll handle that offline" without an owner |
| 50–70 | Outcomes: what must be true that is not true today. Write them as `BRQ` sentences on the wall | Design screens |
| 70–80 | MoSCoW the outcomes for this release. See the [MoSCoW guide](moscow-prioritisation.md) | Let everything stay Must |
| 80–90 | Read back decisions, open questions, and actions. Dates and names | Add a new topic |

Send the notes the same day. A workshop that produces a memory is a conversation, not an elicitation.

## Questions that earn their time

Prefer a real case.

- "Show me the last one you approved, and the last one you refused."
- "What did you look at before you decided?"
- "What happens to the employee if you are away?"
- "Which number changes, and on which day?"
- "Who is not allowed to see this?"
- "What will you still do in a spreadsheet after we go live?"

If the answer is a slogan ("we need transparency"), ask what the person does differently on Monday if they have it.

## Turn notes into requirements without losing the source

1. Highlight statements that are rules, outcomes, or scope boundaries. Leave anecdotes as anecdotes.
2. Give outcomes `BRQ-` IDs and rules `BR-` IDs the same day, while you still remember who said them.
3. Mark each rule as written policy, local habit, or unconfirmed. The CutiFlow BRD keeps that distinction on purpose. A habit can still be implemented. It should not be described as the law.
4. Put anything that would change build effort and was not in the room's decision into a parking lot, not into the BRD.

## Failure modes

- **Interviewing only the sponsor.** You will specify the process they wish they had. Talk to the person who updates the sheet.
- **Workshop as design review.** If there is a mock-up in the first meeting, you will debate buttons and miss the blackout rule.
- **Treating WhatsApp as the process.** It is evidence of the process. The process includes what happens when the chat is lost.
- **Merging `izin` and `cuti`.** In Indonesian offices these are often different: one may not deduct annual balance. Ask. The [example rules](../examples/cutiflow/04-brd.md) keep unpaid leave, sick leave, and annual leave on separate paths for that reason.
- **Writing requirements in the workshop.** Capture decisions. Write requirements afterwards, and send them back for correction.

## What "done" looks like for discovery

You can stop discovery for a release when:

- You can narrate the current process and the people in it do not correct the steps.
- Every Must outcome has a source and a measure, even if the baseline is "not recorded today".
- The awkward cases you know about have a rule or an explicit "we will not handle this" decision.
- Someone who was not in the room can read the BRD and tell you what is out of scope.
