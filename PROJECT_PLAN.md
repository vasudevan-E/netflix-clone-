# 📋 PROJECT_PLAN.md — Netflix Clone Master Plan

## Overview

A full-stack streaming platform clone with adaptive bitrate video delivery, multi-profile user accounts, subscription billing, and a content catalog — built with **React**, **Java Spring Boot**, and **MySQL**.

---

## Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend** | React 18, TypeScript, Vite, TanStack Query, Zustand, HLS.js, Tailwind CSS |
| **Backend** | Java 21, Spring Boot 3, Spring Security, Spring Data JPA, Spring Cloud Gateway |
| **Database** | MySQL 8.0 (Primary + Read Replicas), Flyway migrations |
| **Cache** | Redis 7 (session store, catalog cache, heartbeat buffer) |
| **Messaging** | RabbitMQ (transcoding job queue) |
| **Media** | FFmpeg (ABR transcoding → HLS), MinIO / S3 (object storage) |
| **Build** | Maven (backend), Vite/pnpm (frontend) |
| **Dev Tools** | Git, Docker Compose (local infra), IntelliJ IDEA / VS Code |

---

## High-Level Milestones

### Phase 1 — Foundation (Weeks 1–2)
- [ ] Project scaffolding (this structure)
- [ ] Spring Boot multi-module project setup
- [ ] React + Vite + TypeScript bootstrapping
- [ ] MySQL schema design & Flyway migrations (V1)
- [ ] Docker Compose for local MySQL + Redis

### Phase 2 — Auth & Profiles (Weeks 3–4)
- [ ] User registration & login (JWT access + refresh tokens)
- [ ] Multi-profile support (up to 5 profiles per account)
- [ ] Maturity rating & PIN lock per profile
- [ ] Spring Security filter chain
- [ ] React: Login page, Profile selector screen

### Phase 3 — Catalog & Browse (Weeks 5–6)
- [ ] Title metadata model (movies, series, seasons, episodes)
- [ ] Genre taxonomy & many-to-many mapping
- [ ] Home feed API (trending, genre rows, continue watching)
- [ ] Redis catalog caching layer
- [ ] React: Home screen, Title detail modal/page, Search

### Phase 4 — Media Ingestion & Transcoding (Weeks 7–8)
- [ ] Admin upload API (Presigned URL generation)
- [ ] RabbitMQ job publish on upload complete
- [ ] FFmpeg transcoding worker (480p / 720p / 1080p HLS)
- [ ] HLS manifest (.m3u8) + segments stored in MinIO
- [ ] Media status lifecycle (PENDING → PROCESSING → READY)

### Phase 5 — Playback (Weeks 9–10)
- [ ] Entitlement check (subscription + region)
- [ ] Signed URL / CDN cookie generation for HLS manifest
- [ ] React: HLS.js video player, quality selector, skip-intro
- [ ] Watch progress heartbeat (Redis buffer → MySQL flush)
- [ ] Resume playback from last position

### Phase 6 — Billing & Subscriptions (Weeks 11–12)
- [ ] Subscription plans (Basic, Standard, Premium)
- [ ] Concurrent stream enforcement (plan-based limit)
- [ ] Subscription status checks in entitlement flow
- [ ] React: Plan selection, Account management page

### Phase 7 — Hardening & Launch Prep (Weeks 13–14)
- [ ] API rate limiting (Spring Cloud Gateway)
- [ ] Circuit breakers (Resilience4j) on catalog & recommendation calls
- [ ] Observability: Spring Boot Actuator + Micrometer metrics
- [ ] MySQL read replica routing for catalog queries
- [ ] End-to-end tests
- [ ] Production Docker images & CI/CD pipeline

---

## Domain Modules (Backend)

```
backend/
├── auth/           ← Users, profiles, JWT, session management
├── catalog/        ← Titles, genres, episodes, home feed
├── playback/       ← Entitlement, signed URLs, watch history
├── billing/        ← Plans, subscriptions, stream limits
└── ingestion/      ← Admin upload, transcoding job dispatch
```

---

## Out of Scope (v1)
- Real payment processing (mocked)
- AI-powered recommendations (placeholder data)
- Mobile native apps (web-responsive only)
- Live streaming
