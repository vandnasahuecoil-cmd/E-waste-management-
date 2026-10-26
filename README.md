# E-waste Business Dashboard (India)

A static dashboard for planning a pan-India e-waste collection and aggregation business. No build step and no backend: Vercel serves the `public` folder as it is.

## Tabs

| Tab | What it shows |
| --- | --- |
| E-waste basics | Sources, duty holders, categories, rules and amendments, the collection chain with papers needed, capex, end uses, residue |
| Recyclers by region | 614 recycler and refurbisher units with filters for region, state, type, capacity and contact |
| Analytics | Capacity by state, region and district, unit sizes, top companies, comparison with CPCB's state count, hub-routing insights |
| Roadmap and finance | Network design, MRF layout, instrumentation, logistics, phased roadmap, editable finance model |
| Prices | Price chart from the team sheet and ECOIL benchmarks |

## Folder layout

```
public/
  index.html    page shell
  app.js        all dashboard logic
  data.js       recycler directory, price tables, zero-recycler state list
  favicon.svg
vercel.json     output folder, noindex and security headers
package.json    local preview script only
```

## Deploy on Vercel

1. Create a new GitHub repository and push this folder to it.
2. In Vercel choose **Add New > Project** and import the repository.
3. Set **Framework Preset** to **Other**, leave the build command empty and keep the output directory as `public` (`vercel.json` already sets it).
4. Click **Deploy**.

CLI alternative: run `npm i -g vercel`, then `vercel` in this folder, then `vercel --prod`.

The site sends `noindex` headers so it stays out of search results. Delete the `X-Robots-Tag` block in `vercel.json` if you want it indexed. It has no login: use Vercel Authentication or a password in front of it if the directory should stay private.

## Run locally

```
npm run dev
```

or `python3 -m http.server -d public 8000` and open http://localhost:8000.

## Updating the data

Edit `public/data.js` and redeploy.

- `DATA.rows`: one array per unit: `[id, name, state, district, capacityMTperYear, kind, address, phone, email, source]`. `kind` is `Recycler`, `Refurbisher`, `Recycler (NCR list only)` or `Recycler (TN directory only)`. Only `Recycler` rows feed the Analytics tab.
- `DATA.cp`: CPCB's state-wise count of registered recyclers (2 Jul 2025, from its NGT affidavit).
- `PR`: price tables from the team sheet.
- `ZERO`: states and UTs with no registered recycler in CPCB's table.

## Data sources

- CPCB EPR portal exports: recycler and refurbisher registration lists
- Delhi-NCR dismantler and recycler list (with contacts)
- TNPCB Recycling Directory, status 31 Aug 2025
- CPCB affidavit before the NGT, 2 Jul 2025
- Karnataka hazardous waste recycler list (residue processors)
- Team pricing and capex sheet; ECOIL desk benchmarks (Oct 2026)

## Caveats

- Capacities are permitted capacity under consent (MT per year), not volumes processed.
- The lists are undated or dated at publication. Confirm each recycler's current CPCB registration and SPCB consent before a sale.
- Prices are listings, not offers. Capex, finance inputs and instrumentation costs are planning estimates.
- Not legal advice.
