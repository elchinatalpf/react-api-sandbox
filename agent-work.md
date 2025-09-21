# Agent-Work.md: React API Explorer Project Instructions

## Project Overview
Goal: Build a React 19 app with TypeScript to study and practice all React library APIs via interactive pop-up cards sourced from JSON. Start small (1-2 pages, 3-5 APIs), scale incrementally. Cards display API name, description, code snippet, live demo, and usage (e.g., via Profiler). Use pop-ups/modals for details, practicing portals and accessibility.

Tech Stack:
- React 19 + TypeScript + Vite
- TanStack Router (file-based, type-safe, with loaders for data prefetching)
- TanStack Query (server state, optimistic updates)
- Tailwind CSS 4 (styling)
- JSON Server (mock backend)
- Zod (validation)
- Playwright (E2E testing)
- Additional: ESLint/Prettier/Husky for code quality, Vitest for unit tests, concurrently for dev scripts

Workflow: Agents (GitHub Copilot, Claude) read this file and implement phases. Human: Review changes via Git, commit, and proceed. Use VS Code on Windows/Mac. After each phase, run `npm run lint` and `npm run typecheck` for checks.

- Manual: Create project root if not exists: `npm create vite@latest react-api-explorer -- --template react-ts`. Git init and commit initial.  
  _If possible, automate via script/agent._
- Agent (Copilot/Claude): Install dev deps for tooling: `npm i -D eslint prettier eslint-config-prettier eslint-plugin-react @typescript-eslint/eslint-plugin @typescript-eslint/parser husky concurrently vitest @testing-library/react @testing-library/jest-dom jsdom`
- Agent: Configure ESLint: Create `.eslintrc.json` with extends: ['eslint:recommended', 'plugin:react/recommended', 'plugin:@typescript-eslint/recommended'], plugins: ['react', '@typescript-eslint'], rules for hooks, etc.
- Agent: Configure Prettier: Create `.prettierrc` with semi: true, singleQuote: true, etc. Add ESLint integration.
- Agent: Set up Husky: `npx husky init`, add pre-commit hook: `npm run lint && npm run format`.
- Manual: Update `tsconfig.json` for strict mode: "strict": true.  
  _If possible, automate via script/agent._
- Agent: Add scripts to package.json: "lint": "eslint src --ext ts,tsx", "format": "prettier --write src", "typecheck": "tsc --noEmit".
- Manual: Create README.md with: Project goals, setup instructions (npm i, npm run dev:all), dev scripts, how to run tests/JSON Server, learning focus on React APIs.  
  _If possible, automate via script/agent._
- Git: Commit as "Phase 0: Tooling setup".

### Agent Log (Phase 0)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 1: Project Setup and Installation
- Agent: Install core dependencies: `npm i @tanstack/react-router @tanstack/react-query tailwindcss@latest postcss autoprefixer zod json-server`
- Agent: Init Tailwind: `npx tailwindcss init -p`. Config `tailwind.config.js`: Add content: ['./index.html', './src/**/*.{ts,tsx}'].
- Agent: Add dev scripts to package.json: "dev": "vite", "server": "json-server --watch db.json --port 3001", "dev:all": "concurrently \"npm run dev\" \"npm run server\"".
- Manual: Pin key versions in package.json (e.g., "react": "^19.0.0-rc", "@tanstack/react-query": "^5.0.0"). Run `npm i` to update lockfile.  
  _If possible, automate via script/agent. Agent should determine the latest compatible, stable versions for all dependencies and update package.json accordingly, then run `npm install` to ensure no errors or warnings. Log any version conflicts or issues._
- Manual: Start `npm run dev:all`. Verify blank app runs, no port collisions (adjust PORT env if needed).  
  _If possible, automate via script/agent._
- Git: Commit as "Phase 1: Core setup and deps". Human Review: Run lint/format.

### Agent Log (Phase 1)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 2: Basic Layout and Routing
- Agent: Set up TanStack Router with file-based routing.
  - Create `src/routes` folder: `__root.tsx` (root layout with QueryClientProvider), `index.route.tsx` (homepage), `apis.[category].[apiName].route.tsx` (dynamic detail route).
  - In `main.tsx`: Import createRouter, render RouterProvider. Use route loaders for data prefetching (practice Suspense).
  - Add type-safe params: Use generateRouteTypes or similar for navigation.
- Agent: Basic layout in `__root.tsx`: Header nav, main content. Use Tailwind for grid/styling.
- Manual: Test routes in browser (e.g., /, /apis/hooks/useState).  
  _If possible, automate via script/agent. Use Playwright scripts to automate browser-based checks for routing, navigation, and accessibility where possible._
- Agent: Import React Query DevTools in dev mode.
- Git: Commit as "Phase 2: Routing and layout". Human Review: Navigate routes, check types.

