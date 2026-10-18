# ForgeFlow Progress

## Session: initial plan and tool setup

### Completed

- Confirmed the existing `VOXEL_FRONTIER` project is unrelated.
- Created the independent ForgeFlow project directory.
- Initialized ForgeFlow as an independent Git repository without creating a
  commit.
- Added the initial README, requirements, roadmap, architecture, data-model,
  security, API, Git, CI, AI, deployment, decision, and known-issues docs.
- Added GSD-style project state and the Phase 1 repository-browser plan.
- Installed CodeRabbit CLI `0.9.0` from the official signed Windows archive.
- Completed the first real Git-backed repository-browser slice.
- Added SQLite-backed users, sessions, repository metadata, audit events,
  issues, and pull requests.
- Added authenticated local sign-in/out, repository creation, branch/diff APIs,
  collaboration workspace, and opt-in smart HTTP clone support.
- Added approved-root import/archive flows and an evidence-backed redacted
  secret scan with a security workspace tab.
- Added protected-branch review state, approval freshness checks, and a
  merge-readiness endpoint that refuses unsafe merges.
- Added committed workflow discovery and a non-executing automation plan view.
- Added authenticated provider-neutral AI completions with a local mock,
  bounded requests, and repository-context disclosure disabled by default.
- Added organization creation, membership management, organization-scoped
  repository records, and centralized active-membership authorization.
- Protected every repository API/Git transport path with session and tenant
  checks; added production denial for development login and same-origin checks.
- Added tenant negative tests for cross-organization, pending membership,
  role enforcement, CSRF origin rejection, and no private-content leakage.

### Actual checks

- CodeRabbit candidate signature: valid Authenticode, expected CodeRabbit
  signer, expected Microsoft issuer, Code Signing EKU.
- CodeRabbit installed copies: SHA-256 matched the verified candidate.
- `coderabbit.exe --version`: `0.9.0`.
- `cr.exe --version`: `0.9.0`.
- `coderabbit auth status --agent`: not authenticated.
- `npm run verify`: passed (typecheck, lint, 40 Vitest tests, production build,
  and 8 Playwright browser tests).
- The earlier unauthenticated local `git clone` smoke check passed before tenant
  authorization was enabled; Git HTTP now requires an authenticated session and
  PAT/basic Git-client credentials remain deferred.

### Not run

- CodeRabbit review; authentication is not configured.
- OmniRoute or REA runtime workflows.

### Next task

Next: implement the production OIDC callback and PAT-based Git-client
authentication while preserving the verified tenant/review/security boundaries.
