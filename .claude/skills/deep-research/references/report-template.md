# Report template

The exact structure for the Phase 5 synthesis. Adapt section depth to the topic,
but keep the order and the non-negotiables (citations on every claim, visible
confidence, a contradictions/unknowns section, and a sources table).

Use inline citation markers like `[S3]` that resolve to the sources table at the
bottom. Put a confidence tag — **(High)** / **(Medium)** / **(Contested)** — on
the claims the conclusion depends on.

---

```markdown
# <Report title: the question, answered as a statement>

*Researched <date> · <N> sources across <M> lanes · Overall confidence: High/Medium/Low*

## Executive summary

<3–6 sentences. State the answer FIRST, then the overall confidence and the one
or two reasons that drive it. A reader who stops here should already have the
conclusion and know how much to trust it.>

**Bottom line:** <one sentence — the single most important takeaway>

## Key findings

- **<Finding 1, stated precisely with numbers/dates>** (High) — <one line of
  support> [S1][S4]
- **<Finding 2>** (Medium) — <support; note the weakness that makes it Medium> [S2]
- **<Finding 3>** (Contested) — <both sides, briefly> [S5][S7]
- ...

## <Body section 1 — e.g. a sub-topic, an option, a perspective>

<Prose that develops the findings with evidence. Every factual sentence carries
a citation. Walk the reader from evidence to conclusion rather than asserting.
Quote or give specific numbers where precision matters.>

## <Body section 2 …>

<As many body sections as the decomposition needs — typically one per major lane
or option. For comparisons, a table is often the clearest form:>

| Option | <criterion> | <criterion> | <criterion> | Verdict |
|---|---|---|---|---|
| A | … [S2] | … [S3] | … | … |
| B | … [S6] | … [S6] | … | … |

## Contradictions, caveats & what we couldn't confirm

<The trust-building section. List, honestly:
- where credible sources disagree, and how (don't resolve a genuine dispute by fiat)
- claims that rest on a single or weak source
- questions that stayed open after the gap-filling wave
- anything time-sensitive that may already be changing
Never fill a gap here with a guess — name the gap.>

## Recommendation / outlook  *(if the question asked for one)*

<The actionable answer, conditioned on the user's stated constraints. If the
honest answer is "it depends", say what it depends on and give the decision rule.>

## Sources

| ID | Source | Tier | Date | Note |
|---|---|---|---|---|
| S1 | [<Title>](<URL>) | T1 | <date> | <why it matters / any bias> |
| S2 | [<Title>](<URL>) | T2 | <date> | … |
| … | | | | |

*Tiers: T1 primary/authoritative · T2 reputable secondary · T3 tertiary/weak.*
```

---

## Style notes

- **Lead with the answer**, everywhere — the report, each section, each finding.
  Front-load the conclusion, then defend it.
- **Precision over hedging.** "Grew 23% YoY in 2024 [S2]" beats "grew
  significantly". But where genuine uncertainty exists, name it rather than
  faking precision.
- **No citation, no claim.** If a statement isn't backed by a fetched source,
  either label it explicitly as your inference/synthesis or remove it.
- **Length follows the question.** A focused question gets a tight report; a
  sprawling one earns a long one. Don't pad to seem thorough, and don't compress
  away necessary evidence.
- **Make it skimmable** — bold the load-bearing claims, use tables for
  comparisons, keep the source table complete so the foundation is auditable.
