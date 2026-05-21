# MyTrainer

AI-powered personal trainer. Mobile-first PWA.

See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for the stack and the reasoning behind it.

## Prerequisites

- Node.js 22 (see `.nvmrc`)
- pnpm 10

## Run locally

```bash
pnpm install
pnpm dev
```

Open <http://localhost:3000>.

## Useful scripts

```bash
pnpm dev          # dev server (Turbopack)
pnpm build        # production build
pnpm start        # serve production build
pnpm lint         # ESLint
pnpm typecheck    # TypeScript --noEmit
```

## Deploy

Pushes to `main` deploy to Vercel via the Vercel ↔ GitHub integration. See `ARCHITECTURE.md`.

## CI

GitHub Actions runs `lint`, `typecheck`, and `build` on every push and PR. See `.github/workflows/ci.yml`.
