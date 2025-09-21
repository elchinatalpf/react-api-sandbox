# React API Explorer - Learning Journey

## 🎯 Project Goals
Build an interactive React 19 application to study and practice all React library APIs through interactive pop-up cards sourced from JSON. Starting small (1-2 pages, 3-5 APIs) and scaling incrementally to create a comprehensive React learning platform.

## 🚀 Quick Setup

### Prerequisites
- Node.js 18+
- npm (comes with Node.js)

### Installation
```bash
# Clone the repository
git clone <your-repo-url>
cd react-api-sandbox

# Install dependencies
npm install

# Start development server with JSON Server
npm run dev:all
```

## 📋 Available Scripts

### Development
- `npm run dev` - Start Vite development server
- `npm run dev:all` - Start both Vite dev server and JSON Server concurrently
- `npm run server` - Start JSON Server only (port 3001)

### Code Quality
- `npm run lint` - Run ESLint on src directory
- `npm run format` - Format code with Prettier
- `npm run typecheck` - Run TypeScript compiler checks

### Security & Dependencies
- `npm run security-audit` - Run npm audit for high-level vulnerabilities
- `npm run deps-check` - List installed dependencies

### Testing
- `npm run test:unit` - Run Vitest unit tests (when implemented)
- `npx playwright test` - Run Playwright E2E tests (when implemented)

### Production
- `npm run build` - Build for production
- `npm run preview` - Preview production build

## 🏗️ Tech Stack
- **Frontend**: React 19 + TypeScript + Vite
- **Routing**: TanStack Router (file-based, type-safe)
- **State Management**: TanStack Query (server state, optimistic updates)
- **Styling**: Tailwind CSS 4
- **Backend**: JSON Server (mock REST API)
- **Validation**: Zod (runtime type validation)
- **Testing**: Playwright (E2E) + Vitest (unit tests)
- **Code Quality**: ESLint + Prettier + Husky (pre-commit hooks)

## 🎓 Learning Focus
This project focuses on mastering React 19 APIs through hands-on practice:

1. **React 19 APIs**: Hooks, components, utilities through interactive demos
2. **TypeScript**: Type-safe development with Zod validation
3. **Modern Routing**: File-based routing with TanStack Router
4. **Server State**: Optimistic updates and caching with TanStack Query
5. **Testing**: E2E with Playwright, unit tests with Vitest
6. **Accessibility**: ARIA labels, focus management, keyboard navigation
7. **Performance**: Lazy loading, Suspense, React Profiler integration

## 📁 Project Structure (Planned)
```
src/
├── routes/                    # TanStack Router file-based routing
│   ├── __root.tsx             # Root layout with providers
│   ├── index.route.tsx        # Homepage with API cards
│   └── apis.[category].[apiName].route.tsx  # Dynamic routes
├── components/
│   ├── ApiCard.tsx            # Card component with modal trigger
│   ├── ApiModal.tsx           # Portal-based modal with demos
│   └── LiveDemo.tsx           # Interactive API demonstrations
├── schemas/
│   └── api.schema.ts          # Zod validation schemas
├── hooks/                     # Custom React hooks
├── utils/                     # Helper functions
└── types/                     # TypeScript type definitions
```

## 🧪 Testing Strategy (Planned)
- **Unit Tests**: Vitest for component testing
- **E2E Tests**: Playwright for user flows
- **Accessibility**: Keyboard navigation and screen reader testing
- **Performance**: React Profiler and Lighthouse audits

## 🔄 Development Workflow
This project follows a phase-based development approach:

1. **Phase 0**: Tooling setup ✅
2. **Phase 1**: Core dependencies and Tailwind configuration
3. **Phase 2**: TanStack Router setup with file-based routing
4. **Phase 3**: JSON Server backend and TanStack Query integration
5. **Phase 4**: Initial API cards with portal-based modals
6. **Phase 5**: Expanded APIs and optimistic updates
7. **Phase 6**: Testing setup (Playwright + Vitest)
8. **Phase 7**: Advanced features and deployment

## 🚨 Security Notice
This project follows security-first installation protocols due to npm supply chain attacks in 2025. All dependencies use exact versions without ranges (^, ~) and undergo security audits.

## 🤝 Contributing
This is a learning project. Feel free to explore, experiment, and learn along!

---

**Status**: Phase 0 Complete - Tooling Setup ✅
