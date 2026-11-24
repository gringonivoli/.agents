# Codex prompts for everyday development

Find the situation that matches your work, then copy the quoted prompt into Codex. Replace the example feature, file, branch, or pane name with your own.

## Plan and design

### A ticket leaves product decisions open

> Use `$grill-me` on “Add CSV export.” Read the ticket and inspect the existing filters and permissions. Ask me about decisions that would change the behavior, and recommend an answer for each. Start with which rows to export, who can export them, and what happens when there are zero results.

`$grill-me` starts `$grilling`, which asks you questions in rounds. Once you’ve settled the decisions, use them as acceptance criteria for implementation.

### The team needs to agree on how to handle failures

> Use `$grill-me` on replacing our nightly customer import. Inspect the current job and its callers. Help me decide how to handle partial failures, reruns, and rollback. Give me your recommended answer and the reason for each open decision.

### You need evidence to choose a technical approach

> Use `$research-and-learn` to compare a database-backed job queue with our current scheduler for invoice generation. Read the existing job code and relevant official documentation. Compare retry behavior, duplicate execution, and operational cost under our workload. Recommend an approach and identify which assumptions we can verify locally.

### Several callers need to know the same rules

> Use `$codebase-design` to review how callers build report filters. Trace two real callers and show which rules each has to know. Propose a smaller interface, illustrate it with a before-and-after call, and explain which behavior could be tested through that interface.

### You want to choose a design and make the first change together

> Use `$pair` and consult `$codebase-design`. Each checkout caller applies discount rules differently. Inspect two real callers, propose where the shared rules should live, and show how one caller would use the interface. Let’s agree on the first small change before editing.

## Implement and debug

Start with a test when you can describe the expected result and how to observe it. If a bug is intermittent or you’re investigating a slowdown, start by making the problem repeatable or measurable. A *test seam* is where the test exercises the behavior, such as a screen or a public function.

### You know how a new behavior should work

> Use `$tdd` to preserve the selected date range when a user switches reports. Propose the public interface where you’d test it and confirm it with me. Then write one failing test for the behavior and make the smallest change that passes it.

### You can reproduce a bug and know what should happen

> Use `$tdd` to fix the invoice report that excludes invoices dated on the selected end date. I can reproduce it by selecting May 1 through May 31 with an invoice dated May 31. Propose a test through the report query interface and confirm that seam with me. Then show that the regression test fails before the fix and passes afterward.

### A bug comes and goes

> Use `$diagnosing-bugs`. The invoice list sometimes shows duplicate rows after I change filters quickly. Build a repeatable check for the symptom, narrow down the cause, and rerun the original reproduction after the fix.

### A report has become slower

> Use `$diagnosing-bugs` on the monthly invoice report. With the local fixture of 10,000 invoices, it takes about four seconds to return. Establish a repeatable baseline, identify where the time goes, and use the same fixture to measure the result after the fix.

### You want to steer a refactor one step at a time

> Use `$pair` to simplify the invoice editor’s state handling. Trace what happens when a user edits a line item, then propose one small change we can verify together. Wait for my agreement before editing and show me the result before proposing the next step.

### You want to approve intermediate results on a larger feature

> Use `$phased-delivery` and `$tdd` to add saved report filters. Outline the work and detail the first independently verifiable phase. Include its completion check and proposed test seam so I can approve both together. My first priority is saving and restoring one filter through the existing report screen.

### You’ve reviewed a phase and want the next one to start

Send this as a follow-up in the active task after reviewing the completed phase and the proposed next one.

> I approve the save-and-restore result. Continue with the proposed phase to rename a saved filter. I confirm the saved-filter controls on the report screen as the test seam. Verify that the new name appears when I reopen the report.

## Review and prepare manual QA

### Your committed branch is ready for review

> Use `$code-review` on the committed changes since `main`. Use `docs/saved-filters.md` as the spec. Report standards and spec findings separately, with file and line references. Pay particular attention to how existing saved filters behave after the change.

### Someone needs manual QA cases for an existing feature

> Use `$gherkin-scenarios` for CSV export. Ground the cases in the approved ticket and the current UI. Cover exporting filtered rows, zero results, and permissions. Include any setup a tester needs.

### QA wants to prepare cases from a spec

> Use `$gherkin-scenarios` to draft manual cases from `docs/invoice-import.md`. Cover valid files, rejected rows, and retrying a partial import. Mark the cases as specification-based and call out any test data or app behavior the spec leaves unresolved.

## Keep work moving between sessions

### You need to resume work in a fresh session

> Use `$handoff` so I can continue the saved-filters work in a fresh session. Include the current branch, the decisions we confirmed, the last passing check, and the first task the next agent should pick up. Link to the existing spec and diff.

### You’ve lost the thread of the conversation

> `$wait-what`. I’ve lost track of the import fix. Explain the original symptom, what you’ve confirmed so far, and which decision is in front of me. Use the domain terms in `GLOSSARY.md`.

### The session exposed a problem you keep running into

> Use `$retro` on this session. Find the two places where we did the most avoidable rework. For each, cite what happened and propose one concrete improvement to the repo’s checks or guidance. If `writing-for-agents` is unavailable, use the repository’s existing writing guidance.

### You’re looking for a skill you could reuse

> Use `$find-skills` to look for a skill that audits accessibility in a local React app. Compare the strongest candidates by what they check, how they fit our existing test workflow, and what permissions they need. Give me a shortlist with sources and installation commands.

## Work with terminal panes

### You want to run tests in another Herdr pane

> Use `$herdr` to run the repo’s documented test command in a sibling pane on the right. Keep focus in this pane. Wait for the result and summarize any failing tests.

### You want to check a build in another tuios pane

> Use `$tuios` to inspect the `build` pane in this session. Tell me whether the build is still running, waiting for input, or finished. If it failed, report the first actionable error and the command that produced it.
