# Ankit's Global Claude Code Rules

## Session Start — Do This First (Every Session, No Exceptions)

### 1 — Self-install knowledge book infrastructure

Check if `KNOWLEDGE.html` exists in the project root.
Check if `.claude/skills/session-knowledge-doc/SKILL.md` exists in this repo.

**If the skill is MISSING:**
1. Fetch from `apverse-labs/dotfiles` →
   `.claude/skills/session-knowledge-doc/SKILL.md` via GitHub MCP, write to
   the same path in this repo.
2. Also fetch `.claude/skills/session-knowledge-doc/references/session-block-template.md`
   and `.claude/skills/session-knowledge-doc/references/shell-template.md`
   the same way.
3. Commit:
   ```
   git add .claude/skills/session-knowledge-doc/
   git commit -m "chore: install knowledge book skill"
   git push
   ```

### 2 — Self-install coding standards (always-on)

Check if `.claude/skills/coding-standards-enforcer/SKILL.md` exists in this repo.

**If MISSING:** fetch from `apverse-labs/dotfiles` →
`.claude/skills/coding-standards-enforcer/SKILL.md` via GitHub MCP, write to
the same path here, commit and push. Then apply its standards (inline
documentation + structured logging + change log updates) to all code
written for the remainder of this session — not just when explicitly asked.

```
git add .claude/skills/coding-standards-enforcer/
git commit -m "chore: install coding standards skill"
git push
```

### 3 — Debugging posture (standing instruction, not just session-start)

Whenever the user reports something broken, failing, or erroring — or
pastes an error message — this triggers the `debug-root-cause` skill's
discipline, not just when `/debug-root-cause` is typed explicitly.

Check `.claude/skills/debug-root-cause/SKILL.md` exists in this repo. If
missing, fetch from `apverse-labs/dotfiles` →
`.claude/skills/debug-root-cause/SKILL.md` via GitHub MCP, write here,
commit and push. Then follow it: never propose a fix based on a paraphrased
symptom alone — get real evidence first, every time.

### 4 — Create the knowledge book if missing

Check if `KNOWLEDGE.html` exists in the project root:
- **If YES:** Read it to understand project history. Continue.
- **If NO:**
  1. Read `git log --oneline -20`, `SYSTEM_STATE.md`, `SESSIONS.md`,
     `README.md` to understand what has been built.
  2. Create `KNOWLEDGE.html` from the shell template at
     `.claude/skills/session-knowledge-doc/references/shell-template.md`.
  3. Document the current state as Session 1.
  4. Commit and push:
     ```
     git add KNOWLEDGE.html
     git commit -m "docs: initialise knowledge book"
     git push
     ```

### 5 — Read project state

- Read `KNOWLEDGE.html` if it exists. Use it to understand:
  - What has already been built
  - What session number we are on
  - What was planned for this session
- Do not ask Ankit to re-explain project history. Read the knowledge book first.

---

## Session End — Do This Every Time Code, DB, Config, or Files Were Touched

1. Update `KNOWLEDGE.html` by injecting this session's content at the
   injection points, using `.claude/skills/session-knowledge-doc/SKILL.md`
   for the exact steps, templates, and HTML structure. Read it before
   writing anything. Do NOT rewrite the whole file.

2. Commit the updated knowledge book:
   ```
   git add KNOWLEDGE.html
   git commit -m "docs: S[N] knowledge book — [one-line summary]"
   git push
   ```

3. If `general/changelog.md` exists and this session made any non-trivial code
   change, add an entry under `[Unreleased]` (per `coding-standards-enforcer`).

When Ankit says "document what we built" or "wrap up" — this is what it means.

---

## My context

- I am a non-technical AI PM. Write all documentation in plain English.
- No jargon in explanations. Explain like I am smart but not a coder.
- I work in GitHub Codespaces / Claude Code web. The project repo is the
  working directory.
- When I say "document what we built" or "wrap up" — that means update
  `KNOWLEDGE.html`.

## Code style (applies when no project-level CLAUDE.md overrides this)

- Prefer simple over clever.
- Add plain-English comments on any non-obvious logic (see
  `coding-standards-enforcer` skill for the full documentation standard).
- Never silently delete or overwrite files — confirm first.
- Use the project's structured logger, never raw `console.*` calls, once
  `/install-logging` has been run (see `coding-standards-enforcer`).
- All audit and hygiene reports write to `ops/audits/[skill-name]/` —
  keep this folder per-skill so findings are traceable over time.
- Incident reports write to `ops/incidents/`.
- Session transaction logs write to `ops/logs/session-log/`.
- Before reading code to discover a contract, spec, or flow — check
  `knowledge-book/` first. If a relevant doc exists there, treat it as
  the stated intent and compare code against it, rather than inferring
  intent from code alone.

---

## Why some skills auto-run and others don't

| Skill | Trigger | Runs automatically? |
|---|---|---|
| session-knowledge-doc | Session start | Yes — every session |
| coding-standards-enforcer | Session start | Yes — every session |
| debug-root-cause | Natural language ("this is broken") + `/debug-root-cause` | Yes — on debugging intent |
| All `/audit-*`, `/hygiene-*`, `/install-*`, `/incident-*` skills | Explicit slash command | No — explicit only |

