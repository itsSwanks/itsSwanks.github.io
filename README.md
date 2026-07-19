# Swanks — GitHub Project Dashboard

Source for **https://itsswanks.github.io/** — an animated project hub that lists everything I build, with each project's website hosted underneath it.

- **Live hub:** https://itsswanks.github.io/
- **GitHub repo (public):** `itsSwanks/itsSwanks.github.io` — this directory is a working clone of it.
- **Host:** GitHub Pages (branch `main`, folder `/`). **Push to `main` → live in ~1 minute.**
- **Auth:** the `gh` CLI is logged in as `itsSwanks` (realswanks@gmail.com), so `git push` just works.

> ⚠️ This repo is **public** and contains **only marketing/site HTML + screenshots** — no app source, no secrets. Keep it that way. Full app source lives in **private** repos (e.g. the TYP app is in the private `itsSwanks/typ`).

## Structure

```
index.html          ← the HUB dashboard (the project cards live here)
typ/                ← Project #1: TYP — Track Your Pep (its own site)
  index.html          the TYP landing page   → https://itsswanks.github.io/typ/
  img/*.png           app screenshots (used by the landing page)
  support/index.html  TYP support page       → https://itsswanks.github.io/typ/support/
README.md
```

Live routes today:
| URL | What |
|---|---|
| `https://itsswanks.github.io/` | The hub |
| `https://itsswanks.github.io/typ/` | TYP site |
| `https://itsswanks.github.io/typ/support/` | TYP support (this is TYP's **App Store Support URL**) |

## ➕ How to add a NEW project

Each project = a **subfolder** with its own site + a **card** on the hub. Two steps:

**1. Drop the project's site in a new subfolder.**
Create `myproject/` next to `typ/`, e.g. `myproject/index.html` (+ any `myproject/img/`, `myproject/support/`).
IMPORTANT: use **relative** links inside it (`img/...`, `support/`) — NOT absolute `/img/` — because it's served under the `/myproject/` subpath.

**2. Add a card to the hub.**
Open `index.html`, find the `PROJECT INDEX` grid. Copy the **TYP card** as a template (or replace one of the "coming soon" placeholder cards). Set:
- the card's link/action → `myproject/`
- name, tagline, status badge, tags, an icon (inline SVG), and optionally a preview image (`myproject/img/....png`)
Then bump the numbered slot (`N°002`, etc.) and the "READOUT" counts at the top.

**3. Deploy.**
```bash
cd /Users/s/Projects/GithubDashboard
git add -A
git commit -m "Add <project> to the hub"
git push origin main        # live at itsswanks.github.io/myproject/ in ~1 min
```

## Updating the hub or an existing project
Edit the file(s), then `git add -A && git commit -m "..." && git push origin main`.

## Design notes (keep the bar high)
- The hub is a self-contained single `index.html` — inline CSS/JS, **no external hosts/CDNs/fonts** (GitHub Pages has no CSP issues, but staying self-contained keeps it fast + portable). Draw graphics with CSS/inline SVG.
- Light **and** dark themes via `prefers-color-scheme`; honor `prefers-reduced-motion`.
- Aesthetic: dark "build-index / control-room" — monospace technical accents, editorial headline, numbered project cards, a live clock and stat readout. Each project card may use its own accent; the hub keeps its own neutral identity.
