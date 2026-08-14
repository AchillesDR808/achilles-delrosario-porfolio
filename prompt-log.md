LLM Prompts
- Help me draft a 150–200 word professional bio
for my GitHub profile README. Background: [paste LinkedIn / describe
yourself]. Audience: recruiters and hiring managers in finance.
Make it specific and quantified, not generic.

## FX Hedging Stage 2 — draft and revision (2026-08-13)

- **Draft prompt:** “Draft a buildable model specification for Achilles Del Rosario’s assigned Scenario 1 — U.S. Solar Equipment Importer — with a EUR 4,500,000 receivable and indicative EURUSD forward of 1.0875. Use the Stage 2 named-range contract.”
- **Specific revision made by Achilles:** The first draft described interest rates only as “annual rates.” I revised the assumptions and every rate row to state **ACT/360**, added `T_DAYS`, and made the money-market formulas use `T_DAYS/360`. This removes ambiguity for the Stage 3 workbook build and gives the parity check a consistent basis.
