# Chat2_Node2.5_Instruction_LocalFreightCoreTestSetup.md

**Chat:** #2  
**Node:** 2.5  
**Type:** Instruction (for Antigravity + any reasoning brain)  
**Date:** 2026-08-18

---

## Important Context (Read Fully)

This is a **THROW AWAY / MOCK TEST** only.

- Real Freight project build starts on **Aug 21**.
- This test is only to prove 3 uncertain technical pieces before the real build.
- **No real source code repository** is being created for this test.
- Everything runs on **localhost** and stays on **local file system** only.

---

## Local Project Location (Very Important)

Ayush has already created the folder on his local machine:

```
Desktop / Freight_core_test
```

**Full expected path (Windows style):**
`C:\Users\<AyushUsername>\Desktop\Freight_core_test`

or simply:
`Desktop\Freight_core_test`

Antigravity must work **only inside this local folder**.  
Do **not** create any new GitHub repository for the test code.  
Do **not** push this test project anywhere unless Ayush explicitly asks.

---

## What this test project is for

We need to prove these 3 things work on **mobile Chrome**:

1. `navigator.geolocation` → reliable GPS coordinates + permission behavior
2. Photo capture using `<input type="file" accept="image/*" capture="camera">` + upload to Supabase Storage
3. Supabase table with RLS that allows only INSERT (blocks UPDATE + DELETE)

---

## Current Status

- Records are in: `ayush22cp008/Freight_test_Records` (this repo)
- Test code location: **Local only** → `Desktop/Freight_core_test`
- Running: **localhost only**
- Antigravity role: Setup + implement the 3 test surfaces inside the local folder
- Ayush role: Manual testing on real mobile Chrome + share screenshots/results

---

## Instruction for Antigravity

1. Confirm the local folder `Desktop/Freight_core_test` exists.
2. If it is empty → initialize a clean Next.js + Supabase project inside it.
3. Implement only the minimum needed to test the 3 points above.
4. Keep everything simple and local. No extra features.
5. After setup, report back:
   - Exact local path used
   - How to run (`npm run dev` or equivalent)
   - What URLs / pages are available for testing

Do not invent extra architecture. Keep it minimal for Node 2.5 testing only.

---

## For Reasoning Brains (ChatGPT / Claude / Grok)

When Ayush shares test results:
- All 3 pass → Lock Node 2.5 and prepare Day 1 real build spec
- Any fail → Write targeted diagnosis + fix instruction (separate from investigation)

---

**This file is the single source of truth for the local test project location and rules.**
