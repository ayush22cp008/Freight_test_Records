# Chat2_Node2.5_Instruction_Test1_Geolocation.md

**Chat:** #2  
**Node:** 2.5  
**Test:** 1 of 3 — `navigator.geolocation`  
**Type:** Instruction for Antigravity  
**Date:** 2026-08-18

---

## Goal of this instruction

Create a **minimal local Next.js page** that tests only `navigator.geolocation` on mobile Chrome.

We need proof of:
1. Does the permission prompt appear correctly on mobile Chrome?
2. Does it return coordinates (latitude + longitude)?
3. What is the approximate accuracy?
4. Does it work when the page is opened via localhost from a real phone?

---

## Local Project Rules (Do Not Break)

- Work **only** inside the local folder: `Desktop/Freight_core_test`
- This is a throwaway test. **Do not** create any GitHub repository for this code.
- Everything runs on **localhost** only.
- Keep the project extremely minimal — only what is needed for Test 1.

---

## Exact Steps for Antigravity

### Step 1 — Confirm folder
Check that this folder exists:
```
Desktop/Freight_core_test
```
If it does not exist, create it.

### Step 2 — Initialize Next.js (if not already done)
Inside `Desktop/Freight_core_test` run:

```bash
npx create-next-app@latest . --typescript --tailwind --eslint --app --src-dir --import-alias "@/*" --use-npm --no-turbopack
```

(If the folder already has a Next.js project, skip this step.)

### Step 3 — Create a simple test page

Create or replace the main page with a clean geolocation test page.

**File:** `src/app/page.tsx` (or `app/page.tsx` depending on structure)

Requirements for the page:
- A big clear button: **"Get My Location"**
- On click → call `navigator.geolocation.getCurrentPosition`
- Show loading state while waiting
- On success → display:
  - Latitude
  - Longitude
  - Accuracy (in meters)
  - Timestamp
- On error → display the exact error message (permission denied, timeout, etc.)
- Make the page mobile-friendly (large text, large button)

Use only client-side code (`"use client"`).

### Step 4 — Run the project

```bash
npm run dev
```

Report back:
- Exact local path used
- The localhost URL (usually http://localhost:3000)
- How Ayush should open it on his phone (same Wi-Fi → use computer’s local IP)

### Step 5 — What NOT to do
- Do not add Supabase yet
- Do not add photo capture yet
- Do not add authentication
- Do not add extra pages or features
- Do not push anything to GitHub

---

## Success Criteria (for Ayush to verify)

Ayush will test on real mobile Chrome and check:

- [ ] Permission prompt appears
- [ ] Coordinates are returned
- [ ] Accuracy value is shown
- [ ] Works when opened from phone via local IP

After testing, Ayush will share screenshots + results.

---

## After this instruction is complete

Antigravity should reply with:
1. Confirmation that the page is ready
2. Exact steps for Ayush to open it on phone
3. Any issues faced during setup

Then wait for Ayush’s test evidence before moving to Test 2.
