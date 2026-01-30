# Cost Research Prompt

**Usage:** Run this to get real-world cost estimates for repairs identified as "by others" or without documented costs. Replace placeholders with your values.

---

```
I need to research real-world costs for repairs identified in the property disclosure analysis for [ADDRESS] in [CITY], CA.

The disclosure analysis identified these items that need cost research (they were marked "by others" or had no cost provided):

## ITEMS NEEDING COST RESEARCH

[List the specific items from your disclosure that need pricing, for example:]
- Foundation drainage/grading correction
- French door repair or replacement
- Asbestos testing/abatement (if doing HVAC work)
- [Add other items specific to your property]

## DEPLOY RESEARCH AGENTS

For EACH item above, deploy a separate agent to research Bay Area / [CITY] costs.

### For Each Item, Search For:
1. Repair costs (if issue can be fixed)
2. Replacement costs (if full replacement needed)
3. Labor rates in Bay Area (note: typically 40-60% higher than national average)
4. Materials costs
5. Permit requirements and costs
6. Typical timeline
7. Factors that affect cost (severity, access, etc.)

### For Each Item, Provide:
| Scenario | Low | Average | High |
|----------|-----|---------|------|
| Minor repair | $ | $ | $ |
| Moderate repair | $ | $ | $ |
| Full replacement | $ | $ | $ |

Note: These are RESEARCH ESTIMATES from web sources, not quotes. Actual costs require contractor bids.

## OUTPUT

For each item, create a separate file:
- `[FOLDER_PATH]/analysis/cost-estimates/COST_ESTIMATE_[ITEM].md`

Each file should include:
- Cost ranges with sources cited
- What the work typically involves
- Factors that could increase/decrease cost
- Permit requirements
- Timeline estimates
- Recommendation: repair vs replace

## IMPORTANT DISCLAIMERS

- Label all costs as **[RESEARCH ESTIMATE]**
- Note that actual costs require contractor quotes
- Note Bay Area cost premium vs national averages
- These are for budgeting purposes only
- Costs can vary significantly based on specific conditions
```
