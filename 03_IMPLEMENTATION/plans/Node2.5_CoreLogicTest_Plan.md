# Node2.5_CoreLogicTest_Plan.md

**Chat:** #2  
**Node:** 2.5  
**Status:** ACTIVE  
**Type:** Core logic validation before real build

---

## Goal
Prove 3 uncertain technical pieces work reliably on mobile Chrome before Day 1 of real build.

## Test Project
- Name: `freight-core-test` (throwaway)
- Stack: Next.js + Supabase (same as final)

## 3 Tests

### Test 1 — Geolocation
- API: `navigator.geolocation`
- Questions:
  - Reliable coordinates on mobile Chrome?
  - Permission prompt behavior?
  - Accuracy level?

### Test 2 — Photo + Storage
- Capture: `<input type="file" accept="image/*" capture="camera">`
- Upload to Supabase Storage bucket
- Expect public URL returned

### Test 3 — Immutable Table
- Supabase RLS policy
- Allow INSERT for authenticated user
- Block UPDATE + DELETE completely

## Success Criteria
All 3 tests must PASS with evidence (screenshots / logs) before Node 2.5 is locked and Node 3 begins.

## Roles
- **Antigravity:** Setup test project + implement the 3 test surfaces
- **Ayush:** Manual testing on real mobile Chrome + share evidence
- **Grok (active brain):** Diagnose failures if any, write fix instructions, confirm lock when all pass
