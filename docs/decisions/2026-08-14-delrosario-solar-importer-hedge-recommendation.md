
# CFO Recommendation Memo

**To:** Chief Financial Officer  
**From:** Treasury Analyst  
**Subject:** Hedge recommendation for the €4.5 million receivable  
**Settlement date:** August 13, 2027  
**Recommendation:** Hedge the full receivable with a one-year forward contract

This recommendation uses only the updated FX hedging model specification and market-data memo.

## A. Exposure summary

The company expects to receive **€4,500,000 in 365 days** and reports its results in U.S. dollars. Because the euro amount is fixed while the future EUR/USD exchange rate is unknown, the USD value of the receivable remains exposed to currency movements until settlement.

The current reference spot rate is **1.1573 USD/EUR**, giving the receivable a current translated value of:

\[
€4{,}500{,}000 \times 1.1573
=\$5{,}207{,}850
\]

The primary financial risk is euro depreciation. If EUR/USD declines, each euro received will purchase fewer dollars, reducing the cash available for budgets, margins, and operating commitments. A stronger euro would increase USD proceeds, but retaining that upside requires the company to accept some combination of exchange-rate risk or option-premium cost.

Three settlement scenarios were evaluated:

- Lower spot: \(1.099435\), or 5% below the live spot
- Live spot: \(1.157300\)
- Higher spot: \(1.215165\), or 5% above the live spot

The analysis compares remaining unhedged with a forward, a money-market hedge, a purchased EUR put, and a hypothetical purchased EUR call.

## B. Hedge outcomes

### Summary of settlement proceeds

| Strategy | Lower spot | Live spot | Higher spot |
|---|---:|---:|---:|
| Unhedged | $4,947,458 | $5,207,850 | $5,468,243 |
| Forward | **$5,279,850** | **$5,279,850** | $5,279,850 |
| Money market | **$5,279,888** | **$5,279,888** | $5,279,888 |
| Purchased put | $5,095,350 | $5,095,350 | **$5,355,743** |
| Hypothetical purchased call | $4,834,958 | $5,095,350 | $5,616,135 |

### Unhedged baseline

Remaining unhedged preserves all potential benefit from euro appreciation but also leaves the entire receivable exposed to depreciation.

At the lower settlement spot, USD proceeds decline to approximately **$4.947 million**, which is:

- **$260,393 below** the current translated value;
- **$332,393 below** the forward outcome; and
- **$147,893 below** the protected put outcome.

At the higher spot, unhedged proceeds increase to approximately **$5.468 million**, exceeding forward proceeds by **$188,393**. That upside comes at the cost of having no minimum USD proceeds other than whatever the settlement exchange rate produces.

Because this receivable may support budgeted expenditures and operating commitments, remaining fully unhedged is inconsistent with a treasury objective centered on cash-flow stability.

### Forward hedge

The one-year forward rate is **1.1733 USD/EUR**, producing fixed settlement proceeds of:

\[
€4{,}500{,}000 \times 1.1733
=\boxed{\$5{,}279{,}850}
\]

The forward produces the same proceeds under every settlement scenario. It eliminates both downside risk and upside participation.

The quoted forward is also above the live spot. As a result, the company locks proceeds **$72,000 higher** than the receivable’s current spot-translated value:

\[
\$5{,}279{,}850-\$5{,}207{,}850
=\$72{,}000
\]

In the lower scenario, the forward protects **$332,393** relative to remaining unhedged. In the higher scenario, however, the company gives up **$188,393** of potential unhedged upside.

The forward therefore offers the clearest budget certainty without the explicit upfront premium associated with the put.

### Money-market hedge

The money-market hedge requires the company to:

1. Borrow the present value of the €4.5 million receivable;
2. Convert the borrowed euros to dollars at the live spot;
3. Invest the dollars for 365 days; and
4. Use the eventual receivable to repay the EUR borrowing.

The required EUR borrowing is:

\[
\frac{€4{,}500{,}000}
{1+0.0258(365/360)}
=€4{,}385{,}288.17
\]

After conversion and USD investment, settlement proceeds are:

\[
\boxed{\$5{,}279{,}888}
\]

This is only about **$38 more** than the forward. Economically, the two strategies provide essentially the same degree of protection and nearly identical proceeds.

The money-market hedge is less attractive operationally because it requires immediate borrowing, conversion, investment, and use of credit capacity. The $38 modeled advantage is immaterial relative to the €4.5 million exposure and does not compensate for the added liquidity and administrative requirements.

### Purchased EUR put

The put has a strike of **1.1573 USD/EUR** and costs **0.0250 USD/EUR**, resulting in a total premium of:

\[
€4{,}500{,}000 \times 0.0250
=\$112{,}500
\]

The net protected proceeds are:

\[
€4{,}500{,}000(1.1573-0.0250)
=\boxed{\$5{,}095{,}350}
\]

This floor applies whenever settlement spot is at or below the strike. If the euro appreciates above the strike, the company lets the put expire and converts the receivable at the favorable market rate, less the premium.

