# ttfluence — CV Summary

**Subject:** Anuar Begenov · `anuarbegenov111@gmail.com` / `anuar.begenov@bcc.kz`
**Role on the project:** Co-founder, Lead Engineer
**Period:** February 2024 – present (~2.3 years)
**Sources mined:** 9 production git repositories under `Ttfluence/*` and `Anuar111/*`
**Authorship evidence:** 1,273 personal commits across the project (~42% of 3,022 team commits)

> This document holds three CV-ready drafts (short, long, LinkedIn blurb) plus an
> evidence appendix. Numbers in **[BRACKETS]** are placeholders you should fill in
> with real business metrics (users, revenue, channels, etc.) before sending out.

---

## About ttfluence

ttfluence is a creator-monetization platform that connects social-media creators
(TikTok, Threads, Instagram) with paid promotional campaigns. The product ships
as a **Telegram mini-app** for creators, a **Refine-based admin dashboard** for
operators, finance, and moderators, and a **NestJS microservice backend** that
handles authentication, campaign lifecycle, payments (Qiwi), creator verification
(Apify), social scraping, and audit logging. It runs on **Render** with
**PostgreSQL** + **Redis**, fully Terraform-managed in staging.

---

## Role (one-line)

**Co-founder & Lead Engineer, ttfluence** — built and operate a multi-service
creator-monetization platform spanning Telegram mini-app, Refine admin, NestJS
microservices, PostgreSQL, and Terraform IaC; 1,273 personal commits across 9
repositories alongside two co-founder engineers.

---

## Short version (3–5 bullets · compact CV)

