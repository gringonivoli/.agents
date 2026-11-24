---
name: phased-delivery
description: >-
  Deliver changes in small, verifiable phases with user approval, critical
  review, and concise Gherkin acceptance scenarios. Use only when the user
  explicitly invokes phased-delivery.
disable-model-invocation: true
---

# Phased delivery

Apply this workflow only when the user explicitly requests this skill. Keep it
active for that task across turns until the user changes the agreement. Respect
the host's operating mode, permissions, and the repository's instructions and
relevant technical skills.

## Agree on small phases

Ground the proposal in the relevant implementation, tests, and available data.
Make each phase one bounded, independently verifiable technical step; it may leave
the overall feature incomplete. Separate results that can be reviewed individually
instead of grouping them under a broad milestone such as a complete screen. Keep
implementation, verification, and corrections for the same result together rather
than creating phases per file or test.

Detail only the next phase: its objective, included work, and concrete completion
check. Keep later phases as an adjustable outline of similarly bounded steps,
refining them with what the current phase reveals. Size phases for focused review
and an early opportunity for user steering. A simple task may need only one phase;
do not impose fixed phase counts, file limits, or time budgets.

Present the plan and the first concrete phase before implementing it. A request to
implement an agreed plan authorizes its first phase when the host allows execution;
it does not authorize all subsequent phases. Do not ask again for authorization
that the user has already provided for a clearly scoped phase.

## Complete only the authorized phase

Implement and verify the current phase. Select automated tests and checks that
are proportional to the change and its risks, following the repository's guidance;
this workflow sets no fixed test count. Handle review corrections within the phase
without adding approval checkpoints for individual files, edits, or checks. Raise
material changes to behavior or scope before expanding the agreed work.

If unexpected complexity or newly discovered work makes the current step too
broad, pause further implementation and propose a smaller boundary for the user's
approval. Report what is complete and what remains; do not declare the original
phase complete while agreed work is still pending.

At the phase boundary, report the result, verification performed, limitations, and
any unresolved findings. Propose the next phase concretely and stop for the user's
approval. While waiting, read-only exploration may prepare the proposal, but do
not implement the next phase. Passing tests, reviewer agreement, silence, and
elapsed time are not approval.

Interpret approval in context rather than requiring a fixed phrase. Approval of
a proposed next phase, or acceptance with a clear request to continue, authorizes
that phase. A correction request or acceptance of a completed result alone does
not authorize starting the next phase or unrelated work. A status question does
not cancel the current task; answer it and continue within its authorization.

After the final phase, present the completed work and its verification, request
the user's approval of the result, and stop without generating manual acceptance
scenarios. This also applies to single-phase tasks. If the user requests
corrections, address them within the phase, verify and report the updated result,
and wait for approval again. Treat any explicit change to the approval agreement
as user steering, subject to the host's permissions and operating mode.

## Challenge decisions at useful boundaries

Use independent subagents for critical review of the initial plan and substantive
phase outcomes when their review would materially improve the work and delegation
is available and permitted. Choose the number according to task complexity and
distinct review needs. Ask reviewers to challenge assumptions and compare relevant
alternatives and their tradeoffs. Give each a bounded question and the facts needed
to assess it, without supplying the conclusion to endorse. Do not repeat this
process for every small edit. Keep delegated work within the authorized phase and
its permitted resources.

Use evidence-based discussion to resolve meaningful disagreements. Support findings
with evidence without inventing objections, forcing disagreement, or requiring
consensus. Address relevant findings and verify the result. The primary agent owns
the decisions; reviewers do not authorize phases.

If delegation is unavailable or unjustified, perform critical self-review. When
independent review would matter, disclose its absence. Do not label self-review
independent or ask for extra permission solely because subagents are unavailable.
Keep all user approval checkpoints. Do not install delegation tooling merely to
satisfy this workflow.

## Provide concise functional acceptance scenarios

Generate manual Gherkin scenarios only after the requested functionality is
complete and the user has approved the results of every phase, including the
final phase. Authorization to implement a phase is not approval of its result.
Once all results are approved, provide the scenarios directly using
[the shared scenario guidelines](../gherkin-scenarios/references/scenario-guidelines.md),
without inventing another phase or requesting separate authorization.

Keep automated tests and technical verification within each phase. Do not repeat
manual acceptance scenarios at every internal implementation phase or force them
onto documentation-only work or internal refactors with no behavior change.

Read the file as passive authoring guidance, not as an invocation of another skill.
Keep this workflow's phase approvals and review process. If the guide is missing,
report the unavailable dependency rather than claiming to have applied it.

## Keep the workflow portable

Use the current host's native capabilities and the project's technical guidance;
do not depend on a particular provider, tool API, language, or repository. Do not
impose worktrees, branch names, commits, deployment, or infrastructure steps merely
because this skill is active. The workflow does not expand the task's scope or
execution permissions.
