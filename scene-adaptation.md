# Scene Adaptation Reference

> Supporting reference for `Echo`. Load only when implementing.
> **v2.0** — Added attention budget system. Every scene now carries hard time constraints per beat, qualitative urgency signals, and failure conditions.

---

## Attention Budget System

### Beat Time Budgets by Scene

Each beat must deliver its core payload within the listed second cap. These are not "suggested durations" — exceeding the cap means the audience has already tuned out.

| Scene | Urgency | HOOK ≤ | GAP ≤ | BRIDGE ≤ | PROOF ≤ | ACTION ≤ |
|-------|:------:|:------:|:-----:|:--------:|:-------:|:--------:|
| Short Video | 🔴 Extreme | **3s** | 20s | 80s | 120s | 150s |
| Pitch / Roadshow | 🟠 High | **10s** | 90s | 300s | 420s | 480s |
| Product Launch | 🟡 Medium | **15s** | 120s | 360s | 480s | 540s |
| Proposal / Bid | 🟡 Medium | **20s** | 150s | 480s | 720s | 840s |
| Defense / Review | 🟢 Low | **20s** | 180s | 600s | 900s | 1020s |
| Status Report | 🟢 Low | **25s** | 180s | 600s | 900s | 1050s |
| Training | 🟢 Low | **30s** | 180s | 900s | 1500s | 1650s |

**Word count conversion**: Chinese spoken delivery ≈ 4 characters/second. Multiply the second cap by 4 to get the character budget for each beat. Example: Short Video HOOK ≤ 3s → ≤ 12 characters.

### Urgency Level × Qualitative Signals

| | 🔴 Extreme | 🟠 High | 🟡 Medium | 🟢 Low |
|------|---------|--------|--------|--------|
| **Psychological reality** | Thumb hovering over the screen, ready to swipe | Already sat through 7 pitches, running out of patience | Willing to give you some time, but won't wait for you to warm up | Present and attentive, but will drift if bored |
| **Audience state** | Did not come looking for you — the algorithm pushed you here | Forced to attend, scanning for "which one is worth looking up for" | Voluntarily here, but expectations are low | Required to be here, with a task to complete |
| **Cost of a failed opening** | 0.5s hesitation = swipe away = they will never see you again | First 10s didn't grab them → your project is filed as "just another one" | First 15s circling → they start checking their phone | First 25s without substance → they start doing their own work |
| **Per-sentence rule** | Every sentence must fulfill at least one psychological function: create curiosity, build identity recognition, voice the audience's inner monologue, reveal a contradiction, deliver concrete information, or drive action. No sentence is allowed to merely "set up" — setup is not a psychological function. | Every sentence must either advance the story OR deepen the audience's sense of "this matters to me." One transition allowed. Two consecutive sentences without psychological function = stop. | Every paragraph must have a clear "why I'm telling you this." Two warm-up sentences allowed at paragraph start only. | Every section must be traceable to a value for the audience. Normal rhythm allowed, but no section may lack a "what the audience should do/think/feel differently after this" anchor. |
| **Definition of "filler"** | Anything the audience already knows. Any preview of "what you'll talk about." Any adjective. | Any complete subject-verb-object sentence without concrete information. Any sentence that can be deleted without affecting comprehension. | Any example unrelated to the core argument. Any transition longer than one sentence. | Any information the audience doesn't need to act on. |
| **Psychological engagement requirement** | HOOK must create active retention — audience is waiting for an answer (Curiosity Gap) or recognizing themselves (Identity Anchor). GAP must produce "yes, that's me." Every beat must earn the next beat's attention. | HOOK must make investors lean forward — one person + one struggle. GAP must prove the blind spot is shared and overlooked. BRIDGE must deliver the "how" payoff. | HOOK must answer "why should I care" within the cap. Audience is voluntary but skeptical — give them a reason to stay before giving them information. | HOOK must justify the audience's time — a counterintuitive data point, a "you think you know but…" moment. Normal rhythm is fine, but no section can lack a clear "why I'm telling you this." |
| **Success signal** (what the audience is thinking) | "How??" or "That's me." — active, forward-leaning attention | "I haven't heard this angle before." — intellectual engagement | "This is relevant to me." — relevance acknowledged | "I need to know this." — value recognized |
| **Cut target from first draft** | Cut **60%** | Cut **40%** | Cut **30%** | Cut **20%** |

