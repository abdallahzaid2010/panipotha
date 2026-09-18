# Panipotha — Sri Lankan Past Papers Archive

A static website for hosting and sharing Sri Lankan school past papers (O/L, A/L, term tests), styled like an e-thaksalawa-type portal. Built to run on **GitHub Pages** with no backend server.

## What's included
- `index.html` — homepage: search, filter, preview, share link, gated download
- `login.html` — sign in / create account page
- `papers.json` — the catalog of papers (edit this to add/remove papers)
- `papers/` — put your actual PDF files here
- `assets/css/style.css` — all styling
- `assets/js/app.js` — renders the list, search, preview, share, download gate
- `assets/js/auth.js` — sign-in logic (Firebase Authentication)

## 1. Deploy to GitHub Pages
1. Create a new GitHub repository (e.g. `panipotha`).
2. Upload all these files to the repo, keeping the folder structure.
3. Go to **Settings → Pages**, set Source to the `main` branch, root folder.
4. Your site will be live at `https://YOUR-USERNAME.github.io/panipotha/` within a minute or two.

## 2. Who can add new papers — how access is restricted to you
GitHub Pages has no server, so "who can upload" is controlled the same way GitHub controls everything: **only people added as collaborators on the repository can push changes.**

By default that's just you. As long as you don't add anyone else as a collaborator (or you keep the repo private and only make the *Pages output* public), only you can add, edit, or remove papers. This is a real, meaningful access boundary — not just a UI restriction.

**To add a new paper:**
1. Drop the PDF file into the `papers/` folder.
2. Add an entry for it in `papers.json`, e.g.:
   ```json
   {
     "id": "ol-english-2025-p1",
     "title": "English — Paper I",
     "level": "O/L",
     "subject": "English",
     "medium": "English",
     "year": 2025,
     "type": "Past Paper",
     "file": "papers/ol-english-2025-p1.pdf",
     "size": "1.1 MB"
   }
   ```
3. Commit and push. The site updates automatically — no rebuild step needed.

If typing JSON by hand is annoying, open `admin-helper.html` locally in your browser (don't publish it, or do — it doesn't upload anything by itself) — it lets you fill a form and copies the correctly-formatted JSON entry to your clipboard, ready to paste into `papers.json`.

## 3. Turn on real sign-in (Firebase Authentication)
Downloads are gated behind sign-in, but this needs an auth provider since GitHub Pages can't run its own server. Firebase Authentication is free and built for exactly this (static sites, no backend):

1. Go to [console.firebase.google.com](https://console.firebase.google.com) → **Add project** (free).
2. In your project, go to **Build → Authentication → Get started**, and enable **Email/Password** and (optionally) **Google** as sign-in methods.
3. Go to **Project settings → General → Your apps → Add app → Web (</>)**. Copy the config object it gives you.
4. Open `assets/js/auth.js` and replace the placeholder `FIREBASE_CONFIG` values with your real ones.
5. In the Firebase console, under **Authentication → Settings → Authorized domains**, add your GitHub Pages domain (`YOUR-USERNAME.github.io`).
6. Commit and push. Sign-in and the download gate will now work for real.

Until you do this, the site still works and looks complete, but the "sign in" step is skipped automatically (with a console warning) so visitors can still download — that's intentional, so the site isn't broken while you're setting Firebase up.

## 4. Customising
- Colours, fonts and layout live in `assets/css/style.css`.
- Site name/branding: search for "Panipotha" in `index.html`, `login.html`, and `README.md` and replace with your name.
- Add more filters (e.g. "Zone", "Medium") by adding fields to `papers.json` and extending `app.js`.

## Note on copyright
Only upload papers you have the right to redistribute (e.g. Department of Examinations past papers, which are generally publicly released, or your own school's materials). Avoid republishing copyrighted textbooks or commercial study guides without permission.