### Agent Log (Phase 2)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 3: Mock Backend and Data Fetching
- Manual: Create `db.json` with sample schema (add 3-5 entries initially):  
  _If possible, automate via script/agent._
  {
    "apis": [
      { "id": 1, "name": "useState", "category": "Hooks", "shortDescription": "Manages state", "longDescription": "Detailed explanation...", "exampleCode": "const [count, setCount] = useState(0);", "tags": ["state"], "favorite": false }
    ]
  }
- Agent: Set up Zod schema in `src/schemas.ts`: e.g., import { z } from 'zod'; export const apiSchema = z.object({ id: z.number(), name: z.string(), category: z.string(), shortDescription: z.string(), longDescription: z.string(), exampleCode: z.string(), tags: z.array(z.string()), favorite: z.boolean() });
- Agent: Integrate TanStack Query.
  - Create QueryClient in `__root.tsx` with defaults: { queries: { staleTime: 1000 * 60 } }.
  - In `index.route.tsx`: Use useQuery to fetch '/apis', validate with Zod (e.g., apiSchema.array().parse(data)).
  - For detail routes: Use loaders to prefetch individual API data.
- Manual: Run `npm run dev:all`, verify fetch. Handle errors (e.g., show UI if server down).  
  _If possible, automate via script/agent._
- Git: Commit as "Phase 3: Backend and fetching". Human Review: Check console for Zod validation.

### Agent Log (Phase 3)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 4: Initial API Cards and Pop-ups
- Agent: Create `src/components/ApiCard.tsx`: Renders card with details; on click, opens pop-up modal via React.createPortal.
  - Add live demo: e.g., for useState, a counter component.
  - Start with 3 APIs: useState, useEffect, Fragment. Lazy-load demos with React.lazy + Suspense.
  - Accessibility: Add role="dialog", aria-modal="true", focus trap (useEffect for ESC key), ARIA labels.
- Agent: In homepage: Map fetched data to ApiCard list; handle clicks to open modals.
- Agent: Style with Tailwind (responsive modals, transitions).
- Manual: Test interactions; verify keyboard nav (focus trap, ESC close).  
  _If possible, automate via script/agent. Use Playwright scripts to automate browser-based checks for modals, focus management, and accessibility._
- Git: Commit as "Phase 4: Basic cards". Human Review: Test a11y with browser tools.

### Agent Log (Phase 4)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 5: Adding More APIs and Features
- Agent: Expand db.json with next APIs (e.g., memo, useContext). Update routes/components to handle.
- Agent: Add optimistic updates: Use useMutation for PATCH /apis/:id (toggle favorite), with onMutate rollback.
- Agent: Integrate utilities: forwardRef in modals, startTransition for updates.
- Manual: Review props/types; add custom if needed.  
  _If possible, automate via script/agent._
- Git: Commit as "Phase 5: Expanded APIs". Human Review: Test mutations.

### Agent Log (Phase 5)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 6: Testing and Optimization
- Agent: Set up Playwright: `npx playwright install`. Create tests/e2e.spec.ts: e.g., test loads APIs, clicks open modal, asserts state.
- Agent: Set up Vitest: Add to scripts "test:unit": "vitest". Write unit tests for ApiCard (e.g., renders snapshot, toggles favorite).
- Agent: Add edge cases: Empty list, malformed data (Zod safeParse), network errors (retry), rapid favorites (race conditions), modal ESC.
- Agent: Add GitHub Actions: Create `.github/workflows/ci.yml` with steps: install, lint, typecheck, test:unit, playwright test.
- Manual: Run `npm run test:unit` and `npx playwright test`.  
  _If possible, automate via script/agent. Use Playwright scripts to automate browser-based checks for routing, modals, and accessibility._
- Agent: Wrap app in Profiler/Suspense for performance.
- Git: Commit as "Phase 6: Testing". Human Review: CI run on push.

### Agent Log (Phase 6)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Phase 7: Advanced Expansions and Deployment
- Agent: Add remaining APIs in batches (components like StrictMode, directives like 'use client').
- Agent: Implement advanced: e.g., use server in a component for React 19 practice.
- Manual: Deploy to Vercel/Netlify: Add vercel.json for rewrites if needed.  
  _If possible, automate via script/agent._
- Git: Commit as "Phase 7: Full expansions". Human Review: Production test.

### Agent Log (Phase 7)
- _Agent: Log all actions performed, what was skipped (and why), and any issues encountered during automation for this phase. This section is for recovery and audit._

## Ongoing: Human Review Loops
After each phase:
- Pull changes, run `npm run dev:all`.
- Test manually (browser, console).
- Run lint/format/typecheck.
- If issues: Note here, re-prompt agent.
- Commit and proceed.