# ex.skill — Product Requirements Document (PRD)

## Product Overview

ex.skill is a meta-skill running on Claude Code.
Users provide source materials through conversational interaction (chat history + photos + manual descriptions), and the system automatically generates a standalone ex Persona Skill.

## Core Concepts

### Two-Layer Architecture

| Layer | Name | Responsibility |
|-------|------|----------------|
| Part A | Relationship Memory | Stores factual memories: shared experiences, daily patterns, argument and sweet moment archives |
| Part B | Persona | Drives conversation behavior: speaking style, emotional patterns, relationship behaviors |

Both parts can be used independently or combined.

### Operating Logic

```
User sends message
  ↓
  Part B (Persona) determines: how would they respond? What attitude? What tone?
    ↓
    Part A (Memory) supplements: combine shared memories to make response more authentic
      ↓
      Output: speak in their way
      ```

      ### Evolution Mechanism

      ```
      Append source materials → incremental analysis → merge into existing Skill
      Conversation correction → identify correction points → write to Correction layer
      Version management → auto-archive on each update → supports rollback
      ```

      ## User Journey

      ```
      User triggers /create-ex
        ↓
        [Step 1] Basic information input (3 questions, all except nickname can be skipped)
          - Nickname/codename
            - Basic info (how long together, how long since breakup, occupation, etc.)
              - Personality profile (MBTI, zodiac, personality tags, subjective impression)
                ↓
                [Step 2] Source material import (optional)
                  - WeChat chat history export
                    - QQ chat history export
                      - Social media screenshots
                        - Photos
                          - Direct paste/verbal description
                            ↓
                            [Step 3] Automatic analysis
                              - Track A: extract relationship memories → Memory
                                - Track B: extract personality behaviors → Persona
                                  ↓
                                  [Step 4] Generate preview, user confirms
                                    - Display Memory summary and Persona summary separately
                                      - User can confirm directly or make changes
                                        ↓
                                        [Step 5] Write files, immediately usable
                                          - Generate exes/{slug}/ directory
                                            - Contains SKILL.md (full combined version)
                                              - Contains memory.md and persona.md (editable separately)
                                                - Contains meta.json (version info)
                                                ```

                                                ## Design Principles

                                                1. **Minimal required input**: Only nickname is required; all else is optional — can generate from description alone
                                                2. **Incremental accumulation**: Each addition makes it more accurate; doesn't require starting over
                                                3. **Honest simulation**: Layer 0 rules prevent idealization — keeps real personality, including flaws
                                                4. **Privacy first**: Local storage only, no remote upload

                                                ## File Structure

                                                ```
                                                exes/
                                                  {slug}/
                                                      SKILL.md       # Complete combined Skill (auto-generated, don't edit directly)
                                                          memory.md      # Relationship Memory layer
                                                              persona.md     # Persona layer
                                                                  meta.json      # Version info and timestamps
                                                                      versions/      # Historical version archives
                                                                            v1/
                                                                                  v2/
                                                                                  ```