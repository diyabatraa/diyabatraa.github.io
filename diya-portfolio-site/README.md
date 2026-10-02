# Diya Batra — Portfolio

A static portfolio site. No build step, no dependencies, no framework — three HTML files that
open directly in a browser.

```
index.html                                  main page
projects/financial-health-dashboard.html    project 01
projects/churn-segmentation.html            project 02
```

## Deploying to GitHub Pages

1. Create a repository named `<username>.github.io` on GitHub (for example `diyabatra.github.io`).
2. Push these files to the root of the `main` branch, keeping the `projects/` folder intact.
3. In the repository: **Settings → Pages → Source → Deploy from a branch**, branch `main`, folder `/ (root)`.
4. The site goes live at `https://<username>.github.io` within a minute or two.

For a custom domain, add a file named `CNAME` at the root containing only the domain
(e.g. `diyabatra.com`), then point a CNAME DNS record at `<username>.github.io`.

## Design system

Dark navy base, white typography, electric blue and cyan accents. All three pages share the same
tokens, declared in the `:root` block at the top of each file.

```
Surfaces    --base #05080F   page       --glass rgba(255,255,255,.035)   panels
Lines       --line rgba(125,160,255,.13)          --line-2 rgba(130,190,255,.26)
Text        --white #FFFFFF  --text #E9EFFC  --muted #95A6C6  --dim #66769A
Accents     --cyan #22D3EE   --blue #4D7CFE   --grad 120° cyan → blue
Type        Sora (display) · DM Sans (body) · JetBrains Mono (figures)
```

Depth comes from three layered effects: fixed radial glows and a masked grid behind the content,
translucent panels with `backdrop-filter`, and hairline gradient borders. Hover states lift the
card and add a soft cyan ring. Changing `--cyan` and `--blue` re-themes the whole site.

Chart colours are held separately from the UI accents, because they have to stay distinguishable
from each other rather than just look good:

```
--dv-cyan #0BA3BF   default series / favourable
--dv-coral #EE6048  unfavourable
--dv-violet #7F6EE8 selected company
sequential ramp     --s1 #143A4C → --s5 #45C6DB   (dim → bright, for ordered data)
```

These were validated against the dark surface for lightness, chroma, colour-vision separation and
contrast. If they are changed, keep the three data hues distinct at all pairs — bright UI cyan
(`#22D3EE`) is too light to use as a data mark on this background.

## Editing

- **Copy** is plain HTML — edit the text directly in `index.html`.
- **Project data** lives in the `<script>` block at the bottom of each project page, in the
  `COMPANIES`, `CONTRACTS`, `TENURE`, `DRIVERS` and `SEGMENTS` arrays. Change the numbers and the
  charts, tables and variance flags all recompute from them.
- **The stat counters** in the hero read their targets from `data-count` attributes, with
  `data-prefix`, `data-suffix` and `data-group` for formatting. The visible text in the HTML is the
  final value, so it still reads correctly if the script never runs.
- The only external requests are the Google Fonts stylesheets. Remove those `<link>` tags and the
  pages fall back to system fonts and still work offline.

## Note on the project data

Both project pages carry a visible "Illustrative data" banner. The figures demonstrate the method;
the real Power BI file, notebook and Tableau workbook are referred to as available on request. If
the actual exports are dropped in, replace the arrays described above and delete the `.notice`
block from each page.

## Accessibility

Chart colours were validated for colour-vision separation and contrast against the dark surface.
Every chart is backed by a data table, series are labelled rather than identified by colour alone,
focus rings are visible on every interactive element, and `prefers-reduced-motion` disables the
reveal animations, the counters and all transitions.
