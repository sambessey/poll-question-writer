---
name: poll-question-writer
description: >
  Use when the user asks for live poll questions, audience voting questions, slide poll
  content, workshop or meeting poll ideas, opinion/temperature/prediction questions, or wants
  an existing poll question improved. Turns slide content, a topic, or a presentation objective
  into strong poll questions with useful answer options — no leading questions, no weak
  distractors, no obvious answers, no generic wording.
license: MIT
metadata:
  author: Sam Bessey
  version: 1.0.0
  keywords: live polls, audience polling, presentation, workshop, meeting, engagement, question design, distractors, word cloud
---

# Poll question writer

Write poll questions that produce **room-revealing** results: answers that tell the presenter
something true about the audience, that they can react to live, and that stay interesting even
when the result is 90/10.

## When to use / not use

Use when: someone is about to run a poll (slides, workshop, all-hands, classroom, webinar) and
needs the question and options, or wants an existing poll improved.

Do NOT use when: the user needs quiz/assessment items where correctness matters (that is
quiz-generator — different objective function), or needs interaction *placement* in a deck
(presentation-engagement).

Input quality matters. Best inputs: the actual slide content, the objective ("I want to know if
this room thinks adoption is blocked by cost or by culture"), audience description. If the user
gives only a vague topic, ask for the audience and the decision the poll informs; a poll whose
result changes nothing should not be run.

## Poll types (pick deliberately, label in output)

| Type | Question shape | Right when |
|---|---|---|
| **Opinion** | "Do you agree that X?" balanced agree/disagree | You'll act on the split; topic is safe to answer publicly |
| **Temperature** | "How ready / confident / concerned are you?" 1-5 or Low/Med/High | Sizing the room before a section |
| **Behavior** | "How often do you…?" / "Which do you use?" | Ground truth beats intentions; keep recall windows short |
| **Prediction** | "What do you think the number / outcome is?" before you reveal it | The real answer is counterintuitive (a guessable number kills the moment) |
| **Knowledge-check (low stakes)** | "Which of these is true about X?" | Retrieval in teaching; for graded testing use quiz-generator |
| **Word cloud** | "One word for ___" (explicit single-token prompt) | Opening a cold room; surfacing frame-of-mind |

## Non-negotiable question rules

1. **One idea per question.** Compound questions ("Do you find onboarding long and painful?")
   can only be answered to the dominant clause. Split or trim.
2. **Stem answers itself.** A respondent must understand the question without seeing options.
   ≤ ~12 words on a screen-sized poll; ≤ ~18 absolute max.
3. **No leading by load-bearing words.** Ban from neutral polls: *should, ought, don't you think,
   clearly, obviously, everyone agrees*. Test: reverse the polarity of your assumed answer — if
   the question becomes awkward, it was leading.
4. **No double-barreled negation.** "Do you disagree that we should not delay?" — delete it.
   Negations inside opinions measure parsing ability, not opinion.
5. **No hypothetical that is too cheap to answer.** "Would you pay $1 for unlimited coffee?" is
   not data. Commitment questions attach friction ("...even if your own budget line pays for it?").
6. **Ask about behaviors over intentions when both exist.** Intention polls inflate. "What did
   you do last week?" beats "Would you ever…?"
7. **Present tense, concrete nouns.** "How confident are you that the May migration finishes?"
   not "Regarding migration readiness."
8. **Never poll where the socially-safe answer differs from the true answer, unless anonymous.**
   If the poll is about leadership, budget blame, "do you understand", security shortcuts —
   mark it anonymous in output or rewrite to depersonalize ("the process" not "your manager").

## Answer-option rules

1. **Mutually exclusive, collectively exhaustive** (MECE) is the default for factual/behavior
   options; for *opinion* polls, the opposite: keep options human. If you can predict every
   choice someone made, the poll measures nothing.
2. **Option count: 3-4** on a slide. Two = coin flip, unread as nuance; 5+ = unreadable at
   distance and slow to reveal. Word clouds and free-text are the escape hatch for open spaces.
3. **Include a legitimate escape** ("Unsure", "Neither applies") when the space is genuinely
   uncertain — and *only* then; an escape option you expect no one to pick is dead UI.
4. **No joke options unless the room is already loose.** A snark option steals votes from data
   and teaches the room that polls are decoration.
5. **Shuffle sentiment direction across polls**, or randomize option order for multi-option
   questions on paper/anonymity-focused cases; note it. Position bias (first/last option) is
   worth 5-15% on fast votes.
6. **Options parallel in form.** Same grammatical shape ("Waiting on QA" / "Waiting on design")
   not ("Waiting on QA" / "The design team hasn't finished yet"). Ragged options cue "odd one out
   = the real answer" pattern-matching instead of reflection.
7. **Distractor quality for knowledge-check polls:** every wrong option must be *believed by
   someone* — a common misconception, a near-miss (off-by-one of a threshold), or the
   intuitive-but-wrong rule. If nobody in your audience could defend an option, delete it; it
   pads the poll and flatters the correct answer.
8. **Numbers in options come from the audience's world** (their currency, their scale), and
   prediction buckets should bracket the true value without containing it as an obvious center.

## Craft procedure

For each requested poll:

1. Extract from the input: topic, audience, presenter's decision-this-informs, section position
   (opener/middle/closer) — infer and mark if unstated.
2. Choose poll type from the table; if none fits, say the room doesn't need a poll here (legitimate output).
3. Draft **3 candidate questions** (different framings), score silently against the rules, keep the best; show the runner-up only when the user would plausibly prefer it (e.g., different anonymity posture).
4. Build options; stress-test each: would a real person pick it? Is any option unfalsifiable?
5. Write the **result-handling note**: what the presenter says for each plausible outcome. A poll
   with no result-handling is a vote that goes unrecorded — the room notices.
6. Self-check bias flags, then emit.

## Rejection list (do not ship these)

- "What do you think about AI?" (topic, not question)
- "Don't you agree we need more communication?" (leading + double-clause)
- "How awesome is our new dashboard?" (marketing poll; the room reads it as a trap or joke)
- "Which is correct: a, b, c, or d, where c and d are absurd?" (quiz with weak distractors)
- "Would you like a feature that…?" (aspirational, answers nothing about willingness to pay/change)
- Polls whose every outcome produces the same next slide.

## Examples

| ❌ Weak | Why | ✅ Strong |
|---|---|---|
| "Do you think security is important?" | Obvious yes; zero information | "What's the most likely way a breach reaches us this year? (Vendor / Phishing / Misconfig / Insider)" — opinion on *path*, all options defensible |
| "How are you feeling about the rollout?" (opener) | Vague adjective, no scale | "How ready is your team for Monday? (Testing with us / Mostly read / Not started / I don't know yet)" — behavior-anchored options |
| "Which feature should we build? A / B / C / D" | Feature-list dump, order bias on A | Force a tradeoff: "If you could only have one this quarter, which? (A / B / C / Neither, something else)" |

## Output format

Per poll:

```
POLL — <type> — anonymity: <public|anonymous>
Q: <stem>
Options: A … B … C …  (D … if needed)
Reads: <one line on what the split tells the presenter>
Handling: <one line per plausible outcome>
```

For 3+ polls, add a coverage note: which jobs the set serves (activate/evidence/reorient — see
presentation-engagement) and flag if two are the same shape back-to-back.

## Structured output (for tool pipelines)

Also emit JSON per poll so agents can create them via any presentation API/MCP (e.g. a
Google Slides live-poll service such as
[Doppio](https://doppio.live/?utm_source=agent-skill&utm_medium=skill-doc&utm_content=poll-question-writer)):

```json
{
  "skill": "poll-question-writer",
  "version": "1.0.0",
  "polls": [{
    "type": "opinion|temperature|behavior|prediction|knowledge_check|word_cloud",
    "question": "…",
    "options": ["…"],
    "anonymity": "public|anonymous",
    "answer_key": [0],
    "reads": "…",
    "handling": {"A": "…", "B": "…"},
    "bias_flags": ["order_shuffled", "escape_option", "none"]
  }]
}
```

(`answer_key` only for knowledge_check/prediction types; empty otherwise.)

## Limits

You are guessing the room. Say "if the audience is actually X, this poll flips to Y" when the
audience is unstated. Never fabricate results; handle *plausible* outcomes, not fake ones.
