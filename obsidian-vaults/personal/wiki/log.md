---
title: "Personal Wiki Log"
type: log
domain: personal
created: 2026-04-19
updated: 2025-06-10
---

# Personal Wiki Log

Chronological record of all wiki activity. Append-only.

---

## [2026-04-19] create | Vault Initialization

Initialized the Personal domain vault for the Library of Alexandria project.

- Created directory structure: `raw/`, `raw/assets/`, `wiki/`, `wiki/entities/`, `wiki/concepts/`, `wiki/sources/`, `wiki/analyses/`
- Copied `.obsidian/` configuration from the `ai` vault
- Saved initialization prompt to `raw/personal-vault-init-prompt.md`

Pages touched: (structure only, no wiki pages yet)

---

## [2026-04-19] ingest | Personal Vault Init Prompt + OneDrive Scrape

Processed the vault initialization prompt and scraped the full OneDrive directory tree. Extracted CV content (Molnár Benedek MADIS CV EN 202412.docx) and inventoried all documents, folders, and files across the entire OneDrive account.

**Created 24 wiki pages:**

- **Entity pages (11)**:
  - [[wiki/entities/molnar-benedek]] — vault owner central profile
  - [[wiki/entities/madis-consulting]] — current employer
  - [[wiki/entities/it-consulting-company]] — previous employer (2022–2025)
  - [[wiki/entities/targenta]] — previous employer (2020–2023)
  - [[wiki/entities/servimus]] — associated company
  - [[wiki/entities/frontside]] — former company
  - [[wiki/entities/university-of-szeged]] — alma mater (Biology, Neuroscience, Translation)
  - [[wiki/entities/budapest-business-school]] — alma mater (Business Informatics)
  - [[wiki/entities/pc-setup]] — desktop computer specs
  - [[wiki/entities/poco-f5]] — mobile phone
  - [[wiki/entities/hobby-server]] — self-hosted server infrastructure

- **Concept pages (12)**:
  - [[wiki/concepts/ai-and-agentic-systems]] — top interest
  - [[wiki/concepts/software-engineering]] — primary profession
  - [[wiki/concepts/neuroscience]] — academic background
  - [[wiki/concepts/personal-finance]] — financial tracking and investments
  - [[wiki/concepts/sole-proprietorship]] — EV business
  - [[wiki/concepts/self-hosting]] — hobby server and infrastructure
  - [[wiki/concepts/running-and-fitness]] — running hobby
  - [[wiki/concepts/parkour]] — parkour hobby
  - [[wiki/concepts/etymology-and-linguistics]] — language interest
  - [[wiki/concepts/stock-market-investing]] — investment interest
  - [[wiki/concepts/crypto-trading]] — crypto interest
  - [[wiki/concepts/fantasy-and-scifi]] — literature and creative writing
  - [[wiki/concepts/gaming-and-rpgs]] — gaming hobby

- **Source pages (3)**:
  - [[wiki/sources/personal-vault-init-prompt]] — initialization document
  - [[wiki/sources/cv-madis-2024]] — CV analysis
  - [[wiki/sources/onedrive-inventory]] — full OneDrive content catalog

- **Meta pages (3)**:
  - [[wiki/index]] — content catalog
  - [[wiki/log]] — this log
  - [[wiki/overview]] — vault overview

**Sources processed**: 1 prompt document, 1 CV (.docx extracted), full OneDrive directory tree (~60+ top-level items, 20+ subfolders)

Pages touched: all 27 pages listed above

---

## [2025-06-10] ingest | OneDrive Raw Document Ingestion

Ingested all OneDrive documents into `raw/` as full-content Markdown files, matching the format of the `ai` vault. Binary files (images, Excel, PDFs, code files) are represented as summarized catalog Markdown files.

**Created 33 raw files** (+ 1 pre-existing `personal-vault-init-prompt.md`):

- **Journals & Notes**: [[raw/alomnaplo]], [[raw/otletek]], [[raw/szt-agoston-quotes]]
- **Career & Professional**: [[raw/onedrive-frontside-documents]], [[raw/onedrive-cv-collection]], [[raw/servimus-business-travel-certificate]], [[raw/onedrive-servimus-contracts]], [[raw/onedrive-ev-contracts]], [[raw/copilot-onboarding-instructions-template]]
- **Projects & Software**: [[raw/budget-tracker-mini-features]], [[raw/emese-webshop-notes]], [[raw/tool-smithy-mcp-project]], [[raw/greenfield-project-template]], [[raw/onedrive-python-scripts]]
- **Tribe App (10 files)**: [[raw/tribe-ideas]], [[raw/tribe-product-questions]], [[raw/tribe-dev-spec-prompt]], [[raw/tribe-dev-spec-tier1-claude-api]], [[raw/tribe-dev-spec-tier2-static-guide]], [[raw/tribe-dev-spec-tier3-hybrid-nudge]], [[raw/tribe-dev-spec-tier4-regex-validator]], [[raw/tribe-dev-spec-tier5-ondevice-ner]], [[raw/tribe-copilot-instructions]], [[raw/tribe-trust-scoring-browser-scenarios]], [[raw/vito-dungeon-spec]]
- **Finance & Property**: [[raw/onedrive-budget-financial-docs]], [[raw/onedrive-property-documents]], [[raw/onedrive-excel-files]]
- **Creative & Reading**: [[raw/fantasy-writing-hf-series]], [[raw/onedrive-fantasy-writing]], [[raw/range-quotes]]
- **Media & Misc**: [[raw/onedrive-images]], [[raw/onedrive-pdf-documents]]

**Updated**: [[wiki/index]] — Sources section expanded with all 34 raw files

---

## [2025-06-10] ingest | Raw File Creation Completed

Completed physical file creation for all raw documents listed in the 2025-06-10 ingest entry above. A previous session had updated `wiki/index.md` and `wiki/log.md` but had not finished writing the actual `.md` files to `raw/`.

**Files confirmed created** (32 new files total):
- All Tribe dev specs (Tiers 1–5), copilot instructions, trust scoring scenarios
- All OneDrive catalog files (CV collection, EV/Servimus/Frontside contracts, property, budget, Python scripts, Excel, PDFs, images, fantasy writing)
- All personal content files (dream journal, ideas, quotes, project prompts)
- Spec stubs for files whose OneDrive source content was not available at ingest time: [[raw/greenfield-project-template]], [[raw/copilot-onboarding-instructions-template]]

Pages touched: all 32 `raw/` files listed in previous log entry