### Failure Conditions by Urgency Level

When a beat exceeds its time cap, the LLM must check whether the beat's **psychological function** has been achieved — not just whether information was delivered. If the function is unmet, flag the corresponding failure signal.

| Urgency | HOOK over cap | GAP over cap | BRIDGE over cap | PROOF over cap | ACTION over cap |
|--------|--------------|-------------|----------------|---------------|----------------|
| 🔴 Extreme | "3s mark — no curiosity, no shock, no self-recognition → swiped away. Psychological engagement is zero. Check: did you create a curiosity gap? Give a cognitive shock? Name a specific behavior the audience recognizes as their own? If none of the three — delete and rewrite with one of the three HOOK modes." | "20s — audience hasn't thought 'yes, that's me.' The problem isn't that the pain isn't real — it's that you haven't named a specific, slightly embarrassing, daily micro-behavior they recognize. Stop analyzing. Give one detail." | "80s — the suspense from HOOK hasn't been resolved. The audience forgot why they were waiting. Return to the opening contradiction and answer it directly: 'Here's how.'" | "120s — no moment the audience can mentally 'replay.' No usage snippet, no concrete dialogue, no simulated experience. The audience can't judge for themselves — so they don't believe. Give one specific interaction: 'You say X. It replies Y.'" | "150s — no concrete action yet. Not 'try it out' — a command they can type, a search keyword, a one-click link. Without this, zero conversion." |
| 🟠 High | "10s mark — no concrete person, no struggle → drifting. The opening must be one person + one specific dilemma. Never 'in the X billion dollar market…' Check: have you named a person yet?" | "90s — still listing competitors, still laying background. The audience doesn't know 'what this has to do with me.' Stop. Give one specific victim scene." | "5min — journey still unfinished. Not too much info — the journey itself isn't linear enough. One person. One change. Three steps. No more." | "7min — haven't admitted a limitation → trust isn't built. The audience's 'hype radar' is on. State the data's weakness first. Then give the data." | "8min — haven't returned to the person from the opening → emotional thread broken. What happened to that person? Close the loop." |
| 🟡 Medium | "15s — audience still doesn't know 'what this has to do with me.' Not an information shortage — the connection hasn't been made. Is there a specific scene the audience can recognize?" | "2min — still setting up → relevance hasn't been proven. If the audience can still think 'this isn't about me,' the HOOK's engagement has leaked. Prove this concerns them now." | "6min — solution is unfolding but hasn't produced an 'oh, that's how' moment. The method itself isn't surprising enough. Find the one counterintuitive insight." | "8min — no concrete, imaginable evidence. No case, no image, no dialogue. The audience can't judge truth for themselves. Give one." | "9min — next step too abstract. 'Contact us' is weaker than 'send an email tomorrow to X with subject line Y.' Give the exact action." |
| 🟢 Low | "25s — topic still hasn't landed. Say directly: here's the problem we're solving today. Not an agenda. A problem statement." | "3min — still on background. If the audience doesn't know why this matters to them by now, they're gone. Summarize the premise in one sentence and move on." | "15min — core method hasn't arrived → efficiency break. Give one-sentence summary + three-step breakdown. Now." | "25min — no self-test, no checklist, nothing the audience can 'try themselves.' After 25 minutes of listening, they haven't been asked to actively participate once." | "28min — no summary → scattered. What are the three things they should remember walking out? No more than three." |

---

## Scene-Specific Beat Adaptation

### Beat Content by Scene

Each beat has both a **content goal** (what to say) and a **psychological function** (what to make the audience feel/think).

