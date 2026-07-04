# Attention Budget System for Echo

> Date: 2026-07-03
> Status: Implemented
> Files: `Echo/SKILL.md`, `Echo/scene-adaptation.md`

## Problem

The `scene-adaptation.md` reference labeled HOOK duration as "0-30s" uniformly across all scenes. In practice, a Short Video audience gives the speaker ~1-3 seconds before swiping away — but the LLM saw a 5.5-second opening and considered it within range. The opening lines of generated scripts were too slow: fake rhetorical questions, listing common knowledge, transition words — all burning seconds the audience doesn't have.

**Root cause**: No concept of "attention budget" — how many seconds the audience will give the speaker before tuning out, which varies dramatically by scene type.

**Concrete example**: V4 short-video script opened with "你有没有发现，网上教你写路演 PPT 的东西，基本都对。痛点要尖锐。市场要够大。壁垒要清楚。每页别放太多字。都对。" — 7 sentences, ~17 seconds, before touching the pain point. At 🔴 Extreme urgency, the audience was gone by second 3.

## Design

### Attention Budget Table

Each of the 7 scenes gets a hard per-beat second cap across all 5 beats (HOOK → GAP → BRIDGE → PROOF → ACTION). These are not suggestions — exceeding the cap means the audience has already tuned out.

Four urgency levels: 🔴 Extreme (Short Video), 🟠 High (Pitch), 🟡 Medium (Launch, Proposal), 🟢 Low (Defense, Report, Training).

### Qualitative Signals

Each urgency level carries: psychological reality, audience state, cost of failure, per-sentence rule, definition of filler, and cut target from first draft (60% → 20%).

### Failure Conditions

A 4×5 matrix: for each urgency level × beat, a specific failure signal the LLM must flag when the beat exceeds its cap. Example: 🔴 Extreme HOOK over cap → "3s mark and no contradiction yet → swiped away. Delete every fake 'have you noticed…' question."

### Behavioral Rules (SKILL.md)

Three new LLM rules:
1. **Pre-write budget check**: Before drafting any beat, look up the scene's caps and write them as hard constraints
2. **Post-write budget check**: After each beat, verify both time (chars ÷ 4 vs cap) and quality (per-sentence rule compliance)
3. **Attention emergency signals**: Escalate when HOOK exceeds 2× cap, first two beats exceed 1.5× combined cap, or any beat over cap without auto-compression

### Diagnostic Case

V4 opening failure documented in `scene-adaptation.md` as a concrete anti-pattern: per-sentence diagnosis, root cause analysis, the fix, and four lessons learned.

## Integration

- `scene-adaptation.md`: New Attention Budget System section (top), expanded Danger Signal Detection, new Cut 4 in Cut-to-Bone, Diagnostic Case appendix
- `SKILL.md`: Core Pattern table changed from fixed durations to "Scene-dependent — see Attention Budget Table", Calibrate rule updated, three new behavioral rules added
