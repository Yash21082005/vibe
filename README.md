# Vibe

Vibe is an **AI‑powered project builder** that lets you describe what you want to build in natural language (“Build a Netflix clone”, “Create an admin dashboard”, etc.) and spins up a full project workspace for you.

Each project keeps a history of AI messages and generated code fragments, with a split‑pane UI for **chat**, **live preview**, and **code** so you can iterate quickly.

> Live demo: https://vibe-inky-sigma.vercel.app  
> Source: https://github.com/Yash21082005/vibe

---

## Features

- **Chat‑driven project creation**  
  Type a prompt (or pick from templates like *Netflix clone*, *Kanban board*, *Spotify UI*) and Vibe creates a new project and kicks off an AI “code agent” run in the background.

- **Persistent projects & history**  
  Projects, messages, and generated code fragments are stored in PostgreSQL via Prisma so you can revisit and continue past work.

- **Multi‑pane project workspace**  
  A resizable layout with:
  - Chat/messages stream  
  - Live preview (“Demo”) tab  
  - Code tab with file explorer and syntax‑highlighted files

- **Authentication & usage limits**  
  User accounts handled via Clerk, with a simple **credits/usage** model to control how many AI runs a user can perform and a **pricing/upgrade** path for Pro access.

- **Modern, responsive UI**  
  Built with Radix UI primitives, Tailwind‑style utilities, Lucide icons, dark‑mode support, and smooth toasts for feedback.

---

## Tech Stack

- **Frontend**
  - Next.js (App Router) & TypeScript
  - React 19
  - Radix UI + Tailwind‑style utilities
  - React Hook Form + Zod for form validation
  - React Query for client caching and mutations
  - `react-resizable-panels` for the split layout

- **Backend**
  - tRPC (type‑safe APIs between client and server)
  - Prisma ORM with PostgreSQL (`prisma/schema.prisma`)
  - Inngest for background jobs (`code-agent/run` event)
  - OpenAI via `openai` SDK
  - Rate limiting & credit tracking (`Usage` model)

- **Auth & Identity**
  - Clerk (`@clerk/nextjs`, `@clerk/themes`)

- **Tooling**
  - ESLint, TypeScript, Prisma Client
  - Turbopack dev server (`next dev --turbopack`)

---

## Project Structure (high level)

- `src/app/(home)` – Marketing/home experience (landing page, sign‑in/sign‑up, pricing)
- `src/app/projects` – Project routes and views
- `src/modules/home` – Home page UI (project prompt form, templates, project list)
- `src/modules/projects`  
  - `server/` – tRPC procedures for creating and fetching projects  
  - `ui/` – Project workspace components (header, messages, file explorer, preview/code tabs)
- `src/modules/messages` – Message handling for project chats
- `prisma/schema.prisma` – Database schema for `Project`, `Message`, `Fragment`, and `Usage`
- `prisma/migrations` – Prisma migrations
- `prisma.config.example.txt` – Example Prisma config using `DATABASE_URL`

---

## Getting Started

### Prerequisites

- Node.js 18+  
- PostgreSQL database (local or hosted)  
- NPM / Yarn / PNPM / Bun  
- API keys and config for:
  - **Clerk** (publishable + secret keys)
  - **OpenAI** (`OPENAI_API_KEY`)
  - **Inngest** (event/signing keys)
  - A `DATABASE_URL` for PostgreSQL

> Check the codebase for all `process.env.*` usages and create the matching variables in your environment.

### 1. Clone and install

git clone https://github.com/Yash21082005/vibe.git
cd vibe

# install dependencies
npm install
# or
yarn
# or
pnpm install
# or
bun install