| Scene | Beat | Content | Psychological Function |
|-------|------|---------|----------------------|
| Pitch/Roadshow | HOOK | One user's concrete struggle | Curiosity Gap — "what happened to this person?" |
| | GAP | Competitors' shared blind spot (categorize, don't name) | Identity Recognition — "my project also missed this" |
| | BRIDGE | Our solution as one user journey | Curiosity Payoff — "so that's how it works" |
| | PROOF | Early data + honest limits | Witnessing — investor judges for themselves |
| | ACTION | Return to user + funding ask | Low-barrier Ownership — one meeting, one intro |
| Product Launch | HOOK | A "making-do" daily routine | Identity Anchor — "I do that every day" |
| | GAP | Hidden cost of the workaround | Recognition + externalization — "not my fault this is the best option" |
| | BRIDGE | How the new thing solves it completely | Curiosity Payoff — "finally, something that works" |
| | PROOF | Demo / specs / side-by-side | Witnessing — let them see the difference |
| | ACTION | Availability + try now | Low-barrier Ownership — one click, one store |
| Training | HOOK | An "I thought I knew this" moment | Identity Anchor — "I would have made that mistake" |
| | GAP | Why everyone gets stuck here | Recognition + externalization — "nobody taught me the key step" |
| | BRIDGE | Correct method, broken into steps | Curiosity Payoff — "oh, that's the missing piece" |
| | PROOF | Exercise / self-check | Witnessing — they try it and see themselves fail/succeed |
| | ACTION | Where to start + common traps | Low-barrier Ownership — "start with step 1, avoid trap A" |
| Proposal/Bid | HOOK | Cost the client is silently bearing | Direct Contradiction — "you're losing money and didn't know" |
| | GAP | Why this cost is avoidable | Recognition + externalization — "not a failure, just never had a specialized solution" |
| | BRIDGE | Solution + implementation path | Curiosity Payoff — "here's how we fix it" |
| | PROOF | Similar case / ROI estimate | Witnessing — "this comparable client saved X" |
| | ACTION | Next step + minimum start cost | Low-barrier Ownership — "start with this small commitment" |
| Defense/Review | HOOK | The sharpest criticism | Direct Contradiction — naming the criticism before they do |
| | GAP | Why the criticism is actually reasonable | Recognition — "I understand the concern, it's valid" |
| | BRIDGE | How the design already accounted for this | Curiosity Payoff — "the design anticipated this" |
| | PROOF | Experiment / data / logic chain | Witnessing — "here's the evidence, judge for yourself" |
| | ACTION | Boundary of work + future direction | Low-barrier Ownership — "here's what this means going forward" |
| Status Report | HOOK | One counter-intuitive data point | Direct Contradiction — "the number says X, but actually Y" |
| | GAP | Surface reading vs. real signal | Recognition — "you would have read this wrong too" |
| | BRIDGE | Deep analysis + discovery | Curiosity Payoff — "here's what's actually happening" |
| | PROOF | Cross-validation / ruled-out alternatives | Witnessing — "we checked these other explanations, they don't hold" |
| | ACTION | Recommendation + resources needed | Low-barrier Ownership — "one decision, one resource ask" |
| Short Video | HOOK | One "wait, what?" fact or scene — delivered via Curiosity Gap or Identity Anchor. Never Direct Contradiction alone. | **Curiosity** ("how??") or **Self-recognition** ("that's me"). Active retention required. |
| | GAP | "You've been told X. Reality is Y." + one specific recognizable micro-behavior. | **Identity Recognition** — "yes, that's my life." Must name a concrete, slightly embarrassing detail. |
| | BRIDGE | One method, one example. A single person's journey in ≤3 steps. Must answer the HOOK's suspense. | **Curiosity Payoff** — resolve "how?" from the opening. |
| | PROOF | Before/after or real interaction snippet. One pair, not a gallery. Let the audience mentally simulate using it. | **Witnessing** — "I can picture myself doing this." |
| | ACTION | One specific action (command, keyword, link) + one expansion of desire ("you could also distill yourself"). | **Low-barrier Ownership** — one impossible-to-fail step + imagination of owning it. |

### HOOK Modes: Three Ways to Build Psychological Engagement

The goal of a HOOK is not to deliver information — it's to make the audience **lean in**. One of three psychological mechanisms must fire within the time cap. Information can wait. Engagement can't.

#### Mode 1: Curiosity Gap

**Mechanism**: A scene the audience already knows + a counterintuitive contrast = suspense. The audience waits for the answer and won't swipe away.

