# ReverseMarket (Reqly) — Reverse Marketplace Platform

> **Demand-Driven Commerce Platform**: Instead of buyers endlessly searching catalogs, buyers post their requirements, and verified providers compete with structured, transparently scored proposals.

---

## 1. Product Overview & Problem Statement

### The Problem
Traditional e-commerce and B2B procurement models are **supply-centric**. Buyers must:
- Manually search hundreds of fragmented product listings.
- Sift through opaque pricing models, inaccurate stock indicators, and untrusted reviews.
- Negotiate delivery timelines and custom specifications asynchronously via disjointed channels.

### The Solution
**ReverseMarket** flips the commerce paradigm:
1. **Demand-First RFPs**: Buyers post specific requirements once (using manual structured forms or natural language smart text parsing).
2. **Transparent Matching Engine**: A deterministic 5-factor scoring engine automatically ranks submitted provider proposals with explainable reasons.
3. **Structured Comparison & Selection**: Buyers compare bids side-by-side on price, delivery fit, and provider trust before awarding the engagement.
4. **Milestone Governance & Trust**: Post-selection fulfillment proceeds through structured milestones, integrated messaging, and verified post-delivery reviews.

---

## 2. User Roles & Capabilities

| Role | Core Capabilities |
| :--- | :--- |
| **Buyer** | • Post requirements with budget, quantity, deadline, and specs.<br>• Use Smart NLP Requirement Parser to auto-populate fields.<br>• Access Match Center to inspect 5-factor score breakdowns.<br>• Shortlist, compare up to 4 offers side-by-side, and initiate contextual chat.<br>• Select winning proposals and track 6-stage delivery milestones.<br>• Submit verified 5-star reviews with tags. |
| **Provider** | • Discover active buyer RFPs filtered by category, budget, and match score.<br>• View compatibility previews before submitting bids.<br>• Submit structured proposals with pricing, deliverables, and warranty terms.<br>• Manage offer lifecycle (submit, edit draft, withdraw).<br>• Track active contracts and advance provider milestones (kickoff, staging, dispatch).<br>• Showcase verified reputation and trust metrics. |
| **Admin** | • Executive platform health KPIs (Users, RFPs, Proposals, Contracts, GMV).<br>• User directory with account suspension and login locks.<br>• Moderation queue to pause, resume, or close non-compliant postings.<br>• Proposal moderation to hide or restore misleading offers.<br>• Trust & Safety triage to investigate and resolve violation reports.<br>• Taxonomy sector management and dynamic matching engine weight tuning.<br>• Immutable system audit log with JSON inspector. |

---

## 3. Route Map & Route Guards

All non-public routes are protected by role-aware guards (`RoleGuard.tsx`):

```
Public:
├── /                                Landing Page
├── /login                           Unified Login Page
└── /signup                          Registration Page

Buyer (/buyer/*):
├── /buyer/dashboard                 Buyer Overview & Quick Actions
├── /buyer/requirements              My Requirements List
├── /buyer/requirements/new          Post Requirement (with Smart NLP Parser)
├── /buyer/requirements/:id          Requirement Details & Submissions
├── /buyer/matches                   Match Center & Scoring Explanations
├── /buyer/compare                   Side-by-Side Offer Comparison
├── /buyer/selected                  Engagements & Milestone Tracker
├── /buyer/messages                  Contextual Direct Messaging
└── /buyer/profile                   Account Settings & Notification Preferences

Provider (/provider/*):
├── /provider/dashboard              Provider Dashboard & Analytics
├── /provider/requirements           Browse & Filter Open Buyer RFPs
├── /provider/requirements/:id       Requirement Details & Compatibility Preview
├── /provider/offers                 My Proposals Pipeline
├── /provider/offers/:id             Proposal In-Depth View
├── /provider/engagements            Active Contracts & Milestone Fulfillment
├── /provider/messages               Direct Message Threads
└── /provider/profile                Provider Trust Profile & Capabilities

Admin (/admin/*):
├── /admin/dashboard                 Platform Control Center & Health KPIs
├── /admin/users                     User Governance & Suspension
├── /admin/requirements              Requirements Moderation Queue
├── /admin/offers                    Proposals Inspection & Hiding
├── /admin/reports                   Trust & Safety Triage Queue
├── /admin/categories                Taxonomy & Sector Configuration
├── /admin/matching                  5-Factor Compatibility Algorithm Tuning
└── /admin/audit-log                 Immutable Audit Trail & Payload Explorer
```

