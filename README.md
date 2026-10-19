# UrbanPulse · Data Lab Walkthrough

Self-contained lab guide for the **UrbanPulse Data Lab** hands-on workshop.

> **Scenario:** UrbanPulse Analytics is a software vendor building a Smart City operations platform on Microsoft Fabric. Across 12 modules organized into five goals — **Ingest, Transform, Build Report, Apply AI, Source Control** — attendees build the reference architecture end-to-end: Lakehouse, Mirroring, Eventhouse, Spark notebook + SQL views, Real-Time Dashboard, Direct Lake + Power BI, Fabric Ontologies, Fabric Data Agents, an Azure AI Foundry connected-agent orchestrator, and Fabric Git integration.

---

![Architecture overview](lab-guide/assets/images/architecture-overview.svg)

## Folder Structure

```
urbanpulse-data-lab/
├── README.md                          ← you are here
├── lab-guide/                         ← attendee-facing HTML lab guide (open index.html)
│   ├── index.html                     ← cover page + use case + goal pills + module cards
│   ├── module-0-setup.html … module-11-git-integration.html
│   ├── closing.html                   ← multi-tenant pattern picture + final recap
│   ├── appendix-data-setup.html       ← provisioning the lab data (SQL, Cosmos, Event Hubs)
│   ├── appendix-learn-links.html      ← Microsoft Learn references
│   └── assets/
│       ├── css/data-lab.css           ← single source of branding
│       ├── js/print.js                ← sidebar nav + Ctrl+P helper
│       ├── downloads/                 ← parquet, SQL script, Cosmos data, facility photos
│       └── images/                    ← SVG diagrams and screenshots
├── seed-data/                         ← synthetic source data: sql, cosmos, eventhub, parquet
├── scripts/start-producers.ps1        ← starts the Event Hubs simulators
├── coach-prep/                        ← coach-only material (NOT shared with attendees)
│   ├── README.md                      ← coach role + schedule
│   ├── pre-flight-checklist.md        ← T-90min checklist
│   └── simulator-runbook.md           ← how to run the 3 simulators
├── diagrams/                          ← editable diagram sources
└── .github/workflows/pages.yml        ← publishes lab-guide/ to GitHub Pages
```

All data is synthetic. Connection strings in the docs are placeholders (`SharedAccessKey=...`);
supply your own when you provision the lab.

## How attendees use it

1. Lab machine opens to `lab-guide/index.html`.
2. Attendees follow modules **0 → 10** sequentially (11 is optional), then `closing.html`. Each module is one HTML page, ~20–75 minutes.
3. The sticky sidebar groups modules under each goal so attendees can jump to a phase. The Goals page also has filter pills (All · Ingest · Transform · Build Report · Apply AI).
4. To take an offline copy: **Ctrl+P → Save as PDF** on any page.

## How to export to PDF

Per page (recommended): open the page in Edge or Chrome → **Ctrl+P** → Destination = **Save as PDF** → Layout = **Portrait** → Margins = **Default** → ✅ Background graphics → Save.

Whole guide as one PDF: open `index.html`, save as PDF, then concatenate each module PDF using any PDF merger (Edge supports drag-merge in print preview as of recent builds, or use `pdftk` / Acrobat). The print stylesheet (in `data-lab.css` under `@media print`) handles page breaks, hides the site header, and expands `<details>` blocks automatically.

## What's included per module

| # | Module | Time | Goal |
| --- | --- | --- | --- |
| 0 | Setup & Environment Check | 10m | Sign in, confirm capacity, bookmark Lab Credentials |
| 1 | Workspace Tour & Solution Architecture | 30m | Tour the pre-provisioned workspace + medallion + multi-tenancy |
| 2 | Data Ingestion | 45m | G1 · Three ingest patterns (Parquet upload, Azure SQL mirror, Cosmos mirror) |
| 3 | Real-Time Streaming Ingest | 75m | G1 · 3 Eventstreams + 3 KQL tables fed from Event Hubs |
| 4 | Transform for Analytics | 40m | G2 · Spark notebook for Silver Delta + SQL views for Gold |
| 5 | Live Dashboard | 60m | G3 · KQL queries + Real-Time Intelligence Dashboard |
| 6 | Direct Lake + Power BI | 30m | G3 · Semantic model and 1-page Power BI report |
| 7 | Fabric Ontologies | 25m | G4 · Semantic graph over Lakehouse + Eventhouse data |
| 8 | Fabric Data Agent | 45m | G4 · Hospital Operations agent grounded on KQL |
| 9 | Multi-Agent Catalog *(Optional)* | 20m | G4 · Add Transit Ops agent for a two-domain catalog |
| 10 | Foundry Orchestrator *(Optional)* | 30m | G4 · Azure AI Foundry connected-agent orchestrator |
| 11 | Git Integration *(Optional)* | 30m | G5 · Put the workspace under Azure DevOps Git source control |
| End | Closing | — | Multi-tenant pattern picture + recap of everything you built |
| A | Data Setup | reference | Provisioning Azure SQL, Cosmos DB and Event Hubs with the seed data |
| B | Learn Links | reference | Microsoft Learn references for each module |

## Branding

The lab guide uses a purple palette layered with Microsoft Fabric teal accents and Segoe UI typography. All branding lives in **one CSS file** (`lab-guide/assets/css/data-lab.css`) so it can be re-skinned in one place for future events.

## Source repo

Inspired by and references content from `nickTinMicrosoft/fabric_hackathon_coaches` and `nickTinMicrosoft/fabric_hackathon_attendee` (Goal 2 — Transform). The Hospital Operations Agent's instructions are adapted from `Recipes/HospitalOpsAgent/04_agent_instructions.md`.

## Acknowledgements

- Microsoft Fabric team - for the platform
- @nickTin and the original hackathon coaches - for the simulator + agent recipe

## Licence

[MIT](LICENSE). Microsoft Fabric and other product names are trademarks of their owners; this is a
community workshop, not an official Microsoft offering.
