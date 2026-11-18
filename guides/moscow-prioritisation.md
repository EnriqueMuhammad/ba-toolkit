# MoSCoW prioritisation

MoSCoW is a release decision, not a ranking of how much people care. Something can matter a great deal and still be `Won't` this release, because the release has a date and a team.

The letters:

| Value | Meaning in this toolkit | Test |
| --- | --- | --- |
| Must | The release does not ship without it. If it slips, the release slips or the scope is renegotiated in public. | "Would the business owner refuse go-live if this is missing?" If the answer is no, it is not a Must. |
| Should | Important, and you will do it if no Must is at risk. Dropping it needs a conversation, not a silent cut. | "Will someone be meaningfully worse off every week if we wait one release?" |
| Could | A small improvement you will pick up if a Must finishes early. Nobody re-plans the release around it. | "Is this still worth a sentence in the notes if it does not happen?" |
| Won't | Not this release. It stays written down. | "Are we recording a no, so it does not return next week as a new idea?" |

`Won't` is the most useful value and the one teams skip. An unwritten no comes back as a surprise requirement during build.

## Rules of use

- Prioritise outcomes and rules, not tasks. "Email notification" is a task. "The employee hears the decision without asking HR" is the outcome, and it might be met by email.
- The Must list has to fit the release. If every row is Must, you have not prioritised. You have restated the wishlist. Split the release or drop rows.
- One owner for the priority. A workshop can propose. The business owner decides. In the example that owner is Retno Ayu.
- Do not use MoSCoW as a substitute for sequencing inside a Must. Build order is a separate conversation.
- Revisit only when a [change request](../templates/change-request.md) lands or a Must is discovered to be impossible. Do not re-rank in every standup.

## A 20-minute workshop slice

Use this at the end of a discovery workshop, after the outcomes are on the wall. The [gathering guide](requirement-gathering.md) slots it into the last third of a 90-minute session.

1. Read the release constraint out loud: date, people, and what "ship" means. For CutiFlow, ship means the Operations pilot can stop using WhatsApp for annual leave.
2. For each outcome, ask the Must test above. Write the answer next to the item. Argue the test, not the adjective "critical".
3. Move anything that fails the test to Should, Could, or Won't before you discuss effort.
4. Only then ask which Should items are cheap. Cheap does not promote them to Must. It promotes them up the Should list.
5. Read the Won't list back. Ask "whose request is this, and have we told them?"

## Worked example from CutiFlow

The constraint: one pilot department, a two-person HR team, no payroll project running in parallel. Full wording is in the [BRD](../examples/cutiflow/04-brd.md).

| Item | Value | Why this value and not the next one up |
| --- | --- | --- |
| Employee sees remaining annual leave | Must | Without it, people still message HR, which is the problem the pilot exists to stop |
| Supervisor decision recorded with a comment | Must | A chat approval is the current process. Replacing the chat without a record is not a replacement |
| HR second approval for long, unpaid, or special leave | Must | The business rule is a control, not a preference. Shipping without it means HR finds out after the fact |
| Sick-leave attachment hidden from the supervisor | Must | A privacy failure is worse than the workaround they have today |
| Holiday calendar used in the day count | Must | A balance that counts weekends will be rejected in the first week |
| Monthly CSV for payroll | Must | Payroll will not retype from screen, and payroll integration was refused |
| Half-day annual leave | Must, after CR-001 | It was not in the first baseline. Dimas's team would have kept a side channel for Friday afternoons. The change request made the trade-off explicit |
| Substitute approver while the supervisor is away | Should | Real pain, and the volume in a four-week pilot is small enough that HR can live with waiting. It is the first thing in the next release if the pilot proves otherwise |
| Reminder when a request sits for a working day | Should | Useful, and not required for the record to be correct |
| WhatsApp or Slack notification | Could | Email is enough for the pilot. A second channel is how scope quietly doubles |
| Native mobile app | Won't | Browser on a phone is acceptable to the pilot sponsor. An app is a different project |
| Payroll calculation of unpaid leave | Won't | Payroll owns the money. This release owns the record and the export |
| Recruitment or clock-in | Won't | Different processes. Named here because someone will ask |

Notice half-day leave changed value through a change request, not through a quiet edit. That is the practice this repository is trying to model.

## Smells

- **Everything is Must.** Ask which single item, if missing, cancels go-live. The items that would not cancel it are not Must.
- **Must means "my department".** Finance's blackout is a Must for Finance and a configuration, not a reason to block the Operations pilot. In the example the blackout rule is still Must, because it is one configurable rule, not a Finance-only release.
- **Could means "we do not want to say no".** Use Won't.
- **Priority by loudness.** Write the test next to the row so the loudest person has to answer the same question as everyone else.
