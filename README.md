# dummy1-mhmmd-adipur.github.io

A static GitHub Pages site that serves **two purposes**:

1. **Web apps** — free, browser-based tools that run entirely client-side (no backend).
2. **Universal / App Links** — association files under `/.well-known/` plus per-app deep-link redirect pages.

Live: https://dummy1-mhmmd-adipur.github.io/

---

## Structure

```
/
├── index.html                    # Landing dashboard (lists the web apps)
├── tcg-save-editor/              # Web app: TCG Card Shop Simulator save editor
│   ├── index.html
│   └── pako.min.js               # gzip in the browser
├── mobile/                       # Deep-link / store redirect pages
│   ├── bangga/index.html         # NEW BANGGA
│   ├── bmi/index.html            # BMI Mobile
│   └── ganesha/index.html        # Bank Ganesha
├── .well-known/                  # Universal / App Links association files
│   ├── apple-app-site-association   # iOS Universal Links
│   └── assetlinks.json              # Android App Links
├── .nojekyll                     # Required so GitHub Pages serves the .well-known folder
└── README.md
```

---

## Web apps

### TCG Save Editor — `/tcg-save-editor/`
A browser-based save editor for **TCG Card Shop Simulator** (PC & Nintendo Switch).

- Loads the game's gzip-compressed `GameData` files directly (via [pako](https://github.com/nodeca/pako)).
- Loads the game's gzip-compressed `GameData` files directly and exports a **valid `GameData` file** (gzip header identical to the game's, OS byte `03`) ready to restore via **JKSV**.
- Card, worker, and furniture data sourced from the official [wiki](https://tcgcardshopsimulator.wiki.gg/).
- Runs 100% in the browser — nothing is uploaded.

**Features (by tab):**

- **Player** — player name, coins, shop level & EXP, fame, current day, review average (auto, read-only), unlock room/warehouse counts, tutorial flags.
- **Cards & Collection** — edit every card across **8 sets**: Tetramon, Destiny, Megabot, Fantasy RPG, Cat Job, Ascension, Ghost, Ghost Black. Per card: copies, collected flag, sell/market price, border type (Base→Full Art) and foil. Wiki thumbnails + names, search, and per-set colored thumbnails.
- **Items** — stock count, set/cost/market price, and license-unlock per item (0–499).
- **Workers** — 9 slots with wiki photos, names, stats (restock/checkout speed, fee, salary), price multipliers, pack-type toggles, EXP (max/clear), and hire/fire.
- **Grading** — in-progress graded cards (fast-forward days) and graded card inventory.
- **Achievements & Unlocks** — toggle 100 achievements (with names) + unlock all walls/floors/ceilings decorations.
- **Reviews** — edit the 50 stored customer reviews (name, 1–5 stars, type, time); the average recalculates from the stars.
- **Shop & Stats** — bills (set to 0), all-time statistics (21 metrics), automation settings (Quick Fill / Workbench / Donation), champion cards & tournament info.
- **Furniture** — browse all **43 furniture** items from the MY DIY app, grouped by level, with thumbnails, details (price, description), lock/unlock status vs your shop level, and a **"Set Shop Level"** shortcut to unlock.
- **Raw JSON** — direct JSON editor with search & replace.

> Tip: when repacking a Switch save for JKSV, zip the **files at the root** of the archive (not a wrapping folder, no `__MACOSX`). On macOS use the terminal, not right‑click → Compress.

---

## Mobile app links

Each folder under `/mobile/<app>/` is a small redirect page that detects the
platform and forwards to the correct app store (or opens the app via the
Universal/App Link association below).

| Path | App |
|------|-----|
| `/mobile/bangga/` | NEW BANGGA |
| `/mobile/bmi/` | BMI Mobile |
| `/mobile/ganesha/` | Bank Ganesha |

### Universal / App Links (`/.well-known/`)
- **iOS** reads `/.well-known/apple-app-site-association`.
- **Android** reads `/.well-known/assetlinks.json`.
- The path **must** be `/.well-known/` (with the leading dot) per RFC 8615 — a
  folder named `well-known` (no dot) is ignored by the OS.
- `.nojekyll` is required: GitHub Pages uses Jekyll by default, which skips
  dot-folders; `.nojekyll` disables that so `/.well-known/` is served.

---

## Running locally

Because the apps use `fetch()` and load local assets, open them through a
local web server (not `file://`, which shows a directory listing):

```bash
cd dummy1-mhmmd-adipur.github.io
python3 -m http.server 8000
```

Then visit:
- Dashboard: http://localhost:8000/
- Editor: http://localhost:8000/tcg-save-editor/

---

## Adding a new web app

1. Create a folder, e.g. `my-new-tool/`, with an `index.html` inside.
2. Add a card for it in the root `index.html` dashboard (`#apps` grid).
3. Commit and push — GitHub Pages serves it automatically.

---

Built by [mhmmd.adipur](https://github.com/MhmmdAdipur).
