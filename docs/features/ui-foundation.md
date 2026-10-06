# Feature: UI Foundation (App Shell)

## Purpose
Core shell/layout + shared components used across all modules. Built 
once in Phase 1-2, consumed by every feature module going forward.

## Status: Phase 0 Complete, Phase 1 Starting

## Branding
- Logo: placeholder for now (swap later)
- Org/product name: "RIL Security" (vCISO as product sub-label, 
  matching reference pattern "Nexus Security / vCISO")
- Accent color: blue (consistent across dark/light themes)

## Theme System
- Default: Dark theme on first load
- Toggle location: top bar (icon cluster)
- Persistence: localStorage
- Both themes share same blue accent, differ in background/surface/text colors

## Business Scope Selector (NEW — not in reference UI)
- Type: Dropdown
- Location: top bar, next to logo/sidebar
- Options: "Global (All Businesses)" + list of individual businesses
- Behavior: Global app state (Zustand) — filters ALL data across 
  modules: stat cards, tables, everything data-driven
- Distinct from per-table search boxes (those are local text search 
  within whatever scope is currently selected)

## Sidebar
- All modules visible from reference: Dashboard, Marketplace, People, 
  Assets management, Tools, Documents, Third Party Risk Management, 
  Cybersecurity posture (Gaps, Remediation roadmap), Compliance (NIS2)
- Only People + Assets management functional in pilot
- All others show "Coming soon" placeholder page
- Order/naming: same as reference for now, revisit post-pilot

## Tech Stack (Frontend)
- Vite + React + TypeScript
- Tailwind CSS
- shadcn/ui (component library)
- lucide-react (icons)
- react-router-dom (routing)
- Zustand (state: theme, business scope, sidebar collapsed state)
- Package manager: pnpm

## Folder Structure
See CLAUDE.md / project root docs for full structure. Key points:
- components/layout/ — TopBar, Sidebar, AppShell (shell-level, built once)
- components/shared/ — DataTable, SearchInput, StatCard, Tabs, 
  ThemeToggle, BusinessScopeSelector (reused across all modules)
- components/ui/ — shadcn/ui generated components
- features/<module>/ — isolated per module (assets, people, etc.)
- store/ — small focused Zustand stores (not one giant store)

## Build Order (Step-wise)
1. Phase 0: Scaffold (Vite + Tailwind + shadcn init) — manual, no logic
2. Phase 1: App Shell (TopBar, Sidebar, Theme system, Business scope 
   selector) — test navigation/toggle before Phase 2
3. Phase 2: Shared reusable components (DataTable, SearchInput, 
   StatCard, Tabs) — test in isolation before wiring to real module
4. Phase 3: Asset Management module — Data sub-tab only, mock data
5. Phase 4+: Repeat pattern for Endpoints, Software, Services (later)

## Open Questions
- [ ] None currently — revisit after Phase 1 testing

## Decisions Log
- Phase 0 completed: Vite+React+TS scaffolded, Tailwind v4 (CSS-first 
  config, no tailwind.config.js), shadcn/ui initialized with Radix UI 
  + Nova preset (Lucide icons, Geist font). Base color overridden from 
  default neutral to custom blue theme (dark: navy slate background 
  oklch(0.208 0.042 265.755), primary blue oklch(0.623 0.214 259.815); 
  light: white background, same blue primary). Path alias @/* → ./src/* 
  configured in tsconfig + vite.config.ts. cn utility via shadcn's 
  standalone `cn` package (not local clsx/tailwind-merge composition).