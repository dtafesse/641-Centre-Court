# Verification Prompt

**Usage:** Run this AFTER the initial analysis to verify accuracy. Replace placeholders with your values.

---

```
I need to verify the accuracy of the property disclosure analysis for [ADDRESS].

The analysis files are in: [FOLDER_PATH]/analysis/
The source PDFs are in: [FOLDER_PATH]/disclosures/initial/

## YOUR TASK

Deploy sub-agents to verify that the analysis files accurately reflect what's in the source PDFs.

## VERIFICATION STEPS

### Step 1: Verify All Costs

Deploy an agent to:
- Read ONLY the original source PDFs (NOT the analysis files)
- Extract every dollar amount that appears in any document
- List each cost with:
  - Exact amount
  - Exact text/description from document
  - Document name and section
  - Whether it's a firm price or estimate

Then compare against costs reported in the analysis files. Flag any:
- Costs in analysis that don't match source documents
- Costs in source documents that were missed in analysis
- Any costs that appear to be LLM estimates (not from documents)

### Step 2: Verify Work Status

Deploy an agent to:
- Read the original pest reports and work authorizations
- Identify what work is:
  - COMPLETED (with evidence - handwritten notes, completion certificates)
  - PENDING (authorized but not done)
  - UNSIGNED (proposed but not authorized)
  - BY OTHERS (not in pest company scope)

Compare against what the analysis files say. Flag discrepancies.

### Step 3: Verify Key Findings

Deploy an agent to:
- Read the FINAL_BUYER_REPORT.md
- For each "Critical" or "Major" finding listed:
  - Locate the source document
  - Confirm the finding is accurately described
  - Note the exact page/section for verification

### Step 4: Check for Missing Issues

Deploy an agent to:
- Scan source PDFs for any "yes" answers on disclosure forms
- Check for any red flags that might have been missed:
  - Water intrusion mentions
  - Unpermitted work mentions
  - Foundation/structural issues
  - Insurance claims
  - Disputes or litigation

## OUTPUT

Create: `[FOLDER_PATH]/analysis/status/VERIFICATION_REPORT.md`

Include:

## Cost Verification
| Item | Analysis Says | Source Document Says | Match? |
|------|---------------|---------------------|--------|

## Work Status Verification
| Item | Analysis Says | Source Document Says | Match? |
|------|---------------|---------------------|--------|

## Findings Verification
| Finding | Verified? | Source Document | Notes |
|---------|-----------|-----------------|-------|

## Corrections Needed
List any specific corrections to make to the analysis files

## Missing Items
List anything found in source docs but missing from analysis

After creating the verification report, update any analysis files that have errors.
```