- **Co-founded ttfluence**, a creator-monetization platform connecting
  TikTok/Threads/Instagram creators with paid campaigns; shipped to production
  and **[ADD: # creators / # campaigns / payout volume]** since launch in 2024.
- **Architected the full stack end-to-end**: NestJS monorepo (1 core API + 3
  gRPC microservices), Telegram-mini-app frontend (Next.js + React 19), Refine
  + MUI admin dashboard, PostgreSQL schema (40+ models), and Terraform IaC on
  Render.
- **Led the engineering org with 2 other co-founders**, authoring ~42% of all
  commits (1,273 of 3,022) across 9 repositories over ~2.3 years.
- **Drove platform consolidation in 2026**: unified three separate repos into a
  pnpm/Turborepo monorepo, coordinated major-version upgrades across the stack
  (React 18→19, Next 14→16, NestJS 10→11, Refine 4→5, Tailwind 3→4), and brought
  staging infrastructure under Terraform.
- **Owned production-critical workflows** including Qiwi card payments,
  Apify-based creator verification, multi-link campaign participation, audit
  logging with rollback, and a 5-tier RBAC enforced on both backend and admin.

---

## Long version (8–12 bullets · senior/staff/founder CV)

- **Co-founded ttfluence** in Feb 2024 and have served as Lead Engineer
  alongside two co-founder engineers. Personally authored **1,273 commits
  (~42%) across 9 production repos** over a 27-month span — backend, frontend,
  admin, database, infrastructure, and internal docs. **[ADD business outcome:
  # creators onboarded / # campaigns / payout volume / revenue].**

- **Designed and built the NestJS backend**, a monorepo of one REST core API
  (`core-ttfluence`, 29+ domain modules) and three gRPC microservices
  (`feat-apify` for creator verification, `feat-qiwi` for card payments,
  `feat-scraper` for TikTok/Threads scraping). Co-led ~49% of backend commits
  (354/728) over the project's life.

- **Shipped a production-grade payments stack** integrating Qiwi (card
  tokenization, async status rechecks, idempotent withdrawal refunds), plus a
  forensic SQL toolkit for reconciling race conditions and stuck balances on
  link-verification payouts.

- **Built the creator-verification pipeline** end-to-end: Apify-driven TikTok
  follower scraping behind a gRPC sidecar, async follower-count refresh through
  a BullMQ + Redis job queue, mandatory creator-category onboarding in the
  Telegram mini-app, and a verification flow that degrades gracefully when the
  upstream API fails.

- **Owned the audit and compliance layer**: designed a `@Tracked` decorator
  framework that persists `Command` rows, entity snapshots, and `SideEffect`
  rollback metadata on every admin mutation; surfaced it in the admin dashboard
  with entity-navigation links, `performedBy` filtering, and a `canRollback`
  policy with pre-rollback cleanup hooks — enabling forensic investigation and
  selective reversal of operator actions on a finance-sensitive product.

- **Implemented the 5-tier RBAC system** (Admin / Operator / Finance / Moderator
  / User) used by both the Refine admin and the NestJS backend. Defined a
  `{prefix}.{suffix}` permission convention with explicit overrides and
  wildcard fallbacks, route-level middleware enforcement, and frontend guards
  (`<PermissionGuard>`, `<CanAccess>`, `usePermissions()`) that auto-hide
  Refine CRUD controls. Backend stays authoritative; frontend is UX-only.

- **Built the Telegram mini-app frontend** (Next.js 16 + React 19 + Tailwind 4
  + shadcn/ui + Zustand + TanStack Query/Form). Shipped the 5-step
  registration flow with mandatory category selection, the infinite-scroll
  campaign feed, payment-method management, blocked-user screens, and
  Telegram-specific mobile UX (safe-area padding, iOS drawer behavior,
  swipe-gesture handling). Authored ~46% of frontend commits (177/389) and a
  production-grade Axios refresh interceptor that prevents 401-cascades on auth
  endpoints.

- **Co-built the Refine + MUI admin dashboard** (Next.js 14 + Refine 4 + MUI 6
  + TipTap 3 + xlsx export) covering 19+ resources: projects, participants,
  applications, users, withdrawals, clients, roles, audit log, block reasons,
  and rules. Hand-rolled a custom REST data provider with skip/take pagination
  and JSON-serialized sort tuples to match the backend's `ParseSortPipe`
  contract. Authored ~31% of admin commits (86/274) including the user
  block/unblock unification across drawers and the WYSIWYG → TipTap migration.

- **Owned the database**: PostgreSQL 16 schema across 40+ Prisma models
  (RBAC, projects, participants, multi-link submissions, payments, withdrawals,
  audit, scraped social profiles, referrals, reports), 65+ migrations, and a
  separate forensic SQL repo (`ttfluence-postgres`, **100% solo**) with
  audit/remediation scripts for payment race conditions, stuck assignments,
  lost-link recovery, and bulk moderation actions.

- **Stood up infrastructure as code** (`ttfluence-infra`, **100% solo**):
  Terraform on Render provisioning managed Postgres, Key-Value (Redis), web
  services with full env-var wiring (JWT, GCS service account, Telegram bot
  token, Qiwi credentials), and the staging pipeline pointed at the monorepo's
  shared `staging` branch with `pnpm install --frozen-lockfile` → `prisma
  generate` → `build` → `prisma migrate deploy`.

- **Drove the May 2026 platform consolidation**: scaffolded the
  pnpm/Turborepo monorepo (`ttfluence`), migrated three standalone apps
  (backend, web, admin) into `apps/*`, scaffolded shared packages
  (`api-types`, `eslint-config`, `tsconfig`, `prettier-config`,
  `design-tokens`), converted yarn → pnpm across all apps, wired husky +
  lint-staged + CI workflows, and led a coordinated major-version refresh
  (React 19, Next 16, NestJS 11, Refine 5, TypeScript 6, Tailwind 4, ESLint 9
  flat config, Prisma 6) over a focused two-week sprint.

- **Hardened the platform for production**: helmet CSP + 1 MB body limits +
  strict validation transforms, rate-limited auth endpoints with ADMIN
  enforcement on `/admin/create`, bcrypt cost 12, Telegram `initData`
  cryptographic validation, secret-redacting log middleware, image-only upload
  restrictions with size caps and safe filenames, and CI security scanning via
  Semgrep, Gitleaks, Trivy, and OWASP ZAP.

---

## LinkedIn / cover-letter blurb (one paragraph)

Co-founder and Lead Engineer of **ttfluence**, a creator-monetization platform
connecting TikTok, Threads, and Instagram creators with paid campaigns. Since
February 2024, I have personally authored **~1,300 commits (~42% of the team's
output)** across nine production repositories spanning a Telegram mini-app
(Next.js · React 19 · Tailwind), a Refine + MUI admin dashboard, a NestJS
monorepo backend with three gRPC microservices, a PostgreSQL schema of 40+
models, and Terraform-managed infrastructure on Render. I led platform-critical
workstreams end-to-end — Qiwi card payments, Apify-based creator verification,
multi-link campaign participation, a `@Tracked` audit + rollback framework, and
a 5-tier RBAC enforced on backend and admin — and in 2026 drove a major
consolidation that unified three standalone repos into a pnpm/Turborepo
monorepo and refreshed every major dependency on the stack.

---

## Supporting evidence

### Aggregate metrics (verified from `git log`)

| Metric | Value |
|---|---|
| Repositories | 9 (one additional ops folder is not a git repo) |
| Time span | 2024-02-21 → 2026-05-20 (~27 months) |
| Total team commits (all repos) | 3,022 |
| Anuar's commits | **1,273 (~42%)** |
| Anuar's commits by year | 2024: 442 · 2025: 498 · 2026: 333 (Jan–May) |
| Repos where Anuar is the sole author | 2 (`ttfluence-infra`, `ttfluence-postgres`) |
| Repos where Anuar leads commit share | `ttfluence-backend` (49%), `ttfluence-frontend` (46%), `ttfluence` monorepo (45%) |
| Active core team | 3 co-founder engineers (Anuar + 2) plus occasional contributors |
| Languages | TypeScript (primary), SQL, HCL (Terraform) |

### Per-repository breakdown

| Repo | Role | Anuar / Total | % | Period | Stack |
|---|---|---|---|---|---|
| `ttfluence` (Turborepo monorepo) | Architect / lead | 610 / 1343 | 45% | 2024-02 → 2026-05 | pnpm, Turborepo 2.3, TS 6, Node 22 |
| `ttfluence-backend` | Co-lead backend | 354 / 728 | 49% | 2024-02 → 2026-05 | NestJS 11, Prisma 6, BullMQ, gRPC, Postgres, Telegraf |
| `ttfluence-frontend` (Telegram mini-app) | Co-lead frontend | 177 / 389 | 46% | 2024-02 → 2026-05 | Next.js 16, React 19, Tailwind 4, shadcn/ui, Zustand, TanStack |
| `ttfluence-refine-admin` | Admin features + RBAC | 86 / 274 | 31% | 2025-03 → 2026-05 | Next.js 14, Refine 5, MUI 6, TipTap 3, XLSX |
| `ttfluence-postgres` | DBA / forensic SQL | 5 / 5 | **100%** | 2026-03 → 2026-04 | PostgreSQL, MCP workspace, audit/remediation SQL |
| `ttfluence-infra` | Sole IaC owner | 6 / 6 | **100%** | 2026-05 → 2026-05 | Terraform ≥1.6, render-oss provider |
| `ttfluence-knowledge` | Wiki adopter | 4 / 159 | 3% | 2026-05 → 2026-05 | Obsidian + Claude Code (forked from `claude-obsidian`) |
| `ttfluence-knowledge-legacy` | First docs vault | 1 / 1 | **100%** | 2026-05 | Obsidian vault scaffold (ADRs + runbooks) |
| `rest/ttfluence-admin` (legacy Vite admin) | Early admin dev | 30 / 88 | 34% | 2024-09 → 2025-07 | Vite, react-admin 5, TanStack Query, Netlify |
| `rest/ttfluence-scripts` | Ops scripts | — | — | — | (not a git repo; local utility folder) |

### Consolidated tech stack

**Languages & runtimes**
- TypeScript 6 · Node.js 22 LTS · PostgreSQL 16 · HCL (Terraform 1.6+) · SQL

**Frontend (Telegram mini-app + admin)**
- Next.js 14/16 (App Router) · React 18/19 · Tailwind CSS 3/4 · shadcn/ui + Radix
- Zustand 5 · TanStack Query 5 · TanStack Form 1 · React Hook Form
- Material-UI 6 · Refine 4/5 · TipTap 3 · MUI DataGrid · `xlsx` exports
- Axios with refresh-interceptor · Telegram Web App SDK · `vaul` · `sonner`
- ESLint 9 flat config · Prettier 3 · `class-variance-authority`

**Backend (NestJS monorepo)**
- NestJS 11 (`@nestjs/common`, `@nestjs/microservices`, `@nestjs/swagger`)
- Prisma 6 with `@vegardit/prisma-generator-nestjs-dto` · 65+ migrations
- BullMQ 5 + Redis · Telegraf 4 (Telegram bot) · `nestjs-pino` structured logs
- gRPC via `@grpc/grpc-js` + `ts-proto` · class-validator / class-transformer
- JWT + refresh tokens via Passport (local + JWT strategies) · bcrypt (cost 12)
- `@nestjs/throttler` rate limiting · helmet CSP · request-body limits
- Apify client 2.x · Playwright 1.58 browser pool + proxy rotation
- Google Cloud Storage SDK · `fast-xml-parser` (Qiwi XML)
- Jest 29 · `@testcontainers/postgresql` · `supertest`

**Microservices (gRPC sidecars)**
- `feat-apify` — TikTok follower verification, category sync, bulk updates
- `feat-qiwi` — card-payment creation, async status rechecks, refunds
- `feat-scraper` — TikTok + Threads profile/post/engagement scraping, browser pool, proxy health

**Infrastructure & DevOps**
- Render (managed Postgres, Key-Value/Redis, web services, cron jobs, env groups)
- Terraform ≥1.6 with `render-oss/render` provider 1.x
- Google Cloud Storage · Husky + lint-staged + CI workflows
- pnpm workspaces (migrated from yarn) · Turborepo 2.3 · Corepack
- Semgrep · Gitleaks · Trivy · OWASP ZAP (CI security scans)

**Knowledge & tooling**
- Obsidian vault with ADRs, runbooks, decisions
- Claude Code (CLAUDE.md per repo) · forked `claude-obsidian` for compounding KB

### Theme clusters with commit evidence

**1 · Payments & financial reconciliation**
- `feat(security): enable helmet CSP, 1mb body limit, validation transform` (backend)
- `analyze stuck conditions and unpaid balances for recent race condition upon paying users through link verification` (postgres, solo)
- `qiwi done` / `qiwi pan card` / `save card pan token` / `create withdrawal page` (frontend)
- `withdrawal moved to backend, removed lc stored batches, created polling contract to receive actual data` (admin)

**2 · Creator verification & social scraping**
- `sync verification flow: call apify inline, skip verify on error, added tests` (backend)
- `refactor(user): async follower update on verification via job queue` (backend)
- `feat: rerender drawer immediately with new follower count after verification` (admin)
- `fix race condition for browser pool`, `japyr scraper`, `pool size 1, decodo service proxy` (backend / feat-scraper)

**3 · Audit logging & rollback framework**
- `feat(command): resolve and expose entity names in audit log responses`
- `audit log: performedByName filter, canRollback policy, preRollbackCleanup`
- `feat(audit-log): entity navigation links and enhanced command drawer` (admin)
- `fix(command): trigger business logic on UsersOnProjectsLink rollback`

**4 · User moderation, blocking & RBAC**
- `feat(users): add dedicated user blocking flow with reasons & audit`
- `feat(user): share block/unblock control between edit user and submission drawers`
- `feat(auth): show block reason on blocked-user screen` (frontend)
- `moderation: block 47 users for removed paid publications` (postgres, solo)

**5 · Telegram registration & creator onboarding**
- `feat(registration): restructure registration flow with separate categories step`
- `feat(auth): add mandatory creator category check in auth flow`
- `feat(profile): add CreatorCategorySelectWidget and MandatoryCreatorCategorySelect`

**6 · Monorepo migration & dependency modernization (May 2026)**
- `chore: scaffold ttfluence Turborepo monorepo`
- `chore(admin/web/backend): yarn → pnpm conversion in apps/*`
- `chore(deps): upgrade to React 19 / Next.js 16 / Tailwind CSS 4 / TypeScript 6 / ESLint 9 + flat config`
- `chore: scaffold shared packages, CI workflow, and husky pre-commit`

**7 · Infrastructure as Code (solo)**
- `Initial commit: staging environment Terraform`
- `chore(staging): repoint at Ttfluence/ttfluence monorepo + pnpm`
- `feat(staging): add backend env_vars + companion env_group`

**8 · Security hardening (May 2026)**
- `fix(security): redact secrets in request logs, raise bcrypt cost to 12`
- `feat(auth): rate-limit auth endpoints, require ADMIN for /admin/create`
- `fix(auth): harden Telegram initData validation`
- `feat(storage): restrict uploads to images with size cap and safe names`
- `chore(security): add Semgrep/Gitleaks/Trivy/ZAP scanning workflows`

### Authorship verification

Filter used: commit author email matches one of
`anuarbegenov111@gmail.com` · `anuar.begenov@bcc.kz` · `anuar@Anuars-MacBook-Pro.local`.
Tested across all 9 git repos with `git log --author=... --no-merges --all`.

### Notes for finalizing this CV section

1. Replace every `**[ADD: ...]**` with a real business metric only if you can
   defend it in an interview (creators onboarded, campaigns run, payouts
   processed, revenue, uptime, response-time SLOs, etc.). Leave blank rather
   than invent.
2. The 1,273 commit count is **the floor** — it excludes any commits authored
   from a git identity not listed above. If you used a work laptop or a second
   account that isn't in the filter, the true number is higher.
3. The "co-founder" framing is defensible because the project was founded by
   you and two co-founder engineers (Rodion Makarov, Roman Pshenichnyy);
   commit shares show all three carrying comparable load across the codebase.
4. If a role asks for a single headline number, the cleanest one is
   **"1,273 commits across 9 production repos over 27 months, ~42% of team
   output"** — it's verifiable, specific, and doesn't claim outcomes you'd have
   to substantiate.
