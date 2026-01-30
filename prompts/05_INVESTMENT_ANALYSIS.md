# Investment Analysis Prompt

**Usage:** Run this AFTER completing disclosure analysis, verification, area research, and cost research. This creates the final buy/no-buy recommendation.

---

```
Create a comprehensive INVESTMENT ANALYSIS for [ADDRESS] to help me decide if this property is worth pursuing at $[ASKING_PRICE].

## READ ALL ANALYSIS FILES

Read everything in: `[FOLDER_PATH]/analysis/`

This should include:
- Disclosure analysis files (inspection, pest, seller, permits, environmental, advisory)
- FINAL_BUYER_REPORT.md
- VERIFICATION_CHECKLIST.md
- Area research (crime, schools, market comps)
- Cost research estimates

## CREATE INVESTMENT ANALYSIS

Write to: `[FOLDER_PATH]/analysis/reports/INVESTMENT_ANALYSIS.md`

### 1. EXECUTIVE SUMMARY
One paragraph verdict: Should I pursue this property? Under what conditions?

### 2. PROPERTY SCORECARD

| Category | Rating (1-10) | Notes |
|----------|---------------|-------|
| Location | | |
| Safety/Crime | | |
| Schools | | |
| Physical Condition | | |
| Permit Compliance | | |
| Environmental Risk | | |
| Value vs Market | | |
| **OVERALL** | | |

### 3. TRUE COST OF OWNERSHIP

| Item | Amount | Source | Type |
|------|--------|--------|------|
| Asking Price | $ | MLS | - |
| [List all documented costs] | $ | [Doc name] | DOCUMENTED |
| [List all researched costs] | $X - $Y | Web research | RESEARCH ESTIMATE |
| **TOTAL (Low)** | $ | | |
| **TOTAL (High)** | $ | | |

Clearly separate DOCUMENTED costs from RESEARCH ESTIMATES.

### 4. NEIGHBORHOOD SUMMARY
- Crime: [grade] - [one line summary]
- Schools: [ratings] - [one line summary]
- Market: [trend] - [one line summary]

### 5. VALUE ASSESSMENT
- Asking price per sq ft: $X
- Market average per sq ft: $X
- After repairs, effective price per sq ft: $X
- Is asking price fair given condition?
- What should I offer?

### 6. RISK FACTORS
List the major risks of this purchase, ranked by severity.

### 7. OPPORTUNITY FACTORS
List the positives and upside potential.

### 8. NEGOTIATION STRATEGY

**Based on DOCUMENTED costs only:**
- Minimum credit to request: $X (itemize)
- Items to require seller complete before close
- Contingencies to include in offer

**Do NOT base negotiation on research estimates - those need real quotes.**

### 9. FINAL RECOMMENDATION

**Verdict:** BUY / NEGOTIATE HARD / WALK AWAY

**Conditions for purchase:**
- Maximum price: $X
- Required credits: $X
- Required seller actions: [list]
- Required contingencies: [list]

**Walk away if:**
- [List dealbreakers]
```
