# Stage 5 review — solar importer LLM analysis & validation · Treasury sign-off

Achilles — you submitted Stages 2 through 5 in a single day, so this is the first review you have had from me, and I want to lead with the thing that matters most: the memo is good. Not "good considering the timeline" — good. One line in particular is the most professionally mature sentence anyone wrote in this stage:

> *"The 1.1733 rate is CIP-implied, not an executable dealer quote. The company should obtain and document an approved dealer forward quote before execution."*

Almost every memo in this cohort treats the CIP-implied forward as if it were a price you could trade on. It is not — it is a no-arbitrage construction from spot and two interest rates, and the number a dealer actually shows you will differ by their spread and your credit. You spotted that, and then you did the harder thing: you carried it into the recommendation as a *condition* (*"subject to confirming an executable dealer rate at or near 1.1733"*) rather than burying it as a caveat. That is how a real treasury recommendation is written.

| Criterion | Score |
|---|---|
| LLM execution & comparison | 25 / 25 |
| Hand verification | 25 / 25 |
| Recommendation & executive voice | 25 / 25 |
| Spec retrospective | 17 / 17 |
| Repo polish | 3.2 / 8 |
| **Total** | **96 / 100** |

**What you did well — and why it matters**

- **Every number in the memo reconciles.** I checked all of them independently: $332,393 forward-vs-unhedged protection (5,279,850 − 4,947,458) ✓; $188,393 upside forgone ✓; $184,500 floor gap (5,279,850 − 5,095,350) ✓; $72,000 over spot-translated value ✓; and the premium at 2.16% of $5,207,850 ✓. Nothing drifted between the workbook, the validation doc, and the memo. That consistency is rarer than it should be.
- **Your put breakeven is exactly right.** `S_T = (5,279,850 + 112,500) / 4,500,000` = **1.19830**, which is 3.543% above live spot — your stated 1.1983 and "approximately 3.54%" ✓. You derived it rather than eyeballing it off the table.
- **You diagnosed the $38 correctly, and refused to bank it.** The forward-versus-money-market gap traces to the memo's `F0_in` being displayed at 1.1733 while the money-market chain retains full precision — and you said plainly that it *"is not an economic advantage."* Then: *"The immaterial rounding difference does not justify that added complexity."* A weaker memo would have recommended the money market to capture $38. Recognizing when a difference is noise and saying so is a judgment call, and you made it correctly.
- **You excluded the call for the right reason.** *"The call is excluded because it adds EUR appreciation exposure without protecting against the relevant risk: a weaker euro."* That is the correct economics stated in one sentence, and it is the single most commonly botched point in this assignment.
- **You framed the decision as policy, not optimization.** *"The choice therefore is a treasury-policy decision rather than a search for the highest result in one scenario."* Correct, and it is why your §C reads like advice instead of a scoreboard.

**The one substantive correction — the put premium is not being carried to settlement**

Your put floor is computed as:

```
USD_PUT_floor = FC_AMT × (K_PUT − PREM_PUT) = 4,500,000 × (1.1573 − 0.0250) = $5,095,350
```

That subtracts a premium paid **today** from proceeds received in **365 days**, which mixes two different dates — the same mistake in kind (though much smaller in size) as comparing forward proceeds against today's spot value.

You already know the fix, because you applied it correctly on the other leg: your money-market hedge discounts the EUR receivable at `R_FC` and compounds the USD at `R_USD` precisely because timing matters. Apply the same discipline to the premium:

```
FV_PREM = 112,500 × [1 + 0.0398 × (365/360)] = 112,500 × 1.0403528 = $117,039.70
Put floor (like-for-like) = 5,207,850 − 117,040 = $5,090,810
Breakeven vs. forward      = (5,279,850 + 117,040) / 4,500,000 = 1.19931  → 3.63% above spot
```

