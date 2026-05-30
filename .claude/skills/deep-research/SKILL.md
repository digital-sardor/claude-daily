---
name: deep-research
description: >-
  Deep research harness that produces a long, credible, fully-cited report on
  any question by fanning out parallel subagents across the web, fetching and
  reading primary sources, adversarially verifying every load-bearing claim, and
  synthesizing the findings with explicit confidence levels. Use this whenever
  the user wants a thorough, multi-source, fact-checked investigation — phrases
  like "deep research", "research X for me", "do a deep dive", "write me a
  report on", "compare all the options for", "what's the state of the art in",
  "investigate", or any question that clearly needs many sources rather than a
  single quick answer. Prefer this over a single web search whenever the user
  signals they want depth, rigor, citations, or a comparison. If the question is
  underspecified (no budget, region, use-case, time horizon, etc.), ask 2-3
  sharp clarifying questions FIRST, then run the workflow with the answers woven
  in.
---

# Deep Research

A harness for producing research reports that are **fast** (parallel
subagents), **credible** (tiered sources + adversarial verification), and
**deep** (a research tree, not a single search). The goal is to beat a generic
"Research" button by being explicit about the three things generic tools skim:
where evidence comes from, how independent it is, and how confident we should be.

## The core idea

One agent searching in a loop is slow and shallow. Instead, an **orchestrator**
(you) decomposes the question into independent lanes and dispatches a swarm of
**researcher subagents** that work the web in parallel. You then run an
**adversarial verification** pass that actively tries to break the key claims,
and only then synthesize. Parallelism is what lets a run be deep *and* fast: 10
lanes explored at once finish in roughly the time of one.

```
        ┌─────────────── ORCHESTRATOR (you) ───────────────┐
        │  scope → decompose → dispatch → gap-check → verify → synthesize
        └───────────────────────────────────────────────────┘
                 │ fan out (parallel, same turn)
   ┌─────────┬───┴─────┬─────────┬─────────┐
   ▼         ▼         ▼         ▼         ▼
 lane 1    lane 2    lane 3   lane 4    lane N      ← researcher subagents
 (search + fetch + extract claims + rate sources, each returns a memo)
   └─────────┴─────────┴────┬────┴─────────┘
                            ▼
              gap & contradiction analysis
                            ▼
            second wave: fill gaps + adversarial verifiers
                            ▼
                  cited synthesis (report)
```

## Before you start: scope it

Do NOT fan out on a vague question — you'll waste the whole swarm. If the
request is missing anything that would change the answer (budget, region, time
horizon, intended use, audience, definition of a key term), ask **2–3 sharp
clarifying questions first**, then proceed. If the user said "just go" or the
question is already specific, skip straight to planning. When in doubt, state
the assumptions you're making and proceed rather than stalling.

## Phase 1 — Plan (write a research brief)

Think hard here; a good decomposition is most of the battle. Produce a short
brief, then show the user a one-line plan before spending the swarm:

