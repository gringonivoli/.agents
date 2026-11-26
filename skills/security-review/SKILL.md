---
name: security-review
description: Review code changes for security vulnerabilities (injection, auth flaws, exposed secrets, unsafe dependencies) and report ranked, actionable findings. Use when the user asks for a security review or audit, or before merging changes that touch auth, input handling, data access, or dependencies.
---

# Security Review

Find real, exploitable security problems in a set of changes and report them so the user can act on each one. Precision beats coverage: one confirmed finding is worth more than ten speculative ones.

This skill uses only git, a shell, and file reading. It works the same in any agent harness and with any model.

## Ground rules

- **Read-only.** Don't edit code, commit, or install anything unless the user asks. Suggest fixes; don't apply them.
- **Never attack anything live.** Don't send exploit payloads to running services, real APIs, or production data. Reason from the code, or use a local test if the user approves.
- **Redact secrets.** If you find a credential, show its location and type, never its value: write `<REDACTED>`.
- **The repo's own rules win.** If the repo documents a security policy, follow it, and suppress a check here that the policy explicitly accepts.

## Process

### 1. Pin the scope

Use what the user gave you: a commit, branch, tag, path, or "the whole repo". If they gave nothing, review the current branch against its merge-base with the default branch:

```sh
base=$(git merge-base HEAD origin/main 2>/dev/null || git merge-base HEAD main)
git diff "$base"...HEAD --stat
git diff "$base"...HEAD
```

Include uncommitted work too (`git diff HEAD`). If the diff is empty, or the ref doesn't resolve, stop and say so.

For a whole-repo audit, start with the entry points (routes, handlers, CLI commands, message consumers) and follow untrusted data inward, instead of reading files in order.

### 2. Gather context

- Read any `SECURITY.md`, `CONTRIBUTING.md`, `CODING_STANDARDS.md`, `AGENTS.md`, or `CLAUDE.md` for security rules.
- Identify the stack, the trust boundaries (where untrusted input enters), and the auth model.
- For each changed function, read enough surrounding code to know whether its inputs can be attacker-controlled. A dangerous sink fed only by constants is not a finding.

### 3. Check the changes

Work through each category that applies to the diff. Skip the ones that clearly don't.

- **Secrets:** hardcoded keys, tokens, passwords, or private keys; secrets in logs, error messages, or client bundles; `.env` files committed.
- **Injection:** SQL or NoSQL built by string concatenation; shell commands built from input; template injection; LDAP or XPath injection; `eval` and similar functions applied to input.
- **Path and file handling:** path traversal (`../`) in file reads, writes, or archive extraction; unrestricted uploads (type, size, storage location).
- **Authentication:** missing auth on new routes or handlers; weak session or token handling; tokens without expiry; comparing secrets with a non-constant-time check.
- **Authorization:** object access without an ownership check (IDOR); privilege checks only on the client side; mass assignment of fields like `role` or `isAdmin`.
- **Web:** XSS (unescaped output, `innerHTML`, `dangerouslySetInnerHTML`); CSRF on state-changing requests; permissive CORS (a wildcard origin with credentials); open redirects.
- **Server-side requests:** SSRF from fetching user-supplied URLs; unsafe deserialization (`pickle`, unsafe YAML loaders, Java serialization).
- **Crypto:** home-made crypto; MD5 or SHA-1 for passwords; non-random IVs; `Math.random()` or similar for tokens; TLS verification disabled.
- **Dependencies:** new or upgraded packages in lockfiles. Run the stack's audit tool if it's already available (`npm audit`, `pnpm audit`, `pip-audit`, `cargo audit`, `govulncheck`, `bundle audit`). Flag typosquat-looking names and install scripts.
- **Config and infra:** debug mode on; verbose errors exposed to users; overly broad IAM, file, or container permissions; secrets in CI config; Dockerfiles running as root.
- **Data exposure:** sensitive fields returned by APIs or written to logs; personal data handled without need.
- **Concurrency and logic:** check-then-act races on balances, quotas, or unique resources; missing rate limits on login, OTP, or password reset.

### 4. Verify each candidate

Before you report a finding, confirm it:

1. **Source:** can an attacker control the input? Trace it back.
2. **Sink:** does it reach a dangerous operation without effective sanitization or validation on the way?
3. **Impact:** what can an attacker actually do?

If you can't confirm all three, either drop the candidate or report it as **Needs check** with the specific question that would settle it. Don't pad the report.

### 5. Report

Order findings by severity: **Critical**, **High**, **Medium**, **Low**, then **Needs check**. For each finding:

```
### [Severity] Short title
- Where: path/to/file.ext:LINE
- Issue: one or two sentences on what is wrong.
- Exploit: concrete attacker input or steps, and the result.
- Fix: the specific change, with a short code snippet if it helps.
```

End with a one-line summary: how many findings at each severity, and which categories you checked and found clean.

If you find nothing, say so plainly and list what you checked. "No findings" is a valid result.

## Optional: parallel review

If your harness can run sub-agents with fresh context, you can split step 3 across them (for example, one for injection and input handling, one for auth and authorization, one for secrets, dependencies, and config). Give each one the same scope and these rules, then merge their findings, removing duplicates, before step 4. If your harness can't, do the steps in order yourself. The result should be the same.