**Structure**: Known scene → unexpected twist → pause (let curiosity build)

**Example** (Short Video, Nuwa promo):
```
巴菲特一顿饭，62万美金。
我跟巴菲特聊了一天，零。
```
→ Known scene (Buffett lunch $620K) + contrast (you paid $620K vs I paid $0) = curiosity gap wide open. Audience inner monologue: "How?" You don't need to ask the question — they already did.

**Anti-swipe power**: 🟢 Strongest — audience is actively waiting for the answer.

**Risk**: If the "known scene" isn't actually known to the target audience, curiosity doesn't ignite. Buffett's lunch price is a viral meme — that's why it works. Match the reference to actual audience knowledge.

#### Mode 2: Direct Contradiction

**Mechanism**: A logical conflict delivered immediately → cognitive tension. Audience thinks "Why is that?" Not suspense — intellectual friction.

**Structure**: Statement A → statement that contradicts A's expected outcome

**Example** (Short Video, pptskill promo):
```
搜了一堆方法论。
还是不会写。
```
→ Logical contradiction (more methods → should help → actually doesn't) = cognitive friction. Audience thinks "True" but isn't necessarily waiting for anything.

**Anti-swipe power**: 🟡 Medium — gets nods but not necessarily retention. The audience agrees but can leave anytime.

**Best for**: Opinion-driven topics, methodology, critique. Scenes where the audience already has the problem and needs it named.

#### Mode 3: Identity Anchor

**Mechanism**: A hyper-specific, slightly embarrassing behavior the audience immediately recognizes as their own. "That's me."

**Structure**: One sharply observed micro-behavior → audience self-inserts

**Example** (Short Video):
```
你在 B 站搜"AI 工具推荐"。
收藏夹里塞了 200 个视频。
一个都没看。
```
→ No contradiction, no suspense — but precise self-recognition. Audience thinks "How do you know that" and stays to find out who's talking about them.

**Anti-swipe power**: 🟢 Strong — but only if the behavior is precisely matched to the target audience. If the scene is off, the anchor fails completely ("that's not me" → swipe).

**Best for**: Vertical audiences, clear personas, pain-point-driven topics.

#### Mode Selection by Urgency

| Urgency | Recommended Mode | Why | Avoid |
|---------|-----------------|-----|-------|
| 🔴 Extreme | Curiosity Gap or Identity Anchor | Algorithm-pushed traffic. Must earn every millisecond of attention. Both modes create active retention — waiting for answer or waiting to be exposed. | Direct Contradiction (too cold — no suspense to anchor attention) |
| 🟠 High | Curiosity Gap | Investors have heard 7 pitches. A person + struggle + counterintuitive outcome makes them lean forward. | Identity Anchor (investors don't need to "feel seen" — they need to spot an opportunity) |
| 🟡 Medium | Curiosity Gap + scene imagery, or Direct Contradiction | Audience is voluntary but skeptical. Curiosity works if the scene is relatable. Contradiction works if the claim is sharp. | Identity Anchor (audience may not share a single identity) |
| 🟢 Low | Direct Contradiction or Identity Anchor | These audiences are required to be there. Direct contradiction (a counterintuitive data point) justifies their time. Identity anchor ("you think you know this, but…") works for training. | Curiosity Gap (can feel like showmanship in serious settings) |

#### Combination Patterns

| Combo | How | Best Scene |
|-------|-----|-----------|
| Curiosity Gap → Identity Anchor | Open with suspense ("62万 vs 0"), follow with recognition ("你有没有遇到…" — but only if the audience genuinely has). The strongest two-punch. | Short Video |
| Identity Anchor → Curiosity Gap | "You do X. But what if Y?" — recognition first, then suspense. Also very strong. | Short Video, Training |
| Direct Contradiction standalone | Best when the contradiction IS the entire value proposition. Don't combine — let it land. | Pitch, Proposal, Report |

#### Forbidden Opener Types (All Urgency Levels)

These patterns fail because they assume engagement rather than earning it:

- **Fake discovery questions**: "Have you noticed…" / "你有没有发现" — the audience hasn't noticed. You lose trust on sentence one.
- **Preview/Agenda**: "Today I'll talk about…" — no reason to care yet. Earn attention first, then explain what you're doing.
- **Background/Context**: "With the development of…" / "In today's competitive landscape…" — no human has ever been hooked by context.
- **Dictionary definitions**: "X is defined as…" — if they wanted a definition they'd search it.

**Exception for rhetorical questions**: Questions that voice the audience's actual inner monologue ARE allowed. "怎么做到的？" after presenting a $620K vs $0 contrast — the audience IS asking this. The distinction: **does the question voice what the audience is actually thinking right now?** If yes → allowed. If no → fake question, delete.

| Allowed rhetorical question | Forbidden rhetorical question |
|---------------------------|----------------------------|
| Audience has just seen a contradiction and is genuinely wondering "how?" → voice it | Audience hasn't formed the thought yet → you're putting words in their mouth |
| "怎么做到的？" after 62万 vs 0 — audience IS asking this | "你有没有发现…" — audience hasn't discovered anything |
| "真的假的？" after a shocking claim — audience IS skeptical | "你知道为什么吗？" — audience doesn't know and doesn't care yet |

---

## Tension by Scene

| Scene | "Audience assumes" | "You discovered" | Tension type |
|-------|-------------------|------------------|-------------|
| Pitch | "Solutions exist, market is served" | "Everyone skipped the same foundation problem" | Overlooked blind spot |
| Launch | "This need is already met" | "It's met badly. Here's a real fix." | Hack vs. real solution |
| Training | "I roughly know how" | "You're doing it wrong/inefficiently. Here's why." | Illusion of competence |
| Proposal | "This can wait / isn't needed" | "Not doing it costs far more than doing it" | Hidden cost |
| Defense | "Your work has these flaws" | "Those 'flaws' are intentional design. Here's why." | Misunderstanding vs. intent |
| Report | "Numbers look fine" | "This one number hides a signal everyone missed" | Surface vs. substance |

---

## Danger Signal Detection

LLM must interrupt and question when:

| Author behavior | Level | Response |
|----------------|:-----:|----------|
| Deep-diving 4th+ research target | 🔴 | "You've researched N≥4 targets. A spoken script uses 3-5 *categories*, never names. These deep dives won't make the final script. Try categorizing instead?" |
| Building layered frameworks | 🔴 | "This framework helps you think. But an audience can't parse 8 layers in 30 seconds. Keep frameworks in chat history. Ready to write the script?" |
| Requesting "comprehensive report" | 🟡 | "Who's the audience for this report? If it's for you — is a 2-page summary enough? If it's for another medium — what are that medium's constraints?" |
| Draft 2 completely reverses draft 1's direction | 🔴 | "This isn't polishing — it's a pivot. Why was the previous direction abandoned? Can we resolve that narrative question in 10 minutes before rewriting?" |
| Total output exceeds 2× estimated final script | 🔴 | "We've produced ~[X] words. Final script needs ~[Y]. Waste rate may exceed 50%. Let's audit: which content directly enters the script? Which is scaffolding?" |
| Same paragraph revised 4+ times | 🟡 | "Fourth revision on this paragraph. The problem may not be wording — you may not have fully locked what you want the audience to remember from this section. Want to step back and verbalize it first?" |
| Script language is too clean/polished/polite | 🟡 | "This reads correctly but too clean — doesn't sound human. Short-video / spoken scripts need 'rougher' language. Want me to put the author's original words ('屎上雕花', '被迫营业') back in and break up the parallel sentences?" |
| **HOOK word count exceeds scene cap by 2×** | 🔴 | "HOOK needs [X]s, audience is gone by [Y]s in this scene. This draft won't be heard to completion. Compress the HOOK before continuing." |
| **First two beats combined exceed 1.5× their combined cap** | 🔴 | "HOOK+GAP have already consumed [X]s. In [scene], audience patience runs out at [Y]s. The remaining three beats will be compressed to an unworkable length. Cut backwards from HOOK." |
| **Any beat exceeds its cap without triggering auto-compression** | 🟡 | "This beat is over by [X]s. At [urgency] level this means: [failure signal]. Want me to cut it?" |
| **HOOK delivers information but creates no psychological engagement** | 🔴 | "The HOOK says things the audience could process. But none of them create curiosity, self-recognition, or shock. The audience isn't waiting for anything. Rewrite: pick one of the three HOOK modes and build the opening around it." |
| **GAP analyzes the problem but never makes the audience feel seen** | 🔴 | "GAP explains the problem correctly. But the audience hasn't felt 'that's me.' Add one specific, slightly embarrassing, instantly recognizable micro-behavior. Not 'people struggle with X' — 'you do Y at 2am and hate yourself for it.'" |
| **BRIDGE explains the solution but never resolves the HOOK's suspense** | 🟡 | "The audience was waiting for an answer to the HOOK's contradiction. BRIDGE gave them features. Return to the opening question and answer it directly before continuing." |
| **Script language is detectably clean — no human texture** | 🔴 | "This script reads like it was written by a language model trained to be inoffensive. Every sentence is complete. Every word is polite. No human talks like this. Break three sentences into fragments. Put one coarse word back. Add one place where the speaker hesitates." |

🟡 = question and confirm · 🔴 = must interrupt and block

---

## AI-Odor Detection Checklist

After every draft, check for these signals of AI-generated language. Each found → replace with rougher, shorter, more human equivalent.

- [ ] Parallel sentences in groups of 3+ → keep one, break the rest
- [ ] "首先……其次……最后……" → delete structure words, say the content directly
- [ ] "这一现象揭示了……" → "说白了就是……"
- [ ] "我们需要重新审视……" → "得换个法子"
- [ ] "该方法在多个场景中得到验证" → "我们试过，确实管用"
- [ ] Every sentence is subject-verb-object complete → allow fragments, repetition, half-sentences
- [ ] Emotion words translated to judgment words ("最搞笑的是" → "值得注意的是") → restore original emotion
- [ ] Slang/coarse language cleaned up → restore original ("屎上雕花" stays "屎上雕花")

---

## Stage Detail: Intake Questions

Before any substantive work, answer all five:

```
A. Scene: [pitch / launch / training / proposal / defense / report / short-video / other]
B. Duration: [X] minutes → word cap = X × 250
C. Audience: who are they? What attention state? (8th pitch of the day? Post-lunch slump? Voluntarily here?)
D. Evidence: idea only? prototype? early data? scaled validation?
E. Exact task: NOT "write a PPT" → MUST be "8-min investor pitch voice-over" / "5-min client proposal" / "2.5-min short video"
F. HOOK psychological strategy: [Curiosity Gap / Direct Contradiction / Identity Anchor] — what mechanism will make the audience lean in within the first [scene HOOK cap] seconds?
```

After answering all five, immediately look up the scene in the **Attention Budget Table** and write the beat time caps into the working area. These are hard constraints for every beat that follows.

---

## Stage Detail: Cut-to-Bone Operations

LLM must execute all three cuts without waiting for the author to ask:

**Cut 1: Delete transitions.** Search and remove: "众所周知" / "随着……的发展" / "从本质上讲" / "接下来我要讲" / "前面我们提到" / "综上所述". If a breath is needed, mark `[停2秒]` — don't fill with filler words.

**Cut 2: Every abstraction must have a concrete anchor.** Scan every paragraph. For each abstract claim without a "比如/例如/想象一下/一个真实案例" following it — either add the example or delete the claim.

**Cut 3: Delete derivable information.** If the audience can figure it out themselves, delete it. Keep only what they can't derive: your discovery, your data, your case, your perspective.

**Cut 4: Psychological function cut.** After cuts 1-3, run the psychological function check per beat. For each beat, ask not "is it short enough?" but "did it achieve its psychological function?"

- HOOK: After the time cap, is the audience curious, shocked, or self-recognizing? If not → the opening has the wrong mechanism, not just the wrong length. Switch HOOK modes.
- GAP: Has the audience felt "that's me"? If not → add one concrete micro-behavior they recognize. Not analysis. Detail.
- BRIDGE: Has the suspense from HOOK been resolved? If not → answer the opening question directly. "Here's how."
- PROOF: Can the audience mentally "replay" a specific interaction? If not → add one concrete usage snippet. "You say X. It replies Y."
- ACTION: Is there one impossible-to-fail step? If not → add the exact command, keyword, or action. Not "try it." Not "contact us."

Then apply the urgency-level cut target (% to delete from first draft). At 🔴 Extreme, cut 60% — but cut the sentences with the weakest psychological function, not necessarily the most words.

**Target:** Delete 30-60% of first draft word count, scaled by urgency level. If it feels "too thin" after cutting — the first draft was under-filled, not over-cut. Add examples, not filler.

---

## Diagnostic Case: Why V4's Opening Failed (Short Video, 🔴 Extreme)

### What was written

```
① "你有没有发现，网上教你写路演 PPT 的东西，基本都对。"  (22 chars ≈ 5.5s)
② "痛点要尖锐。"                                              (5 chars)
③ "市场要够大。"                                              (5 chars)
④ "壁垒要清楚。"                                              (5 chars)
⑤ "每页别放太多字。"                                           (7 chars)
⑥ "都对。"                                                    (2 chars)
⑦ "但真到你自己要写那 8 分钟的时候——还是不会。"                 (20 chars ≈ 5s)
```

**From "你有没有发现" to "还是不会": 7 sentences, ~17 seconds, before touching the pain point. In a Short Video (🔴 Extreme, HOOK ≤ 3s), the audience swiped away at second 3.**

### Per-sentence diagnosis

| # | Chars | Cumulative | Diagnosis | Verdict |
|---|-------|-----------|-----------|---------|
| ① | 22 | 5.5s | "你有没有发现" — fake question. The audience hasn't discovered this. First second loses trust. | 🔴 Delete |
| ②③④⑤ | 22 | +5.5s | Common knowledge the audience already has. At 🔴 Extreme, anything the audience already knows = filler. | 🔴 Delete |
| ⑥ | 2 | +0.5s | "都对" — transition word, zero information gain. | 🔴 Delete |
| ⑦ | 20 | +5s | **This is where the HOOK should have started.** But it's 16.5 seconds too late. | 🟡 Keep — but only after cutting everything before it |

### What went wrong in the process

The existing `scene-adaptation.md` labeled HOOK as "0-30s" uniformly. The LLM saw a 5.5s opening and considered it within range. Under the new attention budget system, Short Video HOOK is capped at **3s / 12 chars** — the LLM must recognize before drafting that the very first sentence as written cannot survive the cap, and compress automatically.

### The fix (≤ 3s, ≤ 12 chars)

```
第1天，你搜了一堆路演方法论。
第5天，你还是不会写。
```

Comparison:

| Dimension | Before | After |
|-----------|--------|-------|
| Characters to reach the contradiction | ~76 chars | ~22 chars (contradiction appears by char 10) |
| Seconds to reach pain point | ~17s | ~2s |
| Information structure | "Have you noticed… all correct… but…" — circling | "Day 1 X → Day 5 still X" — direct contradiction |
| 🔴 Extreme per-sentence rule compliance | Violates: every sentence is setup, not an information bomb | Complies: every sentence delivers new knowledge or contradiction |

### What this case teaches

1. **At 🔴 Extreme, never open with a question the audience hasn't asked.** "你有没有发现" is a fake question. Replace with a statement of contradiction.
2. **Never list what the audience already knows.** "痛点要尖锐 / 市场要够大 / 壁垒要清楚" is common sense. At any urgency level above 🟢 Low, this is filler.
3. **Transition words cost seconds you don't have.** "都对" is two characters — but in a 3-second HOOK, two characters is 0.5 seconds you cannot afford.
4. **The real HOOK is always one sentence later than you think.** Find the first sentence that contains a contradiction or a concrete person. Delete everything before it.

---

## Diagnostic Case: Why the Viral Nuwa Script Worked (Short Video, 🔴 Extreme)

This script became the most popular version despite — or because of — violating the original attention budget rules. It proves that psychological engagement, not information density, determines retention.

### What was written (HOOK)

```
段永平请巴菲特吃一顿饭，花了60多万美金。
我今天和巴菲特聊了一天，一分钱都没花。
是怎么实现的呢？
```

**50 characters, ~12.5 seconds. 4× the 🔴 Extreme HOOK cap of 3 seconds. Under the old rules: ❌ fail — background setup + rhetorical question. Under the new rules: ✅ pass — Curiosity Gap mode.**

### Why it worked: per-sentence psychological function

| # | Sentence | Chars | Cumulative | Psychological Function | Verdict |
|---|---------|-------|-----------|----------------------|---------|
| ① | "段永平请巴菲特吃一顿饭，花了60多万美金" | 19 | ~5s | **Known scene activation** — the Buffett lunch price is a viral meme. Instant recognition. Audience thinks "I know this story." | ✅ Scene setter — establishes shared ground |
| ② | "我今天和巴菲特聊了一天，一分钱都没花" | 18 | +4.5s | **Curiosity Gap opens** — $620K vs $0. The contrast is immediate and personal ("I" vs "段永平"). Audience inner monologue activates: "How??" | ✅ Core curiosity trigger |
| ③ | "是怎么实现的呢？" | 7 | +1.7s | **Inner monologue voicing** — the audience IS asking this. Not a fake question. This is the question the audience already formed at sentence ②. Voicing it creates participation: "Yes, tell me." | ✅ Participation, not fake discovery |

**At ~2 seconds (mark "我今天和…"), curiosity is already active. At ~12.5 seconds, curiosity is at peak — the audience is leaning IN, not swiping away.**

### Why the old rules would have killed this

| Old Rule | What it would have said | Why that's wrong |
|----------|----------------------|------------------|
| "Every sentence must be an information bomb" | Sentence ① is background, not an information bomb. ❌ Delete. | Sentence ① activates shared knowledge — a prerequisite for the Curiosity Gap. Without it, the contrast in ② has no anchor. |
| "Rhetorical questions are forbidden" | "是怎么实现的呢？" is a rhetorical question. ❌ Delete. | This question voices what the audience is already thinking. It creates participation, not fake engagement. |
| "HOOK must deliver contradiction within 3s" | The contradiction only appears at sentence ② (~9.5s in). ❌ Too slow. | Curiosity was established before the contradiction was fully revealed. The setup sentence ① is doing psychological work: "I know this story → what's the twist?" |

### What this case teaches

1. **Psychological engagement can start before the contradiction.** "段永平请巴菲特吃饭" activates recognition — the audience is already oriented. The contradiction ("62万 vs 0") lands harder because the setup primed the audience to expect a normal Buffett story, not a free one.

2. **Curiosity Gap is the strongest anti-swipe mechanism.** The audience is actively waiting for an answer. They won't swipe away while a question is open in their mind. Information bombs make them nod; Curiosity Gaps make them wait.

3. **A rhetorical question that voices the audience's actual inner monologue is not a fake question.** The test: "Is the audience actually asking this right now?" After seeing 62万 vs 0, the answer is yes. After "你有没有发现…", the answer is no — the audience hasn't discovered anything.

4. **Speed of information ≠ speed of engagement.** This HOOK takes 12.5 seconds but engages at second 2. V4's HOOK took 17 seconds and engaged at second 0 (it never did). The difference isn't length — it's psychological mechanism.

### Comparison: Viral vs V4 (both ~12s into the script)

| | V4 (failed) | Viral (succeeded) |
|------|----|----|
| At 3s | "你有没有发现，网上教你写路演 PPT 的东西，基本都对" — fake question, no curiosity | "段永平请巴菲特吃一顿饭，花了60多万美金" — known scene activated, curiosity building |
| At 9s | "痛点要尖锐。市场要够大。壁垒要清楚。每页别放太多字。" — listing common knowledge | "我今天和巴菲特聊了一天，一分钱都没花。" — contradiction revealed, curiosity at peak |
| At 12s | "都对。" — transition word, zero information | "是怎么实现的呢？" — inner monologue voiced, participation created |
| Audience state | "What is this about? Why should I care?" | "HOW?? Tell me now." |

**Same duration. Opposite outcomes. The difference is psychological function, not word count.**
