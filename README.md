# ساحل مارکت — Sahel Market → GitHub Pages

Your Figma export, fixed and ready to publish at **https://faezehdanesh.ir**.

`index.html` is **fully self-contained** — the Persian font and all images are
embedded inside it. You only need to upload `index.html` and `CNAME`.

---

## What was fixed

| From the Figma export | Fix |
| --- | --- |
| **Missing font** — everything used `font-family: B Mahsa` (a commercial font that was never bundled), so Persian text fell back to an ugly default. | Embedded the free **Vazirmatn** font (base64) and aliased `B Mahsa` → Vazirmatn, so all text renders correctly with no markup changes. |
| **No document shell / wrong encoding** — no `<html>/<head>/<body>`, no `<meta charset>`; Persian risked showing as mojibake. | Wrapped in a valid HTML5 document with `<meta charset="utf-8">` and `lang="fa" dir="rtl"`. |
| **Images "missing"?** | They were never missing — they're embedded inline as base64 PNGs. Left as-is. |
| Raw stack of frames | Light CSS centers and spaces each frame like a presentation. |

## Known limitation — what Figma could NOT export

The plugin reported these, and they are genuinely blank in the design:

```
REGULAR_POLYGON node is not supported
Failed rendering SVG for Vector
Failed rendering SVG for Layer_1
```

A few small vector shapes / logo marks and one polygon came through as **empty
boxes**. They can't be recovered from the HTML. To restore them: in Figma select
each node, **export it as PNG or SVG**, and drop it in where the empty
`<div data-layer="Layer_1" ...></div>` placeholders are. (Send me the exports and
I'll wire them in.)

---

## Deploy (this session had read-only GitHub access, so upload it yourself)

### 1. Put the files in the repo
**Easiest — GitHub website:**
1. Open `https://github.com/LordEvil1/FigmaDesignPresentation`
2. **Add file → Upload files**
3. Drag in **`index.html`** and **`CNAME`** (and `.nojekyll` if you like)
4. Commit to `main` (or any branch you'll deploy from)

**Or with git locally:**
```bash
git clone https://github.com/LordEvil1/FigmaDesignPresentation
cd FigmaDesignPresentation
# copy index.html, CNAME, .nojekyll in here
git add . && git commit -m "Publish Sahel Market design" && git push
```

### 2. Turn on GitHub Pages
Repo → **Settings → Pages → Build and deployment → Source: “Deploy from a branch”**
→ pick your branch and **/(root)** → **Save**. Live in ~1 min at
`https://lordevil1.github.io/figmadesignpresentation/`.

### 3. Point your domain `faezehdanesh.ir` at GitHub
At your DNS provider add **A** records for the apex domain:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
and the matching **AAAA** (IPv6) records:
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```
(Optional `www`: add a **CNAME** record `www → lordevil1.github.io.`)

The included `CNAME` file already tells Pages to use `faezehdanesh.ir`. After DNS
propagates, go to **Settings → Pages → Custom domain**, confirm `faezehdanesh.ir`,
and tick **Enforce HTTPS**. Propagation can take minutes to ~24h.

---

## Font license
Vazirmatn by Saber Rastikerdar — **SIL Open Font License 1.1**
(see `LICENSE-Vazirmatn-OFL.txt`). Free for commercial use.
