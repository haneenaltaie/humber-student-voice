# Student Voice Board

An anonymous feedback tool built for the Humber Downtown Student Advisory Committee (SAC), Summer '26.

**Live site:** https://humber-student-voice.netlify.app/?v=2

## What it does

Students submit anonymous feedback — ideas, concerns, or suggestions about campus life, academics, facilities, or anything else — with no login required. Submissions are **not** publicly visible; only the SAC (via a private, authenticated dashboard) can read and manage them.

- `index.html` — the public submission form. Anyone can post; no one can read what others wrote.
- `dashboard.html` — a private, sign-in–gated view for reviewing and deleting submissions. Restricted to a single authorized admin account and excluded from search engines (`noindex`).
- `og-image.png , image.png` — social preview image used for link cards (LinkedIn, etc.).

## Tech stack

- Plain HTML/CSS/JS, no build step or framework
- **Firebase Firestore** — stores submissions in a `voices` collection
- **Firebase Authentication** (Google Sign-In) — gates the admin dashboard to one authorized email
- **Firestore Security Rules** — enforce the actual access control server-side:
  - anyone can `create` a submission that matches the expected shape (text length, valid category, starts at 0 votes)
  - only the authenticated admin can `read` or `delete` submissions
  - no one can `update` existing submissions
- Hosted as a static site on **Netlify**

The Firebase config object visible in `index.html` (API key, project ID, etc.) is safe to expose — it's a public client identifier, not a secret. Actual security is enforced by the Firestore rules above, not by hiding this config.

## Privacy model

- No accounts, no cookies, no tracking — submissions carry no identifying information.
- Submissions are write-only from the public's perspective: there is no public list, vote count, or feed to browse.
- Only the SAC admin, signed in with an authorized Google account, can view or remove entries via `dashboard.html`.

## Status

Live and in use for Summer 2026 SAC feedback collection at Humber Downtown.
