# Contributing

Thanks for your interest in contributing. This project follows a [Code of Conduct](CODE_OF_CONDUCT.md) — please read it before participating.

## Getting set up

Follow the [Local Setup](README.md#local-setup) section of the README to get the API running, and the [Admin Console](README.md#admin-console-react-spa) section if you're working on the React admin SPA in `web/admin/`.

Requirements:

- Node.js `22.x` (see `.nvmrc`)
- pnpm `10.12.4` (pinned via the `packageManager` field in `package.json`)

## Making changes

- Keep pull requests focused on a single change; unrelated cleanups make review harder.
- Match the existing code style — run `pnpm format` (Prettier) before committing.
- Add or update tests for behavior you change.
- Update the relevant doc in `docs/` (`OPERATIONS.md`, `CLIENT_INTEGRATION.md`, `ADMIN_GUIDE.md`, `SECURITY_TEST_MATRIX.md`) or the README if your change affects them.

## Before opening a pull request

CI (`.github/workflows/ci.yml`) runs two jobs, `verify` and `admin-verify`. Run the same checks locally first:

**Backend** (repo root):

```bash
pnpm build
pnpm typecheck
pnpm lint
pnpm test
pnpm test:migrations
pnpm test:integration
pnpm dependency:audit
```

`test:migrations` and `test:integration` need a running PostgreSQL instance (`docker compose up -d postgres`) and a `.env` — see [Local Setup](README.md#local-setup).

**Admin SPA** (`web/admin/`):

```bash
pnpm admin:build
pnpm admin:typecheck
pnpm admin:lint
pnpm admin:test
```

End-to-end tests (`pnpm test:e2e` for the backend, `pnpm admin:e2e` for the admin console) aren't run in CI on every push but are worth running locally for changes that touch auth flows or the admin UI — see `web/admin/e2e/README.md`.

## Opening the pull request

- Describe what changed and why, and link any related issue.
- Make sure CI is green before requesting review.
- One approval is required before merging (see `.github/CODEOWNERS`).

## Reporting bugs and requesting features

Use the issue templates under **Issues → New issue**. For security vulnerabilities, see [SECURITY.md](SECURITY.md) instead of opening a public issue.
