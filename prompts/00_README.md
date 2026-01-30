# Property Disclosure Analysis Prompts

Reusable prompts for analyzing real estate disclosure packages with Claude Code.

## Workflow Order

Run these prompts in order:

| Step | Prompt | Purpose |
|------|--------|---------|
| 1 | `01_MASTER_ANALYSIS.md` | Analyze all disclosure PDFs |
| 2 | `02_VERIFICATION.md` | Verify accuracy of analysis |
| 3 | `03_AREA_RESEARCH.md` | Research crime, schools, market |
| 4 | `04_COST_RESEARCH.md` | Research costs for "by others" items |
| 5 | `05_INVESTMENT_ANALYSIS.md` | Final buy/no-buy recommendation |
| 6 | `06_AGENT_EMAIL.md` | Draft email to agent about concerns |
| 7 | `07_OFFER_ANALYSIS.md` | Review offer documents before signing |

## Key Principles

### 1. File Names Vary
Disclosure packages name files differently. The prompts identify documents by content type, not filename. Always list files first and categorize them.

### 2. Preprocessing Large Files
PDFs over 5MB (especially inspection reports, historical permits) should be converted to text first to avoid context limits.

### 3. Parallel Sub-Agents
Deploy multiple sub-agents simultaneously to process document categories in parallel. This is faster and avoids context overflow.

### 4. Cost Documentation Rules

**DOCUMENTED costs:**
- Appear in actual disclosure documents
- Have specific dollar amounts
- Label as `**[DOCUMENTED]**` with source

**RESEARCH ESTIMATE costs:**
- Come from web research, not documents
- Are ranges, not exact amounts
- Label as `**[RESEARCH ESTIMATE]**`
- Note they require contractor quotes

**NEVER:**
- Make up costs that aren't in documents
- Present estimates as documented costs
- Base negotiation strategy on estimates

### 5. Verification is Critical
Always run the verification prompt after initial analysis. Sub-agents can make errors or miss items. Verification catches these.

## Customization

Before using each prompt:
1. Replace `[ADDRESS]` with property address
2. Replace `[FOLDER_PATH]` with path to disclosure PDFs
3. Replace other placeholders as noted
4. For cost research, list specific items from YOUR disclosure

## Output Structure

All analysis files are organized into subfolders under `[FOLDER_PATH]/analysis/`. Files created depend on what's in each property's disclosure package.

```
analysis/
├── reports/           # Summary reports and recommendations
│   ├── FINAL_BUYER_REPORT.md      (from 01)
│   ├── REPAIR_PRIORITIES.md       (from 01, if issues found)
│   ├── INVESTMENT_ANALYSIS.md     (from 05)
│   ├── OFFER_REVIEW_REPORT.md     (from 07)
│   └── [COST_SUMMARY.md]          (optional, consolidates costs)
│
├── inspections/       # Home and pest inspection analyses (from 01)
│   ├── 01_home_inspection_analysis.md
│   ├── 01b_pest_termite_analysis.md
│   ├── [URGENT_ITEMS_*.md]        (if urgent issues found)
│   └── [other inspection files based on disclosures]
│
├── disclosures/       # Seller disclosure analyses (from 01)
│   ├── 02_seller_disclosures_analysis.md
│   ├── 03_permits_certificates_analysis.md
│   ├── 05_advisory_compliance_analysis.md
│   └── [other files based on disclosures present]
│
├── research/          # Area and environmental research
│   ├── 04_environmental_hazards_analysis.md  (from 01)
│   ├── AREA_CRIME_RESEARCH.md     (from 03)
│   ├── AREA_SCHOOL_RESEARCH.md    (from 03)
│   ├── MARKET_COMPS_RESEARCH.md   (from 03)
│   └── [INSURANCE_RESEARCH.md]    (if high-risk area)
│
├── offer/             # Offer document analyses (from 07)
│   ├── 00_document_inventory.md
│   ├── 01_purchase_agreement_analysis.md
│   ├── 02_contingency_risk_analysis.md
│   ├── 03_local_requirements_analysis.md
│   ├── 04_broker_disclosures_analysis.md
│   ├── 05_offer_vs_disclosure_crosscheck.md
│   ├── [06_insurance_research.md] (if fire zone)
│   └── preprocessed/              (for large docs 50+ pages)
│
├── cost-estimates/    # Cost research for specific repairs (from 04)
│   └── COST_ESTIMATE_[ITEM].md    (one per item needing research)
│
└── status/            # Work status and verification tracking
    ├── VERIFICATION_CHECKLIST.md  (from 01)
    └── [property-specific status files as needed]
```

**Note:** Files in `[brackets]` are conditional - created only when relevant to that property. Disclosure packages vary significantly, so the actual files will depend on what documents exist for each property.

## Source Documents

Disclosure PDFs are organized by when you received them:

```
disclosures/
├── initial/           # First disclosure package from agent
│   ├── 0. Coversheet.pdf
│   ├── 1. MLS Information...pdf
│   └── ...
│
└── updates/           # Later document versions, by date received
    ├── 2025-01-15/
    │   ├── pest-report-revised.pdf
    │   └── seller-disclosure-amended.pdf
    └── 2025-01-22/
        └── roof-inspection.pdf
```

## Additional Folders

Beyond the analysis folder, the project may include:

```
[FOLDER_PATH]/
├── contractor/        # Documents and messages for contractor quotes
│   ├── [Relevant inspection PDFs]
│   └── message_to_[name].txt
├── emails/            # Draft emails to agent, seller, etc.
│   └── EMAIL_DRAFT_TO_AGENT.md
└── offer/             # Offer documents from your agent
    └── [Offer PDFs]
```

## Tips

- Start with `01_MASTER_ANALYSIS.md` and let it run fully
- Review output before running verification
- Area research and cost research can run in parallel
- Investment analysis should run after disclosure and cost analysis
- Offer analysis should run when you have draft offer documents, BEFORE signing
- Keep source PDFs - you may need to re-verify findings
- Initialize a git repo to track changes to analysis files
- Use the `contractor/` folder to bundle docs when getting quotes
- Check `updates/` for revised disclosures before finalizing analysis
