# 🧭 Feature-Driven Architecture (FDA) — Overview

Feature-Driven Architecture (FDA) is a **modular and scalable way to structure modern web applications**, designed to reduce complexity in large React/Next.js codebases. Instead of organizing files by type (components, hooks, utils, etc.), FDA organizes by **feature**, creating self-contained, reusable modules.

---

## 🎯 What Is Feature-Driven Architecture?

Traditional folder-by-type architectures often lead to fragmentation — you end up navigating between multiple folders just to work on a single feature. FDA solves this by grouping everything related to a specific feature (UI, logic, state, API) into one cohesive unit.

Each feature owns its own domain logic, minimizing coupling and making refactoring safer and faster.

**In short:** each feature is a mini-application that can live, evolve, and be maintained independently.

---

## 🧩 Core Principles

1. **Feature encapsulation** — Each feature manages its own logic, types, and UI.
2. **Plug-and-play** — Features can be added, removed, or migrated without breaking the app.
3. **Independence** — No direct dependencies between features; share only through `shared/`.
4. **Consistency** — Shared naming conventions and structure across all features.
5. **Scalability** — Works seamlessly from small apps to multi-team monorepos.

---

## 🗂️ Global Directory Structure

```
your-project/
├── src/
│   ├── app/                → Next.js App Router (public & admin routes)
│   ├── feature/            → Core feature modules
│   ├── shared/             → Cross-feature utilities, UI, hooks
│   ├── providers/          → React context providers
│   ├── styles/             → Global styles & design tokens
│   └── types/              → Global shared TypeScript types
├── public/                 → Static assets
├── tests/                  → Integration & e2e tests
└── config/                 → Environment & build configuration
```

---

## 🧱 Feature Structure

Each feature is **self-contained**, following the same internal layout:

```
src/feature/<feature-name>/
├── api/                → Next.js API handlers or client utilities
│   ├── api<Feature>.ts → Main feature API entry (re-exported in /app/api)
│   └── client/         → Optional: feature-specific API client
├── components/         → UI components specific to this feature
├── hooks/              → React hooks for this feature
├── lib/                → Server actions or internal logic
├── queries/            → React Query hooks
├── options/            → Query configuration
├── schemas/            → Zod validation schemas
├── stores/             → Zustand state management
├── types/              → Feature-specific types
└── index.ts            → Central export for the feature API & hooks
```

---

## 🔗 App Router Integration

API handlers are re-exported from their feature modules into the Next.js `app/api` layer:

```ts
// src/app/api/admin/user/route.ts
export { GET, POST } from "@/feature/user/api/apiUser";
```

UI routes can directly consume hooks, queries, and components from the same feature:

```tsx
// src/app/admin/user/page.tsx
import { useUsers } from "@/feature/user/queries/useUsers";
import { UserTable } from "@/feature/user/components/UserTable";
```

---

## 🧠 Shared Logic

| Folder              | Purpose                                               |
| ------------------- | ----------------------------------------------------- |
| `src/shared/ui/`    | Design system & UI primitives (buttons, modals, etc.) |
| `src/shared/lib/`   | Utilities, helpers, constants, config functions       |
| `src/shared/hooks/` | Generic reusable React hooks                          |
| `src/shared/types/` | Global shared types & interfaces                      |

---

## ✍️ Naming Conventions

| Type             | Convention      | Example          |
| ---------------- | --------------- | ---------------- |
| React Query hook | `use` prefix    | `useUserList.ts` |
| Zustand store    | `Store` suffix  | `userStore.ts`   |
| Zod schema       | `Schema` suffix | `userSchema.ts`  |
| API handler      | `api` prefix    | `apiUser.ts`     |
| Component        | PascalCase      | `UserTable.tsx`  |

---

## 🚀 Workflow for New Features

1. Create a folder under `src/feature/<feature>`.
2. Add only the needed layers:

    * `lib/` → server actions & logic
    * `queries/`, `options/` → React Query setup
    * `stores/` → Zustand state
    * `schemas/` → Zod validation
    * `components/` → UI layer
3. Expose APIs via re-exports in `/app/api/...`.
4. Keep cross-feature logic in `src/shared` only.

---

## ⚙️ Core Design Patterns

* **Server Actions** → inside `lib/`
* **API Handlers** → inside `api/`, re-exported in `app/api/`
* **Data Fetching** → `queries/` + `options/` via React Query
* **State Management** → `stores/` via Zustand
* **Validation** → `schemas/` via Zod
* **Type Safety** → `types/` via TypeScript

---

## 💡 Example: User Feature

```
src/feature/user/
├── api/
│   └── apiUser.ts
├── components/
│   └── UserTable.tsx
├── lib/
│   └── userActions.ts
├── queries/
│   └── useUsers.ts
├── stores/
│   └── userStore.ts
├── schemas/
│   └── userSchema.ts
├── types/
│   └── userTypes.ts
└── index.ts
```

---

## 🧩 Why FDA Works

Feature-Driven Architecture makes scaling easier because:

* Teams can work independently on features.
* Code is easier to find, test, and refactor.
* New contributors instantly understand structure.
* Deployments and refactors are safer and faster.

---

Let’s build scalable apps — one feature at a time. 🚀
