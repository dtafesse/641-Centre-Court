# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a real estate disclosure analysis workflow for evaluating a property purchase. It uses Claude Code sub-agents to process disclosure PDFs in parallel, research costs and neighborhood data, and generate buyer reports.

## Workflow

Run prompts in order from `prompts/`:

| Step | Prompt | Purpose |
|------|--------|---------|
| 1 | `01_MASTER_ANALYSIS.md` | Analyze all disclosure PDFs using parallel sub-agents |
| 2 | `02_VERIFICATION.md` | Verify analysis accuracy against source documents |
| 3 | `03_AREA_RESEARCH.md` | Research crime, schools, and market comps |
| 4 | `04_COST_RESEARCH.md` | Research costs for "by others" items |
| 5 | `05_INVESTMENT_ANALYSIS.md` | Generate final buy/no-buy recommendation |
| 6 | `06_AGENT_EMAIL.md` | Draft email to agent about concerns |
| 7 | `07_OFFER_ANALYSIS.md` | Review offer documents before signing |

**Note:** Steps 3-4 can run in parallel. Step 7 runs after you receive draft offer documents from your agent, BEFORE signing.

## Key Architecture Decisions

### Parallel Sub-Agents
Large disclosure packages cannot fit in a single context window. The workflow deploys multiple sub-agents simultaneously, each processing a different document category (inspections, seller disclosures, environmental, advisories, etc.).

### Preprocessing Large Files
PDFs over 30+ pages (home inspection, NHD reports) should be preprocessed by a sub-agent that extracts content to `.txt` files before analysis.

### Cost Documentation Rules
- **DOCUMENTED costs**: From actual disclosure documents with specific dollar amounts. Label as `**[DOCUMENTED]**` with source.
- **RESEARCH ESTIMATE costs**: From web research, not documents. Label as `**[RESEARCH ESTIMATE]**`. Require contractor quotes.
- Never make up costs or present estimates as documented costs.
- Negotiation strategy should only use documented costs.

## Directory Structure

Files created depend on the property's disclosure package. Not all files will exist for every property.

```
disclosures/
├── initial/           # Initial disclosure package PDFs
└── updates/           # Updated disclosures (organized by date received)
    └── YYYY-MM-DD/    # e.g., 2025-01-15/

analysis/
├── reports/           # Summary reports (always created)
│   ├── FINAL_BUYER_REPORT.md      # from prompt 01
│   ├── INVESTMENT_ANALYSIS.md     # from prompt 05
│   └── OFFER_REVIEW_REPORT.md     # from prompt 07
├── inspections/       # Inspection analyses (from prompt 01)
├── disclosures/       # Seller disclosure analyses (from prompt 01)
├── research/          # Area research (from prompts 01, 03)
│   ├── AREA_CRIME_RESEARCH.md
│   ├── AREA_SCHOOL_RESEARCH.md
│   └── MARKET_COMPS_RESEARCH.md
├── offer/             # Offer document analyses (from prompt 07)
│   └── preprocessed/  # Summaries from large docs (50+ pages)
├── cost-estimates/    # COST_ESTIMATE_[ITEM].md (from prompt 04)
└── status/            # Verification and tracking files

contractor/            # Documents and messages for contractor quotes
emails/                # Draft emails to agent
offer/                 # Source offer documents (PDFs)
prompts/               # Reusable analysis prompts (numbered 00-07)
```

See `prompts/00_README.md` for detailed file listing by prompt.

## Critical Constraints

- Always read the coversheet PDF first to get the document list and page counts
- Verify all findings against source documents after initial analysis
- Distinguish between signed and unsigned documents (affects who pays)
- Label all costs with their source type (documented vs research estimate)
- Area research and cost research can run in parallel
- Investment analysis should run last (requires all other data)
