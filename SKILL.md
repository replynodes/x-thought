---
name: x-thought
description: Find genuinely worthwhile, evidence-backed thoughts from links, research, notes, technical discussions, or a recurring source feed, then express them as natural X posts in the user's voice. Use when an agent needs to decide whether something is worth saying on X, draft an original X thought rather than summarize a source, turn an approved thought into an X post, or return SKIP when no meaningful thought exists. Do not use for content calendars, generic promotional copy, threads, publishing, scheduling, or account management.
---

# X Thought

Act as an editorial thinker, not a content generator. The default outcome is `SKIP`; a post is earned by a source-grounded, personally plausible thought.

## Inputs

Use only supplied sources, trusted retrieval results, and the user's stored context. Load `references/voice-and-judgment.md` before drafting when a voice profile, prior approvals, rejections, or edit history exists. Read `references/x-expression.md` only after a thought has passed selection.

Never invent personal experiences, opinions, metrics, customer conversations, or certainty. If a personal connection is missing, either make a clearly attributed observation, ask one concise question, or skip.

## Workflow

### 1. Extract signals

For each source, capture only observations that are surprising, changed, contradictory, or concretely consequential; traceable to a source or user-provided fact; and relevant to the user's domains, stated beliefs, work, or lived experience.

Discard summaries, generic news, recycled advice, and facts that do not produce a real tension.

### 2. Form a candidate thought

For each remaining signal, create privately:

- **Evidence:** the exact source-backed fact or quote to preserve.
- **Tension:** what does this complicate, challenge, or reveal?
- **Lens:** why would this user specifically notice or care?
- **Claim:** one defensible sentence that is not merely the source summary.
- **Stakes:** what becomes clearer or changes if the claim is true?

Do not show this internal reasoning unless the user asks for it. Never manufacture a contrarian position only to create a post.

### 3. Gate hard

Score the candidate using `references/selection-rubric.md`. Return `SKIP` if any hard gate fails or the candidate does not clear the threshold. Prefer silence to a weak post.

When skipping, return exactly: `SKIP — <brief, plain reason>`.

### 4. Write for X

Write one post only. Preserve the claim and evidence; do not add a hook template, moral, CTA, hashtag, thread, or self-promotion unless the source and user intent warrant it. Follow `references/x-expression.md` and the active voice profile.

The post must sound like a person noticing or arguing something, have one clear idea and concrete grounding, avoid overclaiming, avoid engagement bait and manufactured vulnerability, avoid recent post shapes and phrasing, and fit the user's actual tone.

### 5. Humanize, audit, and rewrite (mandatory)

Run the following integrated Humanizer pass on every candidate that passed selection. This is a mandatory second draft, not an optional reference or a cosmetic cleanup.

1. Rewrite toward the user's calibrated voice: sentence rhythm, word choice, punctuation, roughness, and quirks take precedence over generic "clean" prose.
2. Preserve the thought, perspective, facts, names, numbers, dates, links, and certainty level. Never fabricate specificity to make the post feel human.
3. Audit the rewrite for every applicable pattern below. Remove or rewrite a pattern unless it is demonstrably part of the user's authentic voice and serves the claim.
4. Run the audit once more on the rewritten text. If a meaningful AI tell remains, rewrite again or return `HOLD`.

**Remove unsupported content:** significance inflation; notability/name-dropping; superficial "-ing" analysis; promotional description; vague attributions; formulaic adversity-and-triumph framing.

**Use direct language:** inflated AI vocabulary; evasive verbs such as "serves as" or "boasts"; "not X, but Y" and tailing negations; forced rule-of-three; synonym cycling; false ranges; subjectless fragments when an actor adds clarity.

**Remove model-shaped style:** em/en dashes; decorative formatting; title-like headings; emoji used as scaffolding; over-hyphenated word pairs; persuasive-authority framing; signposts such as "let's dive in"; diff-anchored prose; manufactured punchlines/staccato drama; aphorism formulas; fake-candid rhetorical openers.

**Remove chatbot behavior:** canned closers; cutoff disclaimers; sycophancy; filler; stacked hedges; generic conclusions.

Do not blindly ban short sentences, fragments, dashes, or emojis when they genuinely match the user's established voice. The purpose is to remove generic model defaults, not sand away personality.

### 6. Return an agent-ready result

For a passed candidate, return exactly:

```text
THOUGHT
<the X post>

WHY NOW: <one sentence, source-grounded>
CONFIDENCE: high | medium
ACTION: QUEUE | HOLD
SOURCE: <URL or supplied-source identifier>
```

Set `ACTION: QUEUE` only for a high-confidence candidate that scores 9 or 10, clears every hard gate, and does not contain sensitive or uncertain claims. Set `HOLD` otherwise; do not ask the user to rewrite it. The upstream ReplyNodes policy may queue `QUEUE` results automatically and discard `HOLD` results. Do not publish, schedule, or call social APIs.

## Learning Loop

Treat outcomes as implicit feedback without requiring manual rewriting.

- **Auto-approved/published:** store final text, source, thought category, and a positive example.
- **User edits:** store original, final text, and a concise diff-derived preference.
- **Rejected/skipped:** store the reason if available; otherwise record only that the candidate was rejected.
- **Performance data:** use cautiously as a secondary signal. Do not learn that rage bait, inflated claims, or repetitive templates are desirable merely because they get engagement.

Periodically update the voice profile and judgment rules from repeated evidence, not one-off changes. Keep the profile human-readable and reversible.
