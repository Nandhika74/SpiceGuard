# 🌿 SpiceGuard Hub

Real-time, mobile-first project tracker for the four-person SpiceGuard team running a six-month Proof of Concept with **Plant Lipids**.

## ✨ Features

- **Real-time collaboration**: Tasks, milestones, meetings, comments, documents, notifications, and activity updates sync across devices.
- **Invite-only access**: Supabase authentication is restricted to the `allowed_emails` table.
- **Role-based permissions**:
  - All team members can create and edit milestones, tasks, meetings, and documents.
  - Only the Team Lead can delete milestones.
  - Tasks can be deleted by their creator or the Team Lead, with a 10-second undo option.
  - Meetings and documents can be edited or deleted by their creator/uploader or the Team Lead.
- **Milestones**:
  - Progress is calculated automatically from completed tasks.
  - Drag-and-drop reordering, archiving/restoring, and duplication with tasks.
  - Rescheduling records the reason and original date, displays a badge, and writes to `milestone_date_history`.
- **Task workspace**:
  - List, Kanban, and Timeline/Gantt views.
  - Inline editing, reassignment, milestone transfers, priorities, deadlines, overdue warnings, and rich comments.
  - Validation warns when a task deadline exceeds its milestone date.
- **Meetings and inference recorder**:
  - Agendas, rich notes, decisions, critical inferences, guest attendees, and attachments.
  - Convert action items into tasks in any milestone.
- **Research and documents hub**:
  - Upload PDF, DOCX, XLSX, CSV, PPTX, images, and `.ipynb` files up to 25 MB.
  - External links, categories, tags, and document previews.
- **Dashboard and activity log**:
  - PoC completion, final-milestone countdown, upcoming deadlines, overdue alerts, and live activity.
- **Progressive Web App**:
  - Installable on mobile and desktop with online/offline status feedback.

## 👥 Seed Members

| Name | Role |
| :--- | :--- |
| **Nithyasree M** | Team Lead & ML Developer |
| **Nandhika S** | ML Engineer |
| **Sivakumaran S** | Biotech Researcher |
| **Abhijith Sriram V** | IoT Engineer |

## 🛠️ Tech Stack

- React 19 and TypeScript
- Vite and Tailwind CSS
- Supabase Auth, PostgreSQL, Realtime, Row Level Security, and Storage
- Vite PWA
- Lucide React and Motion

## 🚀 Local Setup

### Prerequisites

- Node.js and npm
- A [Supabase](https://supabase.com/) project

### 1. Install dependencies

```bash
npm install
```

### 2. Configure Supabase

Copy `.env.example` to `.env.local` and set:

```bash
VITE_SUPABASE_URL="https://your-project.supabase.co"
VITE_SUPABASE_ANON_KEY="your-anon-key"
```

In the Supabase Dashboard:

1. Open **SQL Editor** and run the complete [`supabase-schema.sql`](./supabase-schema.sql) script.
2. Confirm that the `spiceguard-docs` storage bucket and its policies were created.
3. Add or update authorized members in `public.allowed_emails`:

```sql
INSERT INTO public.allowed_emails (email, full_name, role, is_team_lead, avatar_color)
VALUES ('your-email@example.com', 'Your Name', 'Your Role', FALSE, '#14532D')
ON CONFLICT (email) DO NOTHING;
```

The schema creates the application tables, RLS policies, helper functions, triggers, storage policies, realtime configuration, and starter milestones/tasks.

### 3. Start the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## 📦 Scripts

| Command | Description |
| :--- | :--- |
| `npm run dev` | Start the Vite development server on port 3000 |
| `npm run build` | Create a production build in `dist/` |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run the TypeScript compiler without emitting files |

## 🚢 Deployment

Deploy the Vite application to Vercel, Netlify, or another static hosting provider.

- **Build command:** `npm run build`
- **Output directory:** `dist`
- **Required environment variables:** `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`

Configure the same Supabase environment variables in the hosting provider's project settings. Do not commit `.env.local` or Supabase keys to source control.
