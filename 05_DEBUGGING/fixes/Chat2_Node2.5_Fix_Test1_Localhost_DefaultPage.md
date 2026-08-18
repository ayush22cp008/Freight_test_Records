# Chat2_Node2.5 — Targeted Fix: Test 1 Localhost Default Page

**Node:** 2.5 — Core logic test  
**Test:** 1 of 3 — `navigator.geolocation`  
**Mode:** TARGETED FIX ONLY  
**Related investigation:** `05_DEBUGGING/investigations/Chat2_Node2.5_Investigation_Test1_Localhost_DefaultPage.md`

---

## Objective

Apply the targeted fix for the verified root cause found during investigation.

The `freight-core-test` project is correctly serving on port `3000`, but `src/app/page.tsx` contains the default Next.js starter page because the custom Geolocation page was overwritten during project scaffolding.

## Fix Scope

Modify only the application code required to restore the intended Node 2.5 Test 1 Geolocation Test page.

Primary target:

`C:\Users\ayush\Desktop\Freight_core_test\freight-core-test\src\app\page.tsx`

## Required Actions

1. Inspect the current project before editing.
2. Confirm the current `page.tsx` is the default Next.js boilerplate.
3. Restore/rewrite the intended Geolocation Test UI in `src/app/page.tsx`.
4. The page must allow manual triggering of `navigator.geolocation` and display the result/error information needed for testing.
5. Preserve the existing project architecture and stack.
6. Do not recreate the project.
7. Do not reinstall the project.
8. Do not change unrelated files.
9. Do not change Supabase functionality; that belongs to later Node 2.5 tests.
10. Do not switch tunnel providers or deploy anywhere yet.

## Local Verification

After the fix:

1. Confirm the expected `freight-core-test` Next.js dev server is running.
2. Open `http://localhost:3000`.
3. Confirm the custom Geolocation Test page is visible.
4. Confirm the default text `To get started, edit the page.tsx file.` is gone.
5. Confirm there are no compilation/runtime errors.
6. Confirm the Geolocation test control is present and usable locally.

## Stop Condition

After local verification, STOP.

Do not perform the mobile HTTPS geolocation test yet.
Do not declare Node 2.5 Test 1 PASS.

The next step after this fix is Ayush's manual mobile test through an HTTPS context.

## Required Result Location

Create the fix result at exactly:

`05_DEBUGGING/fixes/Chat2_Node2.5_Fix_Test1_Localhost_DefaultPage_Result.md`

The result file must contain:

### 1. Fix Applied
What was changed and why.

### 2. Files Changed
List every changed file.

### 3. Local Verification
State whether `http://localhost:3000` now shows the intended Geolocation Test page.

### 4. Evidence
Include relevant command/output summaries or other concrete evidence.

### 5. Remaining Step
State that the next step is the HTTPS/mobile manual geolocation test by Ayush.

### 6. Test Status
Use exactly:

`TEST 1 — LOCAL PAGE RESTORED; MOBILE GEOLOCATION TEST PENDING`

Do not mark Test 1 PASS at this stage.

## Workflow

`Verified Investigation → Targeted Fix → Local Verification → Ayush Mobile Test → PASS/FAIL`
