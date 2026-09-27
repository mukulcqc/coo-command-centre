# COO Command Center

A single-file operations dashboard built for one reader: the executive who has to
decide where to spend attention this week. Four views over the same business —
financial, capability, delivery quality and account — each ending in generated
insight statements rather than in another table to interpret.

> **Demonstration build.** Every figure and name in this repository was generated at
> random. Account names, verticals, capabilities and all metrics are invented.
> Nothing here reflects any real organisation, client or commercial data.

<!-- Add once you have one:
![Dashboard](docs/screenshot.png)
-->

---

## The premise

Most executive reporting does the opposite of what it should. A pack arrives with
forty pages of complete, accurate, well-formatted data, and the prioritisation — the
actual work — is left to the person with the least time to do it. Completeness gets
mistaken for usefulness.

This dashboard tries to close that gap in two ways. Every view drills from the
aggregate down to the individual account without leaving the page, so a number that
looks wrong can be interrogated immediately. And every view ends in an **Insights
panel** that states, in sentences, what the data appears to be saying — including
when it contradicts itself.

The charting was the easy part. The design problem was deciding what a view should
conclude and what it should leave for the reader, which is an editorial judgement
more than a technical one.

## The four views

### Unit-wise

Financial and workforce performance by delivery vertical, split three ways:

- **Revenue and HC** — revenue, revenue per head and growth %, quarterly and monthly
- **Gross Margin** — GM and GM% with quarterly detail
- **Headcount Overview** — three sub-analyses:
  - *HC Walk Analysis* — an opening-to-closing bridge, decomposing movement into
    growth, rampdown and automation release
  - *Trend Analysis* — headcount trajectory across periods
  - *Automation Release Analysis* — headcount released through automation, by unit
    and period

### Capability-wise

The same performance cut by capability rather than by vertical, with drill-down
through sub-capabilities and sub-sub-capabilities, each carrying its own metric set.

### Delivery and Quality

Three signal families, each from aggregate to account level:

| Signal | What it covers |
| --- | --- |
| **DQI** | Delivery Quality Index trend across units, then account-wise |
| **SLA** | Quarterly SLA status, financial penalty exposure ($), and line-level detail |
| **VoC** | Customer rating trend, survey cadence preference, and account-wise ratings |

### Account-wise

An FY summary at account level, with growth, rampdown and automation release broken
out per account and month.

## The Insights panel

Each view generates tagged statements from the data on screen, rather than leaving
interpretation to the reader. Tags in use:

| Tag | Meaning |
| --- | --- |
| `Flagged` | The data contradicts itself and needs a human |
| `Biggest lever` | The single largest contributor to the movement shown |
| `Top growth deal` / `Top rampdown` | Largest account-level movement in each direction |
| `Avg vs closing` | Average and closing headcount diverge enough to matter |
| `On track` / `Falling short` / `Net neutral` | Progress against the period's baseline |

The `Flagged` case is the one worth explaining. When a unit's closing headcount runs
higher than its own itemised bridge implies, the parts do not sum to the whole —
something has been booked outside the categories the bridge tracks. Most dashboards
render both numbers and let nobody notice. This one states the gap, in the unit's
own terms, at the point where the reader is already looking.

## Running it

```bash
git clone https://github.com/<your-username>/coo-command-center.git
cd coo-command-center
open index.html
```

No build step, no package install, no backend. Charts render via Chart.js loaded from
a CDN, so the page needs an internet connection the first time it opens.

## How it's built

One self-contained HTML file: markup, styles, data and logic together. The dataset
is embedded as JavaScript constants, which is why the file is large — it has no
backend to fetch from, by design, so it can be opened from disk or served statically
anywhere.

```
index.html      Everything — markup, styles, data, rendering
docs/           Screenshots
README.md
```

Charting is [Chart.js 4.4.1](https://www.chartjs.org/). There are no other
dependencies.

## Synthetic data

The figures were **generated, not masked**. Masking real numbers by rounding, scaling
or offsetting them preserves the shape of the original and is reversible with enough
context. These values were regenerated at random within plausible ranges, so the
distributions, relative sizes and correlations here carry no information about
anything real. Names were invented rather than substituted.

## Built with

Written with [Claude Code](https://claude.com/claude-code), iteratively rather than
from a specification — most of the work went into arguing about what belonged on each
page and what didn't.

## License

MIT