1. **Restate the question** in one precise sentence, with scope and time frame.
2. **Name the key sub-questions** — the 4–12 things that must be answered for
   the report to be complete. These become your *lanes*. Good lanes are
   **independent** (a researcher can work one without needing another's output)
   and **MECE-ish** (minimal overlap, covering the whole question).
3. **Decide the fan-out width.** Scale to complexity:
   - Quick dive: 3–5 lanes
   - Standard report: 6–10 lanes
   - Sprawling / "compare everything" topic: 10–20+ lanes, possibly in batches
4. **Define "done"** — what claims, numbers, or comparisons the final report
   must contain. This is your checklist for the gap analysis later.

Decomposition patterns that work well: **by sub-topic** (facets of the
question), **by stakeholder/perspective** (proponents vs critics vs neutral
data), **by source type** (academic vs industry vs news vs primary docs), **by
option** (one lane per product/candidate/approach being compared), or **by time**
(historical → current → projected). Pick whichever carves the question into
truly independent pieces.

## Phase 2 — Fan out (the swarm)

Spawn one researcher subagent **per lane, all in the same turn** so they run
concurrently. Each subagent gets the full lane brief and the researcher
protocol. Read `agents/researcher.md` and pass its contents as the subagent
instructions, filling in the lane-specific task.

Key rules for the dispatch:
- **Same turn = parallel.** Launch every lane in one batch of tool calls.
  Sequential dispatch defeats the entire point and makes a 10-lane run 10× slower.
- **Give each lane a tight remit** so two subagents don't fetch the same five
  pages. Tell each one explicitly what it owns and what it should ignore.
- **Demand structured returns, not dumps.** Each researcher returns a compact
  *findings memo* (claims + citations + source ratings + open questions), never
  a wall of raw page text. This keeps your context budget for synthesis.
- For very wide topics, run in **batches** (e.g. two waves of 8) rather than one
  giant simultaneous launch.

## Phase 3 — Gap & contradiction analysis

When the memos return, do NOT jump to writing. Read them as an editor:
- **Cross-check the checklist** from Phase 1 — what's still unanswered or thin?
- **Surface contradictions** — where do two memos disagree on a fact or number?
  Contradictions are signal, not noise; they tell you exactly where to dig.
- **Find single-source claims** that are load-bearing for the conclusion. Any
  claim the report's thesis rests on needs corroboration.

Then dispatch a **second, smaller wave** of subagents to (a) fill the gaps and
(b) resolve the contradictions with targeted searches. Repeat at most once or
twice — diminishing returns set in fast, and the goal is a great report, not an
infinite crawl.

## Phase 4 — Adversarial verification

This is the step generic research tools skimp on, and it's where credibility is
won. For each **load-bearing claim** (the handful the conclusion depends on),
spawn a verifier subagent — or run the pass inline for smaller reports — using
`agents/verifier.md`. The verifier's job is not to confirm; it's to **try to
falsify**: find the strongest counter-evidence, check whether the "independent"
sources actually trace back to one origin, check dates and retractions, and
distinguish primary evidence from someone merely repeating it.

Each load-bearing claim comes out of this pass tagged with a **confidence
level** (see `references/methodology.md`):
- **High** — multiple genuinely independent, credible sources; no serious
  contradiction.
- **Medium** — supported but with thin sourcing, some disagreement, or
  staleness.
- **Low / Contested** — single source, weak source, or active disagreement;
  report it *as* contested rather than picking a side.

## Phase 5 — Synthesize the report

Write the report yourself (don't delegate final synthesis — you hold the whole
picture). Follow `references/report-template.md` exactly. Non-negotiables that
make it credible:

- **Every factual claim carries a citation** to a source that was actually
  fetched. No citation may point to a URL no subagent retrieved. If you can't
  cite it, label it as inference or cut it.
- **Lead with the answer.** The executive summary states the conclusion and its
  overall confidence up front, then the body defends it.
- **Confidence is visible**, inline, on the claims that matter.
- **Contradictions and unknowns get their own section.** A report that admits
  what it couldn't confirm is far more trustworthy than one that papers over
  gaps. Never invent a fact to fill a hole.
- **A sources table** lists every cited source with its credibility tier and
  date, so the reader can audit the foundation.

Save the report as a polished Markdown file (e.g.
`research-<topic>-<date>.md`) and give the user the path. Then offer to go
deeper on any section.

## How this beats a generic "Research" button

| | Generic research | This skill |
|---|---|---|
| Coverage | iterative single-threaded search | parallel lanes → broader, deeper |
| Speed at depth | slow (serial) | fast (concurrent fan-out) |
| Sourcing | mixed, unrated | tiered credibility, primary-first |
| Verification | light | adversarial, tries to falsify |
| Citations | sometimes loose | every claim → a fetched source |
| Honesty | tends to paper over gaps | explicit confidence + unknowns |

## Reference files

- `agents/researcher.md` — the protocol/prompt for each lane subagent. Read and
  pass to every Phase 2/3 researcher.
- `agents/verifier.md` — the adversarial verification protocol for Phase 4.
- `references/methodology.md` — search tactics, source-credibility tiers, the
  independence test, and confidence-level definitions. Read when you need the
  detail behind a step.
- `references/report-template.md` — the exact output structure for Phase 5.

## Environment notes

- **With subagents** (Claude Code, Cowork, SDK): run the full parallel workflow
  above — this is the intended mode and what makes it fast.
- **Without subagents** (e.g. plain Claude.ai): you can't fan out. Run the lanes
  yourself *sequentially* — same brief, same researcher protocol, same
  verification and template — just slower. The rigor survives even when the
  parallelism doesn't.
- Tools assumed: `WebSearch` and `WebFetch` (or equivalents) for the
  researchers, and the `Agent`/subagent tool for fan-out. If web tools are
  unavailable, tell the user — this skill cannot do real research without them.
