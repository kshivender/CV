# Shivender Kumar — Digital Résumé

A single-page, self-contained website version of Shivender Kumar's résumé, themed around seismic wiggle traces and stratigraphic horizons — built to be hosted free on **GitHub Pages**.

```
shivender-resume/
├── index.html              ← the entire site (HTML + CSS + JS in one file)
├── Shivender_Kumar_CV.pdf   ← original PDF, linked from the "Download Résumé" button
└── README.md                ← this file
```

There's nothing to build or install — it's plain HTML/CSS/JS, so it runs by just opening `index.html` in a browser, and deploys to GitHub Pages with zero configuration.

---

## 1. Put it on GitHub

1. Create a new repository on GitHub — e.g. `shivender-resume` (or `<your-username>.github.io` if you want it at the root of your GitHub domain).
2. Upload these three files to the repo (drag-and-drop on the GitHub web UI works fine, or via git):

   ```bash
   git init
   git add .
   git commit -m "Initial resume site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/shivender-resume.git
   git push -u origin main
   ```

## 2. Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under "Build and deployment", set **Source** to `Deploy from a branch`.
3. Set **Branch** to `main` and folder to `/ (root)`. Save.
4. Wait 1–2 minutes. Your site will be live at:
   - `https://<your-username>.github.io/shivender-resume/` (normal repo), or
   - `https://<your-username>.github.io/` (if the repo is named `<your-username>.github.io`)

That's the entire deployment — GitHub Pages just serves the static files as-is.

---

## 3. About the "backend" — what's real and what isn't

GitHub Pages **only serves static files** (HTML/CSS/JS). It cannot run a server, a database, or receive form submissions on its own — there is no way around this on GitHub Pages specifically. So for the contact form to actually deliver email, it's wired to a free third-party form backend instead of a fake one. Here are your real options, easiest first:

### Option A — Formspree (already wired in, recommended)
1. Go to [formspree.io](https://formspree.io) and create a free account.
2. Create a new form, and copy the endpoint it gives you (looks like `https://formspree.io/f/abcdwxyz`).
3. In `index.html`, find this line inside the `<form>` tag:
   ```html
   <form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
   Replace `YOUR_FORM_ID` with your real ID.
4. Commit and push. Submissions now arrive in your email — no server code needed. Free tier covers 50 submissions/month.

### Option B — EmailJS
Sends email straight from the browser via JavaScript (no redirect). Good if you want the form to stay on-page and show a "Message sent" confirmation instead of navigating away. Sign up at [emailjs.com](https://www.emailjs.com), and swap the `<form>` for a JS `fetch`/SDK call using their snippet — happy to wire this in if you'd prefer it over Formspree.

### Option C — Skip the form, just use `mailto:`
The email and phone links in the Contact section already work with no setup (`mailto:` and `tel:` links) — if you want zero third parties involved, you could delete the form entirely and rely on those.

### If you want a *real* backend later
That means hosting compute somewhere, which GitHub Pages doesn't do. Cheapest real options: a small serverless function (Cloudflare Workers or Vercel free tier) that receives the form POST and forwards email via an API like Resend or SendGrid. That's a bigger step — only worth it if you outgrow Formspree's free tier.

---

## 4. Common edits

- **Update content:** everything is plain text inside `index.html` — search for the section (`Profile`, `Experience`, `Expertise`, `Education`, `Contact`) and edit directly.
- **Swap the résumé PDF:** replace `Shivender_Kumar_CV.pdf` with a new file of the same name, or update the `href` in the "Download Résumé" button.
- **Colors:** all colors are defined once at the top of the `<style>` block under `:root` (e.g. `--amber`, `--brine`, `--bg-deep`) — change them there and they apply everywhere.
- **Add a custom domain:** in **Settings → Pages**, add your domain under "Custom domain" and follow GitHub's DNS instructions (a `CNAME` record pointing at `<your-username>.github.io`).

---

## 5. Before it's public

- [ ] Replace the Formspree `YOUR_FORM_ID` placeholder (or remove the form).
- [ ] Double check the phone number / email are ones you're comfortable listing publicly.
- [ ] Test on mobile — the layout is responsive, but a quick check never hurts.