The put therefore combines downside protection with upside participation, but its guaranteed proceeds are **$184,500 below** the forward:

\[
\$5{,}279{,}850-\$5{,}095{,}350
=\$184{,}500
\]

At the higher settlement spot, the put produces approximately **$5.356 million**, exceeding the forward by **$75,893**. The put does not outperform the forward after premium unless EUR/USD exceeds:

\[
1.1733+0.0250=\boxed{1.1983}
\]

This break-even rate is approximately **3.54% above** the live spot. Management would therefore be paying $112,500 for upside participation that becomes financially superior to the forward only after a meaningful appreciation of the euro.

### Call option

The specification retains a call strike and premium as shared inputs but explicitly states that they are unused for this EUR receivable. A purchased EUR call would not address the company’s principal risk.

When held alongside the receivable, a call provides additional gains if the euro appreciates but no protection if it depreciates. At the lower and live settlement spots, it reduces proceeds by the $112,500 premium. At the higher spot, it produces the largest modeled result because the company benefits from both the appreciating receivable and the call payoff.

That outcome represents increased EUR exposure rather than hedging. The purchased call should therefore be excluded from the practical hedge alternatives.

## C. Sensitivity interpretation

The five alternatives present distinct tradeoffs among certainty, flexibility, liquidity, and cost.

Under euro depreciation, the forward and money-market hedge provide the strongest protection, holding proceeds near **$5.280 million**. The put provides partial protection through a **$5.095 million net floor**, while the unhedged position and purchased call remain exposed to falling EUR/USD.

Under euro appreciation, the unhedged position participates fully. The put also participates, but its proceeds remain $112,500 below the unhedged result because of the premium. The forward and money-market outcomes remain fixed and therefore sacrifice favorable currency gains.

The decision is consequently not based solely on which strategy has the highest result in one scenario. It depends on the CFO’s priority:

- **Certainty:** Forward or money-market hedge
- **Upside flexibility with a protected floor:** Purchased put
- **Maximum upside with full downside exposure:** Unhedged
- **Additional speculative EUR exposure:** Purchased call

For a known corporate receivable supporting budgets and operating commitments, certainty should generally carry more weight than attempting to profit from exchange-rate movements.

## D. Recommendation

I recommend hedging the **full €4.5 million receivable with the one-year forward at 1.1733 USD/EUR**, subject to confirming that the rate is executable with an approved counterparty.

The forward locks:

\[
\boxed{\$5{,}279{,}850}
\]

This strategy is preferred because it:

- Eliminates uncertainty in the receivable’s USD value;
- Protects $332,393 relative to remaining unhedged in the lower scenario;
- Locks $72,000 more than the current spot-translated value;
- Avoids the put’s $112,500 upfront premium;
- Does not require the borrowing and investment transactions of the money-market hedge; and
- Directly addresses the identified risk of euro depreciation.

The principal cost is the loss of potential appreciation. At the higher scenario, the forward produces $188,393 less than remaining unhedged and $75,893 less than the put. That opportunity cost should be viewed as the price of eliminating an uncertain FX outcome, rather than as a cash premium.

If management has a strong, documented preference for retaining currency upside, the put would be the appropriate alternative. However, that choice would lower guaranteed proceeds by $184,500 relative to the forward and require EUR/USD to exceed 1.1983 before producing a superior net outcome.

## E. Executive justification

### Cash-flow stability

The forward converts an uncertain foreign-currency receivable into a known **$5.280 million settlement cash flow**. This allows management to plan spending, working capital, and operating commitments without depending on the future exchange rate.

### Budget certainty

The forward provides the clearest basis for budgeting because its outcome does not vary with settlement spot. The unhedged and option strategies leave some or all of the USD proceeds dependent on market conditions.

### Liquidity

The forward has no modeled upfront premium and does not require the immediate borrowing and investment transactions needed for the money-market hedge. This preserves cash and financing capacity during the hedge period.

### Optionality

The put offers economically valuable upside participation, but that flexibility is not free. Its net floor is $184,500 below the forward, and the euro must appreciate above 1.1983 before the put becomes the better financial result.

The call does not provide useful optionality for this exposure because the company already owns the economic equivalent of a long EUR position through its receivable. Purchasing another EUR call adds to that position instead of protecting it.

### Premium cost

The put premium is **$112,500**, equal to:

\[
\frac{\$112{,}500}{\$5{,}207{,}850}
\approx 2.16\%
\]

of the receivable’s live spot-translated value. Unless management has a strong view that EUR/USD will rise materially above 1.1983, this is a substantial cost for upside participation.

## Final decision

The forward provides the best alignment with the company’s treasury objective: protecting the USD value of a known EUR receivable. It delivers strong downside protection, fixed budgetable proceeds, limited liquidity impact, and less operational complexity than the money-market hedge.

Accordingly, the company should **execute a full-notional one-year forward for €4.5 million at 1.1733 USD/EUR**, after confirming the dealer rate, counterparty approval, and settlement terms.
