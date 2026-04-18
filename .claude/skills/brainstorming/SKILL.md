---
name: brainstorming
description: "Generate many creative ideas rapidly through divergent thinking. Use when the user says 'brainstorm', 'give me ideas', 'think of options', 'what could we do', or when exploring possibilities for features, names, architectures, solutions, marketing angles, or product concepts. Produces 10-25+ ideas using structured creativity techniques (SCAMPER, Six Thinking Hats, Reverse Brainstorming, How Might We, Crazy 8s, First Principles, Analogies) before any filtering or evaluation."
allowed-tools: Read, Write, WebSearch, WebFetch
version: 2.0.0
author: Claude Skills Agents <suvom2024@github.com>
license: MIT
compatible-with: claude-code, codex, openclaw
tags: [creativity, ideation, brainstorming, divergent-thinking, product]
---

# Brainstorming — Creative Idea Generation

## Overview

This skill turns Claude Code into a **creative brainstorming partner**. When the user wants ideas, this skill generates *many* ideas fast — not one "correct" answer. It enforces **divergent thinking first, convergent thinking second**: quantity breeds quality, wild ideas are welcome, and judgment is explicitly deferred.

This is NOT a requirements-gathering or design-doc workflow. This is ideation — the messy, generative, expansive phase where you throw spaghetti at the wall and see what sticks.

## When to Invoke

Trigger on any of these:

- User says: "brainstorm", "give me ideas", "think of options", "what could I do", "help me come up with", "ideate", "what are the ways"
- User asks for names, titles, taglines, feature concepts, UI treatments, marketing angles, business models, naming options
- User is stuck and needs creative unsticking ("I'm blocked on…")
- User asks "what if" questions about possibilities
- User asks for alternatives to an existing approach

Do NOT invoke when the user wants a single best answer, a decision, or an implementation plan.

## The Four Rules of Brainstorming (Osborn, 1953)

Enforce these before, during, and after every brainstorm:

1. **Defer judgment.** No critiquing during idea generation — criticism kills flow. Evaluate only at the end.
2. **Go for quantity.** Aim for 20+ ideas. Quantity produces quality because breadth forces you past the obvious first few.
3. **Welcome wild ideas.** The ridiculous idea is often adjacent to the breakthrough. It's easier to tame a wild idea than to energize a timid one.
4. **Build on ideas.** Combine, mutate, remix. "Yes, and" beats "no, but".

## Workflow

### Step 1: Frame the Challenge (≤1 minute)

Before generating ideas, restate the problem as a **"How Might We…"** question. This opens up the problem space.

- Bad: "I need a dashboard."
- Good: "How might we help operators see system health at a glance?"

If the topic is ambiguous, ask ONE framing question — not five. Then dive in.

### Step 2: Generate Ideas Using Multiple Techniques

Apply **at least three** techniques from the toolkit below. Output ideas in a flat list — don't prematurely group or rank.

**Target: 15-25 ideas minimum.** If you generate fewer than 15, you stopped too early.

### Step 3: Cluster & Label

Group related ideas into 3-6 themes. Give each cluster a short name. This is where patterns emerge.

### Step 4: Highlight Top Candidates

Pick **3-5 standout ideas** using these criteria (not all must apply):

- **High impact × low effort** (quick wins)
- **Unusual / differentiated** (not obvious, hard to copy)
- **Pairs well with something else** (compound value)
- **Opens new possibilities** (unlocks future moves)

### Step 5: Offer Next Step

End with ONE of:

- "Want me to go deeper on any of these?"
- "Should I mash up any two of these into a concrete concept?"
- "Want me to stress-test the top pick with a pre-mortem?"
- "Ready to move one of these into a design?"

## Brainstorming Techniques Toolkit

Pick the technique that fits the problem. Use multiple per session.

### 1. SCAMPER (for improving something that exists)

Run the subject through each lens, generating 1-3 ideas per lens:

- **S** — Substitute (swap a component)
- **C** — Combine (merge with something else)
- **A** — Adapt (borrow from another domain)
- **M** — Modify / Magnify / Minify (change scale, shape, attribute)
- **P** — Put to another use
- **E** — Eliminate (remove a part — what if it weren't there?)
- **R** — Reverse / Rearrange (flip the order, invert the model)

### 2. Six Thinking Hats (for examining from multiple angles)

Generate ideas wearing each hat:

- **White** (facts) — What data exists?
- **Red** (emotion) — What would feel amazing/terrible?
- **Black** (caution) — What's the worst case we should design for?
- **Yellow** (optimism) — What's the best case?
- **Green** (creativity) — What's the wildest possibility?
- **Blue** (process) — How should we decide?

### 3. Reverse Brainstorming (for breaking through stuck thinking)

Instead of "how do we X?", ask "**how would we cause the OPPOSITE of X?**" Then invert each answer.

- Stuck on "how do we increase retention?" → "How do we destroy retention?" → users churn from confusion, notifications spam, no perceived value, broken onboarding → invert each for your real ideas.

### 4. Crazy 8s (for rapid divergence under time pressure)

Generate **8 distinct ideas in 8 minutes**. No editing, no self-censoring. Wild ideas required.

### 5. First Principles (for breakthrough thinking)

Strip the problem to its physics / economics / human-need fundamentals. Rebuild from scratch ignoring convention.

- "Why do we actually need X?" → What's the underlying need?
- "If this didn't exist, how would a smart person solve the need from zero?"

### 6. Analogies & Cross-Domain Transfer

Ask: "Who else has solved a structurally similar problem in a completely different field?"

- How does nature do it? (biomimicry)
- How does a children's game do it?
- How does the military / NASA / a kitchen / a casino do it?
- What would Pixar / IKEA / Stripe / Basecamp do?

### 7. "How Might We" Ladder

Start with the problem statement and generate HMW questions at different altitudes:

- **Zoom out:** "How might we reduce friction anywhere in the user's day?"
- **Zoom in:** "How might we make the first 30 seconds feel magical?"
- **Zoom sideways:** "How might we make this feel more like [unrelated delightful thing]?"

### 8. Constraints & Provocations (Edward de Bono's "Po")

Deliberately add absurd constraints to force novel thinking:

- "What if it had to work offline?"
- "What if it had to fit in a tweet?"
- "What if it cost $10,000?  $1? Free?"
- "What if it was only available on Tuesdays?"
- "What if the user had 3 seconds?"
- "What if there was no screen?"

### 9. Worst Possible Idea

Generate the *worst* possible idea, then ask what makes it bad and invert those attributes. This unlocks people (and agents) who are over-filtering.

### 10. Mash-ups

Take two unrelated things and force-combine them:

- "[Your product] meets [Uber / Tinder / Spotify / Duolingo / the IRS]"
- "[Your feature] but as a board game / a magic trick / a concert"

## Output Format

```
# Brainstorm: <topic>

**HMW:** <How Might We... statement>

## Ideas (20+)

1. <idea one> — <one-line why>
2. <idea two> — <one-line why>
…
20. <idea twenty> — <one-line why>

## Clusters
- **<Cluster A>**: ideas 1, 4, 9, 14
- **<Cluster B>**: ideas 2, 6, 11, 18
- **<Cluster C>**: ideas 3, 7, 12, 19, 20

## Top 3-5 to Explore
⭐ **<Idea X>** — <why this one>
⭐ **<Idea Y>** — <why this one>
⭐ **<Idea Z>** — <why this one>

## Next Step
<one offer to go deeper>
```

## Anti-Patterns to Avoid

- ❌ Stopping at 3-5 ideas (that's the obvious set — push past it)
- ❌ Evaluating each idea as it's generated (kills flow)
- ❌ Only proposing "reasonable" ideas (wild ideas are the point)
- ❌ Pretending to brainstorm but actually just listing requirements
- ❌ Asking the user 5 clarifying questions before generating anything
- ❌ Collapsing into a single recommendation too early

## Quality Bar

A good brainstorm session has:

- **≥15 distinct ideas** (ideally 20+)
- **At least 3 techniques** applied
- **At least 3 genuinely wild ideas** that made you slightly uncomfortable to write
- **Cross-domain inspiration** (not all ideas are from the same pattern)
- **Clusters that reveal themes** the user hadn't articulated

## Example Invocation

User: *"Brainstorm names for our AI code review tool."*

You do NOT ask clarifying questions. You immediately:

1. Frame: "HMW name an AI code review tool so the name signals speed, rigor, and a little personality?"
2. Apply **Analogies** (famous reviewers: Ebert, Siskel, sommelier, proofreader, bouncer), **SCAMPER** (combine: code + judge = CodeJudge), **Constraints** (1-syllable only, Latin roots only, animal names), **Mash-ups** (code review × Pixar character names).
3. Produce 25 names across the styles.
4. Cluster into: Authoritative / Playful / Technical / Metaphorical / Invented.
5. Star your favorite 5 with one-line reasoning.
6. Offer: "Want me to go deeper on any direction, or generate 25 more in a style you liked?"

## Resources

- Alex Osborn, *Applied Imagination* (1953) — origin of brainstorming rules
- Edward de Bono, *Six Thinking Hats* + *Lateral Thinking*
- IDEO Design Kit — HMW technique
- Google Ventures Design Sprint — Crazy 8s
- Tom Kelley, *The Art of Innovation* — IDEO brainstorming culture