---

## 4. Demo Accounts & One-Click Authentication

For instant prototype evaluation, one-click demo login buttons are provided on `/login`:

| Persona | Demo Email | Password | Role |
| :--- | :--- | :--- | :--- |
| **Buyer** | `buyer.demo@example.com` | `password123` | Buyer |
| **Provider** | `provider.demo@example.com` | `password123` | Provider |
| **Admin** | `admin.demo@example.com` | `password123` | Admin |

---

## 5. Architecture & Technical Design

### A. Data Storage & Prototype Persistence
- **Storage Layer**: Local storage with schema versioning (`reversemarket:v1`) and structured fallback migrations.
- **In-Memory Cache**: React reactive hook (`useMarketplace`) powered by an event-driven pub-sub store (`marketplaceStore.ts`).
- **Resilience**: Corrupted or missing storage states automatically recover to a pristine seeded dataset.

### B. Transparent 5-Factor Matching Formula
The matching engine (`src/utils/matchingEngine.ts`) calculates a normalized score from **0 to 100**:

$$\text{Match Score} = (0.35 \times \text{Relevance}) + (0.25 \times \text{Budget Fit}) + (0.20 \times \text{Delivery Fit}) + (0.10 \times \text{Provider Trust}) + (0.10 \times \text{Offer Quality})$$

1. **Relevance (35%)**: Category match, keyword overlap, structured preference fulfillment, and purpose extraction.
2. **Budget Fit (25%)**: Full score when price $\le$ max budget, with smooth quadratic falloff within configurable budget tolerance percentage (default: 15%).
3. **Delivery Fit (20%)**: Full score when delivery date $\le$ deadline, with graceful penalty within tolerance window (default: 3 days).
4. **Provider Trust (10%)**: Star ratings (normalized to 100), completed contract track record, verification badge, and response speed.
5. **Offer Quality (10%)**: Scope detail length, explicit inclusions/exclusions, warranty provision, and revision transparency.

### C. Natural Language Smart Requirement Parser
The smart parser (`src/utils/smartParser.ts`) applies deterministic multi-pass tokenization:
- **Category Classifier**: Keyword clustering for Computers, Design, Software, IT, Audio/Video, and Furniture.
- **Budget Extractor**: Handles `50k`, `₹75,000`, `between 50k and 75k`, `under 80000`.
- **Deadline Extractor**: Relative time parsing (`in 10 days`, `in 2 weeks`, `next month`).
- **Hardware/Deliverables Tokenizer**: Identifies RAM, SSD, GPU, Apple Silicon, warranties, Figma source files, and dark mode support.
- **Confidence Scoring**: High, Medium, or Low confidence depending on attribute detection density.

---

## 6. Local Setup & Verification Commands

### Prerequisites
- Node.js 18+
- npm 9+

### Setup Commands
```bash
# 1. Install dependencies
npm install

# 2. Run test suite
npm test -- --run

# 3. Run linter
npm run lint

# 4. Run TypeScript check and production build
npm run build

# 5. Launch local development server
npm run dev
```

---

## 7. Known Prototype Limitations & Production Roadmap

| Area | Prototype Implementation | Production Migration Path |
| :--- | :--- | :--- |
| **Persistence** | LocalStorage + PubSub state in browser | PostgreSQL / Prisma with Redis caching & read replicas. |
| **Authentication** | Local token session with role switcher | OAuth 2.0 / OIDC / Supabase Auth with JWT and HTTP-only cookies. |
| **Realtime** | In-tab and cross-tab storage events | WebSockets / Socket.io / Server-Sent Events (SSE) for instant messaging and bid alerts. |
| **Payments & Escrow**| Milestone status simulation | Stripe Connect / Razorpay Route with escrow hold and automated release on milestone sign-off. |
| **Search & Parser** | Client-side Regex / Tokenizer | Vector Embeddings + LLM NLP pipeline (e.g. Gemini 1.5 Flash) with pgvector semantic search. |
| **File Storage** | Base64 and metadata staging | AWS S3 / Cloudflare R2 presigned uploads with virus scanning. |
