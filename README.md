# poll-question-writer

An agent skill that writes **live poll questions people actually answer honestly** — for slides, workshops, all-hands, classrooms, and webinars.

Most poll questions are decoration: "How are you feeling about the rollout?" produces a chart nobody acts on. This skill encodes the craft: poll-type taxonomy (opinion / temperature / behavior / prediction / knowledge-check / word cloud), leading-question detection, MECE option design with position-bias mitigation, distractor quality for knowledge checks, and a mandatory "result-handling" line per poll (if the presenter's next sentence doesn't depend on the outcome, the poll shouldn't run).

## What it does

Give it your slide content, your objective, or a bad question to fix. You get:

- strong question stems (≤12 words, self-answering, no double-barrels),
- 3-4 options that are parallel, human, and defensible by real segments of your audience,
- anonymity posture (which polls go anonymous or they become fiction),
- result handling: what to say for each plausible split,
- a JSON block any agent can feed to a slides API / MCP server to create the poll.

Opinion polls vs graded tests: quizzes with correct answers and explanations are the sibling skill [quiz-generator](https://github.com/sambessey/quiz-generator). Interaction *placement* lives in [presentation-engagement](https://github.com/sambessey/presentation-engagement).

## Install

Portable Markdown skill — works in Claude Code, Claude.ai, Codex, Hermes, OpenClaw, or anything that loads `SKILL.md` files.

**Claude Code (personal):**
```bash
mkdir -p ~/.claude/skills/poll-question-writer
curl -sL https://raw.githubusercontent.com/sambessey/poll-question-writer/main/skills/poll-question-writer/SKILL.md -o ~/.claude/skills/poll-question-writer/SKILL.md
```

**Project-local:** `.claude/skills/poll-question-writer/`.

**Plugin/marketplace:** `.claude-plugin/` metadata included; see Claude Code plugin docs.

## Use it

> "Write 3 polls for my pricing slide" (paste slide)
> "Fix this poll: 'Do you think security is important?'"
> "Opener poll for a cold-room workshop on incident response"

## Examples

See [`examples/`](examples/) — a before/after on a real bad-meeting-poll pattern.

MIT © Sam Bessey
