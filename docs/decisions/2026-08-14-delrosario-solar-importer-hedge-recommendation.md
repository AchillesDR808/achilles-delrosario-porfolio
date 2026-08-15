# CFO Recommendation Memo

**To:** Chief Financial Officer  
**From:** Achilles Del Rosario, Treasury Analyst  
**Subject:** Hedge recommendation for the EUR 4.5 million receivable  
**Settlement date:** August 14, 2027  
**Recommendation:** Hedge the full receivable with a one-year forward contract, subject to obtaining an executable dealer quote.

## A. Exposure summary

The company expects to receive EUR 4,500,000 in 365 days and reports in U.S. dollars. The euro amount is fixed, but its future dollar value depends on EUR/USD at settlement. A weaker euro reduces dollars available for budgets, margins, and operating commitments; a stronger euro increases proceeds but requires accepting foreign-exchange risk or paying for option flexibility.

The live reference spot is 1.1573 USD/EUR. The current translated value of the receivable is:

```text
EUR 4,500,000 x 1.1573 = $5,207,850
```

The analysis evaluates three settlement scenarios: 1.099435 USD/EUR (5% below spot), 1.157300 USD/EUR (live spot), and 1.215165 USD/EUR (5% above spot). It compares unhedged proceeds, a forward, a money-market hedge, and a purchased EUR put. The call is shown only as an illustrative payable/standard-contract input; it is not a hedge for this receivable under the specification.

## B. Hedge outcomes

| Strategy | Lower spot | Live spot | Higher spot |
|---|---:|---:|---:|
| Unhedged | $4,947,458 | $5,207,850 | $5,468,243 |
| Forward | $5,279,850 | $5,279,850 | $5,279,850 |
| Money market | $5,279,888 | $5,279,888 | $5,279,888 |
| Purchased put | $5,095,350 | $5,095,350 | $5,355,743 |
| Call (illustrative only; not a receivable hedge) | N/A | N/A | N/A |

### Unhedged baseline

An unhedged position retains all upside if EUR appreciates, but it leaves the full receivable exposed to depreciation. At the lower scenario, proceeds fall to $4,947,458: $260,393 below the current translated value and $332,393 below the forward outcome. At the higher scenario, proceeds rise to $5,468,243, or $188,393 above the forward. For a known corporate receivable that supports planned spending and operating commitments, this variability is not consistent with a cash-flow-stability objective.

### Forward hedge

The market-data memo provides a CIP-implied one-year forward of 1.1733 USD/EUR. At that rate, fixed forward proceeds are:

```text
EUR 4,500,000 x 1.1733 = $5,279,850
```

The forward eliminates settlement-date EUR/USD uncertainty. It protects $332,393 relative to the unhedged lower scenario and locks $72,000 more than the current spot-translated value. The trade-off is forfeiting $188,393 of upside relative to the unhedged higher scenario. Unlike the put, the forward has no modeled upfront premium.

The 1.1733 rate is CIP-implied, not an executable dealer quote. The company should obtain and document an approved dealer forward quote before execution; the recommendation is to hedge if the executable rate is at or near this modeled level.

### Money-market hedge

The money-market hedge borrows the present value of the EUR receivable, converts the borrowed EUR into USD at spot, invests the USD, and uses the maturity receivable to repay the EUR loan. The borrowing amount is:

```text
EUR_BORROW = EUR 4,500,000 / [1 + 0.0258 x (365/360)]
           = EUR 4,385,288.17
```

The resulting USD proceeds are $5,279,888. This is $38 above the forward result shown above. That difference is caused by rounding `F0_in` to 1.1733 in the market-data memo while the money-market calculation retains more precision from spot and the interest-rate inputs. It is not an economic advantage: before rounding, the forward and money-market hedge are equivalent under covered interest parity.

Operationally, the money-market hedge requires EUR borrowing, immediate currency conversion, USD investment, financing capacity, and related administration. The immaterial rounding difference does not justify that added complexity unless actual all-in borrowing, investment, dealer, and credit costs make it superior to the dealer forward quote.

### Purchased EUR put

The put strike is 1.1573 USD/EUR and the premium is 0.0250 USD/EUR, or $112,500 in total:

```text
EUR 4,500,000 x 0.0250 = $112,500
```

Its protected net floor is:

```text
EUR 4,500,000 x (1.1573 - 0.0250) = $5,095,350
```

The put protects against depreciation while preserving appreciation above its strike, but its floor is $184,500 below the modeled forward proceeds. At the higher scenario, the put returns $5,355,743, or $75,893 more than the forward. The put does not outperform the forward after premium until settlement EUR/USD exceeds 1.1983 USD/EUR, approximately 3.54% above live spot.

## C. Sensitivity interpretation

The forward and money-market hedge provide the greatest certainty: each holds proceeds near $5.280 million across all three scenarios. The unhedged position gives the most appreciation upside but absorbs the full loss from a weaker euro. The put establishes a $5.095 million net floor and maintains upside participation, but that flexibility costs $112,500 and gives up $184,500 of guaranteed proceeds relative to the forward.

The choice therefore is a treasury-policy decision rather than a search for the highest result in one scenario. A forward is the strongest choice where the CFO prioritizes certainty. A put is appropriate only if management values upside participation enough to accept both the premium and a lower guaranteed dollar amount. Remaining unhedged is appropriate only if management is willing to leave the entire budget exposed to EUR/USD. The call is excluded because it adds EUR appreciation exposure without protecting against the relevant risk: a weaker euro.

## D. Recommendation

I recommend hedging the full EUR 4.5 million receivable with a one-year forward, subject to confirming an executable dealer rate at or near 1.1733 USD/EUR, counterparty approval, and settlement terms.

The forward is preferred because it:

- Converts the receivable into a known settlement cash flow of approximately $5.280 million.
- Protects $332,393 relative to remaining unhedged in the lower scenario.
- Avoids the $112,500 put premium.
- Avoids the immediate borrowing, investment, and financing-capacity demands of the money-market hedge.
- Directly addresses the company’s exposure to EUR depreciation.

The principal cost is giving up appreciation beyond the forward rate. That opportunity cost is the price of obtaining a known USD cash flow for a fixed foreign-currency receivable. If management has a documented preference for retaining EUR upside, the purchased put is the appropriate alternative, but management should explicitly accept its lower floor and premium cost.

## E. Executive justification

**Cash-flow stability and budget certainty.** The forward turns an uncertain foreign-currency cash flow into a known dollar amount. This supports reliable spending, working-capital planning, and operating commitments without dependence on a future exchange rate.

**Liquidity.** The forward has no modeled upfront premium and does not require the immediate borrow-convert-invest sequence of the money-market hedge. It therefore preserves cash and credit capacity during the hedge period.

**Optionality and premium cost.** The put provides upside flexibility, but the flexibility is not free. The $112,500 premium equals approximately 2.16% of the receivable’s current translated value. The EUR must settle above 1.1983 before the put produces a better net result than the forward.

## Final decision

Execute a full-notional one-year EUR/USD forward for EUR 4,500,000 after confirming a dealer rate at or near the modeled CIP-implied rate, counterparty approval, and settlement mechanics. This approach best aligns the company’s known receivable with its treasury objective of stable, budgetable U.S.-dollar proceeds.
