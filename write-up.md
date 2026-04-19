# Daily Reflection Tree — Design Write-Up
**Author:** Arun K | **Role:** AI PM Fellowship Assignment | **Company:** DeepThought CultureTech

---

## Why These Questions

The brief asked for three psychological axes in sequence: Locus, Orientation, Radius. The challenge wasn't finding questions — it was finding questions that surface something honest in someone who just finished a 9-hour day and is mildly checked out.

Most reflection tools fail because they're too earnest. "What are you grateful for?" gets a rote answer. "What did you learn?" gets a performance. The goal here was to make the employee *notice* something they hadn't consciously framed — not confess to it.

So each question was designed around a behavioral anchor: a specific moment, a specific instinct, a specific person. Abstract questions about mindset get abstract answers. Concrete questions ("when things got difficult, what was your first instinct?") pull out real signal.

---

## Axis 1 — Locus of Control

**Psychological source:** Rotter (1954) internal vs external locus; Dweck (2006) growth vs fixed mindset.

The entry point splits on day quality — not because the psychology differs, but because a good-day employee and a bad-day employee need different language to surface the same signal. Asking "what made it happen?" to someone who had a good day is natural. Asking it to someone who had a rough day is tone-deaf.

The branching at A1_D2 routes on *how* they describe success/failure — people who cite their own preparation or adaptation get routed to a follow-up about noticing choice; people who cite luck or others get routed to a follow-up about where their mind went first.

**Key trade-off:** I avoided directly asking "do you feel in control?" — that's too leading. Instead, the question asks about *first instinct* — which is where locus actually lives.

---

## Axis 2 — Contribution vs Entitlement

**Psychological source:** Campbell et al. (2004) psychological entitlement; Organ (1988) organizational citizenship behavior.

The challenge here: entitlement is invisible to the person experiencing it. You can't ask "were you entitled today?" — they'll say no. So the entry question uses a behavioral frame: "were you giving or expecting in one interaction?"

The follow-up does the real work. For people who said they gave, I ask what *drove* it — including the honest option "I wanted to be seen doing it." For people who said they needed support, I don't judge it — I ask what they wanted most, which surfaces whether the expectation is reasonable (clarity, load reduction) or recognition-based.

**Key trade-off:** Option "I wanted to be seen doing it" in A2_Q_CONTRIB is intentionally uncomfortable. It'll make some people pause. That pause is the value.

---

## Axis 3 — Radius of Concern

**Psychological source:** Maslow (1969) self-transcendence; Batson (2011) perspective-taking.

This axis is the hardest to surface without moralizing. Telling someone they were self-centric is shame-inducing. The tree avoids this by treating narrow radius as *focus*, not failure — and wide radius as *awareness*, not virtue.

The entry question is concrete: "when you think about today's biggest challenge — who came to mind?" This immediately segments self-referential thinkers (Just me) from other-aware ones (team, colleague, user). The follow-up for self-focused employees doesn't shame them — it asks if there was someone they *could have* noticed, without implying they should have.

**Key trade-off:** The self-centric path explicitly says "that's not selfishness" in the reflection node. This was deliberate — shame kills reflection. Curiosity opens it.

---

## Structural Decisions

**Why JSON over TSV:** JSON handles nested logic better and is more readable without a spreadsheet. Any developer can load it directly.

**Why 35 nodes over the minimum 25:** Each axis needed two question branches (high/low entry, internal/external follow-up) to avoid one-size-fits-all paths. That's 6 question pairs, 3 reflection pairs, 2 bridges, plus decision nodes and bookends.

**The summary node:** Uses interpolation (`{axis1.dominant}`, `{summary_reflection}`) to produce a personalized closing without generating text at runtime. All 8 possible summary strings are pre-written in `summary_reflections`.

---

## What I'd Improve With More Time

1. **Axis 3 needs a third question branch** — the current two-path split is functional but the radius axis is the richest psychologically and deserves more depth.
2. **Carry-forward interpolation across axes** — the SUMMARY node references prior answers, but mid-axis reflections could reference Axis 1 answers to create continuity ("You said you adapted on the fly earlier — that same instinct shows up here too.").
3. **A "neutral" entry option** — "How would you describe today?" currently forces a valence (Productive/Mixed/Tough/Frustrating). Adding "Steady" or "Quiet" would better serve people who had unremarkable days.
4. **Test with real employees at 7pm** — the brief's hint ("would you answer this or click through it?") is the right test. I'd run 5 walkthroughs with real people and kill every question that gets an automatic answer.
