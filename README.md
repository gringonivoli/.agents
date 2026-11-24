# Global agent skills

This repository keeps the skills I use across projects in `~/.agents/skills`. Git gives me a history of changes to my workflows and a way to restore the setup on another machine.

## Start here

Browse the [prompt examples](skills/examples.md) by situation. Each example has a prompt you can copy into Codex and adapt to your project.

- Work out open product decisions before implementation. [`$grill-me`](skills/grill-me/SKILL.md)
- Build agreed behavior one failing test at a time. [`$tdd`](skills/tdd/SKILL.md)
- Review and approve an intermediate result before moving to the next phase. Combine this with `$tdd` when a phase changes behavior. [`$phased-delivery`](skills/phased-delivery/SKILL.md)
- Make an intermittent bug repeatable or measure a slowdown before fixing it. [`$diagnosing-bugs`](skills/diagnosing-bugs/SKILL.md)
- Check a committed branch against both the repo’s standards and the originating spec. [`$code-review`](skills/code-review/SKILL.md)

## Repository layout

- `skills/<name>/SKILL.md` defines each skill. Some directories also contain reference material, scripts, or agent metadata.
- The skill lockfile records installation and source metadata for managed skills. [`.skill-lock.json`](.skill-lock.json)

## Maintaining the collection

When changing a skill, review its supporting files and any examples that refer to the changed workflow. Separate commits for upstream updates and local edits make the history easier to follow. When updating an installed skill, review the lockfile change alongside the skill files.

To restore this layout on another machine, place the checkout at `~/.agents` so the skill definitions land in `~/.agents/skills`.
