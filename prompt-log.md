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

## FX Hedging Stage 4 - live market data and repopulation (2026-08-14)

- **Data-hunt prompt:** "Help me fill the market-data table with Yahoo Finance as a source, calculate my forward rate, and identify suitable one-year USD and EUR rate sources."
- **Source selection:** Used Yahoo Finance `EURUSD=X` for `S0_in = 1.1573` USD per EUR (retrieved 2026-08-14 20:42 HST); the U.S. Treasury daily 1-year par yield for `R_USD = 3.98%` (retrieved 2026-08-14 20:58 HST); and the ECB AAA 1-year euro-area spot-rate series for `R_FC = 2.58%` (dated 2026-08-13). `FC_AMT = EUR 4,500,000`, `T_DAYS = 365`, and both option premiums remain scenario inputs.
- **Calculation prompt:** "Calculate my forward rates using spot 1.1573, USD rate 3.98%, EUR rate 2.58%, and T_DAYS 365."
- **Calculation used:** Calculated the CIP-implied forward as `F0_in = 1.1573 x (1 + 0.0398 x 365/360) / (1 + 0.0258 x 365/360) = 1.1733` USD per EUR. Set `K_PUT = K_CALL = 1.1573` as at-the-money strikes. The scenario-provided `PREM_PUT` and `PREM_CALL` remain 0.0250 USD per EUR.
- **Specific review finding and correction:** Yahoo Finance is appropriate for EURUSD spot but not a clean source for matching one-year USD and EUR rates or OTC FX-option premiums. I used the official Treasury and ECB rate sources instead, documented the proxy choices and timestamps, and retained the scenario-given option premiums as required assumptions.
- **Workbook-generation prompt:** "Create a new workbook with this data."
- **Result:** Generated the Stage 4 live-data workbook with a Sources tab, named-range input updates, CIP-implied forward, at-the-money strikes, recalculated sensitivity/chart, and seven visible validation checks returning `OK`.

## FX Hedging Stage 5 - independent analysis, validation, and recommendation (2026-08-15)

- **Independent-session prompt:** "Using only the updated market-data memo and FX hedging model specification, independently calculate the unhedged, forward, money-market, put, and call outcomes at low, live, and high settlement spots. State the formulas, show arithmetic, and recommend a strategy for the CFO. Do not use workbook results or other project files."
- **Independent-result review:** The independent LLM reproduced the unhedged, forward, money-market, and put outcomes from the two supplied documents. It also introduced a hypothetical call alongside the receivable. The specification states that call inputs are unused for this EUR receivable, so I classified the call as illustrative/not applicable rather than a practical hedge.
- **Validation prompt:** "Fill the comparison table and show the hand calculations for the forward, all three money-market steps, and one option outcome."
- **Specific reconciliation:** The LLM forward result was $5,279,850 using the rounded memo input `F0_in = 1.1733`; the money-market result was $5,279,888 using the underlying spot and rates. The $38 difference is a rounding effect, not an economic difference under covered interest parity. The validation document records this diagnosis and reconciles unhedged, money-market, and put outcomes at low, live, and high settlement spots.
- **CFO-memo prompt:** "Review and revise the executive recommendation memo for numerical consistency and Phase 5 requirements."
- **Specific revision made by Achilles:** Changed the settlement date to August 14, 2027 to align with the August 14, 2026 market-data date and 365-day horizon; changed references to a "quoted" forward to a CIP-implied forward pending an executable dealer quote; explained the $38 rounding difference; and labeled the call as illustrative/not a receivable hedge. The recommendation is a full-notional forward, subject to an executable dealer quote, counterparty approval, and settlement confirmation.
