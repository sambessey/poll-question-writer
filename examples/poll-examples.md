# Examples: poll-question-writer

## Example 1 — meeting poll for a migration planning all-hands (audience: engineers, 120 people)

**User input:** "We're moving auth to a new provider in Q3. I want a poll before the technical section. Meeting room with screens, everyone can vote from their phone."

**Skill output:**

```
POLL — behavior — anonymity: public
Q: How much of your service traffic hits our legacy auth today?
Options: A Almost none (migrated already)  B Some (mixed)  C Most  D No idea / doesn't apply to me
Reads: Real migration surface per team, not estimates from the plan doc.
Handling:
  A dominant → acknowledge early adopters by name in the next 2 minutes, then pivot to the C/D room's blockers
  C dominant → the rollout-timeline slide becomes the talk; slow down here
  D > 25% → add a "find your services" office-hours ask before Q&A
Bias flags: none (option order fixed, no escape-option padding)
```

```
POLL — opinion — anonymity: anonymous
Q: What would most likely break first in the Q3 cutover?
Options: A Session/token compatibility  B Legacy client SDKs  C Rate limits at the new provider  D Our own monitoring can't see the new path
Reads: Where the room believes risk actually lives — feeds directly into the rehearsal plan.
Handling: Name the top choice in the risk slide ("you said B — here's what we did about it"). If it's none of these via write-in volume, take the best write-in verbatim.
Why anonymous: blaming another team's SDK publicly distorts answers (rule: socially-safe vs true).
```

Note what got *rejected* during drafting: "Do you feel confident about the migration?" (temperature, but it invites performative optimism, and its result changes nothing), and "Is our auth provider the right choice? Yes/No" (binary opinion on a decided decision = fake democracy).

## Example 2 — fixing a bad existing poll (the common meeting-host pattern)

**User input:** "Fix this: 'How are we feeling about the big launch?' Options: 🚀 / 😅 / 😬"

**Skill diagnosis:** vague adjective stem; emoji options can't be acted on; the three-way mood split has no distinct handling per bucket; sets a norm that polls are decoration.

```
POLL — temperature — anonymity: public
Q: How ready is your team for launch day?
Options: A Ready to go  B One thing left (name it in chat)  C Not started  D Blocked and waiting on someone
Reads: A/B/C/D map to concrete next actions; B and D are the operational gold.
Handling: If D > 15%, the block-resolution slide moves before the roadmap slide; if C spikes, close with the 30-day support plan, not the vision slide.
```

## Example 3 — word-cloud opener, cold-room conference talk (~200 people)

```
POLL — word_cloud — anonymity: anonymous
Q: One word for how "customer data platform" makes you feel.
Reads: Surface the room's frame of mind (skepticism, boredom, hope) in 20 seconds; low-stakes so the quiet 60% still participate.
Handling: Screenshot the cloud for slide 2's callback ("half this room said 'acronym' — fair, let's make 30 minutes worth it").
```

## Example 4 — knowledge-check poll (teaching context)

```
POLL — knowledge_check — anonymity: public
Q: A user clicks "export all data." Which rule applies?
Options: A Any org admin can export  B Only the account owner, with 2FA, to their verified email  C Exports require legal sign-off  D Only at quarter-end
Answer: B
Reads: Retrieval on the security model just taught; the wrong options are the three real misconceptions from last quarter's incidents.
Handling: ≥70% correct → keep moving; <50% → the export section needs a re-teach now, not at the end.
```

Distractors argued: A = what admins *wish*, C = what they've been told by legal in another workflow, D = a stale policy many still remember.
