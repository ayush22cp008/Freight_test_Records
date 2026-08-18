# Chat2_Node2.5 — Instruction: Test 2 Step 2 — Camera Capture + Supabase Storage Upload

**For:** Antigravity  
**Node:** 2.5 — Core logic testing  
**Test:** 2 of 3 — Camera → Supabase Storage  
**Step:** 2 — Build minimal test page (code only, no deploy yet)  
**Date:** 2026-08-19

---

## Task Summary

Build a minimal throwaway test page in the existing `freight-core-test` Next.js project that:
1. Captures a photo via mobile camera input
2. Uploads the File to Supabase Storage (`test-photos` bucket)
3. Shows upload result (success/error) on the page

**This is NOT production code.** Keep it simple, functional, testable.

---

## Prerequisites

Already prepared (Ayush has `.env.local` ready locally):
- Supabase project: `freight` (URL: `https://jlxwboeyxzfazuykaost.supabase.co`)
- Storage bucket: `test-photos` (public)
- `.env.local` already exists in the project with correct keys — do NOT overwrite it, just verify it's present.

---

## Implementation Steps

### Step 1 — Install Supabase client

```bash
npm install @supabase/supabase-js
```

### Step 2 — Verify `.env.local` exists

Check that `Freight_core_test/.env.local` contains:
```
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
```
If missing, stop and report back — do not proceed without it.

### Step 3 — Create Supabase client file

File: `src/lib/supabase.ts`

```typescript
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!;
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!;

export const supabase = createClient(supabaseUrl, supabaseAnonKey);
```

### Step 4 — Create camera test page

**Important:** Keep the existing Geolocation test (Test 1) completely untouched in `src/app/page.tsx`.

Create a NEW route for Test 2:

File: `src/app/test2/page.tsx`

```typescript
'use client';

import { useState } from 'react';
import { supabase } from '@/lib/supabase';

export default function Test2CameraPage() {
  const [file, setFile] = useState<File | null>(null);
  const [preview, setPreview] = useState<string>('');
  const [uploading, setUploading] = useState(false);
  const [result, setResult] = useState<{
    status: 'idle' | 'success' | 'error';
    message: string;
    path?: string;
  }>({ status: 'idle', message: '' });

  const handleCapture = (e: React.ChangeEvent<HTMLInputElement>) => {
    const selectedFile = e.target.files?.[0];
    if (!selectedFile) return;

    setFile(selectedFile);

    const reader = new FileReader();
    reader.onload = (event) => {
      setPreview(event.target?.result as string);
    };
    reader.readAsDataURL(selectedFile);
  };

  const handleUpload = async () => {
    if (!file) {
      setResult({ status: 'error', message: 'No file selected' });
      return;
    }

    setUploading(true);
    setResult({ status: 'idle', message: 'Uploading...' });

    try {
      const filename = `${Date.now()}-${file.name}`;

      const { data, error } = await supabase.storage
        .from('test-photos')
        .upload(filename, file, {
          cacheControl: '3600',
          upsert: false,
        });

      if (error) {
        setResult({
          status: 'error',
          message: `Upload failed: ${error.message}`,
        });
      } else {
        setResult({
          status: 'success',
          message: 'Upload successful!',
          path: data?.path,
        });
      }
    } catch (err) {
      setResult({
        status: 'error',
        message: `Error: ${err instanceof Error ? err.message : 'Unknown error'}`,
      });
    } finally {
      setUploading(false);
    }
  };

  return (
    <div className="min-h-screen bg-gray-900 text-white p-6">
      <h1 className="text-3xl font-bold mb-6">Test 2 — Camera → Supabase Storage</h1>

      <div className="mb-6">
        <label className="block mb-2 text-lg font-semibold">
          Capture Photo:
        </label>
        <input
          type="file"
          accept="image/*"
          capture="environment"
          onChange={handleCapture}
          className="block w-full border border-gray-600 p-2 rounded bg-gray-800"
        />
      </div>

      {preview && (
        <div className="mb-6">
          <p className="text-lg font-semibold mb-2">Preview:</p>
          <img
            src={preview}
            alt="Preview"
            className="w-64 h-64 object-cover rounded border border-gray-600"
          />
        </div>
      )}

      <div className="mb-6">
        <button
          onClick={handleUpload}
          disabled={!file || uploading}
          className="px-6 py-3 bg-green-600 hover:bg-green-700 disabled:bg-gray-600 rounded font-semibold"
        >
          {uploading ? 'Uploading...' : 'Upload to Supabase'}
        </button>
      </div>

      {result.status !== 'idle' && (
        <div
          className={`p-4 rounded ${
            result.status === 'success'
              ? 'bg-green-900 border border-green-600'
              : 'bg-red-900 border border-red-600'
          }`}
        >
          <p className="font-semibold">{result.message}</p>
          {result.path && (
            <p className="text-sm text-gray-300 mt-2">
              Path: <code className="bg-gray-800 px-2 py-1 rounded">{result.path}</code>
            </p>
          )}
        </div>
      )}

      <div className="mt-12">
        <a
          href="/"
          className="text-blue-400 hover:text-blue-300 underline"
        >
          ← Back to Test 1 (Geolocation)
        </a>
      </div>
    </div>
  );
}
```

---

## Execution Checklist

- [ ] `npm install @supabase/supabase-js` — completes without error
- [ ] `.env.local` verified present with correct Supabase URL + anon key
- [ ] `src/lib/supabase.ts` created with client initialization
- [ ] `src/app/test2/page.tsx` created (NEW route, not modifying Test 1)
- [ ] `npm run dev` — dev server starts
- [ ] Verify Test 1 still loads at `http://localhost:3000` (untouched)
- [ ] Verify Test 2 loads at `http://localhost:3000/test2`
- [ ] Test 2 page shows: camera input, preview area, upload button
- [ ] Build succeeds: `npm run build` (no TypeScript or runtime errors)

---

## Expected Behavior (Desktop smoke test)

1. Page loads
2. Click file input → file picker opens (or camera on mobile)
3. Select/capture an image
4. Image preview appears
5. Click "Upload to Supabase"
6. Button shows "Uploading..."
7. After ~2-3 seconds: success message with object path OR error message

---

## Notes

- This is a **test route**, not production. Will be discarded after Test 2 PASS.
- **Geolocation test (Test 1) must remain unchanged** — do not touch `src/app/page.tsx`.
- Use `capture="environment"` on mobile to trigger rear camera.
- Storage bucket is public, so no authentication needed for read; upload uses anon key.
- Report back: page loads, build succeeds, smoke test results.

---

## What Comes Next

Once this builds and smoke test passes (desktop):
- Deploy to Vercel
- Manual phone test
- Real device upload test
- Evidence collection
- Test 2 result document
