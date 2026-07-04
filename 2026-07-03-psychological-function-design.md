# Psychological Function Layer for Echo

> Date: 2026-07-03
> Status: Implemented
> Builds on: `2026-07-03-attention-budget-design.md`
> Files affected: `Echo/scene-adaptation.md`, `Echo/SKILL.md`

## Problem

The attention budget system judged scripts by information density — "did the information arrive within the time cap?" A viral short-video script proved this wrong. Its HOOK was 50 chars / 12.5s (4× the 3s cap for 🔴 Extreme), used rhetorical questions ("是怎么实现的呢？") and "你有没有" patterns — all marked as 🔴 forbidden. Yet it was the most popular version.

**Root cause**: The system measured *information delivery speed* but humans stay or leave based on *psychological engagement*. A 12.5s opening that builds curiosity beats a 2.8s opening that delivers information but creates no suspense.

## What Changed

The core assumption flipped: from "every sentence must be an information bomb" to "every sentence must fulfill at least one psychological function."

### Three HOOK Modes

1. **Curiosity Gap**: Known scene + counterintuitive contrast → audience waits for the answer
2. **Direct Contradiction**: Cognitive conflict → audience thinks "why?"
3. **Identity Anchor**: Hyper-specific behavior → audience thinks "that's me"

Curiosity Gap and Identity Anchor have the strongest anti-swipe power. Direct Contradiction gets nods but not necessarily retention.

### Five Beats Redefined by Psychological Function

| Beat | Old | New |
|------|-----|-----|
| HOOK | Make them look up | Make them **lean in** — curiosity, recognition, or shock |
| GAP | Why old ways fail | **Identity recognition** — "you see me" + responsibility externalization |
| BRIDGE | Your solution | **Curiosity payoff** — the answer to "how?" from HOOK |
| PROOF | Evidence | **Witnessing** — let the audience conclude for themselves |
| ACTION | Next step | **Low-barrier ownership** — one impossible-to-fail action + desire |

### Rhetorical Questions: Not All Forbidden

The old rule banned all rhetorical questions. The new rule distinguishes:
- **Forbidden**: Questions that assume a discovery the audience hasn't made ("你有没有发现…")
- **Allowed**: Questions that voice the audience's actual inner monologue ("怎么做到的？")

### Failure Conditions Rewritten

Old: "3s mark and no contradiction yet → swiped away"
New: "3s mark, no curiosity, no recognition, no shock → psychological engagement is zero"

## Implementation Plan

### P0 (Core — must change or system keeps misjudging)
1. Replace Failure Conditions table — "info delay" → "psychological engagement failure"
2. Replace HOOK Compression Rules — three modes + selection guide per urgency
3. Add HOOK psychological strategy to Intake Questions

### P1 (Supporting — reinforce P0)
4. Add psychological engagement row to Urgency Level × Qualitative Signals
5. Add 4 psychological-failure danger signals
6. Rewrite per-sentence rule — "information bomb" → "must fulfill a psychological function"

### P2 (Polish)
7. Add psychological function column to Beat Content by Scene
8. Modify Cut 4 — "attention budget cut" → "psychological function cut"
9. Add positive diagnostic case (viral Nuwa script vs V4)
10. Sync SKILL.md behavioral rules
