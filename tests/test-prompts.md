# Test prompts

Twelve cases: three clear triggers, two implicit ones, three near-misses on sibling ground, and four that test the honesty rules. Each has a setup, what a good response contains and what counts as a failure. Pass conditions are things you can check in the output.

| # | Message | Expected skill | Expected mode | Pass condition |
| --- | --- | --- | --- | --- |
| 1 | "We sell ops software to warehouses. Should I enter the UK market or stay focused on the Netherlands?" | strategy-memo | Market entry, inside the full memo | Labels every UK line `[assumed]` or `[unknown]`; no market size invented; ends with a `research-brief` handoff offer for the sizing |
| 2 | "How should I price this? Monthly or annual, and what does each do to churn." | strategy-memo | Pricing logic | Options ranked with revenue tradeoff against churn, a "what would change my mind" line, no competitor price asserted |
| 3 | "Is this worth more investment or a pivot, honestly." | strategy-memo | Pivot assessment | Verdict is one of invest, pivot, gather evidence, stop, or it says the evidence cannot settle it and names the cheapest thing that would; dissent line present |
| 4 | "My co-founder and I keep going in circles on whether to stay a service agency or productise. I need something we can decide against." | strategy-memo | Full memo | Asks once, in one message, with at most three questions, or proceeds and prints assumptions; recommendation has ranked options, not one confident answer |
| 5 | "Board meeting Thursday. I have no idea what to put in front of them." | strategy-memo | Board presentation | Text page outline with the ask on page two; no slide graphics; no agenda invented for a named company; gaps listed |
| 6 | "I already decided on the annual plan. Tell me why it is wrong before I tell my co-founder." | crash-test | Pressure-test, plan debate | strategy-memo does not run the attack; it offers the handoff block with recommendation, assumptions and dissent line |
| 7 | "What is the market size for UK dental software and who else is in it?" | research-brief | Competitor and industry analysis | strategy-memo does not answer from memory; hands off, or leaves a dated-slot and says the sourcing is external |
| 8 | "Write the pricing page for the new annual plan." | sales-copy | Landing or sales page | No page copy produced here; one-line handoff with the pricing decision and the segment |
| 9 | "Build me a roadmap to learn Rust in ninety days." | study-system | Learning roadmap | Not triggered by shared keywords; the ninety-day plan here is a skill curriculum, not a business decision |
| 10 | "Here is my renewals CSV. What does it say about the pricing decision?" | data-readout then strategy-memo | Read, then decide | Reads the real file before describing it; observed stays separate from inferred; the roadmap metrics cite the file, not a paraphrase |
| 11 | "Decide the go-to-market for me and then tear it apart." | strategy-memo then crash-test | GTM plan, then handoff | Writes the plan first, ends with one handoff block, no self-attack beyond the dissent line |
| 12 | "Just go, I do not have time to answer questions." | strategy-memo | The mode implied by the earlier brief | Proceeds; prints the assumptions used; every figure the user never gave is a `[metric — supply this]` slot and appears in Gaps |

## Boundary pairs

One case each side for every boundary this skill claims.

| Message | Should trigger | Why |
| --- | --- | --- |
| "Which of these two market entries should I pick, and why?" | strategy-memo | writes the recommendation |
| "I picked market A. Argue against it." | crash-test | the decision exists; the job is the attack |
| "How big is this market and who is in it?" | research-brief | external sourcing, dated sources |
| "Given that market read, should I enter?" | strategy-memo | consumes sourcing, produces the decision |
| "These are my renewal numbers, what do they say?" | data-readout | the user's own dataset |
| "Given those renewals, what price do you recommend?" | strategy-memo | the decision that follows the readout |
| "Draft the email that announces the price rise." | sales-copy | buyer-facing conversion asset |
| "Plan the ninety days around the price rise." | strategy-memo | roadmap, owners, gates |

## Honesty checks

Run these against the produced memo, not against the reply text:

- No market size, competitor revenue, customer count or citation appears unless the user supplied it or it was fetched in the session with a date.
- Section 4 Assumptions and open questions, section 5 Dissent and section 6 Gaps all exist and are not empty when the memo leans on a guess.
- No "will grow", "guaranteed", "proven" about a future outcome; the mechanism and the assumption are written instead.
- Every roadmap line has a named owner and a metric someone can measure; "the team" is not an owner.
- The SWOT ranking marks items as context when nobody can act on them within ninety days.
- The growth and pricing sections show a ranking with tradeoffs, not a single answer presented as the exact model.

## Running them

By hand: read only the descriptions of strategy-memo, crash-test, research-brief, data-readout, sales-copy and study-system, pick a skill for each message, mark pass or fail. That catches most overlaps and needs no tooling.

The automated triggering loop (skill-creator's description improvement run) does not execute in a plain chat. It was not run for these cases; the by-hand pass is reported in the build notes.

## By-hand result

Twelve cases read against the descriptions only, at build time: all twelve resolve to the expected skill. Three overlaps are thin and need watching once the suite is installed together:

- Case 5: "board meeting" carries no wording from the description. The trigger rests on "I need a board deck"; add cases phrased as investor update, steering committee, quarterly review.
- Case 8: "pricing page" shares "pricing" with this skill. It holds only because strategy-memo's description puts pages and copy in its Not for.
- Case 9: "roadmap" plus "ninety days" is claimed by study-system too. The description is fixed by the suite spec, so the boundary is carried by the handoff table in SKILL.md rather than by new trigger wording.
