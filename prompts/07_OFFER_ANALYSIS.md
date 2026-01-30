# Offer Analysis Prompt

**Usage:** Run this AFTER completing disclosure analysis (prompts 01-05) when your agent sends you offer documents to sign. This prompt analyzes the offer BEFORE you sign.

**When to use:** Once you've shown interest and your agent prepares an offer package for your signature.

---

```
I'm preparing to submit an offer on [ADDRESS] and need to analyze my offer documents before signing.

The offer documents are in: [FOLDER_PATH]/offer/
The disclosure analysis is in: [FOLDER_PATH]/analysis/

## IMPORTANT CONSTRAINTS

- Offer documents vary by transaction - first discover what's in the folder
- Review ALL offer documents thoroughly before the buyer signs
- Cross-reference with disclosure analysis to identify mismatches
- This analysis should happen BEFORE signing, not after

## STEP 0: DISCOVER OFFER DOCUMENTS

First, scan the offer folder to identify all documents present.

Deploy an agent to:
1. List all PDFs in [FOLDER_PATH]/offer/
2. Read any coversheet, summary, or table of contents document first
3. Categorize documents found into:
   - **Core Contract:** Purchase Agreement (RPA, PRDS, or similar)
   - **Contingency Forms:** Any contingency removal, waiver, or advisory forms
   - **Local Addendums:** City-specific forms (Oakland PAA, SF addendums, etc.)
   - **Broker/Agent Disclosures:** Agency, compensation, acknowledgment forms
   - **Other:** Any additional forms specific to this transaction

4. Create a document inventory:

| Document Name | Pages | Category | Requires Signature? |
|---------------|-------|----------|---------------------|
| [filename] | X | [category] | Yes/No |

5. Note any documents that seem unusual or transaction-specific
6. **Flag large documents (30+ pages)** for preprocessing

Write inventory to: `[FOLDER_PATH]/analysis/offer/00_document_inventory.md`

## STEP 0.5: PREPROCESS LARGE DOCUMENTS

Based on Step 0 inventory, identify documents over 30 pages. Common large offer docs include:
- **Preliminary Title Report** (PRELIM, titleLOOK, etc.) - often 50-100+ pages
- **HOA Documents** (CC&Rs, bylaws, financials) - often 100+ pages
- **Escrow Instructions** - can be lengthy
- **Any linked/combined PDFs** - multiple docs merged into one

For each large document, deploy a preprocessing agent to:

1. **Read and extract key content:**
   - For Title Reports: Extract property details, vesting, liens, easements, exceptions, requirements
   - For HOA Docs: Extract fees, special assessments, rules, financial health, litigation
   - For other large docs: Extract sections relevant to buyer decision-making

2. **Write summary to text file:**
   ```
   [FOLDER_PATH]/analysis/offer/preprocessed/
   ├── PRELIM_TITLE_SUMMARY.txt
   ├── HOA_DOCS_SUMMARY.txt
   └── [OTHER]_SUMMARY.txt
   ```

3. **Flag critical issues found:**
   - Title defects or clouds
   - Liens or judgments
   - Unusual easements
   - HOA litigation or financial problems
   - Anything that could affect closing

**If OCR quality is poor (garbled text), note that in the analysis and recommend manual review.**

### Preliminary Title Report - What to Extract

Title reports are critical. Extract and summarize:

| Section | What to Look For |
|---------|------------------|
| **Property Info** | Legal description, APN, address verification |
| **Vesting** | Current owner(s), how title is held, trust info |
| **Liens** | Mortgages, tax liens, mechanic's liens, judgments |
| **Easements** | Utility easements, access easements, unusual restrictions |
| **CC&Rs** | If HOA, reference to recorded CC&Rs |
| **Exceptions** | Standard vs. non-standard exceptions |
| **Requirements** | What must happen before title insurance is issued |
| **Red Flags** | Boundary disputes, encroachments, clouds on title |

**Critical Title Issues to Flag:**
- Liens that won't be paid off at close
- Easements that restrict property use
- Boundary disputes or encroachments
- Missing signatures or breaks in chain of title
- Judgments against seller
- IRS or state tax liens
- Pending litigation involving property

## STEP 1: READ THE OFFER DOCUMENTS

Based on the document inventory from Step 0, deploy sub-agents in parallel to analyze each category.

**Adjust agents based on what documents exist.** Not all transactions have the same forms.

### Agent 1 - Purchase Agreement Analysis

Read the main purchase contract (could be CAR RPA, PRDS, or other) and extract:

**Deal Terms:**
- Offer price
- Initial deposit amount and timeline
- Increased deposit amount and timeline (if any)
- Loan amount and down payment percentage
- Close of escrow date
- Occupancy terms

**Contingencies Section:**
- Inspection contingency: days allowed, waived?
- Appraisal contingency: waived?
- Loan contingency: days allowed, waived?
- Property insurance contingency: days allowed

**Allocation of Costs:**
- Who pays for what inspections
- Title insurance allocation
- Transfer taxes
- HOA document fees (if applicable)

**Other Key Terms:**
- Included/excluded items
- Seller credits
- As-is provisions
- Mediation/arbitration clauses

Write to: `[FOLDER_PATH]/analysis/offer/01_purchase_agreement_analysis.md`

### Agent 2 - Contingency Removal & Waiver Analysis

Read ALL contingency-related forms found in Step 0. Common forms include (but vary by transaction):
- Contingency Removal forms (CR, CR-B, etc.)
- Investigation/Inspection Waivers (BIW, etc.)
- Non-Contingent Offer Advisories (NCOA, etc.)
- Appraisal Contingency Waivers
- Loan Contingency Waivers
- Any form with "waiver", "removal", or "contingency" in the name

For each contingency being removed or waived, document:
1. What contingency is being removed
2. What protection this gives up
3. What risks the buyer is accepting
4. Financial exposure if issues arise

Create a risk summary:
| Contingency | Status | Risk Level | Max Exposure | Mitigation |
|-------------|--------|------------|--------------|------------|

Write to: `[FOLDER_PATH]/analysis/offer/02_contingency_risk_analysis.md`

### Agent 3 - Local Requirements Analysis

Read ALL local/city-specific addendums found in Step 0. Examples vary by city:
- Oakland: PAA (Purchase Agreement Addendum)
- San Francisco: TIC disclosures, rent control, etc.
- Berkeley: Rent stabilization, seismic retrofit
- Other cities: Various local transfer requirements

Extract ANY local requirements found, such as:
- **Sewer Lateral Compliance:**
  - What's required (test, certification, repair)
  - Timeline for compliance
  - Who pays (buyer vs seller)
  - Estimated costs (cross-reference with disclosure analysis)

- **Sidewalk/Curb Requirements:**
  - What's required
  - Timeline
  - Who pays
  - Estimated costs

- **Energy/Water Conservation:**
  - What certifications needed
  - Timeline
  - Who handles

- **Safety Retrofits:**
  - Smoke/CO detectors
  - Seismic requirements
  - Other safety compliance

- **Transfer Taxes:**
  - City transfer tax rate
  - County transfer tax rate
  - Who pays (buyer/seller split)

- **Any Other Local Requirements:**
  - Document anything unique to this jurisdiction

Write to: `[FOLDER_PATH]/analysis/offer/03_local_requirements_analysis.md`

### Agent 4 - Broker Disclosures & Signatures

Read broker-related documents:
- Agency Disclosure
- Broker Compensation Advisory
- Representative Capacity Signature Disclosure
- Additional Agent Acknowledgements

Verify:
- Who represents whom (buyer agent, seller agent, dual agency?)
- Compensation structure
- Any conflicts of interest
- Required signatures and dates

Write to: `[FOLDER_PATH]/analysis/offer/04_broker_disclosures_analysis.md`

## STEP 2: CROSS-REFERENCE WITH DISCLOSURE ANALYSIS

Deploy an agent to read BOTH:
- The offer analysis files just created
- The existing disclosure analysis files

Identify mismatches:

### Condition vs Offer Aggressiveness
- Does property condition justify waiving contingencies?
- Are there significant repair costs that conflict with as-is terms?
- Do environmental risks (fire zone, flood zone) warrant keeping contingencies?

### Cost Alignment
- Do local requirement costs in offer match disclosure estimates?
- Are there surprise costs not budgeted for?
- Is total out-of-pocket consistent with expectations?

### Timeline Feasibility
- Can loan close in time given property issues?
- Are inspection/appraisal windows realistic?
- Are local compliance deadlines achievable?

Write to: `[FOLDER_PATH]/analysis/offer/05_offer_vs_disclosure_crosscheck.md`

## STEP 3: INSURANCE RESEARCH (FOR HIGH-RISK AREAS)

For properties in Oakland Hills or other high-fire-risk areas, deploy an agent to research:

### Fire Insurance
- Is property in State Fire Responsibility Area or Local Fire Area?
- Is property in a FAIR Plan-only zone?
- What insurers write policies in this area?
- Estimated annual premium range
- Deductibles (especially % deductibles for fire)
- Any coverage restrictions

### Research Sources
- California FAIR Plan requirements
- California Department of Insurance resources
- Local insurance broker information

### Key Questions to Answer
- Can you get standard homeowners insurance?
- Will you need FAIR Plan + DIC (Difference in Conditions)?
- What's the realistic annual insurance cost?
- Are there coverage gaps to be aware of?

Write to: `[FOLDER_PATH]/analysis/offer/06_insurance_research.md`

## STEP 4: CREATE FINAL OFFER REVIEW REPORT

Compile all findings into a comprehensive review.

Write to: `[FOLDER_PATH]/analysis/reports/OFFER_REVIEW_REPORT.md`

### 1. OFFER SUMMARY
| Term | Value |
|------|-------|
| Offer Price | $ |
| Initial Deposit | $ |
| Increased Deposit | $ |
| Loan Amount | $ |
| Down Payment | $ (X%) |
| Close of Escrow | [date] |

### 2. CONTINGENCY STATUS

| Contingency | Days | Waived? | Risk Assessment |
|-------------|------|---------|-----------------|
| Inspection | | | |
| Appraisal | | | |
| Loan | | | |
| Insurance | | | |

### 3. WAIVER RISK ANALYSIS

For each waived contingency, explain:
- **What you're giving up:** [specific protection]
- **Worst case scenario:** [what could happen]
- **Financial exposure:** $X - $Y
- **Likelihood:** Low/Medium/High
- **Mitigation available:** [what can still protect you]

### 4. LOCAL COMPLIANCE COSTS

| Requirement | Paid By | Estimated Cost | Source |
|-------------|---------|----------------|--------|
| Sewer Lateral | | $ | |
| Sidewalk | | $ | |
| Water Fixtures | | $ | |
| Smoke/CO | | $ | |
| **TOTAL** | | $ | |

### 5. APPRAISAL GAP RISK

If appraisal contingency is waived:
- Offer price: $X
- Comparable sales support price of: $X - $Y
- Potential gap if appraisal comes low: $X
- Do you have cash to cover the gap?

### 6. LOAN CONTINGENCY RISK

If loan contingency is waived or shortened:
- What happens if loan doesn't fund?
- Deposit at risk: $X
- Are there property issues that could affect financing?
- Is timeline achievable?

### 7. INSURANCE SITUATION

- Zone: [fire zone status]
- Insurance availability: [standard/FAIR Plan only]
- Estimated annual premium: $X - $Y
- Key coverage concerns: [list]

### 8. OFFER VS PROPERTY CONDITION

**Mismatches Found:**
- [List any inconsistencies between property condition and offer terms]

**Assessment:**
- Is this offer appropriately aggressive for this property's condition?
- Are you accepting reasonable risk or excessive risk?

### 9. BUYER PROTECTION RECOMMENDATIONS

Based on the analysis:
1. [Specific recommendation - e.g., "Consider keeping appraisal contingency given fire zone pricing uncertainty"]
2. [Specific recommendation - e.g., "Get pre-approval letter updated to reflect this specific property"]
3. [Specific recommendation - e.g., "Verify insurance quote before removing contingency"]
4. [Additional recommendations as needed]

### 10. PRE-SIGNING CHECKLIST

Before signing, confirm:

**Financial Readiness:**
- [ ] Down payment funds verified and accessible
- [ ] Deposit funds ready to wire
- [ ] Appraisal gap funds available (if waiving appraisal)
- [ ] Closing costs budgeted
- [ ] Post-close repair costs budgeted

**Loan Readiness:**
- [ ] Pre-approval updated for this property
- [ ] Lender aware of property condition issues
- [ ] Lender confirmed timeline is achievable
- [ ] Rate lock strategy discussed

**Insurance Readiness:**
- [ ] Insurance quotes obtained
- [ ] Coverage confirmed available
- [ ] Premium fits budget
- [ ] Understand any coverage limitations

**Local Requirements:**
- [ ] Sewer lateral status understood
- [ ] Sidewalk status understood
- [ ] Know who pays for what
- [ ] Compliance timeline is feasible

**Contingency Decisions:**
- [ ] Understand each waiver risk
- [ ] Have funds to cover worst case
- [ ] Accept the risk consciously (not by accident)

**Documents:**
- [ ] All signature pages identified
- [ ] Understand what you're signing
- [ ] Agent explained all terms
- [ ] Questions answered before signing

## CRITICAL WARNINGS

Flag any of these as HIGH PRIORITY concerns:
- Waiving appraisal contingency without cash reserves for gap
- Waiving loan contingency without lender confirmation
- Waiving inspection contingency on property with known issues
- Short timelines that may be impossible to meet
- Insurance availability concerns not addressed
- Local compliance costs significantly higher than expected
- Mismatch between property condition and offer aggressiveness
```

