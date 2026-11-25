# 🤖 AGENTS.md — Agent Collaboration Guide

This document describes how AI agents (and human contributors) should work within this repository.

---

## Repository Purpose

This is a **Netflix Clone** built with:
- **Frontend:** React (TypeScript, TanStack Query, Zustand, HLS.js)
- **Backend:** Java Spring Boot 3 (Modular Monolith → Microservices path)
- **Database:** MySQL 8.0 with Read Replicas
- **Cache:** Redis
- **Media:** FFmpeg for transcoding, HLS/DASH delivery via CDN

---

## Agent Roles & Ownership

| Agent / Role | Owns | Responsibilities |
| :--- | :--- | :--- |
| **architect** | `docs/architecture/` | ADRs, system design, sequence diagrams |
| **backend-dev** | `backend/` | Spring Boot services, JPA entities, REST APIs |
| **frontend-dev** | `frontend/` | React components, routing, player integration |
| **infra-dev** | `infrastructure/` | Docker, CI/CD, DB migrations, Redis config |
| **qa** | `backend/**/test/`, `frontend/src/**/*.test.*` | Unit, integration, and E2E tests |

---

## Branching Convention

```
main              ← stable, production-ready
develop           ← integration branch
feature/<ticket>  ← feature work  (e.g. feature/AUTH-01-jwt-login)
fix/<ticket>      ← bug fixes
chore/<topic>     ← tooling, deps, CI
```

---

## Commit Message Format

```
<type>(<scope>): <short summary>

type  : feat | fix | chore | docs | refactor | test | perf
scope : auth | catalog | playback | billing | frontend | infra
```

**Example:**
```
feat(auth): add JWT refresh token rotation endpoint
```

---

## Task Board

See [`TASK_BOARD.md`](./TASK_BOARD.md) for the current sprint's task assignments.

---

## Decision Log

All significant architecture and technology decisions are recorded in [`DECISIONS.md`](./DECISIONS.md).

---

## Handoff Protocol

When an agent finishes a task:
1. Update `TASK_BOARD.md` — move task from **In Progress** → **Done**
2. Add a brief entry in `docs/agent-reports/` named `YYYY-MM-DD-<agent>-<topic>.md`
3. Open a PR using the template in `.github/pull_request_template.md`
