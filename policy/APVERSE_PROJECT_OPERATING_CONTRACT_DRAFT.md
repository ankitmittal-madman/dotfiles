# APVerse Engineering Operating Contract (Draft)

**Status:** Draft for co-founder review  
**Policy owner:** Ankit  
**Review cadence:** Weekly  
**Scope:** Engineering quality standards for every APVerse project, including Foofoo and Parent Plus. Product discovery and general product documentation are governed separately. Engineering documentation needed to build, test, operate, and maintain software remains in scope.

## Why this contract comes first

Automation needs one shared definition of engineering quality. This contract gives project setup, stage checks, findings, and proposed fixes the same rules. Without it, separate AI instructions can make conflicting assumptions.

## Intended workflow

**PM describes the agreed product need → guided setup records the project’s technical context → the system identifies the engineering stage → relevant checks run and show evidence → the AI explains findings and may propose a bounded fix → a human reviews high-impact decisions.**

The AI should explain technical terms in plain language, show what it inspected, and label checks that did not run as **NOT RUN**. A non-technical PM should not need ongoing technical coaching. One-time organization administrator setup may be needed for permissions, approved integrations, and protected-branch rules. This definition is awaiting Ankit’s confirmation.

## Standards and approval table

The draft contains engineering principles and a few human-approval examples, but it does **not yet classify every standard as Mandatory, Recommended, or Optional**. Complete this table before calling the contract final.

| Area | Proposed level | What it means | Human approval |
|---|---|---|---|
| Secrets and credentials | Mandatory | Never commit credentials; use approved secret storage. | Always for access or credential policy changes. |
| Relevant automated checks | Mandatory | Run applicable checks and report evidence; unavailable checks are NOT RUN. | A human owner decides whether to accept a failed or unavailable required check. |
| Security, privacy, and sensitive data | Mandatory | Identify sensitive-data handling and security impact; do not silently change policy. | Always for security/privacy policy decisions or sensitive-data handling changes. |
| Tests for changed behavior | Mandatory | Add or update checks that demonstrate the intended behavior. | Human approval for accepting known material gaps. |
| Reliability and recovery planning | Recommended by default; mandatory for production or high-impact services | Record likely failure modes, monitoring, and recovery approach. | Always before production release when recovery is not demonstrated or risk is high. |
| Formatting, typing, and maintainability checks | Recommended by default; mandatory where the project already enforces them | Use the project’s established checks and conventions. | No special approval unless the exception weakens a mandatory control. |
| Architecture or dependency choices | Recommended review | Explain trade-offs and affected systems before broad changes. | Always for broad-impact upgrades or changes that materially alter system boundaries. |

These are starting recommendations for Ankit to confirm or change. “Mandatory” means a project must meet the rule or record an approved exception. “Recommended” means the AI should suggest it and explain when it matters. “Optional” means it is available when useful and does not block progress.

## Human approval is always required for

- Security or privacy policy changes, access-control changes, or changes to how sensitive data is handled.
- Legal or regulatory conclusions.
- Production data writes, deletion, or irreversible database changes.
- Production deployment, publishing, or release decisions.
- Accepting a material security, privacy, reliability, or required-check failure.
- Broad-impact dependency upgrades or architecture changes.
- Any action that spends money, changes user access, or cannot be safely reversed.

The AI may prepare a proposal and evidence, but must wait for the named human decision owner before taking these actions.

## Engineering stages and evidence

| Stage | Minimum engineering evidence to move on |
|---|---|
| Project setup | Project purpose reference, technical owner if known, stack and environments discovered or confirmed, data/risk classification, checks selected. |
| Design | Relevant architecture, API, storage, security, and failure-mode decisions recorded; unknowns called out. |
| Build | Changes are reviewable, tied to agreed acceptance criteria, and follow repository conventions. |
| Verify | Applicable tests and quality checks have recorded results; failures and NOT RUN checks are visible. |
| Release | Deployment steps, monitoring, data migration impact, rollback or recovery approach, and required human approvals are recorded. |
| Operate | Reliability signals, incidents, and technical follow-up work are reviewed and assigned. |

A project may skip a stage only with a recorded reason and an owner. Stage detection must show evidence; it must not rely on a branch name alone.

## Project setup record

Each project should have a small machine-readable record, proposed at `.apverse/project.yml`, containing the contract version, project name, current engineering stage, detected/confirmed stack, environments, risk/data classification, enabled checks, protected branch, and approved exceptions with approver and expiry. The AI should inspect the repository and offer simple choices when a PM does not know a technical answer.

## Findings and safe fixes

Every check result should include its name and version, status (**PASS**, **FAIL**, **NEEDS HUMAN REVIEW**, or **NOT RUN**), evidence, scope inspected, severity, user or business impact, next step, and whether a fix can be proposed automatically.

Automation is read-only by default. It may offer a narrow, reversible fix on a separate branch or pull request when it can validate the change. It must not push directly to a protected branch or perform a human-gated action. Each proposal should explain the change and show check results.

## How this applies across APVerse

The target policy applies to **all APVerse projects**, including Foofoo and Parent Plus. Adoption should be staged: first validate the workflow with representative lower-risk and higher-risk projects, then fix gaps and roll it out across the remaining projects. Pilot projects are a way to learn before broad enforcement; they are not an exemption from the eventual organization standard.

The pilot project names and their risk categories still need to be recorded. Do not assume which project is lower or higher risk without reviewing what data it handles, who uses it, and the impact of failure.

## Ownership and upkeep

Ankit owns this policy. Review it weekly. Each review should capture changes, rationale, effective date, and any migration guidance. Projects may pin a contract version; exceptions need an owner, reason, approver, and expiry date.

## Co-founder decisions still needed

1. **Self-serve definition:** Confirm that “self-serve” means no ongoing technical coaching, while allowing one-time organization administrator setup.
2. **Standards:** Confirm or edit the proposed Mandatory/Recommended levels in the table above; mark any Optional checks and name exceptions that need human approval.
3. **Rollout:** Confirm the lower-risk and higher-risk pilot projects. Foofoo and Parent Plus are both in the all-project target scope.
4. **Engineering scope:** Confirm that product discovery and general product documentation stay in separate policies, while engineering documentation stays here.
5. **Purpose #4:** The original goals listed only three completed purposes and left item four blank. The working interpretation added here is: **establish consistent engineering quality standards and safe automation across every APVerse project.**

## Status and limits

This is a proposed engineering policy, not an enforcement system. It does not yet change Foofoo or Parent Plus, add automated checks, or approve exceptions. Those steps follow after the policy decisions are confirmed.
