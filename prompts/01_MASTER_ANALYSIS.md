# Master Property Disclosure Analysis Prompt

**Usage:** Copy this prompt and replace `[ADDRESS]` and `[FOLDER_PATH]` with your values.

---

```
I have a property disclosure package for [ADDRESS] that I need analyzed. The disclosure PDFs are in [FOLDER_PATH]/disclosures/initial/.

This is a major purchase decision, so I need a thorough analysis.

## IMPORTANT CONSTRAINTS

- There are many PDFs in this folder - you CANNOT fit all in context at once
- You MUST use sub-agents to process documents in parallel batches
- Each sub-agent should focus on a specific category of documents

## STEP 1: READ THE COVERSHEET FIRST

Deploy a sub-agent to read the Coversheet PDF (usually document 0 or first in the folder).

The coversheet typically contains:
- Table of contents listing ALL documents
- Page counts for each document
- Document categories/groupings
- Offer instructions
- Important notes from listing agent

Have the agent extract:
1. Full document list with page counts
2. How documents are categorized
3. Which documents are largest (for preprocessing)
4. Any offer instructions or deadlines
5. Key notes from listing agent

## STEP 2: PREPROCESSING LARGE FILES

Based on the coversheet page counts, identify documents over 30+ pages:
- Home Inspection Reports (often 40+ pages)
- Environmental Booklets (often 100+ pages)
- NHD Reports (often 30+ pages)

For these large documents, deploy a preprocessing agent to:
- Read the PDF and extract key content
- Write a summary `.txt` file to the analysis folder
- This makes content searchable and avoids context limits

If OCR quality is poor (garbled text), note that in the analysis.

Create the analysis output folder:
```
mkdir -p [FOLDER_PATH]/analysis
```

## STEP 3: DEPLOY ANALYSIS SUB-AGENTS

Based on the coversheet categories, deploy sub-agents in parallel. Typical groupings:

**Agent 1 - Inspections:**
- Home Inspection Report
- Pest/Termite Reports
- Work Authorizations (WA)
- Sewer/Sidewalk Inspections

**Agent 2 - Seller Disclosures:**
- Transfer Disclosure Statement (TDS)
- Seller Property Questionnaire (SPQ)
- Agent Visual Inspection Disclosure (AVID)
- Seller supplements
- Improvements list

**Agent 3 - Environmental/Hazards:**
- Natural Hazard Disclosure (NHD)
- Environmental Screening Report
- Property Tax Report
- Lead Paint Disclosure
- Earthquake Safety

**Agent 4 - Advisories & Compliance:**
- Fire/Defensible Space
- All advisory documents
- Compliance statements
- Local addendums (Oakland PAA, etc.)
- Insurance advisories

**Agent 5 - Property Info & Offer Terms:**
- MLS sheet
- Floor plans
- Coversheet offer instructions
- Forms required with offer

Each agent should:
- Read the relevant PDFs for their category
- Extract key findings, issues, and costs
- Write a markdown analysis file to the analysis folder
- Include a "KEY FINDINGS SUMMARY" section at the end

## STEP 4: CREATE SUMMARY REPORTS

After all sub-agents complete, create:

1. `FINAL_BUYER_REPORT.md` with:
   - Executive summary with top 5 concerns ranked by severity
   - Critical findings (dealbreakers)
   - Moderate concerns
   - Positive findings
   - Documented costs table
   - Questions to ask seller/agent
   - Due diligence checklist

2. `VERIFICATION_CHECKLIST.md` with:
   - Table mapping each finding to source document
   - Allows buyer to verify findings against originals

## CRITICAL COST RULES

- **ONLY report costs that appear in the actual documents**
- Label all costs as **[DOCUMENTED]** with the source document name
- **DO NOT estimate costs** - if a cost isn't in the documents, say "cost not provided"
- **DO NOT make up dollar amounts** for repairs, credits, or negotiations
- Note if documents are SIGNED or UNSIGNED - this affects who pays

## OUTPUT FILES

Create files based on what documents exist in the disclosure package. Not all properties will have the same documents.

**Inspections** (`analysis/inspections/`):
- If home inspection exists: `01_home_inspection_analysis.md`
- If pest/termite report exists: `01b_pest_termite_analysis.md`
- If sewer/chimney/roof inspections exist: `01c_[type]_inspection_analysis.md`
- If urgent safety issues found: `URGENT_ITEMS_[TYPE].md`

**Disclosures** (`analysis/disclosures/`):
- If seller disclosures exist (TDS, SPQ, AVID): `02_seller_disclosures_analysis.md`
- If permits/certificates exist: `03_permits_certificates_analysis.md`
- If advisory/compliance docs exist: `05_advisory_compliance_analysis.md`
- For other disclosure types: `[NN]_[type]_analysis.md`

**Research** (`analysis/research/`):
- If environmental/NHD docs exist: `04_environmental_hazards_analysis.md`

**Reports** (`analysis/reports/`) - Always create:
- `FINAL_BUYER_REPORT.md`
- `REPAIR_PRIORITIES.md` (if repair issues found)

**Status** (`analysis/status/`) - Always create:
- `VERIFICATION_CHECKLIST.md`

**Naming convention:** Use numbered prefixes (01, 02, etc.) to group related analyses. Add property-specific files as needed based on the actual disclosure package.

Start by reading the coversheet, then proceed with preprocessing and sub-agent deployment.
```
