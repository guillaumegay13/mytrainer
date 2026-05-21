# MyTrainer — Architecture

## Stack (v0)

- **Framework**: Next.js 16 (App Router, React 19, TypeScript, Turbopack)
- **Styling**: Tailwind CSS v4
- **Client shape**: Mobile-first PWA (web manifest + standalone display)
- **Package manager**: pnpm 10
- **Runtime**: Node.js 22
- **Hosting**: Vercel (Hobby tier, single region, default `iad1`)
- **CI**: GitHub Actions — `lint` + `typecheck` + `build` on every push/PR
- **Source control**: GitHub

Data layer, auth, AI provider, and background jobs are explicitly **not** chosen yet — we'll pick them when the first feature demands them, not before. No microservices, no event bus, no queues, no GraphQL.

## One-paragraph defense

Speed-to-first-user: Next.js + Vercel is zero-config deploy on git push — we get a live URL the day the repo is created, and Tailwind lets us style screens without leaving the component file. Ops cost: Hobby tier on Vercel is $0 until traffic matters, GitHub Actions CI is free at our scale, and we have no servers to keep alive between users. AI-maintainability: Next.js + React + TypeScript + Tailwind is the single most LLM-trained web stack on the planet, file conventions are boring and discoverable (`src/app/<route>/page.tsx`), and an AI engineer can extend it in three months without ever reading a custom framework doc. The whole stack is rentable, replaceable, and well-trodden — exactly what we want before product-market fit.

## Repository layout

```
.
├── .github/workflows/ci.yml   # lint + typecheck + build
├── public/                    # static assets, PWA icon
├── src/
│   └── app/
│       ├── layout.tsx         # root layout, PWA metadata
│       ├── manifest.ts        # web app manifest (Next metadata route)
│       ├── page.tsx           # landing
│       └── globals.css        # Tailwind entry
├── ARCHITECTURE.md
├── README.md
├── next.config.ts
├── package.json
├── pnpm-lock.yaml
└── tsconfig.json
```

## What we will add when the product demands it

- **Auth**: Probably Clerk or Supabase Auth. Decide when the first authenticated screen ships.
- **DB**: Probably Postgres (Neon or Supabase). Decide when we need to persist a workout.
- **AI**: Anthropic Claude via the official SDK, server-side route handlers.
- **Background work**: Vercel cron or QStash. Avoid queues until we have a real reason.

## Non-goals (today)

- Microservices, event bus, GraphQL gateway, custom infra
- Native mobile app (PWA covers it for v0)
- Multi-region, multi-tenant, or enterprise features
- Premature abstraction over auth, DB, or AI provider
