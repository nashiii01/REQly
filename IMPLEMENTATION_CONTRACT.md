# ReverseMarket (Reqly) — Implementation Contract & Baseline Audit

## 1. Current Technology Stack

* **Runtime & Framework**: React 19 + TypeScript (Strict mode) + Vite 8
* **Styling & Design System**: Tailwind CSS v4 (`@tailwindcss/vite`)
* **Icons**: `lucide-react`
* **Test Runner**: Vitest 5 (`vitest run`)
* **Linter**: Oxlint (`oxlint`)
* **State & Persistence**: Typed domain models with centralized reactive store and versioned LocalStorage (`reversemarket:v1`)

---

## 2. Current Folder Structure

```
Reqly/
├── .gitignore
├── .oxlintrc.json
├── IMPLEMENTATION_CONTRACT.md    # Architecture and implementation baseline contract
├── index.html                    # Single-page application entry point
├── package.json                  # Scripts: dev, build, lint, test, preview
├── public/                       # Static public assets
├── src/
│   ├── assets/                   # Logos and iconography
│   ├── components/               # UI and feature components (to be implemented)
│   ├── services/                 # Matching engine, parser, mock API services (to be implemented)
│   ├── store/                    # Centralized reactive store & localStorage sync (to be implemented)
│   ├── types/                    # Domain TypeScript interfaces (User, Requirement, Offer, etc.)
│   ├── utils/                    # Formatting, scoring, and date helpers
│   ├── smoke.test.ts             # Vitest test baseline verification
│   ├── App.tsx                   # Main application root and layout
│   ├── App.css                   # App stylesheet
│   ├── index.css                 # Tailwind CSS v4 root import & design baseline
│   └── main.tsx                  # React DOM mount point
├── tsconfig.app.json
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts                # Vite config with React and Tailwind CSS v4 plugins
```

---

## 3. Current Implemented Features

* [x] **Smallest Stable Foundation**: React 19 + TypeScript + Vite + Tailwind CSS v4 scaffolded and configured.
* [x] **Core Styling & Design System Foundations**: B2B marketplace palette initialized with navy, blue/violet, positive emerald, amber, and red accents.
* [x] **Responsive Shell & Role Switcher UI**: Clean navigation header with active role indicator (Buyer View / Provider View) and hero copy.
* [x] **Linting, Build, and Testing Pipelines**: All passing with zero errors and sub-second verification.

---

## 4. Gaps Relative to the ReverseMarket Problem Statement

1. **Domain Data Models & Seed Data (`src/types/`, `src/services/mockData.ts`)**:
   - `User`, `BuyerProfile`, `ProviderProfile`, `Requirement`, `Offer`, `ShortlistItem`, `MessageThread`, `Message`, `Notification`, `Engagement`, `Milestone`, `Review`, `Report`.
   - Rich realistic seed data (e.g. laptop requirement with 3 competing offers, graphic design requirement, enterprise SaaS requirement).

2. **Deterministic Matching Engine (`src/services/matching/`)**:
   - Formula: `0.35 * relevance + 0.25 * budgetFit + 0.20 * deliveryFit + 0.10 * providerTrust + 0.10 * offerQuality`.
   - Human-readable score breakdown (positive reasons, cautions, missing info).

3. **Smart Requirement Parser (`src/services/parser/`)**:
   - Natural language extractor for title, category, budget, currency, deadline, purpose, and preferences with user editable preview.

4. **Buyer Workflows (`src/components/buyer/`)**:
   - Post Requirement form with validation & Smart Parser toggle.
   - My Requirements dashboard with status badges, countdowns, and quick actions (view, edit, duplicate, pause, close).
   - Match Center with grouped offers, rank score cards, and score explainers.
   - Side-by-side comparison table (up to 4 offers) with responsive swipeable view on mobile.
   - Selection modal with confirmation summary updating requirement, offer, and engagement states.

5. **Provider Workflows (`src/components/provider/`)**:
   - Provider profile and capability setup.
   - Browse requirements with filters (category, budget, delivery, min score) and live compatibility preview.
   - Offer submission form with live score preview, inclusions, exclusions, and validity date.
   - Provider dashboard tracking offer pipeline (Draft -> Submitted -> Viewed -> Shortlisted -> Selected).

6. **Collaboration, Tracking & Safety (`src/components/features/`)**:
   - Contextual requirement-level messaging thread.
   - In-app notification center and action toasts.
   - Post-selection engagement milestone tracker (Accepted -> Work Started -> Progress -> Delivered -> Accepted -> Completed).
   - Trust badges, dispute reporting, and admin moderation queue.

---

## 5. Recommended Implementation Order

1. **Phase 1: Domain Models, Store & Seed Data**:
   - Define all TypeScript types (`types/index.ts`).
   - Implement persistent state store (`store/marketplaceStore.ts`) backed by `localStorage` (`reversemarket:v1`) with seed data and "Reset Demo Data" action.
   - Add demo account authentication switcher (`buyer.demo@example.com` and `provider.demo@example.com`).

2. **Phase 2: Deterministic Matching Engine & Smart Parser**:
   - Implement `calculateMatch()` and `explainScore()` with unit tests.
   - Implement natural language text parser for requirements with regex/heuristic extractors.

3. **Phase 3: Buyer Experience & Match Center**:
   - Requirement creation form + Smart Parser UI.
   - My Requirements list and status management.
   - Match Center with score breakdown cards.
   - Side-by-side comparison dashboard (up to 4 offers).
   - Selection confirmation modal and state transition.

4. **Phase 4: Provider Experience & Offer Lifecycle**:
   - Requirement discovery and filtering with compatibility preview.
   - Offer creation with live preview and draft/submit/withdraw capabilities.
   - Provider dashboard and offer pipeline.

5. **Phase 5: Messaging, Notifications & Engagement Tracking**:
   - Requirement-level messaging threads.
   - In-app notifications & toast system.
   - 6-step engagement milestone tracker with rating & review system.

6. **Phase 6: Moderation, Responsive Polish & Final Verification**:
   - Admin moderation queue and reporting workflow.
   - Mobile and accessibility audit (focus states, labels, zero dead buttons).
   - End-to-end test verification and demo script rehearsal.

---

## 6. Compatibility Constraints & Risks

* **Execution Policy on Windows PowerShell**:
  - `npm` directly in PowerShell can trigger `PSSecurityException` for `.ps1` scripts; use `npm.cmd` or `npx.cmd` in Windows environments.
* **Local Storage Limits & Schema Evolution**:
  - Version keys as `reversemarket:v1` and handle JSON parse errors gracefully with fallback to seeded data.
* **Deterministic Matching vs. AI Hallucination**:
  - The matching engine and parser must remain 100% deterministic, testable, and transparent without unexplainable black-box logic.
* **Zero Dead Buttons Rule**:
  - All interactive buttons (Pause, Close, Withdraw, Select, Shortlist, Message, Reset) must perform observable state changes.

---

## 7. Exact Verification Commands

* **Run Dev Server**:
  ```powershell
  npm.cmd run dev
  ```
* **Run Unit Tests**:
  ```powershell
  npm.cmd test
  ```
* **Run Linter**:
  ```powershell
  npm.cmd run lint
  ```
* **Build for Production**:
  ```powershell
  npm.cmd run build
  ```
