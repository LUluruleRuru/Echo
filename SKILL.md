---
name: Echo
description: Use when the user needs to generate a spoken presentation script (pitch, talk, training, proposal, defense, or short-video voice-over) and is at risk of over-researching, building unnecessary frameworks, or writing "slide text" instead of speakable language. Also use when the user's draft sounds too clean, too polite, or detectably AI-generated — lacking the roughness of real human speech.
---

# Voice-Over Script Generation

## Overview

Generate a stage-ready spoken script in the shortest path. **Speak first, write later.** Slides are a byproduct of the script, not the other way around.

## When to Use

- User needs a spoken presentation (pitch, launch, training, proposal, defense, short video)
- User shows signs of over-researching, framework-building, or treating scaffolding as the building
- User's draft sounds like a document being read, not a person talking
- User's language is too clean/formal — detectable as AI-generated

## Core Pattern

Every spoken script follows one arc: **HOOK → GAP → BRIDGE → PROOF → ACTION**

| Beat | Duration | Psychological Function | Rule |
|------|----------|----------------------|------|
| HOOK | **Scene-dependent** — see Attention Budget Table | **Make them lean in** — create curiosity (Curiosity Gap), self-recognition (Identity Anchor), or cognitive shock (Direct Contradiction). Not "get attention." Get *retention*. | Hard cap: establish psychological engagement within the scene's HOOK budget. At 🔴 Extreme: ≤3s. Choose one of the three HOOK modes (see scene-adaptation.md). Never open with fake discovery questions, previews, or background. |
| GAP | **Scene-dependent** — see Attention Budget Table | **Make them feel seen** — identity recognition + responsibility externalization. "Yes, that's me. And it's not my fault." | Hard cap: audience must think "that's me" within the scene's GAP budget. Name a specific, recognizable micro-behavior — not a general problem. |
| BRIDGE | **Scene-dependent** — see Attention Budget Table | **Pay off the curiosity** — resolve the HOOK's suspense. Answer "how?" directly. | Hard cap: answer the HOOK's open question within the scene's BRIDGE budget. One person's journey in ≤3 steps. |
| PROOF | **Scene-dependent** — see Attention Budget Table | **Let them witness** — the audience concludes for themselves. Not "I claim X" — "here, see for yourself." | Hard cap: provide one mentally-replayable interaction or comparison within the scene's PROOF budget. A usage snippet, not a feature list. |
| ACTION | **Scene-dependent** — see Attention Budget Table | **Make ownership feel inevitable** — one impossible-to-fail step + desire to own it. | Hard cap: give one specific, executable action within the scene's ACTION budget. A command, a keyword, a link. Not "try it." |

**Scene adaptation:** See [scene-adaptation.md](scene-adaptation.md) for how each beat shifts across pitch/launch/training/proposal/defense/report/short-video.

## Two Non-Negotiable Rules

### 1. Speak before you write
Record yourself telling the story to a friend. Transcribe. That's draft zero. Anything you can't say naturally doesn't belong in the script. No exceptions.

### 2. Find the tension before you write anything else
Tension = what the audience assumes vs. what you discovered. If you can't name both sides in one sentence each, stop. You're not ready to write.

Before drafting, answer the **tension checklist**:
1. Who's the real enemy? (concrete thing, not abstract concept)
2. Who's the victim, and when do they hurt most?
3. What's the cost? (wasted what? missed what? embarrassed how?)
4. What's the most vivid scene? (one image they'll remember)

## LLM Behavioral Rules

These rules govern the LLM, not the human author.

### Calibrate before executing
Before any research or writing: confirm the exact task ("8-min pitch deck voice-over", not "write a PPT"), duration cap (words = minutes × 250), audience attention state, and what evidence exists. Immediately after confirming the scene:

1. Look up the **Attention Budget Table** in `scene-adaptation.md` and write the per-beat second caps into the working area.
2. Select the **HOOK psychological strategy**: Curiosity Gap / Direct Contradiction / Identity Anchor (see `scene-adaptation.md` HOOK Modes for selection guide per urgency level).
3. Write both the time caps AND the chosen HOOK mode at the top of the draft. These are hard constraints, not suggestions.

### Interrupt on danger signals
Stop and question when: draft 2 reverses draft 1's direction (not polish — pivot), research volume exceeds 2× the estimated final script, 4+ similar sub-tasks in a row, frameworks growing more abstract while drifting from the final medium.

See `scene-adaptation.md` Danger Signal Detection for the full table, including attention-budget-specific signals.

### Beat time budget check (pre-write)
Before drafting any beat, look up the scene in the Attention Budget Table and set hard constraints.

**Execution steps:**
1. Identify scene → look up urgency level and per-beat second caps from the table
2. Convert seconds to character budget: char cap = seconds × 4 (Chinese spoken delivery ≈ 4 chars/s)
3. Confirm the **HOOK psychological strategy** (Curiosity Gap / Direct Contradiction / Identity Anchor)
4. Write the character cap AND psychological function goal for each beat into the working area

