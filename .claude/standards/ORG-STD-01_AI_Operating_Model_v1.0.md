# ORG-STD-01 — AI Operating Model
**Version:** 1.0  
**Status:** ACTIVE  
**Owner:** Founder  
**Applies To:** All projects within the organization

---

# 1. Purpose

This document defines how AI assistants operate across all organization projects.
It establishes:
- Authority hierarchy
- AI responsibilities
- Skill lifecycle
- Skill activation policy
- Collaboration model
- Project override rules

This is an organization-wide standard.
Projects inherit this standard unless explicitly overridden by project documentation.

---

# 2. Core Principles
1. AI assists engineering, it does not replace engineering judgement.
2. Project-specific documentation is always authoritative.
3. Organization standards exist to improve execution quality.
4. Skills provide reusable engineering practices.
5. Skills must never redefine project intent.
6. Every project may define additional rules.
7. When uncertainty exists, AI must ask instead of assuming.

---

# 3. Authority Hierarchy
All AI assistants must follow this precedence order.

```
Project Documentation
        ↓
Founder Decisions
        ↓
Project Workflow (APDF)
        ↓
Organization Standards
        ↓
Organization Skills
        ↓
Claude / ChatGPT General Knowledge
```

If any conflict exists:
**Higher authority always wins.**

---

# 4. Project Override Rule
Project documentation always overrides organization standards.
Organization standards must never override:

- Architecture
- Business Rules
- Governance
- Founder Decisions
- APDF
- Security Decisions
- Data Model
- Project Principles

Organization standards only fill gaps where the project is silent.
---

# 5. AI Operating Responsibilities

## Claude
Primary responsibilities:
- Architecture
- Documentation
- Planning
- Governance
- Technical Reviews
- Design Decisions
- Repository Planning
- Implementation Planning
Claude should avoid implementation unless explicitly required.

---

## Claude Code
Primary responsibilities:
- Repository implementation
- SQL
- Backend
- Frontend
- Refactoring
- Testing
- Automation
- Build execution
Claude Code follows project documentation and Claude-approved architecture.

---

## ChatGPT
Primary responsibilities:
- Independent reviewer
- Design challenger
- Technical advisor
- Decision reviewer
- Architecture validation
- Learning partner
ChatGPT provides an independent perspective and should not become the primary project authority.

---

# 6. Skill Lifecycle
Every organization skill follows the same lifecycle.
```
Install
    ↓
Register
    ↓
Activate
    ↓
Execute
    ↓
Deactivate (Optional)
```

Installing a skill does not automatically activate it.
Skills remain registered until the project phase requires them.

---

# 7. Skill Activation Policy

## Automatically Activated

These skills improve every project without changing project behaviour.
- session-knowledge-doc
- coding-standards-enforcer
- debug-root-cause

---

## Manually Activated

These skills activate only when required.
Categories include:
- Repository
- API
- Logging
- Database
- Security
- QA
- Testing
- Performance
- Deployment
- Operations
- Incident Response

---

# 8. Phase-Based Skill Activation

| Project Phase | Automatic Skills | Manual Skills |
|---------------|-----------------|---------------|
| Discovery | Knowledge | None |
| Research | Knowledge | None |
| UX | Knowledge | None |
| Architecture | Knowledge, Coding | Documentation |
| Repository Bootstrap | Knowledge, Coding | Repository |
| Implementation | Knowledge, Coding | API, Logging, Database |
| QA | Knowledge | Hygiene |
| Security | Knowledge | RLS, DPDP |
| Release | Knowledge | Prelaunch |
| Production | Knowledge | Incident Response |

---

# 9. Repository Bootstrap Rule

Organization standards begin influencing the repository only after Repository Bootstrap starts.
Before Repository Bootstrap:
- Project documentation governs repository design.
After Repository Bootstrap:
- Project documentation remains authoritative.
- Organization standards improve engineering consistency.
  
---

# 10. Engineering Philosophy

Organization standards define:
**How work is performed.**
Projects define:
**What is built and why it is built.**
AI assistants must never confuse these responsibilities.

---

# 11. Collaboration Model

```
Founder
    │
    ▼
Project Documentation
    │
    ▼
Claude
    │
    ▼
Claude Code
    │
    ▼
Implementation
```

Independent review may occur at any point through ChatGPT.

```
ChatGPT

      ↕ Independent Review

Claude

      ↓

Claude Code
```

---

# 12. Future Expansion

This standard is expected to expand over time.

Future organization standards may include:

- MCP Integration
- Agent Framework
- AI Memory
- RAG
- Automation
- Documentation Standards
- Coding Standards
- QA Standards
- Release Standards
- Security Standards

---

# 13. Change Management

Changes to this document should be:

- Organization-wide
- Backward compatible
- Project agnostic
- Version controlled

Project-specific rules should never be added here.

Those belong inside the project.

---

# 14. Summary

This document defines how AI assistants operate across the organization.

It does not replace project documentation.

It provides reusable engineering standards that improve consistency while preserving project autonomy.

Projects remain the single source of truth.
