# Agent Email Prompt

**Usage:** Run this AFTER completing disclosure analysis to draft an email to your agent. Replace placeholders with your values.

---

```
Help me draft a friendly email to my real estate agent about concerns found in the disclosure package for [ADDRESS].

**Context:**
- Agent name: [AGENT NAME]
- Asking price: $[PRICE]
- We like the home but have concerns about out-of-pocket costs

**Read the analysis files in:** `[FOLDER_PATH]/analysis/`

**Email requirements:**
- Friendly, conversational tone - NOT formal or stiff
- Do NOT use bullet points or bold formatting
- Do NOT make it sound AI-generated - use natural language
- Keep it concise - no long explanations
- Mention I reviewed the docs and used AI tools to help make sense of them

**Structure:**
1. Opening - we like the home, but have concerns after reviewing disclosures
2. Key concerns - mention the major issues found, focusing on:
   - Unsigned documents (who's responsible?)
   - Costs that would fall to buyer
   - Safety concerns flagged by inspectors
   - Any red flags (permit issues, water intrusion, etc.)
3. Ask for their experience - are these typical for older homes in this area?
4. Ask how to think about this for our offer strategy

**Important:**
- Only mention DOCUMENTED costs from the disclosures
- Don't include LLM cost estimates
- Don't be confrontational - ask questions, seek guidance
- Keep it to 5-6 short paragraphs max

**For costs, only mention items that are:**
- Actually in the disclosure documents with real dollar amounts
- Unsigned/unclear who pays
- Would clearly fall to buyer after closing

Write the draft to: `[FOLDER_PATH]/emails/EMAIL_DRAFT_TO_AGENT.md`
```

---

## Example Output

The email should read like this (natural, conversational):

```
Hi [Agent],

We really like the home, but after going through the disclosures I have
some concerns about the out-of-pocket costs and wanted to get your take.
I used some AI tools to help make sense of everything.

The pest reports show about $X in repairs, but the work authorizations
aren't signed. Is the seller expecting us to take that on, or is there
room to negotiate?

[2-3 more short paragraphs about specific concerns]

Based on your experience with older [CITY] homes, are these typical
issues or more on the concerning side? How should we be thinking about
all this when putting together our offer?

Thanks!
[Your name]
```

## What NOT to do

- Don't use bullet points or numbered lists
- Don't bold or format text
- Don't write long explanations of each issue
- Don't include estimated costs (only documented ones)
- Don't sound like a legal document or formal complaint
- Don't make it adversarial
