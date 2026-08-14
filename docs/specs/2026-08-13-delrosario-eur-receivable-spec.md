# EUR Receivable FX Hedge Model — Technical Specification

| Field | Value |
|---|---|
| Created by | Achilles Del Rosario |
| Date | 2026-08-13 |
| Version | 0.1 |
| Role / audience | Treasury Analyst / CFO |
| Status | Stage 2 workbook design contract |

This specification defines the workbook before it exists. All market figures below are **indicative — replaced with live data at Stage 4**. Use named ranges, never cell addresses.

## 1. Problem statement

The company expects to receive **EUR 4,500,000** on **2027-08-13** (365 days from inception) and reports in USD. The EUR amount is fixed, but its USD value is not: a weaker euro reduces cash available for the budget, margin, and operating commitments. The workbook will compare unhedged proceeds with forward, money-market, and put-option hedges so the CFO can weigh certainty, liquidity use, and upside participation.

## 2. Inputs — named-range contract

| Name | Indicative placeholder | Unit / basis | Stage 4 source |
|---|---:|---|---|
| `FC_AMT` | 4,500,000 | EUR | Receivables contract / ledger |
| `S0_in` | 1.1000 | USD per EUR | ECB EUR exchange-rate reference; access date logged |
| `F0_in` | 1.1229 | USD per EUR, 1-year forward | Executable bank/dealer or Refinitiv/Bloomberg quote; timestamp logged |
| `R_USD` | 4.25% | Annual %, ACT/360 | U.S. Treasury 1-year yield or USD money-market rate; access date logged |
| `R_FC` | 2.15% | Annual %, ACT/360 simplification | ECB euro-area money-market/EUR deposit rate; access date logged |
| `K_PUT` | 1.1000 | USD per EUR | At/near-spot OTC dealer strike |
| `K_CALL` | 1.1000 | USD per EUR | At/near-spot call strike; standard-contract input, unused for this receivable |
| `PREM_PUT` | 0.0250 | USD per EUR | OTC EUR put premium from dealer; expiry and timestamp logged |
| `PREM_CALL` | 0.0250 | USD per EUR | Indicative call premium; standard-contract input, unused for this receivable |
| `T_DAYS` | 365 | Days | Calculated from inception and settlement dates |

Every value is **indicative — replaced with live data at Stage 4**. Inputs are editable only on the Inputs tab and referenced everywhere through their names.

## 3. Tab architecture

- **Cover** — title, exposure summary, author, version, and update date.
- **Legend_Key** — yellow editable-input, black-formula, and gray-output conventions.
- **Inputs** — all ten names, units, sources, timestamps, and placeholder flags.
- **Forward_Calc** — forward proceeds and audit check.
- **Money_Market_Calc** — visible borrow, convert, and invest pipeline plus parity check.
- **Option_Calc** — put premium, payoff, and base-case option proceeds.
- **Sensitivity** — 11-row settlement-spot comparison and one line chart.
- **Notes_Assumptions** — quote convention, exclusions, source notes, and definitions.

## 4. Assumptions and constraints

Use simple interest and ACT/360: `T_DAYS/360`. Rates are USD per EUR; a lower rate is adverse for this EUR receivable. The hedge is full-notional, entered at inception, and held to settlement. Bid-ask spreads, transaction costs, taxes, hedge accounting, credit risk, collateral, and financing of the premium are excluded. The put premium is paid at inception and deducted from reported settlement proceeds without financing. Covered interest parity should hold within rounding tolerance. `K_CALL` and `PREM_CALL` are retained only for the shared input contract.

## 5. Calculation flow

**Forward hedge:** `USD_FWD = FC_AMT × F0_in`. It is constant across settlement spots.

**Money-market hedge:** Show each of these as a separately labeled calculation:
1. `FC_BORROW = FC_AMT / (1 + R_FC × T_DAYS/360)`.
2. `USD_NOW = FC_BORROW × S0_in`.
3. `USD_MM = USD_NOW × (1 + R_USD × T_DAYS/360)`.

The receivable repays the FC loan at settlement, leaving `USD_MM`. Also calculate `F_IMPLIED = S0_in × (1 + R_USD × T_DAYS/360) / (1 + R_FC × T_DAYS/360)`.

**No hedge and put option:** For each `S_T`, calculate `USD_NO_HEDGE(S_T) = FC_AMT × S_T`. Calculate `USD_PUT(S_T) = FC_AMT × MAX(S_T, K_PUT) − FC_AMT × PREM_PUT`. The put supplies a floor at `K_PUT`, net of premium, and preserves upside above the strike. No receivable formula uses `K_CALL` or `PREM_CALL`.

## 6. Sensitivity plan

Create `S_T_grid` from `0.95 × S0_in` to `1.05 × S0_in` in 1% steps: 11 scenarios including `S0_in`. Each row shows `S_T`, `USD_NO_HEDGE`, `USD_FWD`, `USD_MM`, and `USD_PUT`, all in USD. One line chart plots settlement spot on the x-axis and USD proceeds on the y-axis.

The chart must show the CFO that unhedged proceeds move one-for-one with EURUSD, forward and money-market proceeds are flat, and the put protects the downside while participating above `K_PUT`.

## 7. Validation rules (check figures)

1. `F_IMPLIED` equals `F0_in` within 0.0001 USD/EUR, and `USD_MM` equals `USD_FWD` within $500; otherwise flag **CHECK FORWARD/RATES**.
2. `FC_BORROW × (1 + R_FC × T_DAYS/360)` equals `FC_AMT` within 0.01 EUR.
3. If `S_T ≤ K_PUT`, `USD_PUT = FC_AMT × K_PUT − FC_AMT × PREM_PUT`; if `S_T > K_PUT`, it equals `FC_AMT × S_T − FC_AMT × PREM_PUT`.
4. The grid has 11 values, begins at `0.95 × S0_in`, ends at `1.05 × S0_in`, and includes `S0_in`.
5. There are no error cells, no hard-coded gray-cell outputs, and every output updates when an Inputs-tab named range changes.

## 8. Outputs

Gray formula cells are labeled exactly: `USD_FWD`, `USD_MM`, `F_IMPLIED`, `USD_NO_HEDGE`, `USD_PUT`, and `USD_FLOOR_PUT`. `USD_FLOOR_PUT` is the minimum `USD_PUT` on `S_T_grid`. The output area also contains the base-case row at `S_T = S0_in`, full sensitivity table, parity status, and comparison chart. Every result is a formula-driven settlement-date USD proceeds measure; the workbook contains no recommendation.

## Change log

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-13 | Achilles Del Rosario | Initial Stage 2 specification |
