# ForgeFlow

ForgeFlow is an original, self-hosted developer platform for Git hosting,
collaboration, automation, security, and AI-assisted development. It is
inspired by common developer-platform workflows without copying proprietary
source code, assets, branding, or access controls.

## Current milestone

The first usable slice is a **local, read-only repository browser** backed by a
real Git repository:

1. Open one explicitly allowed local repository.
2. Resolve its current `HEAD` and default ref.
3. Browse the committed tree.
4. Read bounded text files.
5. Inspect recent commits.

The repository now contains a verified local foundation with collaboration,
security, workflow-planning, provider-neutral AI, organizations, memberships,
and tenant-scoped repository authorization slices. Production OIDC identity,
Git-client credentials, safe write transport, isolated CI, packages, full AI
retrieval, and cloud workspaces are not represented as complete merely because
they appear in the roadmap.

## Scope boundary

`C:\Users\Sandeep\VOXEL_FRONTIER` is a separate Three.js voxel game and is not
ForgeFlow source, fixture data, or a migration target. ForgeFlow lives in this
independent repository at `C:\Users\Sandeep\FORGEFLOW`.

## Planned architecture

- **Web:** Next.js, React, TypeScript, accessible design system.
- **API:** Go modular monolith with typed contracts and an explicit Git adapter
  boundary.
- **Persistence:** PostgreSQL for product metadata; Redis or an equivalent
  queue/cache only where a measured need exists.
- **Git:** real bare repositories and native Git plumbing first; a mature
  backend such as Gitea remains an integration option for advanced hosting
  features.
- **Workers:** separate processes for indexing, notifications, AI jobs, and
  CI orchestration.
- **Untrusted execution:** isolated runners, never repository-controlled
  commands inside the privileged API process.

The local authorization mode assigns repositories to organizations and requires
an active membership for private repository reads. Development login is a test
and local-workspace convenience only; it is refused in production unless the
explicit E2E test flag is used by the test harness.

## Planning and project state

- Product requirements: [`docs/PRD.md`](docs/PRD.md)
- System architecture: [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md)
- Data model: [`docs/DATA_MODEL.md`](docs/DATA_MODEL.md)
- Security design: [`docs/SECURITY.md`](docs/SECURITY.md)
- Git hosting boundary: [`docs/GIT_HOSTING.md`](docs/GIT_HOSTING.md)
- Roadmap: [`docs/ROADMAP.md`](docs/ROADMAP.md)
- Resumable GSD state: [`.planning/STATE.md`](.planning/STATE.md)
- Active phase plan: [`.planning/phases/01-repository-browser-PLAN.md`](.planning/phases/01-repository-browser-PLAN.md)

## Checks

Install dependencies and run the complete verified Phase 1 slice:

```powershell
npm ci
npm run verify
```

`verify` runs TypeScript checking, ESLint, 40 Vitest unit/integration tests,
the production Next.js build, and eight Playwright browser tests against a
disposable real Git repository. `npm run setup:demo` creates a local demo
repository under the system temp directory and writes the ignored
`var/repositories.json` catalog. Start the product with `npm run dev` after
running that setup command.

Required external capabilities for later phases are tracked explicitly rather
than assumed:

- Git is available locally.
- Docker is not currently available in the workspace.
- CodeRabbit CLI `0.9.0` is installed at the official per-user path, but its
  account is not authenticated.
- OmniRoute is installed locally but its gateway is not currently running.
- REA CLI `6.5.0` is installed; no live reference target or connected MCP
  session is currently established.
- AI defaults to a local mock provider. Configure the server-only
  `FORGEFLOW_AI_BASE_URL` and `FORGEFLOW_AI_API_KEY` only after reviewing the
  provider's retention and data-processing policy. Repository context remains
  disabled unless `FORGEFLOW_AI_ALLOW_REPOSITORY_CONTEXT=true` is explicit.

## Development principles

1. Real Git behavior must be tested against disposable repositories.
2. Server-side authorization is required for every private-resource read or
   mutation.
3. Untrusted repository content, workflow files, logs, comments, and model
   output are treated as data, never as trusted instructions.
4. Planned, partial, mocked, blocked, and verified capabilities are labeled
   separately.
5. Each atomic task must leave a reproducible check and an updated planning
   state.
