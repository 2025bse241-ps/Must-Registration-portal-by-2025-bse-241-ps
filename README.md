# MUST Online Application Portal

Click here for preview 

http://127.0.0.1:8484/index.html 

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
