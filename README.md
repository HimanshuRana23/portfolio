# himanshurana.com — portfolio

Personal portfolio site for **Himanshu Rana**, Product Manager (B2B SaaS · 0→1 platforms · AI products).

Live: **https://himanshurana.pages.dev**

## What this is

A single static page. No framework, no build step, no dependencies — `index.html` contains all
markup, CSS and JavaScript; everything else is an image in `assets/`. Open `index.html` in a
browser and it works.

```
index.html              the whole site (markup + CSS + JS)
assets/                 portraits, company logos, product screenshots (webp)
Himanshu-Rana-CV.pdf    the downloadable CV linked from the hero
```

## Editing

Almost everything you'd want to change lives in one of three places in `index.html`:

| What you want to change | Where to look |
| --- | --- |
| Hero headline, intro copy, About text | the HTML near the top, after `<!-- ══ HERO ══ -->` |
| Case studies — titles, metrics, full write-ups | the `const CASES = [...]` array in the `<script>` |
| Roles and organisations | the `const ORGS = [...]` array |
| Colours, spacing, type | the `:root { --bg: … }` custom properties at the top of `<style>` |

Each case study is one object with these fields:

- `cat` — filter category: `platform`, `ai`, `growth`, `ops`
- `t` / `sub` — card title and subtitle
- `metrics` — the three figures shown on the card
- `ctx` / `p` / `cons` / `a` / `ship` / `r` — context, problem, constraints, approach, how it shipped, result
- `how` — how the number was measured (instrument, window, comparison basis)
- `learn` — what you'd do differently
- `shot` / `dia` — key into `SHOTS` (product screenshot) or `DIA` (inline SVG diagram)

Blank lines inside `a` are written as `\n\n` and become paragraphs.

## Deploying

Cloudflare Pages watches the `main` branch. Push to `main` and it redeploys — no build command,
no output directory, it serves the repo root as-is. A push to any other branch gets its own
preview URL, which is the safe way to look at a change before it's live.

Every deployment is listed in the Cloudflare dashboard and can be rolled back with one click,
so a bad edit is never more than a minute of downtime.

## Checking a change before you push

There's no build, but `index.html` uses relative asset paths, so serve it rather than opening
the file directly if you want the screenshots to load:

```sh
python3 -m http.server 8000    # then open http://localhost:8000
```

## Editing the CV

`Himanshu-Rana-CV.pdf` is generated from a separate `cv.html` source (not in this repo).
If you edit the PDF, replace the file here and push — the hero download link picks it up
automatically.
