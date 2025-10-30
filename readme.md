# 🧭 Feature-Driven Architecture (FDA) for Next.js & React

> *Stop arguing about folder structures — start shipping features.*

![FDA Banner](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Szz7jX61ZUJG5QuPlFw7NA.jpeg)

---

## 🚀 What Is FDA?

**Feature-Driven Architecture (FDA)** is a scalable way to organize modern React or Next.js projects — built around **features**, not file types.
Instead of scattering logic across folders (`components/`, `hooks/`, `api/`, ...), FDA makes each feature **a self-contained mini-app** with its own UI, logic, state, and API.

It’s the architecture used in **Klickbee CMS** — but it’s framework-agnostic and works beautifully in any Next.js project.

---

## 🧩 Why It Matters

| Problem                        | FDA Solution                          |
| ------------------------------ | ------------------------------------- |
| Bloated `components/` folder   | Every feature owns its components     |
| Refactors break unrelated code | Features are isolated & independent   |
| Hard onboarding for new devs   | Predictable, self-contained structure |
| No scalability for large teams | Each team can own a feature domain    |

FDA gives you **clarity, velocity, and maintainability** — no more “where do I put this file?” debates.

---

## 🗂️ Folder Structure Example

```
src/
├── app/                  → Next.js App Router (public & admin routes)
├── feature/              → Core feature modules
│   ├── user/
│   │   ├── api/          → Next.js API handlers
│   │   ├── components/   → UI specific to user feature
│   │   ├── queries/      → React Query hooks
│   │   ├── stores/       → Zustand state
│   │   ├── schemas/      → Zod validation
│   │   └── lib/          → Server actions / business logic
│   └── settings/...
├── shared/               → Cross-feature logic (UI, hooks, lib)
├── providers/            → React context providers
├── styles/               → Global styles & tokens
└── types/                → Shared TypeScript types
```

👉 Each feature is **plug-and-play** — add or remove one without touching the others.

---

## 💡 Core Concepts

* 🧠 **Feature encapsulation** — a feature is a domain, not a folder.
* ⚙️ **Reusability by isolation** — logic is portable and testable.
* 🧱 **Predictable patterns** — same internal structure across all features.
* 🚀 **Ready for scaling** — from solo dev to multi-team monorepo.

---

## 🧠 Design Patterns

| Concern        | Location                | Tech                   |
| -------------- | ----------------------- | ---------------------- |
| Server actions | `lib/`                  | Next.js server actions |
| API handlers   | `api/`                  | Next.js route handlers |
| Data fetching  | `queries/` + `options/` | React Query            |
| Local state    | `stores/`               | Zustand                |
| Validation     | `schemas/`              | Zod                    |
| Typing         | `types/`                | TypeScript             |

---

## 🧬 Example Integration

```ts
// src/app/api/admin/user/route.ts
export { GET, POST } from "@/feature/user/api/apiUser";
```

```tsx
// src/app/admin/user/page.tsx
import { useUsers } from "@/feature/user/queries/useUsers";
import { UserTable } from "@/feature/user/components/UserTable";

export default function Page() {
  const { data } = useUsers();
  return <UserTable users={data} />;
}
```

---

## 🛠️ Tech Stack (Recommended)

* **Next.js 15** — App Router + Server Actions
* **TypeScript** — Static typing
* **React Query** — Data fetching layer
* **Zod** — Validation
* **Zustand** — State management
* **TailwindCSS** — Styling
* **ESLint + Prettier** — Consistent formatting

---

## 📖 Learn More

* [📘 Full Documentation →](./overview.md)
* [🧩 Feature Examples →](./examples/)
* [💬 Discussion & RFCs →](./discussions)

---

## 🤝 Contributing

FDA thrives on community feedback.
You can help by:

* Suggesting improvements to structure or naming
* Adding examples for specific frameworks
* Writing about your FDA adoption experience

> The first contributor to open a PR gets a permanent mention in the README ⚡

---

## 🧑‍💻 Author

**Julien Mauclair** — Founder of [Klickbee CMS](https://github.com/klickbee)
🧠 *Building scalable architecture for modern web teams.*
[LinkedIn](https://linkedin.com/in/julien-mauclair-🧑‍💻-36358a12b) • [Medium](https://medium.com/@Jmauclair)

---

## 🧱 License

MIT © 2025 — Use, remix, and build freely.

---

## 🧠 TL;DR

> Organize by feature, not by type.
> FDA = clarity + scalability + autonomy.
> Stop managing chaos, start shipping features. 🚀
