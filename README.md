# NCAA Financial Power Index

**v19 · May 2026**

A scored ranking of **138 FBS college football programs** on their **Financial Power Score (FPS)** — a composite index measuring donor wealth capacity, NIL coordination, athletics revenue, fundraising execution, endowment depth, and donor concentration risk.

## Live Site

Deployed via Cloudflare Pages: `[your-project].pages.dev`

---

## FPS Formula

```
FPS = 0.35 × Wealth Capacity
    + 0.22 × NIL Coordination
    + 0.18 × Athletics Revenue
    + 0.10 × Athletics Fundraising
    + 0.07 × Endowment Strength
    + 0.08 × (100 − Blended Risk)
```

All components use percentile-rank normalization (0–100) across 138 schools.

---

## Repo Structure

```
ncaa-fps/
├── index.html          ← Self-contained dashboard (all data embedded)
├── README.md
├── .gitignore
└── data/
    └── NCAA_Financial_Power_Dashboard_v19.xlsx   ← Source data reference
```

The dashboard is a **single self-contained HTML file** — no build step, no server, no external data calls required. All 138 schools are embedded as JSON.

---

## Deployment

### Cloudflare Pages (recommended)

1. Push this repo to GitHub
2. Go to `dash.cloudflare.com` → Workers & Pages → Create → Pages
3. Connect to GitHub → select this repo
4. Build settings: Framework = **None**, Build command = *(empty)*, Output directory = `/`
5. Deploy → Cloudflare assigns `your-project.pages.dev`

Updates: re-upload/push `index.html` → Cloudflare auto-redeploys in ~30 seconds.

### Custom domain

Add in Cloudflare Pages → Custom Domains after initial deploy.

---

## Data Sources

| Source | What it covers |
|--------|----------------|
| [EADA](https://ope.ed.gov/athletics/) | Athletics revenue, all FBS public schools |
| [Knight-Newhouse](https://knightnewhousedata.org/) | ~230 public school finances, FY2024 |
| [CNBC Valuations](https://www.cnbc.com/2025/12/19/cnbc-official-college-sports-valuations-2025-top-75-athletic-programs.html) | Top 75 by revenue, FY2024 confirmed |
| [247Sports](https://247sports.com/season/2025-football/compositeteamrankings/) | Recruiting composite rankings |
| [IPEDS](https://nces.ed.gov/ipeds/use-the-data) | Individual school endowment |
| [On3 NIL](https://www.on3.com/nil/) | NIL collective spend estimates |

---

## Annual Update Schedule

| Data | Typical release | Action |
|------|----------------|--------|
| Athletics revenue (FY2024) | Dec 2026 | Update `ath_rev` → rescore → rebuild |
| Endowment | Jan annually | Update `ENDOWMENT_B` → rescore → rebuild |
| NIL collective changes | Ongoing | Update collective names/notes → rebuild |
| Conference changes | As announced | Update `CONF_2026` dict → rebuild |

**Note:** UCLA, Oregon, and Washington FY2023 figures are pre-Big Ten. FY2024 data (expected Dec 2026) will add ~$49M per school.

---

## Coverage

138 schools · 2026 conference alignment · 1,617 donor classifications
