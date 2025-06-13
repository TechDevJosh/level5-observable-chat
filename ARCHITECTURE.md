# Level 5: Real-Time Observable Chat Application

## 🧠 Overview

This is a real-time, multi-room chat application built with a modular AI-assisted workflow. The system slice was scaffolded using Next.js + Tailwind + Supabase and hardened through human-in-the-loop debugging and observability planning.

It is part of a larger composable architecture designed under the Modular Assembly Framework.

---

## 🧱 Stack

| Layer         | Tech                                            |
| ------------- | ----------------------------------------------- |
| Frontend      | Next.js 15 App Router, Tailwind CSS             |
| Backend       | Supabase (PostgreSQL + Realtime)                |
| Auth          | LocalStorage (temporary), planned Supabase Auth |
| Observability | Custom `logMessage()` + metrics stub            |
| CI/CD         | Manual for now, planned DevSecOps scaffold      |
| Deployment    | Localhost (planned: Vercel)                     |

---

## 🧩 Features

- Multi-room support: `#general`, `#dev`, `#support`
- Realtime streaming of messages via Supabase Channels
- Username remembered in `localStorage`
- Observer function logs total message volume by room
- Room selector updates query + subscription live
- Message rendering with chat alignment (future bubble UX)

---

## 🗺 System Component Map

┌────────────────────────────┐
│ User Interface │
│ - Room select │
│ - Message list + input │
└────────────┬───────────────┘
│
▼
┌────────────────────────────┐
│ Chat Controller │
│ - useState (input, room) │
│ - useEffect (subscription)│
│ - sendMessage() helper │
└────────────┬───────────────┘
│
▼
┌────────────────────────────┐
│ Supabase Layer │
│ - messages table (RLS off)│
│ - Realtime subscription │
└────────────┬───────────────┘
│
▼
┌────────────────────────────┐
│ Observability Stub │
│ - logMessage(room) │
│ - In-memory count │
└────────────────────────────┘

yaml
Copy
Edit

---

## 📉 Cost Constraints

- **Hosting**: Free-tier Supabase + Vercel (planned)
- **Realtime**: Realtime WebSocket over Supabase, no extra infra
- **Storage**: PostgreSQL `messages` table
- **Optimization**: Uses client-side localStorage (no auth lookup)

---

## 🔒 QA & Hardening (Next Step)

### Use this directive:

Act as a Senior Realtime Security Engineer.

Review message insertion and sanitization. Are we at risk for XSS?

Simulate a large payload insert. Do oversized inputs crash the app?

Audit localStorage name usage. Can it be spoofed?

Check whether Supabase RLS is enabled. If not, recommend RLS policy to isolate rooms per user.

Propose schema evolution for message moderation (is_flagged, deleted_at).

yaml
Copy
Edit

---

## 👥 Role Delegation Matrix

| Module        | Human Role        | AI Assistant Role                   |
| ------------- | ----------------- | ----------------------------------- |
| Realtime Chat | Frontend Engineer | Scaffold initial code, add tailwind |
| Supabase      | DBA / Architect   | Create schema + insert logic        |
| Observability | DevOps            | AI generated `logMessage()` stub    |
| QA            | Security Engineer | Prompt-based test scenarios         |

---

## 🔧 Deployment Plan (Planned)

- Push to GitHub → connect to Vercel
- Add Supabase keys to Vercel env vars
- Test `npm run build` for SSR compatibility

---

## 🧠 Lessons from Level 5

- Tailwind + PostCSS CLI issues are common on Windows/OneDrive — recommend moving projects to `C:/Projects`
- RLS must be added ASAP before public launch
- Local-only user names are effective for demoing multi-user presence logic

---