So the floor is about $4,540 lower and the breakeven sits ~9 bp higher than your memo states. It does not change your recommendation — the forward still wins on your stated objective, and it wins by slightly more. But the principle is worth internalizing: **any cash flow in the comparison has to be stated as of the same date.** On a EUR 450 million exposure rather than 4.5 million, that $4,540 becomes $454,000, and nobody would call it rounding.

**The weakest part — the retrospective, even though it scored full marks**

Your retrospective is 84 words. It cleared the threshold, so it earned the full 17, but I would be doing you no favors by leaving it there. Compare what it says:

> *"Date inconsistencies were also found."*

Which dates? In which document? Did the LLM invent a settlement date, or misread `T_DAYS`, or carry the Stage 2 date into a Stage 4 context? You found something real and then did not write it down, so nobody — including future you — can act on it.

The strongest observation you *do* make is that the LLM *"would assume data and or create educated hypotheticals when it came inputs it viewed as missing, such as the K_CALL and PERM_CALL."* That is exactly the failure mode this stage exists to teach: an LLM handed an underspecified contract will not stop and ask, it will confabulate a plausible value and present it with the same confidence as a derived one. The v2 fix writes itself — your spec should state, for every named range, either the formula or the words "not used; do not infer" — and that sentence would have been worth more than the closing paragraph about the LLM's "great potential."

Two typos to fix while you are in there: *"do too the use of"* → "due to", and *"the the Codex LLM"*.

**Repo polish — 4.8 points, the largest single gap in your grade**

Three of five items are open, and all three are quick:

1. **`LICENSE`** — add one at the repo root (MIT is fine for coursework).
2. **Repository description** — the one-line field at the top right of the GitHub repo page is empty. Something like *"FIN 321 portfolio — FX hedging analysis for a EUR 4.5M receivable (U.S. solar equipment importer)."*
3. **Per-directory READMEs** — only `models/builds/` has one. `analysis/`, `data/`, `docs/`, `docs/decisions/`, and `docs/specs/` need a short one each saying what lives there and why.

Two tidy-ups that are not graded but do affect how the repo reads to anyone you show it to: `docs/decisions/model spec template.md` is an unfilled template sitting in your decisions folder, and you have two hedge-framing memos, one of which still carries literal template braces — `2026-08-07-{delrosario}-{U.S. Solar Equipment Importer}-hedge-framing.md`. Delete the template, keep the memo you actually wrote, and rename it without the braces.

One last note, on Stage 4 rather than this one: your market-data memo is a clean, well-sourced provenance table — spot from Yahoo Finance, `R_USD` from Treasury.gov, `R_FC` from the ECB, each timestamped — but it stops there. The stage also asked for the FX Hedging Lab cross-check and a short narrative on which checks resolved and how, and that section is absent; that is what holds Stage 4 at 78 rather than the 90s your other stages are earning. Worth knowing where the points went.

— Treasury

---

### How to work this review — professional workflow

Treat this PR the way an analyst treats feedback from Treasury — a review is a proposal to engage with, not a checklist to rubber-stamp:

1. **Read it yourself first.** Understand each point and form your own view before changing anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM (pushback pass).** Paste this review and your spec into your AI assistant and ask it to (a) explain anything you're unsure of more deeply, and (b) argue the *other side* — where might the reviewer be wrong, and what would you give up by making each change. You're building judgment, not just executing edits.
3. **Decide, then draft the changes with the LLM.** For the points you accept, have the AI help implement them — you specify exactly what and why. Your spec is the prompt; precise in, correct out.
4. **Verify — non-negotiable.** Re-run your own checks (`scripts/recalc.py`, the parity tie-out, sensitivity continuity, no error cells) and confirm the numbers before you commit. An AI will hand you a confident wrong edit; verification is what makes the result *yours*.
5. **Close the loop on the PR.** Reply in the thread with what you changed, what you pushed back on and why, then commit and push. Writing down the reasoning is exactly how this works on a real team.

*This is the same human-in-the-loop discipline the whole project is built on: the LLM drafts, you edit and verify, and you own the result.*
