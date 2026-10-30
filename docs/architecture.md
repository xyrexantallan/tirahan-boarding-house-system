# Architecture

## High-Level
- **Frontend:** React single-page app, deployed on Vercel.
- **Backend:** Supabase provides authentication, PostgreSQL, and file storage.
- **Communication:** React calls Supabase directly via the Supabase JS client.

## Folder Structure
src/
├── app/ router, providers, layouts
├── features/ one folder per business module
├── components/ui/ shared UI primitives
├── lib/ supabase client, utilities
├── hooks/ shared hooks
└── types/ generated database types

## Data Flow
1. User submits a form (React Hook Form + Zod).
2. TanStack Query mutation calls the Supabase API.
3. On success, the query cache is invalidated and the list refetches.
4. Supabase row-level security enforces role-based access.

## Database Tables
- users
- tenants
- rooms
- assignments
- meter_readings
- invoices
- invoice_line_items
- payments
- maintenance_requests
- maintenance_updates
- audit_logs
- notifications
- settings

## Security
- Authentication handled by Supabase Auth.
- Row-level security policies restrict Staff from editing billing data.
- All secrets live in `.env`, never committed to Git.

## Deployment
- Frontend: Vercel (connected to GitHub `main` branch).
- Backend: Supabase (free tier).