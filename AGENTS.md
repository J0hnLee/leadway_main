# AGENTS.md

This repo is a Next.js 15 + React 19 app with Tailwind + TypeScript.
These notes guide coding agents and automation in this workspace.
Prefer minimal, focused changes that match existing patterns.
If instructions conflict, follow repo configs first, then these notes.

## Environment
- Node.js >= 20 (`package.json` engines).
- Package manager: `pnpm@9.1.0`.
- App runs in Next.js App Router (`app/`).

## Core Commands (pnpm)
- Install: `pnpm install --frozen-lockfile`
- Dev server: `pnpm dev`
- Build: `pnpm build`
- Start prod server: `pnpm start`
- Analyze bundle: `pnpm analyze`

### Linting & Formatting
- Lint: `pnpm lint`
- Auto-fix lint: `pnpm lint:fix`
- Prettier check: `pnpm prettier`
- Prettier write: `pnpm prettier:fix`
- Format (TS/TSX/MD): `pnpm format`

### Unit/Integration Tests (Jest)
- Run all tests: `pnpm test`
- Run a single file: `pnpm test -- path/to/test-file.test.tsx`
- Run by name: `pnpm test -- -t "test name"`
- Watch mode: `pnpm test -- --watch`

### E2E Tests (Playwright)
- Headless run: `pnpm e2e:headless`
- UI runner: `pnpm e2e:ui`
- Single file: `pnpm e2e:headless -- e2e/path/to/spec.ts`
- Single test by title: `pnpm e2e:headless -- -g "test name"`
- Uses `pnpm dev` via Playwright `webServer`.

### Storybook
- Dev server: `pnpm storybook`
- Build: `pnpm build-storybook`
- Test runner (smoke/plays): `pnpm test-storybook`

### Other Utilities
- Coupling graph: `pnpm coupling-graph` (outputs `graph.svg`).
- Postinstall patches: `pnpm postinstall` (runs automatically).

## Code Style
Follow ESLint + Prettier configurations in repo.
Prettier settings: 2 spaces, 120 width, no semicolons, trailing comma es5.
Tailwind class sorting is enforced by `prettier-plugin-tailwindcss`.

### Imports
- Keep imports sorted (ESLint `sort-imports`).
- Order: external, builtin, internal, sibling, parent, index.
- Internal paths include top-level folders and `env`, `theme`, `public/**`.
- Alphabetize within groups, case-insensitive.
- Use absolute imports from repo root (TS `baseUrl: "."`).

### Naming & Files
- Components: `PascalCase` files and exports (e.g., `Button/Button.tsx`).
- React hooks: `useX` naming.
- Next.js pages/layouts: default export in `app/`.
- Use `camelCase` for variables, `SCREAMING_SNAKE_CASE` for constants.
- Prefer named exports for reusable components/utilities.

### TypeScript
- Strict mode enabled; avoid `any`.
- `noUncheckedIndexedAccess` is on; handle possibly `undefined`.
- Prefer `type`/`interface` definitions near usage.
- Export component props as `SomethingProps`.
- Use `VariantProps` with `cva` patterns when applicable.

### React/Next.js Patterns
- Use `"use client"` only when needed for client components.
- Keep server components default unless browser APIs are required.
- Metadata is exported as `metadata` in `app` routes.
- Favor functional components and hooks.

### Styling
- Tailwind CSS is the primary styling approach.
- Use `class-variance-authority` + `tailwind-merge` for variants.
- Prefer `className` composition via `twMerge` or `cva`.

### Error Handling
- Fail fast for impossible states: `throw new Error(...)`.
- Use early returns for invalid inputs or empty data.
- Avoid silent failures; surface errors to callers.
- Keep error messages concise and actionable.

### Testing Practices
- Jest tests live in standard `*.test.ts(x)` or `*.spec.ts(x)` files.
- Avoid reaching into `e2e/` from Jest (ignored by config).
- Playwright tests live in `e2e/`.
- Keep tests deterministic; avoid time-based flakiness.

## Repository Conventions
- ESLint ignores `.next/`, `dist/`, `build/`, `coverage/`, `*.d.ts`.
- Lint rule: unused vars prefixed with `_` are allowed.
- Pre-commit hook enforces Conventional Commits (see README).

## Cursor / Copilot Rules
- No `.cursor/rules`, `.cursorrules`, or `.github/copilot-instructions.md` found.
- If added later, append their guidance here.

## Output Expectations for Agents
- Keep changes minimal and localized.
- Match existing formatting and quoting (`"` double quotes).
- Prefer small, focused PRs/commits unless asked otherwise.
- Update tests only when behavior changes.
- Avoid unrelated refactors.

## Quick Reference
- Lint + format: `pnpm lint` and `pnpm prettier`.
- Unit tests: `pnpm test -- -t "name"`.
- E2E tests: `pnpm e2e:headless -- -g "name"`.
- Storybook test: `pnpm test-storybook`.

## Notes on Paths
- Absolute imports resolve from repo root (example: `components/Button/Button`).
- CSS entrypoint in `app/layout.tsx` imports `styles/tailwind.css`.
- Tailwind config: `tailwind.config.js`.
- ESLint config: `eslint.config.mjs`.
- Prettier config: `prettier.config.js`.
- Jest config: `jest.config.js`.
- Playwright config: `playwright.config.ts`.

## Environment Variables
- Use `env.mjs` with `@t3-oss/env-nextjs` + `zod`.
- Add new vars to `server` or `client` and `runtimeEnv`.
- Keep runtime env keys mirrored to avoid undefined access.

## When Adding New Code
- Follow existing folder structure under `app/`, `components/`, `styles/`.
- Create stories for UI components (`*.stories.tsx`) when relevant.
- Keep props typed and documented via interfaces.
- Use `React.ReactNode` for children props as needed.
- Avoid default exports except for Next.js pages/layouts.

## What Not To Do
- Do not add new formatting tools or linters.
- Do not change `package.json` scripts unless requested.
- Do not add semicolons or change quotes to single.
- Do not bypass lint rules with `eslint-disable` without justification.

## Contacts
- Project is based on Next.js Enterprise Boilerplate by Blazity.
- See `README.md` for project background and links.
