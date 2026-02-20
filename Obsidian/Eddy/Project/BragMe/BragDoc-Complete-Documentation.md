# BragDoc - Complete Project Documentation

> **Synced from**: `/Users/eddy/Documents/personal-sd-project/brag-app/brag-web`
> **Sync Date**: 2025-12-29
> **Status**: MVP Complete - Phase 1 ✅

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Product Development Requirements (PDR)](#product-development-requirements-pdr)
3. [System Architecture](#system-architecture)
4. [Tech Stack](#tech-stack)
5. [Code Standards](#code-standards)
6. [Design Guidelines](#design-guidelines)
7. [Codebase Summary](#codebase-summary)
8. [Database Setup Guide](#database-setup-guide)
9. [Authentication Configuration](#authentication-configuration)
10. [Login Disable Feature](#login-disable-feature)
11. [Deployment Guide](#deployment-guide)
12. [Project Roadmap](#project-roadmap)
13. [Development Journals](#development-journals)

---

## Project Overview

**BragDoc** - A SaaS web app for professionals to collect and organize work achievements for promotion reviews. Never forget an accomplishment again.

### Features
- **Capture Achievements**: Log code commits, design work, leadership impact, and more
- **Categorization**: Organize entries by type for easy retrieval during reviews
- **Search & Filter**: Find specific accomplishments using keywords or dates
- **AI Features (Pro)**: Automated summaries and impact analysis

### Tech Stack
- **Frontend**: React + Vite + TypeScript (Cloudflare Pages)
- **Backend**: Express.js + TypeScript (Railway)
- **Database**: Neon (PostgreSQL) + Prisma ORM
- **Auth**: Better-Auth
- **Payments**: Polar.sh (Merchant of Record)
- **Storage**: Cloudflare R2 (S3-compatible)

### Project Status
- [x] Requirements gathering
- [x] Tech stack decision
- [x] MVP implementation
- [ ] Testing
- [ ] Deployment

---

## Product Development Requirements (PDR)

### Vision
Web app helping professionals collect and organize work achievements for promotion reviews.

### Problem Statement
Professionals forget their accomplishments when promotion time comes. They struggle to recall specific contributions, metrics, and impact from months or years of work.

### Solution
A simple app to log achievements as they happen - code commits, design work, emails, meeting notes, presentations - creating a searchable "brag document" for performance reviews.

### Target Users
- Software engineers
- Designers
- Product managers
- Any professional tracking career growth

### Business Model
**Freemium SaaS**
- Free tier: Limited entries (e.g., 50/month)
- Pro tier: Unlimited entries, AI summaries, exports, integrations

### Core Features (MVP)

#### P0 - Must Have
1. User authentication (signup/login)
2. Create/edit/delete achievements
3. Categorize achievements (code, design, leadership, etc.)
4. Search and filter achievements
5. Basic dashboard view

#### P1 - Should Have
1. File uploads (screenshots, docs)
2. Tags and custom categories
3. Date range filtering
4. Export to PDF/Markdown

#### P2 - Nice to Have (Post-MVP)
1. AI-powered summaries
2. GitHub integration
3. Slack integration
4. Team/manager sharing
5. Mobile app (React Native)

### Data Model (Conceptual)

```
User
├── id, email, name, plan, createdAt

Achievement
├── id, userId, title, description
├── category, tags[], date
├── attachments[], createdAt, updatedAt

Category
├── id, userId, name, color, icon

Subscription
├── id, userId, plan, status, polarCustomerId
```

### Success Metrics
- User signups
- Weekly active users
- Achievements logged per user
- Free-to-paid conversion rate
- Monthly recurring revenue (MRR)

### Constraints
- MVP in 2-4 weeks
- Single developer
- Budget: minimal infrastructure cost
- Must be maintainable by someone learning Express.js

### Decisions Made
| Decision | Choice | Date |
|----------|--------|------|
| Frontend | React + Vite | 2024-12-27 |
| Backend | Express.js + TypeScript | 2024-12-27 |
| Database | Neon (PostgreSQL) | 2024-12-27 |
| ORM | Prisma | 2024-12-27 |
| Auth | Better-Auth | 2024-12-27 |
| Payments | Polar.sh | 2024-12-27 |
| Storage | Cloudflare R2 | 2024-12-27 |
| Hosting | Cloudflare Pages + Railway | 2024-12-27 |

---

## System Architecture

### Overview
BragDoc is a full-stack SaaS web application designed for high performance, developer productivity, and low operational cost.

### Tech Stack Summary

| Layer | Technology | Rationale |
|-------|------------|-----------|
| **Frontend** | React + Vite | Fast development, excellent ecosystem, user preference |
| **Backend** | Express.js + TypeScript | Standard Node.js framework, type safety, easy to learn |
| **Database** | Neon (PostgreSQL) | Serverless PostgreSQL, scales to zero, generous free tier |
| **ORM** | Prisma | Type-safe database access, excellent developer experience |
| **Auth** | Better-Auth | Open-source, flexible, handles complex auth flows easily |
| **Payments** | Polar.sh | Merchant of Record (MoR), handles global tax/VAT compliance |
| **File Storage** | Cloudflare R2 | S3-compatible, zero egress fees, cost-effective |
| **Hosting** | Cloudflare Pages (FE) + Railway (BE) | Optimized for frontend performance and backend simplicity |

### High-Level Architecture

```mermaid
graph TD
    User([User])

    subgraph "Frontend (Cloudflare Pages)"
        ReactApp[React + Vite App]
    end

    subgraph "Backend (Railway)"
        ExpressAPI[Express.js API]
        PrismaORM[Prisma ORM]
        AuthSrv[Better-Auth Server]
    end

    subgraph "Storage & Infrastructure"
        NeonDB[(Neon PostgreSQL)]
        R2Storage[Cloudflare R2]
        Polar[Polar.sh Payments]
    end

    User <--> |HTTPS| ReactApp
    ReactApp <--> |REST API| ExpressAPI
    ExpressAPI <--> PrismaORM
    PrismaORM <--> NeonDB
    ExpressAPI <--> AuthSrv
    ExpressAPI <--> R2Storage
    ExpressAPI <--> Polar
```

### Data Flow

1. **Authentication**: Users authenticate via Better-Auth. Sessions are managed on the backend and validated on each API request.
2. **Achievement Management**:
   - Frontend sends CRUD requests to the Express API
   - API validates requests using Zod and business logic in Services
   - Prisma ORM interacts with Neon PostgreSQL to persist data
3. **File Uploads**:
   - Frontend requests a pre-signed URL from the Backend
   - Frontend uploads the file directly to Cloudflare R2 using the pre-signed URL
   - Metadata about the file is stored in the database
4. **Payments**:
   - Users are redirected to Polar.sh for checkout
   - Polar.sh sends webhooks to the Backend to update subscription status

### Database Provider Support

The application supports multiple PostgreSQL providers via environment configuration:

| Provider | Environment | Use Case |
|----------|-------------|----------|
| Local (Docker) | Development | Fast local iteration |
| Supabase | Production | Managed PostgreSQL with extras |
| Neon | Production | Serverless PostgreSQL |

Provider is auto-detected from `DATABASE_URL` at startup. No code changes needed to switch providers.

### Security
- **Authentication**: Managed by Better-Auth with secure session handling
- **Authorization**: Role-based access control (Free vs. Pro tier) implemented in backend middleware
- **Data Protection**: SSL/TLS for all communications. Environment variables for sensitive secrets
- **API Validation**: Input validation for all endpoints using Zod

### Infrastructure Costs (Estimated)

#### Current Stack Pricing (2025)

| Service | Free Tier | Production Cost |
|---------|-----------|-----------------|
| Neon | 0.5GB, 100 compute hrs | Launch: $19/mo, Scale: $69/mo |
| Railway | $5 credit (Hobby) | Hobby: $5/mo, Pro: $20/mo |
| Cloudflare Pages | Unlimited | $0 |
| Cloudflare R2 | 10GB storage, 0 egress | $0.015/GB beyond free |
| Better-Auth | Unlimited | $0 |
| Polar.sh | 4% + ~2.9% payment fees | Revenue-based only |

#### Cost Scenarios

| Scale | Users | Est. Monthly Cost |
|-------|-------|-------------------|
| **MVP (Free Tiers)** | <100 | **~$5** |
| **Early Growth** | 100-1K | **$25-50** |
| **Production** | 1K-10K | **$70-150** |

#### Recommended MVP Setup (~$5/mo)
- Neon Free Tier (0.5GB sufficient for <1000 users)
- Railway Hobby ($5 minimum)
- Cloudflare R2 Free (10GB)
- Better-Auth (free, self-hosted)

---

## Tech Stack

### Approved Stack (2024-12-27)

| Layer | Technology | Rationale |
|-------|------------|-----------|
| **Frontend** | React + Vite | User preference, fast dev experience |
| **Backend** | Express.js + TypeScript | Beginner-friendly, huge ecosystem |
| **Database** | Neon (PostgreSQL) | Serverless, scales to zero, free tier |
| **ORM** | Prisma | Type-safe, excellent DX |
| **Auth** | Better-Auth | Open-source, unlimited users, free |
| **Payments** | Polar.sh | 4% MoR fee, handles VAT/tax |
| **File Storage** | Cloudflare R2 | $0 egress fees, S3-compatible |
| **Frontend Host** | Cloudflare Pages | Unlimited bandwidth free tier |
| **Backend Host** | Railway | Simple deploy, ~$5/mo |

### Architecture Diagram

```
┌─────────────────┐     ┌─────────────────┐     ┌──────────────┐
│   React + Vite  │────▶│  Express.js API │────▶│  Neon (PG)   │
│ (Cloudflare)    │     │   (Railway)     │     │  (Serverless)│
└─────────────────┘     └────────┬────────┘     └──────────────┘
                                 │
                        ┌────────▼────────┐
                        │  Cloudflare R2  │
                        │  (File Storage) │
                        └─────────────────┘
```

### Future Mobile Support
- React Native recommended for code reuse
- Backend API already mobile-ready
- PWA possible as interim solution

---

## Code Standards

### General Principles
- **Type Safety**: Use TypeScript for both frontend and backend. Avoid `any`
- **Consistency**: Follow established patterns for naming and structure
- **Simplicity**: Keep functions small and focused (Single Responsibility Principle)
- **Documentation**: Document complex logic and API endpoints

### Naming Conventions
- **Files/Folders**: `kebab-case` (e.g., `user-profile.tsx`, `auth-service.ts`)
- **Classes/Interfaces/Types**: `PascalCase`
- **Variables/Functions**: `camelCase`
- **Constants**: `UPPER_SNAKE_CASE`
- **Database Tables/Fields**: `snake_case` (Prisma standard)

### Frontend Standards (React + Vite)
- **Components**: Functional components with hooks
- **Styling**: Tailwind CSS for layout and components
- **State Management**:
  - Server state: TanStack Query
  - UI state: React Context or simple `useState`
- **Project Structure**:
  ```text
  src/
  ├── components/    # Reusable UI components
  ├── features/      # Feature-based organization (e.g., auth, achievements)
  ├── hooks/         # Custom React hooks
  ├── lib/           # Third-party library configuration
  ├── services/      # API calls and external services
  ├── types/         # TypeScript definitions
  └── utils/         # Helper functions
  ```

### Backend Standards (Express.js)
- **Controller/Service Pattern**: Controllers handle requests; Services handle business logic
- **Error Handling**: Centralized error handling middleware
- **Validation**: Use `zod` for request body and parameter validation
- **Project Structure**:
  ```text
  src/
  ├── controllers/   # Route handlers
  ├── services/      # Business logic
  ├── middleware/    # Express middleware
  ├── routes/        # API route definitions
  ├── types/         # TypeScript definitions
  └── utils/         # Helper functions
  ```

### Database Standards (Prisma)
- Use migrations for all schema changes
- Descriptive naming for models and relations
- Use `@map` to keep database fields `snake_case` while using `camelCase` in TS

### Git Workflow
- Feature branches from `main`
- Concise, imperative commit messages (e.g., `feat: add achievement creation`)
- PR reviews before merging to `main`

---

## Design Guidelines

**Aesthetic**: Refined Minimal
**Inspiration**: Notion meets Linear - clean, typography-driven, professionally calm
**Core Principle**: Content-first with subtle delight; every pixel earns its place

### 1. Color System

#### Base Palette

```css
:root {
  /* Neutral Scale - Warm undertones for approachability */
  --color-white: #FFFFFF;
  --color-gray-50: #FAFAFA;
  --color-gray-100: #F5F5F4;
  --color-gray-200: #E7E5E4;
  --color-gray-300: #D6D3D1;
  --color-gray-400: #A8A29E;
  --color-gray-500: #78716C;
  --color-gray-600: #57534E;
  --color-gray-700: #44403C;
  --color-gray-800: #292524;
  --color-gray-900: #1C1917;
  --color-black: #0C0A09;

  /* Primary Accent - Deep Indigo (confidence, achievement) */
  --color-primary-500: #6366F1;  /* Main accent */
  --color-primary-600: #4F46E5;
  --color-primary-700: #4338CA;

  /* Success - Muted emerald */
  --color-success-500: #10B981;

  /* Warning - Warm amber */
  --color-warning-500: #F59E0B;

  /* Error - Soft rose */
  --color-error-500: #F43F5E;
}
```

#### Usage Rules

| Element | Color |
|---------|-------|
| Page background | `--color-white` |
| Card/panel backgrounds | `--color-gray-50` |
| Primary buttons | `--color-primary-600` |
| Primary button hover | `--color-primary-700` |
| Body text | `--color-text-primary` |
| Secondary/meta text | `--color-text-secondary` |
| Borders | `--color-border` |
| Links | `--color-primary-600` |

### 2. Typography

**Font Stack**: Geist (Vercel)

```css
:root {
  --font-display: 'Geist', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-body: 'Geist', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-mono: 'Geist Mono', 'SF Mono', 'Fira Code', monospace;
}
```

#### Type Scale

| Element | Size | Weight | Line Height |
|---------|------|--------|-------------|
| Page title (h1) | 36px | Bold | Tight |
| Section title (h2) | 24px | Semibold | Tight |
| Card title (h3) | 18px | Semibold | Snug |
| Body text | 16px | Normal | Relaxed |
| Small text | 14px | Normal | Normal |
| Caption/meta | 12px | Medium | Normal |

### 3. Component Specifications

#### Buttons
- Primary: `--color-primary-600` background, white text
- Secondary: White background, border, gray text
- Ghost: Transparent background, gray text
- Border radius: `8px`
- Padding: `8px 16px`

#### Inputs
- Border: `1px solid --color-border`
- Border radius: `8px`
- Focus: Primary color ring
- Padding: `10px 12px`

#### Cards
- Background: White
- Border: `1px solid --color-border-subtle`
- Border radius: `12px`
- Shadow: Subtle (`0 1px 2px rgba(0,0,0,0.03)`)
- Hover: Enhanced shadow

#### Category Tags
- Pill-shaped (`border-radius: 9999px`)
- Subtle backgrounds with contrasting text
- Uppercase, small font size (12px)
- Letter spacing: Wide

### 4. Spacing Scale
- Base unit: `4px`
- Component internal padding: `16px`
- Card padding: `20-24px`
- Section gaps: `32-40px`
- Page sections: `48-64px`

### 5. Shadows & Depth
- Cards at rest: `0 1px 2px rgba(0,0,0,0.03)`
- Cards on hover: `0 1px 3px rgba(0,0,0,0.05)`
- Dropdowns/popovers: Medium shadow
- Modals: Extra large shadow
- Focus states: Primary color ring with 30% opacity

### 6. Border Radius
- Buttons/Inputs: `8px`
- Cards: `12px`
- Modals: `16px`
- Avatars: `9999px` (circle)
- Tags/badges: `9999px` (pill)

### 7. Animation & Motion
- Fast feedback: <150ms
- Subtle hover effects
- Card lift on hover: `translateY(-2px)`
- Button press: `scale(0.98)`
- Easing: `cubic-bezier(0.4, 0, 0.2, 1)`
- Respect `prefers-reduced-motion`

### 8. Iconography
**Recommended**: Lucide Icons (MIT license)
- Inline with text: 16px
- Buttons: 18px
- Navigation: 20px
- Empty states: 48-64px

### 9. Accessibility
- Focus indicators on all interactive elements
- Color contrast: AAA for body text, AA minimum
- Touch targets: Minimum 44x44px on mobile
- Semantic HTML

### Quick Reference: Do's and Don'ts

#### Do
- Use generous whitespace
- Keep shadows subtle
- Animate sparingly but purposefully
- Maintain consistent 4px/8px grid
- Use the primary accent sparingly for emphasis

#### Don't
- Add decorative elements without purpose
- Use more than one accent color prominently
- Animate everything
- Use harsh borders
- Overcrowd the interface

---

## Codebase Summary

*Last updated: 2025-12-28*

### Project Overview
BragDoc MVP is fully implemented. The application features a functional achievement tracking system with user authentication, usage limits, and a responsive dashboard.

### Directory Structure
```text
.
├── client/             # React + Vite frontend
│   ├── src/
│   └── playwright/     # E2E testing
├── server/             # Express.js + TypeScript backend
│   ├── src/
│   └── vitest.config.ts # Backend testing
├── docs/               # Project documentation
├── plans/              # Implementation plans and reports
├── railway.toml        # Backend deployment configuration
└── package.json        # Workspace configuration
```

### Implementation Status
- **Core Requirements**: Fully implemented as per PDR
- **Tech Stack**: React, Express, Prisma, Better-Auth, Tailwind CSS
- **Testing**: Playwright (E2E) and Vitest (Integration) configured and passing
- **Deployment**: Railway (Backend) and Cloudflare Pages (Frontend) configured

### Key Components
- **Frontend**: React 18, TanStack Query, Better-Auth client, Tailwind CSS
- **Backend**: Express.js, Prisma ORM, Better-Auth server-side integration
- **Testing Infrastructure**:
  - **Playwright**: Located in `client/` for end-to-end user flow testing
  - **Vitest**: Located in `server/` for unit and integration testing of API endpoints
- **Deployment**:
  - **Railway**: `railway.toml` handles the backend service deployment and database migrations
  - **Cloudflare Pages**: Frontend deployment with automatic preview builds

---

## Database Setup Guide

BragDoc supports three database providers. Choose based on your needs:

| Provider | Best For | Cost |
|----------|----------|------|
| Local (Docker) | Development, testing | Free |
| Supabase | Production, teams | Free tier available |
| Neon | Production, serverless | Free tier available |

### Quick Start

#### Option 1: Local PostgreSQL (Recommended for Development)

```bash
# 1. Start local database
pnpm db:local:start

# 2. Copy environment template
cp .env.local.example .env

# 3. Run migrations
cd server && pnpm db:migrate

# 4. Start development
pnpm dev
```

#### Option 2: Supabase

1. Create project at [supabase.com](https://supabase.com)
2. Go to Project Settings > Database > Connection string
3. Copy the connection strings:

```bash
# Copy Supabase template
cp .env.supabase.example .env

# Edit .env with your credentials:
# - DATABASE_URL: Use "Transaction" tab, add ?pgbouncer=true
# - DIRECT_URL: Use "Direct" tab
```

4. Run migrations:
```bash
cd server && pnpm db:migrate
```

#### Option 3: Neon PostgreSQL

1. Create database at [neon.tech](https://neon.tech)
2. Copy connection string from dashboard
3. Update `.env`:

```env
DATABASE_URL="postgresql://user:pass@ep-xxx.region.aws.neon.tech/neondb?sslmode=require"
DIRECT_URL="postgresql://user:pass@ep-xxx.region.aws.neon.tech/neondb?sslmode=require"
```

4. Run migrations:
```bash
cd server && pnpm db:migrate
```

### Connection String Formats

#### Local PostgreSQL
```
postgresql://postgres:postgres@localhost:5432/bragdoc?schema=public
```

#### Supabase
```
# Application queries (pooled)
postgres://postgres.[PROJECT]:[PASS]@[REGION].pooler.supabase.com:6543/postgres?pgbouncer=true

# Migrations (direct)
postgresql://postgres:[PASS]@db.[PROJECT].supabase.co:5432/postgres
```

#### Neon
```
postgresql://[USER]:[PASS]@ep-[ID].[REGION].aws.neon.tech/[DB]?sslmode=require
```

### Troubleshooting

- **"Connection refused" to local database**: Ensure Docker is running (`docker ps`), start database (`pnpm db:local:start`)
- **"Prepared statement already exists" with Supabase**: Ensure `?pgbouncer=true` is in DATABASE_URL
- **"IPv6 connection failed" with Supabase**: Use the pooler connection string (IPv4 compatible)
- **Migrations fail**: Ensure DIRECT_URL is set (bypasses connection pooler)

---

## Authentication Configuration

### Current Status: Email Verification DISABLED

**Changed**: 2025-12-29
**Location**: `server/src/lib/auth.ts:18`

#### What Was Changed

```typescript
requireEmailVerification: false  // Changed from: true
```

#### Why This Was Disabled

- **Development convenience**: Allows signup/login without email verification
- **No Mailgun required**: Verification emails need Mailgun API configured
- **Faster testing**: Skip verification step during local development

#### How to Re-Enable (Production Setup)

1. **Configure Mailgun** in `.env`:
   ```bash
   MAILGUN_API_KEY="your-api-key"
   MAILGUN_DOMAIN="your-domain.mailgun.org"
   ```

2. **Enable verification** in `server/src/lib/auth.ts:18`:
   ```typescript
   requireEmailVerification: true,
   ```

3. **Restart server** to apply changes

### Other Authentication Controls

#### Login Maintenance Mode
Toggle via environment variable:
```bash
LOGIN_DISABLED="true"   # Blocks login/signup (503 response)
LOGIN_DISABLED="false"  # Normal operation (default)
```

**Location**: `server/src/index.ts:27-41`
**Blocks**: `/api/auth/sign-in/*`, `/api/auth/sign-up/*`
**Allows**: Session checks, logout

#### Google OAuth (Optional)
Enable by adding to `.env`:
```bash
GOOGLE_CLIENT_ID="your-client-id"
GOOGLE_CLIENT_SECRET="your-secret"
```

Auto-enables when both values present (`server/src/lib/auth.ts:52-56`)

### Current Auth Flow

#### Development (Current)
1. User signs up with email/password
2. ✅ Account created immediately (no verification)
3. ✅ User can login right away

#### Production (When Re-enabled)
1. User signs up with email/password
2. 📧 Verification email sent via Mailgun
3. ⏳ User clicks verification link
4. ✅ User can login

### Security Notes

- **Dev only**: Disabled verification acceptable for local development
- **Production**: MUST enable verification + configure Mailgun
- **Passwords**: Still hashed via better-auth (secure regardless of verification setting)

---

## Login Disable Feature

### Overview
Temporary login disable feature for maintenance mode using environment-based kill switch (KISS principle).

### How It Works

#### Backend
- `LOGIN_DISABLED` env variable controls auth availability
- Middleware in `server/src/index.ts` intercepts login/signup requests
- Returns 503 Service Unavailable when disabled
- Existing sessions continue to work (logout allowed, login blocked)

#### Frontend
- Login and Signup forms handle 503 responses gracefully
- Shows user-friendly "temporarily disabled for maintenance" message
- Works for both email/password and Google OAuth flows

### Usage

#### Local Development

1. **Enable login disable:**
   ```bash
   # In .env file
   LOGIN_DISABLED="true"
   ```

2. **Restart server:**
   ```bash
   pnpm dev
   ```

3. **Re-enable login:**
   ```bash
   # In .env file
   LOGIN_DISABLED="false"
   ```

#### Production (Railway)

1. **Disable login:**
   - Go to Railway dashboard → Your service → Variables
   - Add/update: `LOGIN_DISABLED=true`
   - Server auto-restarts, login disabled immediately

2. **Re-enable login:**
   - Set `LOGIN_DISABLED=false` or remove the variable
   - Server auto-restarts, login re-enabled

### What Gets Blocked

**Blocked endpoints:**
- `/api/auth/sign-in/email` (email login)
- `/api/auth/sign-up/email` (email signup)
- `/api/auth/sign-in/social` (Google OAuth)

**Still allowed:**
- Session validation (existing logged-in users can continue)
- Logout functionality
- Protected API endpoints (for existing sessions)

### Implementation Files

- `server/src/lib/env.ts:22` - Env variable schema
- `server/src/lib/auth.ts:8` - Helper function
- `server/src/index.ts:27-41` - Middleware check
- `client/src/components/auth/LoginForm.tsx:25,36` - Frontend handling
- `client/src/components/auth/SignupForm.tsx:27,38` - Frontend handling

### Trade-offs

**Pros:**
- Zero code complexity
- Instant effect via env restart
- No database changes
- Works for all auth methods

**Cons:**
- Requires server restart to toggle
- No per-user exemptions (admin bypass not implemented)
- Existing sessions continue (not a full lockdown)

---

## Deployment Guide

### Overview
BragDoc uses a split hosting strategy for optimal performance and cost.

### Hosting Providers
- **Frontend**: [Cloudflare Pages](https://pages.cloudflare.com/)
- **Backend**: [Railway](https://railway.app/)
- **Database**: [Neon PostgreSQL](https://neon.tech/)
- **File Storage**: [Cloudflare R2](https://www.cloudflare.com/developer-platform/r2/)

### Environment Variables

#### Backend (Railway)
| Variable | Description |
|----------|-------------|
| `DATABASE_URL` | Prisma connection string for Neon |
| `BETTER_AUTH_SECRET` | Secret key for auth sessions |
| `BETTER_AUTH_URL` | The URL of the backend API |
| `FRONTEND_URL` | The URL of the frontend application |
| `R2_ACCESS_KEY_ID` | Cloudflare R2 access key |
| `R2_SECRET_ACCESS_KEY` | Cloudflare R2 secret key |
| `R2_BUCKET_NAME` | Cloudflare R2 bucket name |
| `POLAR_API_KEY` | API key for Polar.sh integration |
| `POLAR_WEBHOOK_SECRET` | Secret for verifying Polar.sh webhooks |

#### Frontend (Cloudflare Pages)
| Variable | Description |
|----------|-------------|
| `VITE_API_URL` | The URL of the backend API on Railway |

### Deployment Process

#### 1. Database
1. Create a new project in Neon
2. Copy the connection string
3. Run `npx prisma migrate deploy` during the CI/CD process or manually before deployment

#### 2. Backend (Railway)
1. Connect your GitHub repository to Railway
2. Add the required environment variables
3. Railway will automatically deploy on every push to the specified branch

#### 3. Frontend (Cloudflare Pages)
1. Connect your GitHub repository to Cloudflare Pages
2. Select `Vite` as the framework preset
3. Set the build command to `npm run build` (or equivalent)
4. Set the output directory to `dist`
5. Add the `VITE_API_URL` environment variable
6. Cloudflare will automatically deploy on every push

### CI/CD Workflow
- **Linting & Type Checking**: Run on every Pull Request
- **Testing**: Run automated tests before deployment
- **Deployment**: Triggered automatically upon merging into the `main` branch

---

## Project Roadmap

### Phase 1: MVP (P0 Features) - ✅ Complete
Goal: A functional "Brag Document" application with user auth and basic CRUD.

- [x] **Infrastructure Setup**
  - Setup GitHub Repository & Monorepo structure
  - Configure Prisma with Neon PostgreSQL
  - Setup Better-Auth for authentication
  - Initialize React + Vite frontend and Express.js backend
- [x] **Authentication**
  - Implementation of Signup, Login, and Logout
  - User session management
- [x] **Achievement Management**
  - CRUD operations for Achievements
  - Category management (Basic)
- [x] **Dashboard & UI**
  - Dashboard view listing achievements
  - Search and filter functionality
- [x] **Deployment**
  - Deploy frontend to Cloudflare Pages
  - Deploy backend to Railway

**Note**: Deployment readiness confirmed with `railway.toml` and Cloudflare Pages configuration. MVP features are fully implemented and verified.

### Phase 2: Enhanced Features (P1 Features)
Goal: Improve usability and organization.

- [ ] **File Management**
  - Integrate Cloudflare R2 for file uploads (screenshots, docs)
- [ ] **Advanced Organization**
  - Tags and custom categories
  - Date range filtering
- [ ] **Export Capabilities**
  - Export achievements to PDF/Markdown

### Phase 3: Monetization & Polish (P1/P2)
Goal: Launch Pro tier and refine user experience.

- [ ] **Monetization**
  - Integrate Polar.sh for subscriptions
  - Implement Pro tier features and limits
- [ ] **Polish**
  - Refined UI/UX and mobile responsiveness
  - Comprehensive testing (Unit & Integration)

### Phase 4: AI & Integrations (P2 Features)
Goal: Long-term growth and automated workflows.

- [ ] **AI Features**
  - AI-powered summaries of accomplishments
  - Impact analysis suggestions
- [ ] **Integrations**
  - GitHub integration (pull achievements from commits/PRs)
  - Slack integration (log achievements directly from Slack)
- [ ] **Collaboration**
  - Team/manager sharing features
- [ ] **Mobile App**
  - Native mobile experience (React Native)

---

## Development Journals

### Journal Entry 1: Project Initialization (2024-12-27)

**The Birth of BragDoc**

The project was initialized with the vision of solving the "amnesia" problem professionals face during promotion cycles. Starting a new SaaS project is always a mix of excitement and paralyzing choice.

**Technical Decisions:**
- Monorepo structure using `pnpm` workspaces
- React + Vite for frontend
- Express.js + TypeScript for backend
- Prisma ORM with Neon PostgreSQL

**Key Insight**: Constraints are friends. Setting a "minimal infrastructure cost" constraint early forced evaluation of "scale-to-zero" providers like Neon and Railway.

---

### Journal Entry 2: MVP Implementation Complete (2025-12-28 19:30)

**The MVP Grind: From Planning to (Technical) Completion**

Over 48 hours, moved from raw plans to a functionally complete MVP. Implemented Better-Auth for security and built Achievement CRUD logic with usage limits.

**Technical Challenges:**
- Auth: Better-Auth with Google OAuth redirect URL configurations
- Logic: "Soft delete" pattern initially missed deleted records in `findAll` queries
- Limits: Hardcoded 100 entries/year limit for free tier

**Brutal Truth**: At "MVP Complete" without a single commit - high-risk technical debt.

**Lessons Learned:**
- Check-in early, check-in often
- Service layers are essential for fixing bugs in one place

---

### Journal Entry 3: Architectural Decisions (2025-12-28 20:00)

**Why We Chose This Stack**

Finalized architectural blueprint, moving from "hobby" setups to "MoR-ready" infrastructure.

**Key Decisions:**
- **Auth**: Better-Auth (Self-hosted) - Own the database tables, no external dependencies
- **Payments**: Polar.sh - 4% fee is a steal vs global tax/VAT legal overhead
- **Database**: Neon PostgreSQL - "Branching" feature is game-changer for migrations

**Decision Framework**: Developer Speed > Operational Cost > Portability

**Lessons Learned:**
- Merchant of Record is non-negotiable for global SaaS
- Type-safety (Zod + Prisma + TypeScript) is a productivity multiplier

---

### Journal Entry 4: Supabase Pivot (2025-12-28 21:00)

**Flexibility or Fragmentation?**

Despite initial Neon commitment, planned for Supabase Database Support with Local Fallback. Strategic shift to allow seamless switching between local Postgres, Neon, and Supabase.

**Technical Approach:**
- Environment-based provider detection via URL parsing
- Docker Compose for local PostgreSQL
- Zod schemas for fail-fast validation

**Brutal Truth**: Feels like architectural indecision, but prevents "forced migration" later.

**Lessons Learned:**
- Provider Agnostic is a Spectrum
- Environment Validation is Core Logic

---

### Journal Entry 5: Implementation Plan Complete (2025-12-28 21:30)

**The MVP Blueprint: 65 Hours of Theoretical Grind**

Comprehensive implementation plan complete: Six phases, 65 hours estimated effort, tech stack locked.

**Stack Finalized:**
- React+Vite, Express.js, Prisma, Neon PostgreSQL, Better-Auth
- Quota: 100 achievements/year (Freemium)
- Strategy: Vertical Slice + Complete Schema Upfront
- Email: Mailgun (transactional)
- Auth: Google OAuth only (Apple deferred)

**Brutal Truth**: Planning is the easy part. 65-hour roadmap is reaction to past technical debt—desperate attempt to avoid "refactor-on-day-three" syndrome.

**Lessons Learned:**
- Deferred features are "Technical Debt" in disguise
- Constraints are features (100/year limit prevents database bloat)
- The Plan ≠ The Product

---

## Quick Reference

### Development Commands
```bash
# Start local database
pnpm db:local:start

# Run migrations
cd server && pnpm db:migrate

# Start development
pnpm dev

# Run tests
pnpm test

# Build for production
pnpm build
```

### Important File Locations
- **Auth Configuration**: `server/src/lib/auth.ts`
- **Environment Schema**: `server/src/lib/env.ts`
- **Prisma Schema**: `server/prisma/schema.prisma`
- **Railway Config**: `railway.toml`
- **Design System**: See Design Guidelines section above

### Key URLs
- Frontend (local): `http://localhost:5173`
- Backend (local): `http://localhost:3000`
- Neon Dashboard: [neon.tech](https://neon.tech)
- Railway Dashboard: [railway.app](https://railway.app)
- Cloudflare Pages: [pages.cloudflare.com](https://pages.cloudflare.com)

---

**End of Documentation**

*For questions or updates, refer to the main repository at `/Users/eddy/Documents/personal-sd-project/brag-app/brag-web`*
