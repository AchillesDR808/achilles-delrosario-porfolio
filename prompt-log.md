LLM Prompts
- Help me draft a 150–200 word professional bio
for my GitHub profile README. Background: [paste LinkedIn / describe
yourself]. Audience: recruiters and hiring managers in finance.
Make it specific and quantified, not generic.

## FX Hedging Stage 2 — draft and revision (2026-08-13)

- **Draft prompt:** “Draft a buildable model specification for Achilles Del Rosario’s assigned Scenario 1 — U.S. Solar Equipment Importer — with a EUR 4,500,000 receivable and indicative EURUSD forward of 1.0875. Use the Stage 2 named-range contract.”
- **Specific revision made by Achilles:** The first draft described interest rates only as “annual rates.” I revised the assumptions and every rate row to state **ACT/360**, added `T_DAYS`, and made the money-market formulas use `T_DAYS/360`. This removes ambiguity for the Stage 3 workbook build and gives the parity check a consistent basis.

## FX Hedging Stage 3 - workbook build and audit (2026-08-14)

- **Build prompt:** "Using my model specification, build the workbook it specifies. Every requirement in the spec's build contract is binding: all ten named ranges, formulas only (no pasted values), cover page, Legend/Key tab with the color convention, all three hedge families, the +/-5% sensitivity table with chart, and the validation checks computed in the workbook. Give me the result as a downloadable .xlsx file."
- **Audit prompt:** "Revise the Excel for mistakes and fit the Stage 3 guidelines. Do not commit anything; state what I should fix."
- **Specific audit findings and revision made by Achilles:** The first workbook lacked a visible call-hedge calculation, contained hard-coded constants within formulas, had an incomplete cover-page data-provenance block, and did not consistently use green text for formulas. I rebuilt it with a dedicated `Call_Calc` tab; named blue assumption cells for day count, sensitivity increment, grid size, and validation tolerances; the completed provenance block; and the required yellow-input, blue-assumption, green-formula, and gray-output convention. The revised workbook displays seven formula-driven validation checks, all returning `OK`.
- **Final generation prompt:** "Make a new Excel workbook with the audit changes. Do not commit anything."
