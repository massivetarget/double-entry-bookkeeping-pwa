# Double-Entry Bookkeeping PWA

**SOLID · Mobile-First · Offline-First**

Professional-grade double-entry bookkeeping Progressive Web App that runs completely offline.

## Architecture Pillars (Non-Negotiable)

1. **SOLID Principles** – Every module has a single responsibility. Domain depends only on abstractions. Concrete IndexedDB, network and UI adapters are injected at the composition root.
2. **Mobile-First** – All screens designed and tested for 320–430 px viewports first. Desktop is progressive enhancement. Touch targets ≥ 44×44 px. Critical actions in the thumb zone.
3. **Offline-First** – IndexedDB (via repository layer) is the source of truth. Service Worker caches the app shell. All core features (create journal, post, reverse, Trial Balance, etc.) succeed with zero network.

## Stack

- TypeScript + React 18 + Vite
- Dexie (IndexedDB wrapper) behind repository interfaces
- vite-plugin-pwa for Service Worker + Web App Manifest
- Clean Architecture / Hexagonal layout

## Domain Layer (pure)

- `Account`, `Journal`, `JournalLine`, `Company`, `AccountingPeriod`
- Value object: `Money` (bigint minor units)
- Domain services: `JournalPostingService`, `TrialBalanceCalculator`, `ChartOfAccountsService`
- Repository interfaces only – no concrete storage imports

## Running locally

```bash
cd double-entry-bookkeeping-pwa
npm install
npm run dev
```

Then open the URL shown (usually http://localhost:5173).  
Install via browser “Add to Home Screen” for the full PWA experience.

## Key acceptance criteria implemented

- Unbalanced journals are rejected at the domain level
- Posted journals are immutable; reverse path creates linked inverse entry
- Trial Balance generated 100 % from local data
- Offline banner + local-only persistence
- Mobile-first responsive shell with bottom navigation
- Backup download (JSON) works offline

## Project structure

```
src/
  domain/           # Entities, value objects, services, repository interfaces
  application/      # Composition root (DI wiring)
  infrastructure/   # IndexedDB repositories, future sync
  presentation/     # React UI (pages, components, hooks, styles)
```

This codebase is the executable realisation of the Web App PRD.
