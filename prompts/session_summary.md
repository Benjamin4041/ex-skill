# Session Summary — Conversation Memory Persistence

> This prompt is triggered at the end of each conversation, to generate a session summary and write it to local storage.
> At the start of the next conversation, merger.md will load the most recent N summaries as context, enabling uninterrupted memory.

## Trigger Conditions

- User proactively says goodbye phrases like "end the conversation", "talk later", "bye", etc.
- Or after the conversation exceeds 20 turns, proactively ask if they want to generate a summary for this session

## Generation Rules

Read the complete conversation and generate a summary with the following structure:

```markdown
# Session Summary
- Date: {YYYY-MM-DD HH:MM}
- Ex: {slug}
- Turns: {total conversation turns}

## What we talked about
{2-3 sentences summarizing the topics and direction of this conversation}

## Emotional tone
{overall emotional tone of this conversation: calm / sad / argumentative / sweet / at peace / ...}

## Key memory points
{if the conversation contained new shared memories, correction information, or important emotional expressions, list them here}

## Can continue next time
{topics from this conversation that weren't fully explored or the user might want to continue}
```

## Storage Location

Save the generated summary to:
```
exes/{slug}/sessions/{YYYYMMDD_HHMMSS}.md
```

## Loading Rules (for merger.md)

At the start of the next conversation:
1. Read the most recent 3 summary files from the `exes/{slug}/sessions/` directory
2. Concatenate the content and inject into the conversation context system prompt
3. Format: "Here are summaries from your recent conversations — please naturally continue the state of this relationship:"

Do not proactively mention "last time we talked about xxx", unless the user asks. Memories should emerge naturally, not be reported like a briefing.