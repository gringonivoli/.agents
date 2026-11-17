---
name: gherkin-scenarios
description: >-
  Draft manual Gherkin acceptance scenarios for a requested functionality,
  grounded in requirements and available evidence. Use only when the user
  explicitly invokes gherkin-scenarios.
disable-model-invocation: true
---

# Gherkin scenarios

Use this skill only when explicitly requested. Handle the scenario-authoring
request directly, without introducing implementation phases, an implementation
plan, or approval checkpoints. Any existing approval agreement for implementation
still applies; requesting scenarios does not authorize advancing that work.

Read [the scenario guidelines](references/scenario-guidelines.md) before drafting.
They define the shared authoring criteria. Report a missing reference rather than
claiming to have applied guidance that could not be read.

## Review the candidate scenarios

Use independent subagents for critical review of relevant coverage and the
feasibility and clarity of the data and steps when their review would materially
improve the work and delegation is available and permitted. Choose the number
according to task complexity and distinct review needs. Ask reviewers to challenge
unsupported assumptions and suggest alternatives in scenario selection or wording
when useful. Give them bounded questions, the request, and supporting evidence
without supplying a conclusion or case count to endorse. Reuse a review that
already covers these scenarios in an active workflow instead of duplicating it.

Use evidence-based discussion to resolve meaningful disagreements, grounding
findings in the requirements and evidence without inventing objections, forcing
disagreement, or requiring consensus. The primary agent owns the final scenario
selection and wording. Do not require user approval of intermediate drafts unless
requested. If delegation is unavailable or unjustified, perform critical self-review.
When independent review would matter, disclose its absence; do not describe
self-review as independent or ask for extra permission solely because subagents
are unavailable.

## Keep the request within scope

Authoring may use read-only inspection and calculations to establish expected
results. Invoking this skill alone does not authorize product implementation,
fixture or database changes, test execution, or output files. Those actions need
a request that includes them. Do not install delegation tooling merely to provide
an independent review.

Return the scenarios in the response, together with only the setup, limitations,
and evidence needed to use them. Respect the host's operating mode, permissions,
and relevant project instructions; do not assume a particular provider or stack.
