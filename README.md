# MUST Online Application Portal

A complete, self-contained front-end for the Mbarara University of Science and
Technology online application portal — sign in, create an account, recover a
password, and a full applicant dashboard (stages, documents, fee, messages,
profile).

No build step, no framework, no CDN, no server. Every font and icon is bundled,
so the site works offline and uploads to GitHub Pages as-is.

## Pages

| File | What it does |
|---|---|
| `index.html` | Sign in — validation, show/hide password, remember me, demo account |
| `register.html` | Create account — 2-step wizard, password strength, issues an application number |
| `forgot.html` | Password reset — email → 6-digit code → new password |
| `dashboard.html` | Applicant panel — overview, application, documents, fee, messages, profile |

Demo credentials (the sign-in page has a **Fill demo credentials** button):

```
email:    demo@must.ac.ug
password: Must@2026
```

## Upload to your own GitHub (no coding)

1. Go to <https://github.com/new>, name the repository (e.g. `must-portal`),
   keep it **Public**, click **Create repository**.
2. On the new repo page click **uploading an existing file**.
3. Drag the **whole contents of this folder** in — `index.html`,
   `register.html`, `forgot.html`, `dashboard.html`, the `assets` folder and
   `.nojekyll` (if your file manager hides dot-files, upload everything else;
   the site still works).
4. Click **Commit changes**.
5. Open **Settings → Pages**, set **Source = Deploy from a branch**,
   **Branch = main**, folder **/ (root)**, then **Save**.
6. Wait 1–2 minutes. Your live link is
   `https://<your-username>.github.io/<repo-name>/`.
7. In **Settings → Pages** also set **Custom domain** only if you own one —
   not required.

Replacing the site later: upload the changed file(s) with
**Add file → Upload files**, commit, and the live site updates in about a minute.

## What to change first

Everything is plain HTML/CSS. Open the file in any text editor.

- **Brand colours** — `assets/css/app.css`, top of the file, the `:root` block:
  `--brand` (royal indigo), `--gold` (accent), `--paper` (background).
  The dark theme is the `[data-theme="dark"]` block right below it.
- **Crest / logo** — replace `assets/img/must-crest.png` (square PNG, 256×256,
  transparent or white background works best).
- **Programmes** — the `<select>` lists in `register.html` and
  `dashboard.html`. Edit the `<option>` lines; the dashboard saves whatever it
  is given.
- **Deadline** — `assets/js/dashboard.js`, the `DEADLINE` constant. It also
  drives the "closes in N days" counter.
- **Fee amount** — search for `UGX 50,000` in `dashboard.html`.
- **Messages** — the `MESSAGES` array at the top of `assets/js/dashboard.js`.
- **Contact details** — search for `admissions@must.ac.ug` and the phone number.
- **Page titles / description** — the `<head>` of each page (good for search
  engines and link previews).

## How the demo works (and what it is not)

This is a **front-end demonstration**. Accounts, the session and application
progress are stored in the visitor's own browser via `localStorage`; passwords
are hashed with SHA-256 before storage, never kept in plain text.

Nothing leaves the device. That means:

- No real accounts, no email or SMS is sent, no payment is charged.
- The six-digit recovery code is displayed on screen (a real deployment emails it).
- "Attaching" a document just marks it received locally.
- Clearing browser data deletes the demo account.

To make it real you need a backend. Minimum viable stack:

1. **Auth + database** — Supabase, Firebase, or a small Node/PHP API with
   Postgres/MySQL. Store users, applications, documents and payments.
2. **Email** — a transactional provider (Postmark, Resend, SES) for
   verification and recovery codes.
3. **File storage** — S3 or Supabase Storage for document uploads, with
   virus and image-clarity checks.
4. **Payments** — a mobile money / bank gateway (MTN MoMo, Airtel Money,
   Flutterwave, Pesapal) with server-side confirmation and receipts.
5. **HTTPS** — mandatory; also required for clipboard and crypto APIs.

The markup and styles can stay exactly as they are; swap the `localStorage`
calls in `assets/js/app.js` and `assets/js/dashboard.js` for API requests.

## Accessibility and performance notes

- Keyboard reachable, visible focus rings, skip links, `aria-live` errors,
  labelled inputs, `aria-current` navigation.
- Respects `prefers-reduced-motion` and `prefers-color-scheme`; the dashboard
  has a manual light/dark toggle.
- Mobile-first from 360px, no horizontal scrolling, no layout shift.
- No web requests at runtime: fonts and icons are bundled in `assets/`.
- Print-friendly application summary (dashboard → My application → Print).

## File map

```
index.html  register.html  forgot.html  dashboard.html
README.md
.nojekyll
assets/
  css/app.css            design system + every page style
  js/app.js              auth screens: validation, hashing, wizard, OTP
  js/dashboard.js        dashboard: stages, documents, fee, messages, theme
  img/must-crest.png     university crest
  fonts/                 Fraunces + Source Sans 3 + JetBrains Mono (offline)
```
