# House Disclosure Analysis Template

A reusable workflow for analyzing real estate disclosure packages using Claude Code.

## Quick Start

1. **Create a new repo from this template** (click "Use this template" on GitHub)
2. **Name it after the property** (e.g., `123-main-street`)
3. **Drop disclosure PDFs** into `disclosures/initial/`
4. **Run the prompts** in order (see workflow below)
5. **Commit after each step** to track your analysis history

## Workflow

Run prompts from `prompts/` in order:

| Step | Prompt | Purpose |
|------|--------|---------|
| 1 | `01_MASTER_ANALYSIS.md` | Analyze all disclosure PDFs |
| 2 | `02_VERIFICATION.md` | Verify accuracy against source docs |
| 3 | `03_AREA_RESEARCH.md` | Research crime, schools, market comps |
| 4 | `04_COST_RESEARCH.md` | Research costs for repair items |
| 5 | `05_INVESTMENT_ANALYSIS.md` | Generate buy/no-buy recommendation |
| 6 | `06_AGENT_EMAIL.md` | Draft email to agent about concerns |
| 7 | `07_OFFER_ANALYSIS.md` | Review offer docs before signing |

**Note:** Steps 3-4 can run in parallel. Step 7 runs after you receive draft offer documents.

## Folder Structure

```
disclosures/
├── initial/           # Drop your disclosure PDFs here
└── updates/           # Put updated docs in dated folders
    └── YYYY-MM-DD/    # e.g., 2025-01-15/

analysis/              # Generated analysis files go here
├── reports/
├── inspections/
├── disclosures/
├── research/
├── offer/
├── cost-estimates/
└── status/

offer/                 # Your offer documents (when ready)
contractor/            # Docs for getting contractor quotes
emails/                # Draft emails
prompts/               # The analysis prompts
```

## When You Get Updated Disclosures

1. Create a dated folder in `disclosures/updates/` (e.g., `2025-01-20/`)
2. Drop the new PDFs there
3. Re-run relevant prompts to update your analysis
4. Commit to track the change

## Usage Tips

- Replace `[FOLDER_PATH]` in prompts with your repo's path
- Replace `[ADDRESS]` with the property address
- Commit after each prompt step to track analysis evolution
- Check `disclosures/updates/` before finalizing any analysis

See `prompts/00_README.md` for detailed documentation.
