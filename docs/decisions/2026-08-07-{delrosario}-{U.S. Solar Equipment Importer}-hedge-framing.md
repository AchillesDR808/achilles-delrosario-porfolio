
---

USD proceeds = FC_AMT × F0_in

Step 1  Borrow FC today:      Borrow = FC_AMT / (1 + R_FC × T_DAYS/360)
        (sized so the receivable exactly repays the loan at settlement)
Step 2  Convert at spot:      USD_now = Borrow × S0_in
Step 3  Invest in USD:        Proceeds = USD_now × (1 + R_USD × T_DAYS/360)

F_implied = S0_in × (1 + R_USD × T/360) / (1 + R_FC × T/360)   ≈   F0_in

Net proceeds at settlement spot S_T:
  = FC_AMT × max(S_T, K_PUT)  −  FC_AMT × PREM_PUT

  ✗ "C7 = C4/(1+C5*C6/360)"                        ← dies with the workbook
✓ "Compute the FC borrowing amount by dividing
   FC_AMT by (1 + R_FC × T_DAYS/360); this sizes
   the loan so the receivable repays it exactly
   at settlement."                                ← buildable in any tool

