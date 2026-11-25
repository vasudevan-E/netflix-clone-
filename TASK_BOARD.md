# 📌 TASK_BOARD.md — Sprint Task Board

> **Current Sprint:** Sprint 1 — Foundation & Scaffolding
> **Sprint Dates:** TBD
> **Updated:** 2026-11-25

---

## 🗂️ Backlog

| ID | Title | Domain | Estimate | Assigned To |
| :--- | :--- | :--- | :--- | :--- |
| AUTH-01 | User registration endpoint | auth | 3h | — |
| AUTH-02 | JWT login (access + refresh tokens) | auth | 4h | — |
| AUTH-03 | Multi-profile CRUD | auth | 3h | — |
| AUTH-04 | Profile PIN lock | auth | 2h | — |
| CAT-01 | Title entity & Flyway migration V2 | catalog | 3h | — |
| CAT-02 | Genre taxonomy & title_genres join | catalog | 2h | — |
| CAT-03 | Home feed API (trending row) | catalog | 4h | — |
| CAT-04 | Redis caching for genre rows | catalog | 3h | — |
| PLAY-01 | Entitlement check service | playback | 3h | — |
| PLAY-02 | Signed URL generation for HLS | playback | 3h | — |
| PLAY-03 | Watch progress heartbeat endpoint | playback | 2h | — |
| ING-01 | Presigned upload URL endpoint | ingestion | 2h | — |
| ING-02 | RabbitMQ transcoding job publisher | ingestion | 3h | — |
| ING-03 | FFmpeg HLS transcoding worker | ingestion | 6h | — |
| FE-01 | Vite + React + TypeScript scaffold | frontend | 2h | — |
| FE-02 | Login & profile selector screens | frontend | 4h | — |
| FE-03 | Home screen with carousel rows | frontend | 5h | — |
| FE-04 | HLS.js video player component | frontend | 4h | — |
| INFRA-01 | Docker Compose (MySQL + Redis + MinIO) | infra | 3h | — |
| INFRA-02 | Flyway V1 schema migration | infra | 2h | — |
| INFRA-03 | GitHub Actions CI pipeline | infra | 3h | — |

---

## 🔄 In Progress

| ID | Title | Assigned To | Started |
| :--- | :--- | :--- | :--- |
| INFRA-00 | Project scaffolding & repo structure | architect | 2026-11-25 |

---

## ✅ Done

| ID | Title | Completed | PR |
| :--- | :--- | :--- | :--- |
| — | Dev environment setup (JDK 21, Maven, MySQL, Redis, FFmpeg, Node) | 2026-11-25 | — |

---

## ❌ Blocked

| ID | Title | Blocker |
| :--- | :--- | :--- |
| — | — | — |

---

## Notes
- Task IDs follow the pattern `<DOMAIN>-<NUMBER>` (e.g. `AUTH-01`, `FE-03`).
- Use these IDs in branch names: `feature/AUTH-01-user-registration`
- Update this board whenever a task moves between columns.
