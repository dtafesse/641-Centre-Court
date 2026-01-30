# Area Research Prompt

**Usage:** Run this AFTER the disclosure analysis to research the neighborhood. Replace placeholders with your values.

---

```
I need to research the area around [ADDRESS] in [NEIGHBORHOOD], [CITY], CA [ZIP].

This is for a property I'm considering purchasing. I've already analyzed the disclosure documents and now need neighborhood context.

## DEPLOY RESEARCH AGENTS IN PARALLEL

### Agent 1: Crime & Safety Research

Search for:
- Crime rates in [NEIGHBORHOOD] vs [CITY] overall vs state average
- Types of crime (property vs violent)
- Crime trends (improving or worsening)
- Safety ratings from NeighborhoodScout, Niche, CrimeGrade, etc.
- Recent news about crime in this specific area

Provide:
- Overall safety grade/rating
- Comparison to city average
- Is this considered safe for this city?

Write to: `[FOLDER_PATH]/analysis/research/AREA_CRIME_RESEARCH.md`

### Agent 2: School Research

Search for:
- Elementary schools serving this address - names and ratings
- Middle schools serving this address - names and ratings
- High schools serving this address - names and ratings
- Overall school district rating
- Private school options nearby

Use GreatSchools, Niche, or similar for ratings (1-10 scale).

Provide:
- Assigned public schools with ratings
- Test scores vs state average
- Notable private alternatives

Write to: `[FOLDER_PATH]/analysis/research/AREA_SCHOOL_RESEARCH.md`

### Agent 3: Market Research

Property details for comparison:
- Address: [ADDRESS]
- [X] bed / [X] bath
- [X] sq ft (note if discrepancy with public records)
- Built [YEAR]
- Lot: [X] sq ft
- Listed at $[PRICE]

Search for:
- Recent comparable sales in [NEIGHBORHOOD] (last 6 months)
- Price per square foot in the area
- Average days on market
- Are homes selling above or below asking?
- Market trends (appreciating, stable, declining)

Provide:
- 3-5 comparable recent sales with prices
- Price per sq ft analysis
- Is asking price fair, high, or low?
- Market outlook

Write to: `[FOLDER_PATH]/analysis/research/MARKET_COMPS_RESEARCH.md`

## IMPORTANT

- Cite sources where possible
- Note the date of any statistics
- Flag if data is limited or unavailable
- These are research findings, not guarantees
```
