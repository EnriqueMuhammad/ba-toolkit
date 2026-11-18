# Change request — CR-[nnn] [short title]

## How to use this template

Raise this when a baselined requirement, rule, or scope item needs to change. Do not edit the BRD first and "mention it" in a meeting. The point of the form is the decision, the options you considered, and the documents you will update if it is accepted.

> **Guidance.** Delete this block before you circulate the request. Keep at least two options besides the one you prefer. "Do nothing" is always one of them.

| Field | Value |
| --- | --- |
| ID | CR-[nnn] |
| Title | [short title] |
| Raised by | [name, role] |
| Date raised | [YYYY-MM-DD] |
| Status | Draft / Under analysis / Accepted / Rejected / Deferred |
| Decision by | [name] |
| Decision date | [YYYY-MM-DD or blank] |
| Baseline affected | [BRD version, story IDs] |

## 1. What is being asked

[The change in plain language. One paragraph. Include an example with real-looking data if a quantity is involved.]

## 2. Why now

[The trigger. Who is blocked, what event exposed the gap, and what happens if you wait until the next release.]

## 3. Options

| Option | Description | Effect on the baseline | Reason to prefer or reject |
| --- | --- | --- | --- |
| A. Do nothing | [Leave the baseline as it is] | None | [what pain remains] |
| B. [Smallest change that solves the trigger] | [description] | [rules and requirements touched] | [recommendation or not] |
| C. [Larger change someone will suggest] | [description] | [what else it drags in] | [why it is or is not in this request] |

Recommended option: [letter]. [One sentence why.]

## 4. Impact if the recommended option is accepted

| Area | Impact |
| --- | --- |
| Business rules | [IDs to add or edit, or "none"] |
| Requirements and stories | [IDs] |
| Process | [which step in the BPMN changes] |
| Data | [new field, new value, or none] |
| Tests | [cases to add or change] |
| People | [who must do something new, or stop doing something] |
| Time and cost | [small / medium / large, with the reason. Do not invent a day count you cannot defend.] |

## 5. Decision

| Decision | Conditions | Documents to update |
| --- | --- | --- |
| [Accepted / Rejected / Deferred] | [conditions, or "none"] | [BRD, FSD, stories, RTM, tests] |

## 6. Trace

After the decision, update the traceability matrix in the same change as the requirement text. A change request that is "accepted" in email and absent from the matrix will be built twice or not at all.
