# AI Water & Carbon Footprint Calculator

A single-file, client-side web app to estimate the **water** and **carbon** footprint of AI usage (e.g., ChatGPT prompts). Built for **GitHub Pages**—no backend, no tracking, fully portable.

**Live site:** `https://madhur-sabherwal.github.io/AI-Water-Carbon-Footprint-Calculator/`
**File:** `index.html` (one page; includes UI, logic, and chart)

---

## Why this exists

AI isn’t “virtual” in environmental terms. Every prompt hits GPUs in data centers that consume **electricity** (→ CO₂ based on grid mix) and **cooling water** (directly at the data center and sometimes upstream at power plants). Most conversations quote a single number; this calculator puts the **assumptions in your hands** so you can model different realities.

---

## What it does

* **Inputs:** prompts/day, days/month, PUE, **Wh/prompt**, **mL/prompt** water, **gCO₂/kWh** grid intensity, optional **L/kWh** power-plant water.
* **Outputs:** Daily and monthly **water (L)**, daily **CO₂ (g)**, monthly **CO₂ (kg)**, plus a bar chart.
* **Presets:** Frugal / Typical / Heavy usage, renewables-rich vs fossil-heavy grids, and inclusion of power-plant water.
* **Quality of life:** LocalStorage (auto-save), **CSV export**, single static file (no build step).

---

## Methodology (plain English)

**Energy → Emissions**

```
kWh/day  = (prompts/day × Wh/prompt × PUE) / 1000
CO₂/day  = kWh/day × grid_intensity (gCO₂/kWh)
CO₂/month = (kWh/month × grid_intensity) / 1000  (kg)
```

**Water**

```
Direct water/day (L)  = (prompts/day × mL/prompt) / 1000
Power-plant water/day (L) = kWh/day × (L/kWh)
Total water/day (L)   = Direct + Power-plant water
```

> **Assumptions are editable** because the real values vary by model size, context length, hardware generation, data-center design, ambient temperature, and grid mix.

---

## Presets (editable starting points)

| Preset                | Wh/prompt | Water mL/prompt | PUE | Grid gCO₂/kWh | Power-plant L/kWh |
| --------------------- | --------: | --------------: | --: | ------------: | ----------------: |
| Frugal                |       0.2 |              10 | 1.2 |   (unchanged) |       (unchanged) |
| Typical               |       0.5 |              30 | 1.3 |   (unchanged) |       (unchanged) |
| Heavy                 |       1.5 |              50 | 1.5 |   (unchanged) |       (unchanged) |
| Renewables-rich grid  |         — |               — |   — |        **80** |                 — |
| Fossil-heavy grid     |         — |               — |   — |       **800** |                 — |
| Add power-plant water |         — |               — |   — |             — |           **1.5** |

Use these for sensitivity testing—**don’t** present them as universal truth.

---

## Quick start (GitHub Pages)

1. Ensure the root file is **`index.html`** (no spaces).
2. Repo → **Settings → Pages** → Source: **Deploy from a branch**, Branch: `main`, Folder: `/ (root)`.
3. Wait \~1–2 minutes for Pages to publish; hard-refresh your URL.

**404?**

* Confirm the filename is exactly `index.html`.
* Clear caches/hard-refresh (Ctrl/Cmd+Shift+R).
* If you move files into underscored folders, add a root **`.nojekyll`** file.

---

## Local development

Just open `index.html` in a browser. Everything is embedded:

* **Tailwind (Play CDN)**
* **Chart.js** (for the bar chart)
* Vanilla JavaScript (no build tools)

---

## File structure

```
/
└── index.html   # Single-page app (HTML + JS + minimal CSS via Tailwind CDN)
```

---

## Configuration

All knobs are visible in the UI:

* **Prompts/day, days/month**
* **PUE** (typical 1.1–1.6)
* **Wh/prompt** (workload-dependent; start with 0.5 Wh for a “typical” inference)
* **Water mL/prompt** (midpoint of public estimates for inference; change as needed)
* **Grid gCO₂/kWh** (region-specific; get your ISO/RTO utility number)
* **Power-plant L/kWh** (optional; depends on generation tech and cooling)

---

## Privacy & Security

* No cookies, no analytics, no outbound calls.
* Inputs are saved to **LocalStorage** on your device for convenience.

---

## Roadmap (pull requests welcome)

* URL-based **shareable configurations** (query params)
* **Unit toggles** (imperial/metric)
* **Training mode** (GPU-hours → kWh calculator)
* Regional presets (grid intensity, L/kWh) with citations
* Accessibility refinements and print-ready report

---

## FAQ

**Q: Are these numbers “accurate”?**
**A:** They’re **transparent estimates**. Swap in your organization’s measured data for Wh/prompt, PUE, grid intensity, and water factors to tighten accuracy.

**Q: Why split “direct” vs “power-plant” water?**
**A:** To separate **data-center cooling** from **upstream generation** water. Both matter; not all disclosures include both.

**Q: Can I embed this in my site?**
**A:** Yes. It’s a single HTML file. Host it anywhere that serves static files.

---

## License

MIT — use it, fork it, improve it. Attribution appreciated.

---

## Attribution

Concept and implementation by Madhur Sabherwal and AI assistant. Built for pragmatic ESG conversations: **assumptions explicit, math auditable, results actionable**.
