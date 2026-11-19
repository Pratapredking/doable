# Repository Guidelines

## Project Structure & Module Organization

This is a Next.js 15 App Router application written in TypeScript. Routes and server handlers live under `app/`; team-scoped APIs use `app/api/teams/[teamId]/...`. Reusable UI is in `components/`, with domain components grouped under `ai/`, `issues/`, `projects/`, and `shared/`. Client data hooks and server-side helpers live in `lib/hooks/` and `lib/api/`. Prisma schema, migrations, and seed data are in `prisma/`; static assets belong in `public/`. Use the `@/` alias for imports from the repository root.

## Build, Test, and Development Commands

- `npm install` installs dependencies and generates the Prisma client through `postinstall`.
- `npm run dev` starts the local Next.js development server.
- `npm run build` generates Prisma types and creates a production build.
- `npm start` serves the production build.
- `npm run lint` runs the Next.js ESLint configuration.
- `npm run db:migrate` creates and applies development migrations.
- `npm run db:push` syncs the schema without creating a migration; use only for local prototyping.
- `npm run db:seed` populates development seed data.

## Coding Style & Naming Conventions

Keep TypeScript strict and prefer explicit domain types over `any`. Follow the existing two-space indentation and nearby quote/semicolon style; avoid formatting unrelated code. Name React components and exported types in PascalCase, functions and variables in camelCase, and hooks with a `use` prefix. Use kebab-case filenames such as `ai-chatbot.tsx`; Next.js handlers remain `route.ts`. Keep client-only modules marked with `'use client'`, and keep database and secret-dependent code on the server.

## Testing Guidelines

No automated test framework or coverage threshold is currently configured. Before submitting, run `npm run lint` and `npm run build`, then manually exercise affected dashboard and API flows. When adding tests, prefer colocated `*.test.ts` or `*.test.tsx` files and cover authorization, validation, tool failures, and React Query cache updates. Add the corresponding test script to `package.json`.

## Commit & Pull Request Guidelines

Recent history generally uses short Conventional Commit-style subjects: `feat:`, `fix:`, `chore:`, and `refactor:`; optional scopes are acceptable, for example `fix(ui): prevent dialog overflow`. Keep each commit focused. Pull requests should explain the user-visible change, link relevant issues, list verification commands, and include screenshots or recordings for UI changes. Call out Prisma migrations, new environment variables, and API compatibility changes explicitly.

## Security & Configuration

Copy `.env.local.example` to `.env.local`; never commit real database, OAuth, Groq, Resend, or auth secrets. Every team-scoped API mutation must verify both authentication and team membership/role before accessing data.
