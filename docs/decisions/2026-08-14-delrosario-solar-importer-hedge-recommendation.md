
The forward hedge is the strongest strategy for this €4.5 million receivable: it locks $5,279,888, eliminates downside, and beats the put in most modeled scenarios.

| EURUSD at settlement | Unhedged | Forward | Money market | Put |
|---:|---:|---:|---:|---:|
| 1.0994 | $4,947,458 | **$5,279,888** | **$5,279,888** | $5,095,350 |
| 1.1110 | $4,999,536 | **$5,279,888** | **$5,279,888** | $5,095,350 |
| 1.1226 | $5,051,615 | **$5,279,888** | **$5,279,888** | $5,095,350 |
| 1.1342 | $5,103,693 | **$5,279,888** | **$5,279,888** | $5,095,350 |
| 1.1457 | $5,155,772 | **$5,279,888** | **$5,279,888** | $5,095,350 |
| 1.1573 | $5,207,850 | **$5,279,888** | **$5,279,888** | $5,095,350 |
| 1.1689 | $5,259,929 | **$5,279,888** | **$5,279,888** | $5,147,429 |
| 1.1804 | **$5,312,007** | $5,279,888 | $5,279,888 | $5,199,507 |
| 1.1920 | **$5,364,086** | $5,279,888 | $5,279,888 | $5,251,586 |
| 1.2036 | **$5,416,164** | $5,279,888 | $5,279,888 | $5,303,664 |
| 1.2152 | **$5,468,243** | $5,279,888 | $5,279,888 | $5,355,743 |


These results reconcile to the model’s sensitivity table.

Recommendation:
- Hedge 100% with a one-year forward, subject to replacing the modeled rate with an executable dealer quote.
- Target a rate close to the model’s CIP-implied 1.173308 USD/EUR. The money-market hedge produces the identical $5,279,888 because the workbook deliberately sets the forward at covered-interest parity. 
- Prefer the forward operationally: it provides the same economics without borrowing €4,385,288, converting it immediately, and investing approximately $5.075 million.
- Use the money-market hedge only if its actual all-in borrowing/investment costs beat dealer forward pricing after spreads, fees, and credit usage.
- Do not select the put at the modeled premium. It costs $112,500, produces a $5,095,350 floor, and only overtakes the forward when settlement EURUSD exceeds approximately 1.1983, about 3.5% above current spot. 
- The call calculation is a payable-case illustration and is not an appropriate hedge for this EUR receivable, consistent with the technical specification.

As a neutral diagnostic—not a probability forecast—equal-weighting the 11 scenarios gives approximately $5.280M forward/MM, $5.208M unhedged, and $5.166M put. The workbook passes all parity, repayment, option-continuity, and grid checks with no detected formula errors.
