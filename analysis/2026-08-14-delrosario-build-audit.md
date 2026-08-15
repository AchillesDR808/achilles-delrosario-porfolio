
---

# FX Hedging Stage 3 Build Audit

**Student:** Achilles Del Rosario  
**Scenario:** Scenario 1 — U.S. Solar Equipment Importer  
**Workbook:** `models/builds/2026-08-14-Del Rosario-solar-importer-model.xlsx`  
**Audit date:** 2026-08-14  

## Finding 1 — Required named-range and formula contract

**Checked:** Confirmed all ten required named ranges exist and point to the intended input cells: `FC_AMT`, `S0_in`, `F0_in`, `R_USD`, `R_FC`, `K_PUT`, `K_CALL`, `PREM_PUT`, `PREM_CALL`, and `T_DAYS`.

**Found:** The revised workbook contains all ten names. Calculated outputs reference named ranges rather than fixed cell addresses.

**Action taken:** Confirmed the named-range mapping and retained formula-driven calculations throughout the model.

## Finding 2 — Call hedge was missing from the initial build

**Checked:** Reviewed whether all required hedge families were visibly modeled.

**Found:** The initial workbook showed forward, money-market, and put calculations, but did not show a separate call calculation.

**Action taken:** Added a `Call_Calc` tab for the payable variant. It calculates the USD call premium, call outlay at `S0_in`, and the call payoff/outlay rule as a function of settlement spot `S_T`.

## Finding 3 — Hard-coded constants inside formulas

**Checked:** Reviewed formulas for embedded constants that should be model assumptions.

**Found:** The initial version embedded items such as the 360-day basis, 1% sensitivity increment, and validation tolerances directly in formulas.

**Action taken:** Added blue assumption inputs with named ranges for `DAY_BASIS`, `STEP_PCT`, `GRID_HALF_STEPS`, `PARITY_TOL`, `USD_TOL`, and `AMT_TOL`. Formulas now reference these inputs.

## Finding 4 — Presentation and provenance requirements

**Checked:** Compared the workbook formatting and cover page against the Stage 3 rubric.

**Found:** The initial workbook did not consistently use green text for formulas and its cover page needed a clearer data-provenance statement.

**Action taken:** Applied the required convention: yellow for scenario inputs, blue for assumptions, green for formulas, and gray for outputs. Added a cover-page data-provenance block stating that inputs are indicative placeholders pending Stage 4 live market data.

## Final validation

The workbook displays seven visible formula-driven checks. All return `OK`, including forward parity, money-market versus forward proceeds, foreign-currency repayment, put continuity, call payoff at strike, the 11-row sensitivity grid, and inclusion of `S0_in`.
