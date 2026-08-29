# Glean Compass — Drift Detector

A single-file prototype built for a **Glean product management** conversation. It takes one
narrow question — *is the work a team is actually doing still attached to the priorities
they said they had?* — and builds the smallest surface that answers it credibly.

Open `index.html`. No build step, no dependencies, no backend.

```bash
python3 -m http.server 4791 --directory .
```

## The problem it picks

Every company has a Q3 priority list and a Jira board, and by week six they have quietly
come apart. Nobody notices, because noticing requires someone to hold both artifacts in
their head at once. Two failure shapes matter:

- **Orphaned work** — a real, sustained effort with no priority behind it. Thirty-four
  tickets, four engineers, three weeks, linked to nothing on the Q3 list.
- **Stalled priority** — the mirror image. A stated goal with no tickets, PRs, docs or
  threads against it in eighteen days, and an owner field that was never filled in.

Both are invisible to a status report, because a status report is written by the people who
would have to notice.

## The product argument

The prototype exists to defend three positions, and the UI is arranged so each one is
visible rather than asserted.

**1. Precision over recall, deliberately.** The view shows two flags, not forty. A drift
detector that surfaces everything is a second backlog, and a second backlog gets muted in a
week. The bar is set so that a flag is worth the thirty seconds it costs to check — the
Metrics tab makes the resulting precision, coverage and the gap between them explicit rather
than hiding the tradeoff.

**2. Every flag shows its evidence before it asks for a decision.** Each card carries the
raw signal (34 Jira tickets + 6 PRs + 1 design doc, all tagged `billing-v2`), the best
semantic match and its score (0.28, below the 0.60 bar), and whether any explicit link
exists. The reviewer is never asked to trust a number they cannot audit. This is the whole
difference between a tool people act on and a tool people learn to ignore.

**3. Dismissal is training data, not a delete button.** Dismissing a flag requires a reason
— *tracked elsewhere*, *intentionally exploratory*, *wrong owner*, *too low-priority* — and
those reasons are what tune the detector for that team. The alternative, a bare ✕, throws
away the only labelled data the system will ever get for free.

There is also a third option on the resolution path that matters more than it looks: *this
is its own priority — propose adding it*. Sometimes the work is right and the priority list
is wrong, and a tool that can only ever conclude "the work is wrong" will be wrong a lot.

## Metrics & trust

The second tab is the argument that this could ship. It carries flag precision, coverage,
the guardrails that keep the detector from becoming noise, and a staged path from
*suggest-only* to autonomy — the sequence a team would actually need to walk before letting
something like this act without review.

## What it is not

A working detector. The semantic scores, ticket counts and metrics are authored to make the
decision structure legible and defensible in conversation. The point on display is the
product judgment — where the precision bar sits, what a flag must show before it earns a
decision, and what dismissal is for — not an implementation.
