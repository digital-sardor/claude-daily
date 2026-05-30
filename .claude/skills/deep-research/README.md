# deep-research skill

A Claude skill for producing **fast, credible, deep** research reports — designed
to outperform a generic one-click "Research" feature.

## What it does

Given a research question, it:

1. **Scopes** the question (asks 2–3 clarifying questions if it's vague).
2. **Decomposes** it into independent *lanes* — a research tree.
3. **Fans out** a swarm of researcher subagents that work the lanes **in
   parallel**, each searching the web, fetching primary sources, extracting
   claims, and rating source credibility.
4. **Analyzes gaps & contradictions**, then sends a second targeted wave.
5. **Adversarially verifies** every load-bearing claim — actively trying to
   *falsify* it, checking source independence, recency, and primary-source backing.
6. **Synthesizes** a fully-cited report with visible confidence levels and an
   honest "what we couldn't confirm" section.

Parallelism is the trick: exploring 10+ lanes at once makes a deep run *fast*
(this is the "108 agents in 8 minutes" pattern).

## Why it's more credible than a generic research tool

| | Generic research | This skill |
|---|---|---|
| Speed at depth | serial, slow | concurrent fan-out, fast |
| Sourcing | mixed, unrated | tiered (primary-first), dated |
| Verification | light | adversarial — tries to disprove |
| Citations | sometimes loose | every claim → a fetched source |
| Honesty | papers over gaps | explicit confidence + unknowns |

## Files

```
deep-research/
├── SKILL.md                      # the orchestration workflow (entry point)
├── agents/
│   ├── researcher.md             # prompt/protocol for each parallel lane
│   └── verifier.md               # adversarial verification protocol
└── references/
    ├── methodology.md            # decomposition, search tactics, credibility tiers, confidence
    └── report-template.md        # exact output structure
```

## How to use it

The skill triggers automatically when you ask for a deep dive, a report, a
comparison, or "research X for me". Or invoke it explicitly: **`/deep-research`**.

Examples that trigger it:
- "Do deep research on the state of solid-state battery commercialization."
- "Research the best self-hosted password managers for a small team and write me
  a report."
- "Compare GLP-1 drugs on efficacy, side effects, and cost — cited."

**Best in an environment with subagents** (Claude Code, the SDK, Cowork), where
the parallel fan-out runs at full speed. Without subagents it still works — the
lanes just run sequentially. It requires web search + fetch tools to do real
research.

## Installation

It lives at `.claude/skills/deep-research/` in this repo, so it's available in
any Claude Code session opened here. To use it elsewhere, copy the
`deep-research/` folder into that project's `.claude/skills/` (or your global
`~/.claude/skills/`).
