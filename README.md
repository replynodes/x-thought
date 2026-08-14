# x-thought

An autonomous X writer for Hermes Agent and ReplyNodes.

It does not generate content to fill a calendar. It reads sources, decides whether there is a real thought worth expressing, and returns `SKIP` when there is not.

## What it does

`x-thought` combines the complete writing runtimes of:

- [blader/humanizer](https://github.com/blader/humanizer): voice-aware rewriting and a two-pass audit for AI-writing patterns.
- [sergebulaev/x-skills](https://github.com/sergebulaev/x-skills): X-native posts, threads, replies, quote posts, hook study, repurposing, planning, profile work, and audience insight.

On top, `x-thought` adds an editorial decision layer:

```
sources → signals → thought selection → X draft → humanizer → X audit → QUEUE | HOLD | SKIP
```

A post is earned. Silence is a valid output.

## Modes

| Mode | Use |
|---|---|
| `thought-scan` | Read source feeds, research, discussions, or news and find a thought worth sharing. |
| `post` | Write one native X post from a supplied claim or idea. |
| `thread` | Develop multiple independently useful claims into a thread. |
| `reply / quote` | Add a useful reply or quote post; skip empty agreement. |
| `hook study` | Study a post's mechanism and make original options. |
| `repurpose` | Rebuild an article, LinkedIn post, video, newsletter, or notes for X. |
| `plan` | Create an editorial X plan that leaves room for reactive posts and `SKIP`. |
| `profile` | Write an X bio, header guidance, and pinned post. |
| `audience insight` | Find questions, language, and gaps in available audience or competitor data. |

## Autonomous output

```text
<MODE IN UPPERCASE>
<the X text>

WHY NOW: <one source-grounded sentence>
CONFIDENCE: high | medium
ACTION: QUEUE | HOLD
SOURCE: <URL or source identifier>
```

For `thought-scan`, the skill returns:

```text
SKIP — <brief reason>
```

when it cannot form an evidence-backed, personally plausible, non-obvious thought.

`QUEUE` is reserved for high-confidence drafts that pass the editorial selection, Humanizer, and X-native checks. `HOLD` is for drafts that should not enter the queue.

## Install in Hermes

Clone this repository into Hermes's skills directory:

```bash
git clone https://github.com/replynodes/x-thought.git ~/.hermes/skills/x-thought
```

Or add the repository path to Hermes's `skills.external_dirs` configuration.

Then use it in an agent request:

```text
Use x-thought in thought-scan mode. Read these sources, find at most one thought worth queuing, otherwise return SKIP.
```

## Design rules

- Never invent a personal experience, opinion, metric, customer conversation, or certainty.
- Do not summarize a source and call it a thought.
- Do not manufacture contrarianism, vulnerability, takeaways, or engagement bait.
- Match the user's voice profile rather than generic “human” prose.
- Run the bundled Humanizer rewrite and final audit on every draft.
- Use X-native structure, not compressed LinkedIn copy.
- Do not publish, schedule, or manage accounts. ReplyNodes owns execution.

## Repository structure

```text
SKILL.md                         orchestration and editorial gate
references/                      x-thought's selection and voice profile
components/humanizer/            complete blader/humanizer runtime
components/x-skills/             complete sergebulaev/x-skills runtime
```

The bundled upstream components retain their MIT licenses:

- `components/humanizer/LICENSE`
- `components/x-skills/LICENSE`

## ReplyNodes integration

ReplyNodes should treat `x-thought` as the thinking and writing layer:

1. Collect sources and user context.
2. Invoke `x-thought`.
3. Persist the output, source, result, and outcome.
4. Automatically queue only `ACTION: QUEUE` according to the product's policy.
5. Feed publish, rejection, edits, and performance outcomes back into the user's voice and judgment profile.

Publishing, scheduling, social API access, and account management belong outside this repository.
