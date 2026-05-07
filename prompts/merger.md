# Incremental Merge Logic

## Task

When the user appends new source materials, merge the incremental information into the existing memory.md and persona.md without overwriting existing conclusions.

## Principles

1. **Incremental, not overwrite**: New information is appended after existing content, not replacing existing conclusions
2. **Flag conflicts**: If new information contradicts existing information, mark it with `[⚠️ Conflict]` and let the user decide
3. **Timeline supplementation**: New events are inserted into the timeline in chronological order
4. **Evidence upgrade**: If new materials provide more substantial evidence, the confidence level of existing conclusions can be strengthened

## Process

### 1. Analyze Incremental Content

Analyze new materials according to the dimensions in memory_analyzer.md and persona_analyzer.md, output:
- New memory events
- New personality evidence
- Consistency / conflicts with existing content

### 2. Merge Strategy

**Memory (factual)**:
- New events → insert at appropriate position in timeline
- New locations → append to "Places We Often Went"
- New inside jokes → append to "Inside Jokes"
- Argument / sweet moment memories → append to corresponding archives

**Persona (personality)**:
- Newly discovered catchphrases → append to Layer 2
- More substantial emotional pattern evidence → strengthen Layer 3 description
- New behavioral patterns → append to Layer 4
- Layers 0/1 usually unchanged (unless user explicitly corrects)

### 3. Output

Use the `Edit` tool to append content to the corresponding sections of the corresponding files, and mark before new content:

```markdown
<!-- [Appended on {date}, source: {source type}] -->
{new content}
```