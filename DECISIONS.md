# 📒 DECISIONS.md — Architecture Decision Record (ADR) Log

This file tracks all significant architecture, technology, and design decisions made during development of the Netflix Clone. Each entry records the **context**, **decision**, and **rationale** so future contributors (human or AI) can understand *why* a choice was made, not just *what* was chosen.

---

## ADR-001 — Java Spring Boot as the Backend Framework
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Need a backend framework for a production-grade streaming platform with auth, catalog, playback entitlement, and billing.

**Decision:**
Use **Java 21 + Spring Boot 3** with Spring Security, Spring Data JPA, and Spring Cloud Gateway.

**Rationale:**
- Mature ecosystem; battle-tested for auth (JWT), REST APIs, and DB transactions
- Java 21 Virtual Threads provide high-concurrency I/O handling without reactive complexity
- Spring Boot Actuator + Micrometer give observability out of the box
- Strong IDE tooling and team familiarity

**Alternatives Considered:**
- Node.js / Express — lighter, but weaker typing and ecosystem for complex domain logic
- Quarkus — good, but smaller community and fewer ready-made starters

---

## ADR-002 — Modular Monolith First, Microservices Later
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Full microservices architecture adds distributed transaction complexity and operational overhead that slows initial development.

**Decision:**
Organize the Spring Boot backend as a **Modular Monolith** with strict package/module boundaries (`auth`, `catalog`, `playback`, `billing`, `ingestion`). The **Transcoding Worker** is a separate deployable from day one (CPU-bound, long-running).

**Rationale:**
- Fast iteration without distributed systems complexity in the early phase
- Module boundaries make future extraction to separate Spring Boot services straightforward
- Transcoding *must* be separate from day one because FFmpeg is CPU-intensive and blocks JVM threads

---

## ADR-003 — MySQL as Primary Database
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Need a relational database for users, catalog metadata, subscriptions, and watch history.

**Decision:**
Use **MySQL 8.0** as the primary transactional database with **Flyway** for schema migrations and **HikariCP** for connection pooling. Add Read Replicas for catalog queries.

**Rationale:**
- ACID compliance for billing and concurrent stream limit enforcement
- Relational model fits Movie → Season → Episode hierarchy and Genre/Cast many-to-many
- Read replicas isolate high-volume catalog reads from transactional writes
- MySQL 8 window functions and CTEs support complex feed queries

**Alternatives Considered:**
- PostgreSQL — equally capable, MySQL chosen for broader managed-cloud availability
- MongoDB — rejected; relational constraints needed for billing integrity

---

## ADR-004 — Redis for Caching and Watch-Progress Buffering
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Home feed rows are read millions of times and rarely change. Watch progress heartbeats at 10-second intervals create unsustainable write pressure on MySQL.

**Decision:**
Use **Redis** as:
1. **L2 cache** for catalog/genre rows (TTL-based invalidation)
2. **Write-behind buffer** for watch progress heartbeats (flush to MySQL every ~60s or on pause/exit)

**Rationale:**
- Cache hit eliminates MySQL round-trip for 95%+ catalog reads, keeping API latency < 20ms
- Write-behind reduces heartbeat writes to MySQL by ~99% under load

---

## ADR-005 — HLS Adaptive Bitrate Streaming with FFmpeg
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Users are on a wide range of network speeds. A single `.mp4` file forces a fixed quality tradeoff.

**Decision:**
Pre-transcode all videos into **HLS** (`.m3u8` + `.ts` segments) at multiple bitrates (`360p`, `480p`, `720p`, `1080p`) using **FFmpeg**. Serve via CDN. Use **HLS.js** in the React player for ABR segment switching.

**Rationale:**
- ABR lets the player switch quality mid-stream as bandwidth changes — smooth UX
- Segments allow byte-range-free random seeks without downloading the entire file
- CDN caches segments at edge — massive scale without backend load

---

## ADR-006 — React (Vite + TypeScript) for the Frontend
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Need a UI for browsing, profile management, search, and in-browser video playback.

**Decision:**
Use **React 18** with **Vite**, **TypeScript**, **TanStack Query** (server state), **Zustand** (client state), **HLS.js** (player), and **Tailwind CSS** (styling).

**Rationale:**
- React's component model fits carousels, hover-preview cards, and profile switching patterns
- TanStack Query deduplicates API calls and caches catalog rows, making back-nav instant
- Vite's ESM-first dev server gives <100ms HMR — fast iteration cycle
- TypeScript enforces API contract types across the codebase

---

## ADR-007 — Video Delivery via Object Storage + CDN (Not Through Spring Boot)
**Date:** 2026-11-25
**Status:** Accepted

**Context:**
Routing video bytes through the Spring Boot application tier would saturate thread pools, memory, and network bandwidth.

**Decision:**
Spring Boot **never streams video bytes directly**. It issues short-lived **Signed URLs** (or Signed Cookies) pointing to the CDN origin-backed by Object Storage (MinIO locally, S3-compatible in production). The React player fetches `.m3u8` manifests and `.ts` segments directly from the CDN.

**Rationale:**
- Keeps the Spring Boot tier stateless and horizontally scalable
- CDN edge caches popular video chunks, reducing origin load dramatically
- Signed URLs/Cookies enforce entitlement at the CDN layer without added latency

---

_Add new ADRs below using the same format._
