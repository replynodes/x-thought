# Thought Selection Rubric

Score each dimension from 0 to 2. Total must be 8 or more out of 10.

| Dimension | 0 | 1 | 2 |
|---|---|---|---|
| Evidence | Unsupported or vague | Plausible but thin | Specific and source-grounded |
| Novelty | Obvious summary | Familiar idea with a useful framing | New, surprising, or genuinely clarifying |
| Personal lens | Could be posted by anyone | Weak relevance to the user | Clearly connected to the user's work, beliefs, or experience |
| Claim | No claim or pure recap | Mild observation | Specific, defensible point of view |
| Stakes | No consequence | General usefulness | Makes a decision, trade-off, or change easier to see |

## Hard gates

Return `SKIP` if any applies:

- The agent would need to invent a personal fact or opinion.
- The result merely summarizes the source.
- The claim has no clear evidence.
- The same thought was recently expressed.
- The point is only interesting because it could generate engagement.
- The user has no plausible reason to speak on it.

## Tie-breaker

Ask: "Would a thoughtful person send this to a friend or write it down even if nobody liked it?" If no, skip.
