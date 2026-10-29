# APVerse Project Operating Contract (Draft)

**Status:** Phase 1 draft for review  
**Purpose:** Give every APVerse project a clear, repeatable way to move from a product problem to a tested, reviewable release. A non-technical AI PM should be able to follow the workflow without day-to-day technical coaching.

## 1. Recommendation: build the bootstrap contract first

Start with the shared project contract and bootstrap flow. It defines the common language, stage gates, authority rules, and safety boundaries that later checks and automated corrections must follow. Adding more isolated audit skills before this exists would expand the toolkit without making it consistently adoptable or automatically triggered.

## 2. Desired operating flow

**PM explains the user problem and desired outcome → assistant asks a guided intake → project manifest records the agreed context → stage gate selects relevant checks → checks run and show evidence → assistant explains failures in plain English → safe fixes are proposed on a branch/PR → a human approves product, security, legal, data, and release decisions.**

The workflow should explain technical terms when they first matter, show the user what it inspected, and distinguish verified facts from assumptions. It must not claim a check passed when it did not run.

## 3. Policy principles

1. Project intent, approved business rules, and project architecture remain authoritative for that project. APVerse standards fill gaps; they do not silently rewrite product decisions.
2. The PM provides the product context and approves product trade-offs. The system should translate that context into engineering work, acceptance criteria, and evidence.
3. Every stage has an entry condition, required evidence, quality checks, exit condition, and named decision owner.
4. Checks are selected from declared project context and changed files. Stack and stage detection can suggest values, but must show evidence and ask when confidence is insufficient.
5. Automation is read-only by default. It may create a proposed fix on an isolated branch when the change is bounded and reversible. It must not push directly to a protected branch, alter production data, change access/security policy, publish, or deploy without the required human approval.
6. Every finding links to evidence, severity, user/business impact, suggested next action, and whether an automatic correction is allowed.
7. Project frameworks are versioned. Updates include compatibility notes, migration guidance, and a way to pin or adopt a version.
8. Product and engineering quality are both in scope: problem validation, measurable outcomes, user experience, accessibility, privacy, security, reliability, test coverage, operability, and release readiness.

## 4. Standard project stages

| Stage | PM question | Minimum evidence to exit | Typical checks |
|---|---|---|---|
| Discovery | Is this a real user problem worth solving? | User/problem statement, evidence, target user, desired outcome, known assumptions. | Evidence quality, duplicate initiative check, risk/data questions. |
| Definition | What outcome and scope are we committing to? | Requirements, non-goals, success metric, acceptance criteria, dependencies. | Requirement completeness, metric measurability, edge-case prompts. |
| Design | How should the experience and system behave? | User flow, design decisions, architecture/data/API decisions where relevant. | Accessibility, privacy, security, failure states, contract review. |
| Build | Is implementation progressing against agreed intent? | Traceable changes, updated documentation, reviewable code. | Formatting, types, tests, dependency and secret scans, changed-area checks. |
| Verify | Does it work for the intended users and failure cases? | Test evidence, known limitations, product acceptance. | Automated tests, integration checks, exploratory checklist, accessibility checks. |
| Release | Can we safely expose this to users and recover if needed? | Approved release notes, monitoring, rollback/mitigation plan, support readiness. | Deployment config, migration compatibility, launch checklist, human approvals. |
| Operate | Is the product delivering the outcome after release? | Usage/quality metrics, incidents, user feedback, follow-up decisions. | Monitoring/alert review, reliability, outcome review, incident learning. |

A project may skip a stage only with a recorded reason and owner. The workflow should not infer project maturity from a branch name or folder alone.

## 5. Guided project intake

The intake should ask in plain language: (1) Who has the problem? (2) What are they trying to do? (3) What evidence shows the problem matters? (4) What should improve and how will we measure it? (5) What is explicitly out of scope? (6) Does the project handle personal, financial, health, or otherwise sensitive information? (7) What platforms and external services are involved? (8) What environments and release process exist? (9) Who owns product, technical, security/privacy, and release decisions? (10) What constraints or deadlines are real?

If a PM cannot answer a technical question, the assistant should inspect the repository or offer simple choices with explanations. It should not require the PM to guess a framework, database, or deployment design.

## 6. Project manifest (proposed)

Each project should carry a validated manifest such as .apverse/project.yml with: framework version, project name, product owner, technical owner (if available), current stage, declared stack, environments, risk/data classification, enabled checks, protected branch, and project-specific exceptions with approver and expiry. The manifest is the machine-readable source for check selection; human-readable project docs remain the source for intent and decisions.

## 7. Finding and remediation contract

Each result should include: check ID and version; status (PASS, FAIL, NEEDS HUMAN REVIEW, or NOT RUN); evidence and inspected scope; severity; affected user/business outcome; recommended next step; whether a fix may be proposed automatically; and required approver. Unknown or unavailable checks must be NOT RUN, never PASS.

Automated corrections should be limited to narrow, reversible changes with a clear test or validation path. The system should prepare a branch/PR, describe the diff and evidence, run applicable checks, and wait for review. Security/privacy policy, legal conclusions, schema/data deletion, dependency upgrades with broad impact, access changes, production writes, and releases require human decision.

## 8. Definition of done for a project change

A change is ready for review when it maps to an agreed product need, acceptance criteria are addressable, relevant checks ran with recorded results, failures are fixed or explicitly accepted by the right owner, documentation reflects material behavior/architecture changes, and the change is reviewable. A release has a separate gate for production readiness and human approval.

## 9. Phase 1 success criteria

- A non-technical PM can start a sample project from the guided intake without technical coaching.
- The assistant explains what it inspected and what it still needs in plain English.
- The project manifest validates and reports missing/invalid fields clearly.
- A project can identify its stage and applicable checks with evidence, while allowing the PM to correct an uncertain suggestion.
- The workflow produces no false PASS for a check that was unavailable or not run.
- High-impact changes are held for an explicit human approval.
- Tool-specific instructions point to one versioned canonical contract rather than drifting copies.

## Draft review questions

1. Confirm that self-serve means no ongoing technical coaching, while allowing one-time organization administrator setup.
2. Confirm mandatory versus recommended standards and which risks always require human approval.
3. Choose one simple and one higher-risk pilot project.
4. Define APVerse policy owner and review cadence.
5. Provide the missing purpose number 4 from the original goals.

## Draft note

This is a proposed organization contract for review. It does not yet change project repositories or enforce checks.