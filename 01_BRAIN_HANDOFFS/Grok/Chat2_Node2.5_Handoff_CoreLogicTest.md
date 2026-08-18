# Chat2_Node2.5_Handoff_CoreLogicTest.md

**Brain:** Grok  
**Chat:** #2  
**Node:** 2.5 (Core logic test)  
**Date:** 2026-08-18

---

## Project identity
- **Project:** Freight (temp name, final TBD)
- **Hackathon:** AI Builders Hackathon (Devpost) — Aug 21–Sep 15, 2026
- **Builder:** Ayush (solo)
- **Build window:** ~4 days, starts Aug 21
- **Stack:** Next.js + Supabase (DB + Auth + Storage) + Vercel — mobile-responsive web app. NO native Android/iOS, NO Expo, NO background GPS.
- **This repo:** `ayush22cp008/Freight_test_Records` (mock/practice only)
- **Real records repo:** Will be created later as `Freight_Records`

---

## What this product is (LOCKED)
**Evidence notary, NOT a detention calculator.**

Driver logs 3 events: Arrival → Check-in → Departure  
Each event: GPS + server timestamp + photo (mandatory at Arrival + Departure)

Immutable (insert-only). AI generates factual evidence summary only.  
Core principle: *"We do not decide who is right. We create a reliable evidence record."*

---

## Core MVP — 7 items (LOCKED)
1. Driver-only login (driver ID), trip pre-seeded
2. 3 events only: Arrival → Check-in → Departure
3. GPS + server timestamp on every event
4. Photo mandatory at Arrival + Departure
5. Immutable storage (insert-only, RLS)
6. In-app chronological timeline
7. AI evidence summary (single LLM call, deterministic data only)

---

## Node 2.5 — ACTIVE
3 technically uncertain pieces being tested in throwaway project `freight-core-test`:

1. `navigator.geolocation` on mobile Chrome
2. Photo capture + Supabase Storage upload
3. Immutable/insert-only Supabase table (RLS)

Antigravity executing setup. Ayush testing manually on mobile Chrome.

---

## What next brain / Grok should do
When Ayush shares Node 2.5 test results:
- All 3 pass → Confirm Node 2.5 LOCKED. Write Day 1 implementation spec for Antigravity.
- Any fail → Diagnose + targeted fix instruction. Do not proceed to Node 3 until all pass.
