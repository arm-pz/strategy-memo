# strategy-memo

An agent skill that turns a business question into a decision document: situation analysis, a recommendation written as ranked options with the tradeoff each one carries, and an execution roadmap with milestones, owners and success metrics. It covers competitive analysis, market and customer research, the business model canvas, growth and pricing, a go-to-market plan, a SWOT ranked by actionability, the ninety-day, one-year and three-year roadmaps, a board deck outline and a pivot assessment. Every line is labelled as something you supplied, something assumed, or something unknown, and figures nobody has stay as slots rather than becoming facts.

Install: `npx skills add arm-pz/strategy-memo --skill strategy-memo`

Ask it things like:

- "Should I enter this market? Here is what we sell and what it costs us."
- "How should I price this? Monthly or annual, and what does each do to churn."
- "Who are my competitors and which gap is worth exploiting first."
- "Is this worth more investment or a pivot, honestly."

## What you get

| Mode | Output |
|---|---|
| Competitive map | Competitors by positioning, evident strength, the gap, and what exploiting it costs |
| Market and customer read | Segments, pains, willingness to pay and buying behaviour, each labelled by evidence |
| Business model canvas | One page, nine boxes, with the thin ones marked and what they block |
| Growth options | Options ranked against your resources, each with mechanism, cost and the number that kills it |
| Pricing logic | Model options, who pays more and less, revenue tradeoff against churn, reversibility |
| Go-to-market plan | Entry sequence, channel choice with the reason, week-by-week launch with gates |
| SWOT | Ranked by actionability, with the items that are context only listed as context |
| Roadmap | Ninety-day in weeks plus one-year and three-year milestones, owners and metrics |
| Board presentation | Text outline of the deck: page order, the sentence each page proves, the ask |
| Pivot assessment | A verdict that can be invest, pivot, gather evidence or stop, with the dissent line |
| Full memo | The decision document: situation, recommendation, execution, assumptions, dissent, gaps |

Every mode ends with an Assumptions and open questions block, a dissent line arguing against its own recommendation, and a Gaps list naming each missing figure.

## Not for

Pressure-testing a decision you have already made and leaned toward: that is `crash-test`, and this skill hands off to it rather than running the attack itself. Not external sourcing of market size or competitor facts, which belongs to `research-brief`; this skill consumes what it returns and leaves the rest as slots. Not your own numbers read out of a spreadsheet (`data-readout`), not the pages, emails or audience content that execute the plan (`sales-copy`, `platform-content`), and not career documents (`career-track`, `recruiter-lens`, `applicant-kit`). It writes strategy in text; it does not draw slides.

## Install

```
npx skills add arm-pz/strategy-memo --skill strategy-memo
```

Or copy `skills/strategy-memo/` into your agent's skills directory (`.claude/skills/`, `.agents/skills/`, `.cursor/skills/` or `.qoder/skills/`). With Claude Code plugins, `.claude-plugin/plugin.json` makes the repo installable as a plugin; add it to your marketplace repo as an entry pointing at `arm-pz/strategy-memo`.

## Structure

```
strategy-memo/
├── README.md
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── strategy-memo/
│       ├── SKILL.md                    # intake, modes, output format, quality bar, handoffs
│       └── references/
│           ├── frameworks.md           # the shape of each analysis and what it must not fake
│           └── memo-format.md          # situation, recommendation, execution, board deck outline
└── tests/
    └── test-prompts.md
```

## Siblings

Part of a suite of eight content and strategy skills. The boundary is one owner per verb: this skill writes the recommendation, `crash-test` attacks it, `research-brief` sources what is external, `data-readout` reads your own numbers.