---

## Output Structure

Create these files in `[FOLDER_PATH]/analysis/offer/`:

```
analysis/offer/
├── 00_document_inventory.md        # List of all offer docs found
├── preprocessed/                   # For large docs (30+ pages)
│   ├── PRELIM_TITLE_SUMMARY.txt
│   ├── HOA_DOCS_SUMMARY.txt
│   └── [OTHER]_SUMMARY.txt
├── 01_purchase_agreement_analysis.md
├── 02_contingency_risk_analysis.md
├── 03_local_requirements_analysis.md
├── 04_broker_disclosures_analysis.md
├── 05_offer_vs_disclosure_crosscheck.md
└── 06_insurance_research.md        # Only if high-fire-risk area
```

And add to `[FOLDER_PATH]/analysis/reports/`:
```
analysis/reports/
└── OFFER_REVIEW_REPORT.md
```

## When to Use This Prompt

- After disclosure analysis is complete (prompts 01-05)
- BEFORE signing offer documents
- When you have the draft offer package from your agent
- Before submitting to listing agent

## Key Principles

1. **Discover first** - Scan the offer folder before assuming what's there
2. **Review BEFORE signing** - Not after
3. **Cross-reference everything** - Offer terms should align with property condition
4. **Quantify risks** - Put dollar amounts on worst-case scenarios
5. **Check insurance early** - Especially for fire zones
6. **Verify local requirements** - They add up quickly
7. **Conscious risk acceptance** - Understand what you're waiving

## Notes on Offer Document Variability

Offer packages differ based on:
- **State:** California uses CAR or PRDS forms; other states differ
- **City:** Local addendums vary (Oakland PAA, SF disclosures, etc.)
- **Transaction type:** Trust sales, REO, short sales have extra forms
- **Agent/Brokerage:** Some add proprietary disclosures
- **Offer strategy:** Non-contingent offers include additional waivers

Always start with Step 0 to inventory what's actually in the folder before analyzing.

## Handling Large Documents

Some offer documents can be 50-200+ pages:
- **Preliminary Title Reports** - Often linked/combined with underlying documents
- **HOA Packages** - CC&Rs, bylaws, budgets, meeting minutes, litigation disclosures
- **Condo/Co-op Docs** - Financial statements, reserve studies, insurance certificates
- **Commercial Offers** - Environmental reports, surveys, lease abstracts

**For these large docs:**
1. Preprocess in Step 0.5 before main analysis
2. Extract key summaries to `.txt` files
3. Reference summaries in later analysis steps
4. Flag critical issues for buyer attention
5. Note if OCR quality prevents full extraction

This prevents context window overflow and ensures thorough review.
