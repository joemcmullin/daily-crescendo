# MPJ Waitlist — Stage 2 demand-validation landing page

A trackerless, static landing page for the Music Practice Journal demand smoke
test (Apex Studio OS, Stage 2). Deploys free on GitHub Pages. Source of truth for
this page lives in `AppOpportunities2026/candidates/music-practice-journal/stage2/`;
this repo is the **deployment copy**.

**What's done for you:** repo built, `index.html` in place, `.nojekyll` added (so
Pages serves the file as-is), `.gitignore`, and an initial commit. **What needs
your accounts:** 2 placeholder edits → push → enable Pages → Formspree → domain.

---

## Step 1 — Edit two placeholders in `index.html`
Search-and-replace these across the repo:

| Placeholder | Where | Replace with |
|-------------|-------|--------------|
| `REPLACE_WITH_CONTACT` | **all 5 pages** | a real reply email (footer + legal pages) |
| `REPLACE_WITH_FORM_ENDPOINT` | `index.html` | your Formspree form URL (Step 4) |
| `REPLACE_PER_CHANNEL` | `index.html` | leave as-is; set `utm_source` per shared link (Step 6) |
| `REPLACE_WITH_SITE_URL` | `index.html` (OG/Twitter tags) | your live URL, e.g. `https://yourdomain.app` |
| `og-image.png` | add a 1200×630 share image at repo root | the social-card image |
| `[EFFECTIVE DATE]` | `privacy.html`, `terms.html`, `accessibility.html` | the date you publish |

> Governing law is set to **Virginia** (Apex Development Studio LLC's registered state, per the lawyer-reviewed ScreenPass docs). The Terms include a binding-arbitration + class-action-waiver clause mirrored from those reviewed docs — **have counsel give the pre-launch arbitration clause and the "founding price" wording a final glance** before you rely on them.

Quick way to do the contact email across every file:
```bash
cd ~/Projects/mpj-waitlist
grep -rl REPLACE_WITH_CONTACT . | xargs sed -i '' 's/REPLACE_WITH_CONTACT/you@yourdomain.com/g'
```

**The site has 5 pages** — `index.html` (the landing page) plus theme-matched
`privacy.html`, `terms.html`, `support.html`, `accessibility.html` (linked from
the footer, sharing `doc.css`). The legal pages are solid drafts — **have them
reviewed before you rely on them**, and fill the date/state placeholders above.

Also (the single most important asset): replace the hero placeholder block (the
`<div class="hero">…</div>`) with a 10-second **screen recording of the Live
Activity practice timer running in the Dynamic Island, phone on a music stand.**
Drop an `<video autoplay muted loop playsinline>` or an animated GIF in its place.
The whole pitch is "see it while you play" — this clip carries the page.

## Step 2 — Push to GitHub (you're authenticated as `joemcmullin`)
From this folder:
```bash
cd ~/Projects/mpj-waitlist
gh repo create mpj-waitlist --public --source=. --remote=origin --push
```
(That one command creates the public repo and pushes `main`. Web fallback: create
an empty public repo named `mpj-waitlist` at github.com/new, then
`git remote add origin https://github.com/joemcmullin/mpj-waitlist.git && git push -u origin main`.)

## Step 3 — Enable GitHub Pages
```bash
gh api -X POST repos/joemcmullin/mpj-waitlist/pages -f 'source[branch]=main' -f 'source[path]=/'
```
Or: repo → Settings → Pages → Source = `main` / `/ (root)` → Save.
Live in ~1 min at **https://joemcmullin.github.io/mpj-waitlist/**. Open it to confirm.

## Step 4 — Formspree (no backend)
1. Free account at formspree.io → New Form → copy its endpoint
   (`https://formspree.io/f/XXXXXXXX`).
2. Paste it over `REPLACE_WITH_FORM_ENDPOINT` in `index.html`, commit, push.
3. Submit the form once yourself; confirm the email + the 3 qualification answers
   (`current_method`, `frequency`, `switch_reason`) + `is_teacher` + `utm_source`
   land in the Formspree inbox. **Do this before spending a dollar on ads.**

## Step 5 — Domain (~$12/yr, the only required pre-ad spend)
Register one clean candidate domain (the real app name comes at Stage 3, so don't
overthink it; avoid the marks "Andante / Modacity / Tonara"). Then:
- Rename `CNAME.example` → `CNAME`, put only the domain on line 1, commit, push.
- At your registrar, add DNS for an **apex domain**:
  - A records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  - (or a `www` CNAME → `joemcmullin.github.io`)
- Repo → Settings → Pages → set the custom domain + check "Enforce HTTPS".

## Step 6 — Per-channel UTM links (for the traffic test)
Share a different URL per channel so conversion segments by source. Append to the
live URL:
```
?utm_source=reddit_piano
?utm_source=asa
?utm_source=meta
?utm_source=pianoworld
?utm_source=teacher_email
```
(`index.html` copies `utm_source` into each form submission via the hidden field —
but the static page won't auto-read the query string into that field, so either
set it per-link in a duplicated file, or just rely on Formspree's referrer data +
launching one channel at a time. Simplest: run one channel at a time and label the
batch in your tracking sheet.)

## Pre-flight checklist
- [ ] Hero clip dropped in (Live Activity timer on a music stand)
- [ ] Formspree endpoint wired; test submission received with all fields
- [ ] Contact email set
- [ ] Page live over HTTPS (github.io URL at minimum)
- [ ] Domain pointed (optional but recommended — it's the app's future site)
- [ ] Then run `stage2/TRAFFIC.md` ($100–250) and `stage2/INTERVIEW.md`

When you've got qualified-conversion %, reserve-click rate, and the interview read
on Andante switch-intent, bring them back and we apply `stage2/GATE.md`.
