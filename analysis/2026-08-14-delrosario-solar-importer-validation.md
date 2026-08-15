
Validation and Reconciliation

## Comparison: Independent LLM vs. Workbook

| Strategy | Settlement spot | LLM result | Workbook result | Difference | Diagnosis |
|---|---:|---:|---:|---:|---|
| Unhedged | 1.099435 | $4,947,458 | $4,947,458 | $0 | Matches |
| Forward | 1.099435 | $5,279,850 | $5,279,888 | $(38) | `F0_in` is rounded to 1.1733 in the memo; workbook uses full CIP precision |
| Money market | 1.099435 | $5,279,888 | $5,279,888 | $0 | Matches |
| Put | 1.099435 | $5,095,350 | $5,095,350 | $0 | Matches |
| Call | 1.099435 | N/A | N/A | — | Not a receivable hedge under the specification |
| Unhedged | 1.157300 | $5,207,850 | $5,207,850 | $0 | Matches |
| Forward | 1.157300 | $5,279,850 | $5,279,888 | $(38) | Same forward-rounding difference |
| Money market | 1.157300 | $5,279,888 | $5,279,888 | $0 | Matches |
| Put | 1.157300 | $5,095,350 | $5,095,350 | $0 | Matches |
| Call | 1.157300 | N/A | N/A | — | Not a receivable hedge under the specification |
| Unhedged | 1.215165 | $5,468,243 | $5,468,243 | $0 | Matches |
| Forward | 1.215165 | $5,279,850 | $5,279,888 | $(38) | Same forward-rounding difference |
| Money market | 1.215165 | $5,279,888 | $5,279,888 | $0 | Matches |
| Put | 1.215165 | $5,355,743 | $5,355,743 | $0 | Matches |
| Call | 1.215165 | N/A | N/A | — | Not a receivable hedge under the specification |

Discrepancies
— Forward versus money-market difference

The forward result is $5,279,850, while the money-market result is
$5,279,888. The $38 difference is caused by rounding F0_in to 1.1733
in the market-data memo. The money-market calculation retains more
precision from spot and interest-rate inputs. This is not an economic
difference under covered interest parity.


Hand Verification Calculations

- Forward Proceeds
USD_FWD = FC_AMT x F0_in
        = 4,500,000 x 1.1733
        = $5,279,850
