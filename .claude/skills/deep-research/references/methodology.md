# Methodology reference

The detail behind the workflow in `SKILL.md`. Read the relevant section when you
need more than the summary.

## Table of contents
- [Decomposition: building a good research tree](#decomposition)
- [Search tactics](#search-tactics)
- [Source credibility tiers](#source-credibility-tiers)
- [The independence test](#the-independence-test)
- [Confidence levels](#confidence-levels)
- [Calibrating fan-out width and cost](#calibrating-fan-out)
- [Common failure modes](#common-failure-modes)

## Decomposition

The single highest-leverage step. A question well-divided is half-researched.
You want lanes that are:

- **Independent** — a researcher can complete the lane without waiting on
  another lane's output. Dependencies force serialization and kill the speed
  advantage.
- **Collectively exhaustive** — together the lanes cover the whole question, so
  the report has no blind spot.
- **Minimally overlapping** — two lanes fetching the same sources is wasted
  swarm. Give each an explicit "you own / you ignore" boundary.

Decomposition patterns:
- **By facet** — the natural sub-topics (e.g. for "is X a good investment":
  fundamentals, competition, risks, valuation, management, macro).
- **By option** — one lane per candidate when comparing (each product, model,
  city, vendor), plus a lane for the comparison criteria themselves.
- **By perspective** — proponents, critics, and neutral primary data as separate
  lanes; surfaces controversy a single search would average away.
- **By source type** — academic, industry/practitioner, journalistic, and
  primary-document lanes, so the report rests on a balanced base.
- **By time** — origins/history, current state, and outlook/projections.

For most reports a *hybrid* is best: e.g. one lane per option, plus a "risks &
criticism" lane and a "primary data" lane cutting across all options.

## Search tactics

- **Generate query variety.** For each lane, vary vocabulary, specificity, and
  framing. Synonyms, jargon vs plain language, and the negation of the
  hypothesis all surface different corners.
- **Use the funnel.** Broad survey queries to map the space → targeted queries
  at the best leads → primary-source queries (paper titles, dataset names,
  official site, filing numbers).
- **Operators help.** Site-scoping (`site:gov`, `site:edu`, a specific outlet),
  exact-phrase quoting, year filters, and `filetype:pdf` for reports/papers.
- **Follow the citation upstream.** When a page says "according to a 2024 study"
  or "the report found", your next move is to find that study/report itself.
- **Search for the counter-case on purpose.** Append "criticism", "limitations",
  "debunked", "failed", "controversy", or the opposing thesis. The disconfirming
  search is what separates research from confirmation.

## Source credibility tiers

- **T1 — Primary / authoritative:** peer-reviewed research, official statistics
  and registries, regulatory filings, court records, primary datasets, technical
  standards and specs, first-party docs, direct statements from the responsible
  party. The bedrock of a defensible report.
- **T2 — Reputable secondary:** established news outlets with editorial
  standards, recognized expert commentary, research from credible industry
  firms, textbooks and review articles. Good for synthesis and context.
- **T3 — Tertiary / weak:** encyclopedias and wikis, content aggregators, vendor
  marketing, op-eds, forum and social posts, anonymous or low-reputation
  sources. Fine as leads and for color; chase them upstream before relying on
  them. A load-bearing claim should not stand on T3 alone.

Always record each source's **date** and any **conflict of interest** (a vendor
on its own product, an advocacy group on its own cause, a funder's stake in the
result).

## The independence test

The most common way confident-sounding research is wrong: **circular sourcing.**
Ten outlets report the same statistic, but all ten trace to a single press
release. That's *one* source. Before counting corroboration:

1. For each supporting source, find what *it* cites.
2. If multiple sources collapse to the same origin, count the origin once.
3. Genuine corroboration means independent methods or independent data reaching
   the same conclusion — e.g. two separate studies, or an official dataset *and*
   an independent audit.

A claim with three truly independent T1/T2 sources is High confidence. A claim
with "many" sources that all echo one origin is, at best, Medium.

## Confidence levels

Apply to every load-bearing claim, inline in the report:

- **High** — multiple genuinely independent, credible (T1/T2) sources; primary
  source located; no serious unrebutted counter-evidence; current.
- **Medium** — real support but with one weakness: thin sourcing, some
  staleness, partial disagreement, or only secondary sources.
- **Low / Contested** — single source, weak (T3) source, active expert
  disagreement, or strong counter-evidence. Report it *as* uncertain or
  contested; never launder Low into a confident statement.

## Calibrating fan-out

- Width tracks complexity, not enthusiasm: 3–5 lanes for a focused dive, 6–10
  for a standard report, 10–20+ for "compare everything" surveys.
- Each lane is cheap relative to its value, but context and wall-clock aren't
  free. Prefer **two waves** (initial fan-out, then a targeted gap-filling wave)
  over one enormous launch — the second wave is far better aimed because it's
  informed by the first.
- Stop when waves stop changing the picture. The deliverable is a great report,
  not exhaustive coverage of the internet.

## Common failure modes

- **Fanning out on a vague question.** Scope first; a swarm pointed at an
  ambiguous prompt produces an ambiguous report. Worth the 2 clarifying questions.
- **Sequential dispatch.** Launching subagents one at a time forfeits the entire
  speed advantage. Same turn = parallel.
- **Raw-dump returns.** If subagents return whole pages, your context drowns
  before synthesis. Enforce the compact memo format.
- **Skipping verification.** The verification pass is where credibility is made;
  skipping it produces confident-but-fragile reports — exactly the failure mode
  this skill exists to beat.
- **Citation drift.** Citing a URL nobody fetched, or attaching a real URL to a
  claim it doesn't actually support. Every citation must trace to fetched text
  that says what the claim says.
- **Burying the lede / hiding gaps.** Lead with the answer and its confidence;
  give unknowns their own section. Admitted uncertainty builds trust; concealed
  uncertainty destroys it.
