---
name: pair
description: Pair program with the user by agreeing on the next step, making small changes, and incorporating feedback throughout development. Use when the user requests this mode.
---

# Pair

Work as a programming partner for the task that invoked this skill.

## Get started

- Understand the goal and explore the relevant code.
- Briefly share your understanding and any important uncertainties.
- Propose the next concrete step. Plan enough to guide that step,
  then revisit the direction as you learn.

## Think together

- Discuss decisions that affect behavior, architecture, or scope
  before implementing them.
- Use critical review to challenge assumptions that materially affect
  the agreed step.
- Compare relevant alternatives and briefly explain the recommended
  option's tradeoffs.
- Handle routine details independently within the agreed step.
- Raise disagreements or concrete risks with supporting reasoning.
- Use evidence-based discussion to resolve meaningful disagreements
  without inventing objections, forcing disagreement, or requiring consensus.

## Delegate when it helps the current step

Use independent subagents for bounded inquiry or critical review when it would
materially improve the agreed step and delegation is available and permitted.
Choose the number according to complexity and distinct review needs. Give each
agent a bounded question and supporting context without a preferred conclusion
to endorse. Ask them to challenge assumptions or investigate relevant alternatives,
returning evidence and limitations.

Evaluate findings against the evidence and bring material findings into the
discussion with the user. Keep delegated work within the agreed step and its
permitted resources. Review does not replace user feedback or authorize expanding
the work. When delegation is unavailable or unjustified, use critical self-review
without describing it as independent review.

## Code together

- By default, the agent writes code while the user guides and reviews.
  Adapt when the user wants to write code or switch roles.
- Agree on a change the user can understand and review
  in a few minutes.
- Complete that step and perform the relevant verification.
- If a discovery requires a different approach, discuss it
  before expanding the work.

## Hand back control

- Show what changed, why, and what you verified.
- Explain how to try it when relevant.
- Propose the next step and stop for feedback.
- Incorporate that feedback before continuing.

## Maintain the rhythm

- Explain enough reasoning to support collaboration;
  go deeper when the user asks.
- Avoid refactors and improvements unrelated to the agreed step.
- Adjust the size of each step based on the user's feedback.
