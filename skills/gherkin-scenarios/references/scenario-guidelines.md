# Manual Gherkin scenario guidelines

These are passive authoring criteria. They do not activate another skill, create
approval checkpoints, or authorize implementation or test execution.

## Establish the expected behavior

Identify the requested functionality from the task and conversation. Inspect the
relevant requirements, implementation, tests, and available data as needed; do not
expand the review to unrelated features. Ask only when an unresolved ambiguity
changes the expected outcome or prevents a usable scenario.

Use confirmed requirements as the expected behavior. If the implementation
contradicts them, explain the discrepancy rather than turning the existing
behavior into a requirement. Distinguish acceptance criteria from checks of what
currently exists. If only a specification is available, identify the scenarios as
specification-based instead of implying that the implementation was inspected.

## Select meaningful coverage

Size the set to the requirements and risks, with no fixed minimum or maximum.
Cover the main flows, relevant variants, and meaningful boundaries or failures.
Each case should protect a distinct behavior or boundary. Avoid redundant cases
and exhaustive combinations that add no useful confidence; do not combine
unrelated behaviors merely to reduce the scenario count or invent artificial
edge cases.

## Make the scenarios usable

- Prefer existing fixtures or fake sources when available. Verify which data are
  available in the target environment; do not present a test-only fixture as data
  that a user can find in the running application.
- Check the actual identifiers, visible labels, and available user actions before
  choosing steps. Do not ask a tester to edit a read-only field or use an interface
  that is not available for the requested kind of test.
- If suitable data are absent, identify the limitation and propose explicit setup
  data without claiming that they already exist. If a requested boundary is
  inaccessible, explain the required setup or offer a reachable alternative while
  preserving the distinction. Do not modify sources to manufacture the case.
- State the preconditions that affect the result and how to restore the starting
  state when cases would otherwise affect each other. Use a known reset mechanism;
  if none is known, identify the required restoration instead of inventing a
  command or endpoint. Avoid setup ceremony that adds no value to a simple case.
- Verify calculations, units, dates, and rounding when they affect the result.
  Distinguish raw input values from displayed formatting and respect the observed
  precision of the interface. Do not guess expected values that depend on missing
  information.
- Assert observable outcomes at the requested boundary, such as UI values,
  messages, enabled actions, or API responses. Avoid assumptions about internal
  methods or storage that the tester cannot observe.

## Write and present the scenarios

Use English Gherkin keywords and Spanish narrative. Preserve real identifiers,
UI labels, commands, and other literal values even when they are not Spanish.
Use `Feature`, `Background`, tables, and `Scenario Outline` only when they improve
clarity; keep each scenario focused on a meaningful behavior.

Return fenced `gherkin` with concise steps. Add only the context needed to prepare,
repeat, and interpret the cases. Do not generate automation glue or test code
unless requested. These manual acceptance scenarios do not replace automated
tests.

Distinguish proposed scenarios from tests or manual checks actually executed, and
observed evidence from assumptions or required setup. Do not imply that unfinished
behavior has been implemented or verified.