**Design principle:** Always-on = cheap to apply continuously, expensive to
retrofit later (documentation, logging discipline, knowledge book entries,
evidence-based debugging). On-demand = consequential changes that need a
deliberate human decision to trigger (dependency removal, security policy
changes, secret rotation, compliance findings, production deploys).

Documentation and debugging discipline should happen passively, every time,
with no effort. Audits and hygiene fixes change real code and data — they
should only ever run when a developer deliberately asks for them.

---

## Skill installation pattern (applies to every skill below)

Every skill listed below follows the same install pattern unless otherwise
noted:

1. Check if `.claude/skills/[skill-name]/SKILL.md` exists in this repo.
2. If missing, fetch it from `apverse-labs/dotfiles` →
   `.claude/skills/[skill-name]/SKILL.md` via GitHub MCP, write it into the
   same path in this repo, commit and push.
3. Read and follow that skill file exactly.

Skills with a `references/` folder (currently: `session-knowledge-doc`,
`install-logging-infrastructure`) need their reference templates fetched
the same way, preserving the folder structure.

---

## Audit skills — data, security & infrastructure

### /audit-deps — Dependency & Security Audit
**Purpose:** npm/pnpm/yarn vulnerability scan, unused packages, duplicate
functionality, Expo/framework SDK compatibility.
**Dependencies:** `package.json` present. GitHub MCP for first install.
**Auto-fixes:** Yes, on confirmation.

### /audit-edge-functions — Edge Function Error Boundaries Audit
**Purpose:** Every backend function checked against the project's own error
standard — auth, DB errors, external API failure, empty/null handling, timeouts.
**Dependencies:** Backend functions in a recognised location. Supabase MCP
if redeploying. Ideally an architecture/API standards doc exists.
**Auto-fixes:** Yes, on confirmation.

### /audit-rls — RLS Policy Correctness
**Purpose:** Every table's Row Level Security policies verified as correct,
not just enabled — catches silent zero-access and cross-user data leaks.
**Dependencies:** Supabase MCP (queries `pg_policies`/`pg_tables` directly).
**Auto-fixes:** Yes, on confirmation.

### /audit-data-integrity — Data Integrity Checks
**Purpose:** FK violations, orphaned records, NULL/empty fields that cause
silent application failures.
**Dependencies:** Supabase MCP.
**Auto-fixes:** Partial — auto-fixes only when violation count < 5; larger
counts flagged for manual review.

### /audit-eas — Expo & EAS Pre-Submission
**Purpose:** app.json/app.config audit, EAS build profiles, permissions,
OTA update config — pre-App-Store/Play-Store checklist.
**Dependencies:** Must be an Expo project (self-checks and exits if not).
`eas` CLI for build:inspect.
**Auto-fixes:** Partial — config only.

### /audit-performance — Performance Baseline
**Purpose:** Measures actual performance against the project's own
documented NFR targets — does not invent thresholds.
**Dependencies:** A documented performance/NFR target doc. Asks the user for
targets if none found, rather than guessing.
**Auto-fixes:** No — measurement only.

### /audit-prelaunch — Pre-Launch Checklist Automation
**Purpose:** Turns the project's own documented pre-launch checklist into a
programmatic PASS/FAIL report; flags non-automatable items as MANUAL.
**Dependencies:** A pre-launch checklist doc somewhere in the repo. Asks
which doc/section if ambiguous or multiple candidates found. Supabase MCP
for DB-backed items.
**Auto-fixes:** No — verification only.

### /audit-dpdp — DPDP Legal Compliance
**Purpose:** India DPDP Act 2023 compliance — sensitive data in third-party
analytics, consent flow completeness, data subject rights (export, deletion,
audit retention).
**Dependencies:** Supabase MCP.
**Auto-fixes:** **NEVER — report only, even on explicit "just fix it"
request.** Compliance findings always require human/legal review before any
code change.

### /audit-api-contract — API Contract Audit
**Purpose:** Verifies frontend and backend agree on request/response shapes
— catches client/backend drift from separate editing sessions.
**Dependencies:** Project must have both client and backend code with
discoverable call sites; self-checks and exits if not applicable.
**Auto-fixes:** Yes, on confirmation per side (backend or client, whichever
is actually wrong).

### /audit-onboarding-funnel — Onboarding Funnel Audit
**Purpose:** Walks the actual onboarding/first-run code path, flags every
point a user could silently drop off — validation traps, infinite loaders,
dead-end error states, broken resume logic.
**Dependencies:** A discoverable onboarding/first-run flow; self-checks and
exits if not applicable.
**Auto-fixes:** Yes, on confirmation for CRITICAL/HIGH findings.

