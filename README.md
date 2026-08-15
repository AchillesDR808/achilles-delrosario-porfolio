# Achilles Del Rosario | Finance Portfolio

Aloha! I am Achilles Del Rosario, a Finance student at the Shidler College of Business, University of Hawaii at Manoa. I am building practical skills in financial analysis, treasury, and consulting-oriented problem solving.

- [Resume](RESUME.md)
- [Prompt log](prompt-log.md)

## Featured Project: FX Hedging Analysis

**Scenario:** U.S. Solar Equipment Importer  
**Exposure:** EUR 4,500,000 receivable  
**Objective:** Evaluate unhedged, forward, money-market, and option alternatives using live market-data inputs and recommend a hedge for the CFO.

| Stage | Artifact | Description |
|---|---|---|
| Stage 2 | [Technical specification](docs/specs/2026-08-13-del-rosario-solar-importer-spec.md) | Build contract, named ranges, calculation logic, and validation rules. |
| Stage 3 | [Workbook](models/builds/2026-08-14-delrosario-solar-importer-model.xlsx) | Formula-driven FX hedge model with sensitivity analysis and live checks. |
| Stage 3 | [Build audit](analysis/2026-08-14-delrosario-build-audit.md) | Audit findings, fixes, and validation evidence. |
| Stage 4 | [Market-data memo](data/2026-08-14-delrosario-market-data.md) | Input values, sources, timestamps, and CIP-forward method. |
| Stage 5 | [Validation and reconciliation](analysis/2026-08-14-delrosario-solar-importer-validation.md) | Independent LLM comparison, hand calculations, and rounding reconciliation. |
| Stage 5 | [CFO recommendation](docs/decisions/2026-08-14-delrosario-solar-importer-hedge-recommendation.md) | Executive recommendation for a full-notional forward, subject to an executable dealer quote. |
| Stages 2-5 | [Prompt log](prompt-log.md) | Record of AI prompts, review findings, and revisions. |

### Key conclusion

The recommended strategy is a full-notional EUR/USD forward because it provides stable, budgetable USD proceeds for a known EUR receivable. The money-market hedge is economically equivalent before rounding but requires borrowing, conversion, investment, and credit capacity. The put preserves upside at a premium cost; the call is not a hedge for this receivable under the specification.

## Repository layout

```text
analysis/        Validation and build-audit documents
data/            Market-data memo and source documentation
docs/specs/      Technical specifications
docs/decisions/  CFO-facing recommendations and decision records
models/builds/   Excel hedge-model workbooks
```

> The Stage 5 specification retrospective will be added separately by the author.
