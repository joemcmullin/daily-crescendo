# Daily Crescendo — Stage 2 waitlist / demand-validation site

A trackerless, static landing page (+ Privacy / Terms / Support / Accessibility)
for the **Daily Crescendo** music-practice app demand smoke test (Apex Studio OS,
Stage 2). Deploys free on GitHub Pages. Source of truth lives in
`AppOpportunities2026/candidates/music-practice-journal/stage2/`; this repo is the
**deployment copy**.

**Done for you:** all 5 pages built and branded *Daily Crescendo*, `dailycrescendo.com`
wired into the OG/social tags, `.nojekyll`, `.gitignore`, committed. **Needs your
accounts:** fill the contact email → push → enable Pages → Formspree → point your
domain. (Site URL is already set; domain is already bought.)

---

## Step 1 — Fill the remaining placeholders

| Placeholder | Where | Replace with |
|-------------|-------|--------------|
| `REPLACE_WITH_CONTACT` | all 5 pages | a real **monitored** inbox (e.g. `support@dailycrescendo.com` once it exists, or a forwarder). This receives privacy/deletion requests, so it must actually be read. |
| `REPLACE_WITH_FORM_ENDPOINT` | `index.html` | your Formspree form URL (Step 4) |
| `og-image.png` | add a 1200×630 image at repo root | the social-card preview image |
| `[EFFECTIVE DATE]` | `privacy.html`, `terms.html`, `accessibility.html` | the date you publish |

Already set for you: the OG/Twitter site URL (`https://dailycrescendo.com`) and the brand name throughout.

> **Legal:** Governing law = **Virginia** (Apex Development Studio LLC's registered state). The Terms carry a binding-arbitration + class-action-waiver clause mirrored from your lawyer-reviewed ScreenPass docs. The HIPAA/health layer was intentionally excluded. **Before you rely on these, have counsel glance at the pre-launch arbitration clause, the "founding price" wording, and a Class 9 + 41 trademark clearance for "Daily Crescendo"** (sound-alike to existing "Crescendo" software marks).

Quick contact-email fill across every file:
```bash
cd ~/Projects/daily-crescendo
grep -rl REPLACE_WITH_CONTACT . | xargs sed -i '' 's/REPLACE_WITH_CONTACT/support@dailycrescendo.com/g'
```

Also (highest-value asset): swap the hero placeholder block (`<div class="hero">…</div>`'s
inner mock) for a 10-second **screen recording of the Live Activity practice timer in
the Dynamic Island, phone on a music stand** (`<video autoplay muted loop playsinline>`
or a GIF). The animated mock is good enough to launch with if you don't have footage yet.

## Step 2 — Push to GitHub (you're authenticated as `joemcmullin`)
```bash
cd ~/Projects/daily-crescendo
gh repo create daily-crescendo --public --source=. --remote=origin --push
```
(Creates the public repo and pushes `main`. Web fallback: create an empty public repo
`daily-crescendo` at github.com/new, then
`git remote add origin https://github.com/joemcmullin/daily-crescendo.git && git push -u origin main`.)

## Step 3 — Enable GitHub Pages
```bash
gh api -X POST repos/joemcmullin/daily-crescendo/pages -f 'source[branch]=main' -f 'source[path]=/'
```
Or: repo → Settings → Pages → Source = `main` / `/ (root)`.
Live in ~1 min at **https://joemcmullin.github.io/daily-crescendo/** — open it to confirm before pointing the domain.

## Step 4 — Formspree (no backend)
1. Free account at formspree.io → New Form → copy the endpoint (`https://formspree.io/f/XXXXXXXX`).
2. Paste it over `REPLACE_WITH_FORM_ENDPOINT` in `index.html`, commit, push.
3. Submit the form once yourself; confirm the email + answers (`current_method`, `frequency`,
   `switch_reason`, `is_teacher`, `utm_source`) land in the inbox. **Do this before spending on ads.**

## Step 5 — Point your domain (dailycrescendo.com — already registered)
- Rename `CNAME.example` → `CNAME`, put exactly `dailycrescendo.com` on line 1 (delete the comments), commit, push.
- At your registrar, add DNS for the apex domain:
  - A records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  - `www` CNAME → `joemcmullin.github.io`
- Repo → Settings → Pages → set custom domain `dailycrescendo.com` + check **Enforce HTTPS**.

## Step 6 — Per-channel UTM links (traffic test)
Append a different `?utm_source=` per channel so conversion segments by source:
`?utm_source=reddit_piano` · `?utm_source=asa` · `?utm_source=meta` · `?utm_source=pianoworld` · `?utm_source=teacher_email`.
Simplest: run one channel at a time and label the batch in your tracking sheet (`stage2/TRAFFIC.md`).

## Pre-flight checklist
- [ ] Contact email filled (monitored inbox)
- [ ] Formspree wired; test submission received with all fields
- [ ] Hero clip dropped in (or launch with the animated mock)
- [ ] `og-image.png` added; `[EFFECTIVE DATE]` stamped
- [ ] Live over HTTPS at `dailycrescendo.com`
- [ ] Then run `stage2/TRAFFIC.md` ($100–250) + `stage2/INTERVIEW.md`

When you have qualified-conversion %, reserve-click rate, and the interview read on
Andante switch-intent, bring them back and we apply `stage2/GATE.md`.