**Pre-write calibration template:**
> "Scene: [scene], Urgency: [🔴🟠🟡🟢] [level]. HOOK mode: [Curiosity Gap / Direct Contradiction / Identity Anchor].
> Per-beat caps: HOOK ≤ [N]s/[N]chars (goal: [curiosity / recognition / shock]), GAP ≤ [N]s/[N]chars (goal: "that's me"), BRIDGE ≤ [N]s/[N]chars (goal: resolve suspense), PROOF ≤ [N]s/[N]chars (goal: let them witness), ACTION ≤ [N]s/[N]chars (goal: one impossible-to-fail step).
> Beginning HOOK draft."

### Beat time budget check (post-write)
After completing each beat's draft, run two automatic verifications.

**A. Time check:** count characters ÷ 4, compare against the beat's second cap. If over cap → flag the failure signal from the Failure Conditions table, enter compression mode.

**B. Psychological function check:** against the beat's psychological function goal — did it achieve it?
- HOOK: After the cap, is the audience curious / shocked / self-recognizing? If not → the mechanism is wrong, not just the length. Switch modes.
- GAP: Has a specific, recognizable micro-behavior been named? If the audience could think "that's not me" → add one concrete detail.
- BRIDGE: Has the suspense from HOOK been directly answered? If not → return to the opening question and answer it.
- PROOF: Is there a mentally-replayable interaction? ("You say X. It replies Y.") If not → add one.
- ACTION: Is there one impossible-to-fail step? If it's "try it out" or "contact us" → make it concrete.

**Post-write check template:**
> "[BEAT] draft: [N] chars ≈ [X]s. Cap: [Y]s.
> Time: [✅ / ⚠️ over by Zs]
> Psychological function: [achieved / not achieved — specific failure].
> [If failed: switch mode / add detail / resolve suspense / add interaction / concretize action]."

### Attention-related emergency signals
When attention budget violations are detected, escalate immediately:

| Signal | Level | Response |
|--------|:-----:|----------|
| HOOK word count exceeds scene cap by 2× | 🔴 | "HOOK needs [X]s, audience is gone by [Y]s in this scene. This draft won't be heard to completion. Compress the HOOK before continuing." |
| First two beats combined exceed 1.5× their combined cap | 🔴 | "HOOK+GAP have already consumed [X]s. In [scene], audience patience runs out at [Y]s. The remaining three beats will be compressed to an unworkable length. Cut backwards from HOOK." |
| Any beat exceeds its cap without triggering auto-compression | 🟡 | "This beat is over by [X]s. At [urgency] level this means: [failure signal]. Want me to cut it?" |

### Never sanitize human speech
This is the highest-priority rule for spoken scripts.

- User says "屎上雕花" → keep "屎上雕花". Never "polishing in the wrong direction".
- User says "被迫营业" → keep it. Never "lacking intrinsic motivation".
- User says "刷手机" → keep it. Never "attention fragmentation".

After drafting, run an **AI-odor check**: flag every sentence that's too parallel, too complete, too polite. Break them. Allow fragments. Allow repetition. Human speech is rough — the script should be too.

### User's original words have absolute priority
When the user provides vivid, emotional, specific language — extract the "human skeleton" and preserve its tone. Never "upgrade" user language to standard written form.

## Quick Reference

| Stage | Time | Output |
|-------|------|--------|
| 1. Intake | 10min | 6 constraints confirmed (scene, duration, audience, evidence, exact task, HOOK psychological strategy) |
| 2. Find tension | 20-60min | Tension type + 4-item checklist + ≤30-word core sentence |
| 3. Draft | 1-2hr | Record → transcribe → structure → fill (script first, slides never) |
| 4. Cut to bone | 20-40min | Delete transitions, abstract-without-example, derivable info. Cut 30-50%. |
| 5. Extract slides + prep | 20-30min | ≤1 element per slide. One-sentence fallback. Live checklist. |

## Common Mistakes

| Symptom | Root cause | Fix |
|---------|-----------|-----|
| Script sounds like a document | Wrote slides first, then "translated" to speech | Delete. Record from scratch. |
| Draft 3 reverses draft 2's direction | Core narrative decision wasn't made before drafting | Stop. Lock the tension first. |
| Research is 5× the script length | Research became the goal instead of the means | Cap at 1.5× final script word count. |
| Language is too clean, detectably AI | LLM sanitized the human voice out | Run AI-odor check. Put the user's rough words back. |
| HOOK starts broad then narrows | Task wasn't specified precisely enough | First sentence must name the exact task. |
| HOOK is correct but no one stays | Delivered information but created no psychological engagement — no curiosity, no recognition, no shock | Switch HOOK modes (Curiosity Gap / Identity Anchor / Direct Contradiction). Information can wait. Engagement can't. |
| Audience agrees but doesn't act | GAP got nods (audience agreed "yes, that's a problem") but never made them feel "that's MY problem" | Add one specific, recognizable micro-behavior. Not "people struggle with X" — "you do Y at 2am." |
| High retention in first half, sharp drop in second | BRIDGE explained the solution but never resolved the HOOK's suspense — audience forgot what they were waiting for | Return to the HOOK's open question and answer it directly before continuing. |
