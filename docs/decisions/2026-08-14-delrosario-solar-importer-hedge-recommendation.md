Using only the [market-data memo](https://github.com/AchillesDR808/achilles-delrosario-porfolio/blob/main/data/2026-08-14-delrosario-market-data.md) and [hedging-model specification](https://github.com/AchillesDR808/achilles-delrosario-porfolio/blob/main/docs/specs/2026-08-13-del-rosario-solar-importer-spec.md), the forward is the strongest CFO hedge: it locks approximately **$5.280 million**, uses no modeled upfront premium, and is effectively identical to the money-market hedge.

----- 

## Inputs and assumptions

- Receivable \(Q = €4{,}500{,}000\)
- Live spot \(S_0 = 1.1573\) USD/EUR
- Lower settlement spot \(S_L = 0.95S_0 = 1.099435\)
- Higher settlement spot \(S_H = 1.05S_0 = 1.215165\)
- One-year forward \(F_0 = 1.1733\)
- USD rate \(r_{USD}=3.98\%\)
- EUR rate \(r_{EUR}=2.58\%\)
- Time fraction \(t=365/360=1.0138889\)
- Put strike \(K_P=1.1473\)
- Call strike \(K_C=1.1673\)
- Put and call premiums: \(p_P=p_C=0.0250\) USD/EUR, or **$112,500** for the full notional

As directed by the specification, rates use simple interest and ACT/360. All hedges cover the entire receivable and are held to settlement. Bid-ask spreads, transaction costs, taxes, credit risk, collateral, hedge accounting, and premium financing are excluded. Option premiums are deducted without financing.

“Live spot” below means the memo’s \(1.1573\) rate used as the settlement scenario—not a newly retrieved market quote.

## Formulas

Unhedged:

\[
USD_{UNH}(S_T)=Q S_T
\]

Forward:

\[
USD_{FWD}=QF_0
\]

Money-market hedge:

\[
EUR_{BORROW}=\frac{Q}{1+r_{EUR}t}
\]

\[
USD_{NOW}=EUR_{BORROW}S_0
\]

\[
USD_{MM}=USD_{NOW}(1+r_{USD}t)
\]

\[
F_{IMPLIED}=S_0\frac{1+r_{USD}t}{1+r_{EUR}t}
\]

Long EUR put:

\[
USD_{PUT}(S_T)=Q\max(S_T,K_P)-Qp_P
\]

The specification explicitly says the call inputs are unused for this EUR receivable. To satisfy the requested comparison, I calculate a hypothetical **long EUR call held alongside the receivable**:

\[
USD_{CALL}(S_T)
=QS_T+Q\max(S_T-K_C,0)-Qp_C
\]

This is not a conventional hedge for a EUR receivable: it increases EUR upside exposure and provides no downside floor.

## Money-market calculation

\[
EUR_{BORROW}
=\frac{4{,}500{,}000}
 {1+0.0258(365/360)}
=€4{,}385{,}288.17
\]

\[
USD_{NOW}
=4{,}385{,}288.17(1.1573)
=\$5{,}075{,}094.00
\]

\[
USD_{MM}
=5{,}075{,}094.00
 [1+0.0398(365/360)]
=\$5{,}279{,}888.14
\]

The implied forward is:

\[
F_{IMPLIED}
=1.1573
\frac{1+0.0398(365/360)}
     {1+0.0258(365/360)}
=1.1733085
\]

This differs from the quoted forward by only \(0.0000085\) USD/EUR. Money-market proceeds exceed forward proceeds by just **$38**, so covered-interest parity holds within the specification’s tolerance.

## Settlement outcomes

Rounded to the nearest dollar:

| Strategy | Lower: 1.099435 | Live: 1.157300 | Higher: 1.215165 |
|---|---:|---:|---:|
| Unhedged | $4,947,458 | $5,207,850 | $5,468,243 |
| Forward | **$5,279,850** | **$5,279,850** | $5,279,850 |
| Money market | **$5,279,888** | **$5,279,888** | $5,279,888 |
| Long put | $5,050,350 | $5,095,350 | **$5,355,743** |
| Hypothetical long call | $4,834,958 | $5,095,350 | $5,571,135 |

### Interpretation

- **Lower spot:** The forward and money-market hedges produce about **$332,400 more** than remaining unhedged. The put limits the decline, but its net floor is only **$5,050,350**.
- **Live spot:** The forward produces **$72,000 more** than the unhedged receivable and **$184,500 more** than the put.
- **Higher spot:** The unhedged position and put outperform the forward. The put delivers **$75,893 more** than the forward while preserving most of the favorable currency movement.
- **Call:** Its high-spot result is largest because it doubles exposure to EUR appreciation above the strike. That is speculative leverage, not downside protection. At lower and live spots, the call merely reduces proceeds by its $112,500 premium.

The put’s net proceeds exceed the forward only when:

\[
S_T-p_P>F_0
\]

\[
S_T>1.1733+0.0250=\boxed{1.1983}
\]

Thus, the euro must finish more than approximately **3.54% above the live spot** before the put outperforms the forward.

## CFO recommendation

Adopt the **full-notional forward hedge**, subject to confirming an executable dealer quote.

It provides approximately **$5.280 million of certain settlement proceeds**, exceeds both the unhedged and put outcomes at the lower and live scenarios, and avoids the put’s **$112,500 upfront premium**. The money-market hedge is economically equivalent, but it requires borrowing EUR, converting immediately, investing USD, and using financing capacity for only about **$38** of modeled improvement.

Choose the put instead only if management deliberately values upside participation above \(1.1983\) USD/EUR and accepts a net guaranteed floor approximately **$229,500 below** the forward:

\[
\$5{,}279{,}850-\$5{,}050{,}350=\$229{,}500
\]

Do not use the long call as the receivable hedge; it fails to protect the company against the identified risk—a weaker euro.