### /audit-rollback-readiness — Rollback Readiness Audit
**Purpose:** Before a risky deploy, verifies a real rollback path exists —
migration Down scripts, redeployable previous version, feature flag coverage.
**Dependencies:** Most useful with a documented branch/deployment convention
(`SYSTEM_STATE.md` or equivalent); works without one but asks the user to
identify the production branch manually.
**Auto-fixes:** **Report only** — does not execute deploys, does not modify
migrations without explicit confirmation.

---

## Hygiene skills — code quality & secrets

### /hygiene-deadcode — Dead Code Removal
**Purpose:** Finds unused functions, variables, commented-out blocks, stale
console.logs, orphaned files.
**Dependencies:** None beyond repo access.
**Auto-fixes:** Yes, on confirmation — always shows the report first.

### /hygiene-secrets — Secrets Hygiene Audit
**Purpose:** Maps every secret across env files and configs, flags
hardcoded values in source.
**Dependencies:** None beyond repo access.
**Auto-fixes:** **Never — report + rotation advice only.** Never prints
actual secret values anywhere, including its own output.

### /hygiene-testsync — Test-App Sync
**Purpose:** Keeps a test/mirror module of business logic synced with the
real source of truth — catches drift in scoring weights, constraint rules,
type definitions.
**Dependencies:** Project must have a separate test-mirror of business
logic; self-checks and exits if not applicable.
**Auto-fixes:** Yes, once the source-of-truth/mirror direction is confirmed
by the user.

### /install-logging — Logging Infrastructure Installer
**Purpose:** Scaffolds the org-standard logging stack — System Logger, User
Journey Logger (if user-accounts exist), lightweight client logger,
transaction export script (if DB-backed events exist), CHANGELOG.md. Re-run
anytime as a compliance check instead of reinstalling.
**Dependencies:** None to install. Supabase MCP if scaffolding the
transaction export script.
**Auto-fixes:** Scaffolds infrastructure directly; for compliance-check mode
(replacing raw `console.*` calls project-wide), asks before mass-applying.

---

## Debugging & reliability skills

### /debug-root-cause — Root Cause Debugging Discipline
**Purpose:** Forces evidence-based debugging — reproduce with real output
before proposing a fix, check every system layer in order, state the root
cause as a falsifiable claim with confirming evidence, re-verify the
original failing scenario after fixing (not just typecheck/tests).
**Trigger:** Also activates on natural language ("X is broken"), not just
the slash command — see Session Start §3.
**Dependencies:** None required. Most effective with a logger and
`logs/hygiene-reports/debug-log.md` history already in place.
**Auto-fixes:** Yes, but strictly scoped to the confirmed root cause only —
no incidental "while I'm in here" changes.

### /incident-postmortem — Incident Postmortem
**Purpose:** Structures a resolved incident into timeline, verified root
cause, impact, and concrete action items with owners. Blameless — documents
system gaps, not individual mistakes.
**Dependencies:** Most useful after `/debug-root-cause` has produced a
`debug-log.md` entry for the incident; works without one but needs more
manual input.
**Auto-fixes:** **Never — report only.** Run only after the underlying fix
is already confirmed working.

---

## Full skill registry

| Trigger | Skill | Type | Auto-fixes? |
|---|---|---|---|
| Session start | session-knowledge-doc | Always-on | N/A — documents only |
| Session start | coding-standards-enforcer | Always-on | Shapes new code, doesn't retrofit |
| Natural language + `/debug-root-cause` | debug-root-cause | Always-active posture | Yes, scoped to confirmed cause only |
| `/audit-deps` | audit-dependencies | On-demand | Yes, on confirmation |
| `/audit-edge-functions` | audit-edge-functions | On-demand | Yes, on confirmation |
| `/audit-rls` | audit-rls-policies | On-demand | Yes, on confirmation |
| `/audit-data-integrity` | audit-data-integrity | On-demand | Partial, small counts only |
| `/audit-eas` | audit-eas-presubmission | On-demand | Partial, config only |
| `/audit-performance` | audit-performance-baseline | On-demand | No — measurement only |
| `/audit-prelaunch` | audit-prelaunch-checklist | On-demand | No — verification only |
| `/audit-dpdp` | audit-dpdp-compliance | On-demand | **Never** — report only |
| `/audit-api-contract` | audit-api-contract | On-demand | Yes, on confirmation per side |
| `/audit-onboarding-funnel` | audit-onboarding-funnel | On-demand | Yes, on confirmation |
| `/audit-rollback-readiness` | audit-rollback-readiness | On-demand | **Never** — report only |
| `/hygiene-deadcode` | hygiene-dead-code | On-demand | Yes, on confirmation |
| `/hygiene-secrets` | hygiene-secrets | On-demand | **Never** — report + rotation advice only |
| `/hygiene-testsync` | hygiene-test-sync | On-demand | Yes, after direction confirmed |
| `/install-logging` | install-logging-infrastructure | On-demand | Scaffolds into `code/shared/utils/` + `general/changelog.md` |
| `/incident-postmortem` | incident-postmortem | On-demand | **Never** — report only |

When adding a new skill in future, classify it against the always-on vs
on-demand principle above before deciding which trigger pattern it gets.
