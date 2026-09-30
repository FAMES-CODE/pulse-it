<div align="center">

# 💓 Pulse It

**Uptime and API monitoring, made simple.**

Track your endpoints, measure response times, and get notified about incidents before your users do.

![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=nextdotjs)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-7-2D3748?logo=prisma)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-06B6D4?logo=tailwindcss&logoColor=white)


</div>

---

## ✨ Overview

**Pulse It** is a full-stack monitoring SaaS built with Next.js. It lets you register HTTP endpoints ("monitors"), checks them automatically on a schedule through a background worker, and turns the results into a clear dashboard: uptime, response times, check history and incidents.

## 🚀 Features

- **Monitor management**: create, list, search, filter, enable/disable and delete monitors
- **Fully configurable checks**: name, URL, HTTP method, custom headers, request body, expected status code, interval and timeout
- **Background worker**: a dedicated process runs the checks on schedule, independently of the web app
- **Dashboard overview**: global stats, monitor health and recent activity at a glance
- **Detailed monitor view**: uptime, response-time charts, check history, incidents and configuration
- **Incident tracking**: failed checks are recorded so you can see when and why a service went down
- **GitHub authentication**: sign in with GitHub through Auth.js
- **Light / dark theme**: with a polished UI built on shadcn/ui and Tailwind CSS

## 🧱 Tech Stack

| Layer      | Technology                                          |
| ---------- | --------------------------------------------------- |
| Framework  | Next.js 16 (App Router), React 19, TypeScript       |
| UI         | Tailwind CSS 4, shadcn/ui, Base UI, Lucide, next-themes |
| Charts     | Recharts                                            |
| Database   | PostgreSQL + Prisma 7 (`@prisma/adapter-pg`)        |
| Auth       | Auth.js v5 (next-auth) + Prisma adapter, GitHub OAuth |
| Validation | Zod                                                 |
| Tooling    | ESLint, Prettier, tsx                               |

## 🏗️ Architecture

Pulse It runs as two cooperating processes sharing one database:

```
┌────────────────────┐        ┌──────────────────┐
│  Next.js web app   │◄──────►│   PostgreSQL     │
│  (UI + auth + API) │        │   (via Prisma)   │
└────────────────────┘        └────────▲─────────┘
                                       │
                              ┌────────┴─────────┐
                              │  Monitor worker  │
                              │  (scheduled      │
                              │   HTTP checks)   │
                              └──────────────────┘
```

```
├── app/          # Routes, layouts and pages (App Router)
├── components/   # UI components (shadcn/ui + app components)
├── hooks/        # Custom React hooks
├── lib/          # Shared utilities (Prisma client, helpers)
├── prisma/       # Database schema and migrations
├── worker/       # Background process running the monitor checks
├── public/       # Static assets
├── auth.ts       # Auth.js configuration
└── proxy.ts      # Route protection
```

## 🛠️ Getting Started

### Prerequisites

- Node.js 20+
- A PostgreSQL database
- A [GitHub OAuth app](https://github.com/settings/developers) (callback URL: `http://localhost:3000/api/auth/callback/github`)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/FAMES-CODE/pulse-it.git
cd pulse-it

# 2. Install dependencies
npm install

# 3. Configure environment variables
cp .env.example .env   # then fill in the values below
```

### Environment variables

```env
DATABASE_URL="postgresql://user:password@localhost:5432/pulseit"
AUTH_SECRET="generate-with: npx auth secret"
AUTH_GITHUB_ID="your-github-oauth-client-id"
AUTH_GITHUB_SECRET="your-github-oauth-client-secret"
```

### Database setup

```bash
npx prisma generate
npx prisma migrate dev
```

### Run the app

```bash
# Terminal 1: web app
npm run dev

# Terminal 2: background worker that runs the checks
npm run worker
```

Open [http://localhost:3000](http://localhost:3000) and sign in with GitHub.

## 📜 Available Scripts

| Script              | Description                            |
| ------------------- | -------------------------------------- |
| `npm run dev`       | Start the Next.js dev server           |
| `npm run build`     | Build for production                   |
| `npm run start`     | Start the production server            |
| `npm run worker`    | Start the monitoring worker            |
| `npm run lint`      | Lint the codebase                      |
| `npm run typecheck` | Run the TypeScript compiler (no emit)  |
| `npm run format`    | Format code with Prettier              |


## 👤 Author

**Amine Ferkani**

- GitHub: [@FAMES-CODE](https://github.com/FAMES-CODE)
- LinkedIn: [linkedin.com/in/amineferkani](https://linkedin.com/in/amineferkani)

---

<div align="center">Built with Next.js, Prisma and a lot of pulse checks 💓</div>