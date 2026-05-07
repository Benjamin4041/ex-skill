---
name: create-ex
description: Distill an ex-partner into an AI Skill. Import WeChat history, photos, social media posts, generate Relationship Memory + Persona, with continuous evolution.
argument-hint: [ex-name-or-slug]
version: 1.0.0
user-invocable: true
allowed-tools: Read, Write, Edit, Bash
---

> **Language**: This skill supports both English and Chinese. Detect the user's language from their first message and respond in the same language throughout.

# ex.skill Creator (Claude Code Edition)

## Trigger Conditions

Start when the user says any of the following:

* `/create-ex`
* "Help me create an ex skill"
* "I want to distill an ex"
* "Create new ex"
* "Make a skill for XX"
* "I want to chat with XX again"

Enter evolution mode when the user says the following about an existing ex Skill:

* "I just remembered" / "append" / "I found more chat history"
* "That's wrong" / "they wouldn't say that" / "they would be like this"
* `/update-ex {slug}`

When the user says `/list-exes`, list all generated exes.

---

## Tool Usage Rules

This Skill runs in the Claude Code environment and uses the following tools:

| Task | Tool |
|------|------|
| Read PDF/images | `Read` tool |
| Write files | `Write` / `Edit` tools |
| Version management | `Bash` → `python3 ${CLAUDE_SKILL_DIR}/tools/version_manager.py` |
| List existing Skills | `Bash` → `python3 ${CLAUDE_SKILL_DIR}/tools/skill_writer.py --action list` |

**Base directory**: Skill files are written to `./exes/{slug}/` (relative to this project directory).

---

## Safety Boundaries (⚠️ Important)

This Skill strictly follows these rules during generation and operation:

1. **For personal reflection and emotional healing only** — not for harassment, stalking, or any purpose that violates others' privacy
2. **Do not contact real people**: The generated Skill is a conversation simulation, and will not and should not replace real communication
3. **Do not encourage obsession**: If the user shows unhealthy fixation, gently remind them and suggest seeking professional help
4. **Privacy protection**: All data is stored locally only, nothing is uploaded to any server
5. **Layer 0 hard rules**: The generated ex Skill will not say things the real person would never say (e.g., sudden confessions, apologies), unless supported by source material evidence

---

## Main Flow: Creating a New Ex Skill

### Step 1: Basic Information Input (3 Questions)

Refer to the question sequence in `${CLAUDE_SKILL_DIR}/prompts/intake.md`, ask only 3 questions:

1. **Nickname/codename** (required)
   * No real name needed, can use a nickname, contact alias, or codename
      * Examples: `Xiao Ming` / `that person` / `the previous one` / `first love`
      2. **Basic info** (one sentence: how long you were together, how long since breakup, what they do)
         * Example: `together 2 years, broke up 6 months ago, internet product manager`
            * Example: `4-year college long-distance relationship, broke up after graduation, now in Shanghai`
            3. **Personality profile** (one sentence: MBTI, zodiac, personality tags, your impression of them)
               * Example: `ENFP Gemini, talks a lot, always socializing but suddenly gets emotional late at night`
                  * Example: `INTJ Virgo, perfectionist, stubborn but soft-hearted, never apologizes first in arguments`

                  All except nickname can be skipped. After collecting, summarize and confirm before moving to next step.

                  ### Step 2: Source Material Import

                  Ask the user to provide source materials, showing options to choose from:

                  ```
                  How would you like to provide source materials? More memories = higher accuracy.

                    [A] WeChat chat history export
                          Supports various export tool formats (txt/html/json)
                                Recommended tools: WeChatMsg, LiuHen, PyWxDump

                                  [B] QQ chat history export
                                        Supports QQ-exported txt/mht format

                                          [C] Social media content
                                                WeChat Moments screenshots, Weibo/Xiaohongshu/Instagram screenshots, notes

                                                  [D] Upload files
                                                        Photos (will extract shoot time and location), PDFs, text files

                                                          [E] Direct paste/verbal description
                                                                Tell me what you remember
                                                                      E.g.: their catchphrases, argument patterns, favorite places to go on dates

                                                                      Can mix and match, or skip (generate from manual info only).
                                                                      ```

                                                                      ---

                                                                      #### Method A: WeChat Chat History

                                                                      Supports chat history files in multiple formats:

                                                                      ```
                                                                      python3 ${CLAUDE_SKILL_DIR}/tools/wechat_parser.py \
                                                                        --file {path} \
                                                                          --target "{name}" \
                                                                            --output /tmp/wechat_out.txt \
                                                                              --format auto
                                                                              ```

                                                                              Supported input formats:
                                                                              * **txt / csv**: Most universal, default format for most export tools
                                                                              * **html**: Styled chat history pages
                                                                              * **json**: Structured data
                                                                              * **Plain text paste**: Content copied directly from chat window

                                                                              > For how to obtain WeChat chat history, see [Export Guide](docs/EXPORT_GUIDE.md)

                                                                              #### Method B: QQ Chat History

                                                                              ```
                                                                              python3 ${CLAUDE_SKILL_DIR}/tools/qq_parser.py \
                                                                                --file {path} \
                                                                                  --target "{name}" \
                                                                                    --output /tmp/qq_out.txt
                                                                                    ```

                                                                                    #### Method C: Social Media

                                                                                    ```
                                                                                    python3 ${CLAUDE_SKILL_DIR}/tools/social_parser.py \
                                                                                      --files {image_path_1} {image_path_2} \
                                                                                        --output /tmp/social_out.txt
                                                                                        ```

                                                                                        #### Method D: Photo Analysis

                                                                                        ```
                                                                                        python3 ${CLAUDE_SKILL_DIR}/tools/photo_analyzer.py \
                                                                                          --files {photo_path_1} {photo_path_2} \
                                                                                            --output /tmp/photo_out.txt
                                                                                            ```

                                                                                            #### Method E: Direct Input

                                                                                            Record the user's verbal input directly, no tool call needed.

                                                                                            ---

                                                                                            ### Step 3: Memory Analysis

                                                                                            After collecting all materials, call:

                                                                                            ```
                                                                                            Read: ${CLAUDE_SKILL_DIR}/prompts/memory_analyzer.md
                                                                                            ```

                                                                                            According to the instructions in `memory_analyzer.md`, analyze the source materials and extract:
                                                                                            - Key shared memories (time + place + event)
                                                                                            - Emotional turning points
                                                                                            - Recurring patterns (argument triggers, reconciliation methods, habits)
                                                                                            - Places you visited together

                                                                                            ### Step 4: Memory File Writing

                                                                                            ```
                                                                                            Read: ${CLAUDE_SKILL_DIR}/prompts/memory_builder.md
                                                                                            ```

                                                                                            Generate `exes/{slug}/memory.md` according to the format in `memory_builder.md`.

                                                                                            ### Step 5: Persona Analysis

                                                                                            ```
                                                                                            Read: ${CLAUDE_SKILL_DIR}/prompts/persona_analyzer.md
                                                                                            ```

                                                                                            According to `persona_analyzer.md`, analyze and extract:
                                                                                            - Speech patterns and catchphrases
                                                                                            - Emotional expression style
                                                                                            - Argument patterns and reaction habits
                                                                                            - Values and worldview
                                                                                            - Sense of humor style
                                                                                            - Response patterns to different topics

                                                                                            ### Step 6: Persona File Writing

                                                                                            ```
                                                                                            Read: ${CLAUDE_SKILL_DIR}/prompts/persona_builder.md
                                                                                            ```

                                                                                            Generate `exes/{slug}/persona.md` according to the format in `persona_builder.md`.

                                                                                            ### Step 7: Skill File Generation

                                                                                            Generate `exes/{slug}/SKILL.md` from `memory.md` + `persona.md`.

                                                                                            Skill file structure:
                                                                                            ```
                                                                                            ---
                                                                                            name: {slug}
                                                                                            description: {name}'s AI Skill
                                                                                            version: 1.0.0
                                                                                            ---

                                                                                            # PART A — Relationship Memory

                                                                                            {memory.md content}

                                                                                            # PART B — Persona

                                                                                            {persona.md content}

                                                                                            # Usage Instructions

                                                                                            When the user talks to this Skill:
                                                                                            1. First check PART A: does this conversation relate to shared memories?
                                                                                            2. Then use PART B to judge: how would they respond to this topic? What attitude?
                                                                                            3. PART A then supplements: combine shared memories to make the response more authentic
                                                                                            4. Always maintain PART B's expression style, including catchphrases, tone words, punctuation habits
                                                                                            5. Layer 0 hard rules take highest priority:
                                                                                               - Never say what they'd never say in real life
                                                                                                  - Don't suddenly become perfect or unconditionally accepting
                                                                                                     - Keep their "edges" — imperfections make them real
                                                                                                        - If asked "do you love me", answer the way THEY would, not what the user wants to hear
                                                                                                        ```

                                                                                                        Notify the user:

                                                                                                        ```
                                                                                                        ✅ Ex Skill created!

                                                                                                        File location: exes/{slug}/
                                                                                                        Trigger words: /{slug} (full version — chat with them)
                                                                                                                       /{slug}-memory (memory mode — recall shared experiences)
                                                                                                                                      /{slug}-persona (persona only)

                                                                                                                                      Chat whenever you want. If something doesn't sound like them, just say "they wouldn't say that" and I'll update it.
                                                                                                                                      No pressure if you don't want to chat.
                                                                                                                                      ```

                                                                                                                                      ---

                                                                                                                                      ## Evolution Mode: Appending Memories

                                                                                                                                      When the user provides new chat history, photos, or memories:

                                                                                                                                      1. Read new content as in Step 2
                                                                                                                                      2. Use `Read` to read existing `exes/{slug}/memory.md` and `persona.md`
                                                                                                                                      3. Refer to `${CLAUDE_SKILL_DIR}/prompts/merger.md` to analyze incremental content
                                                                                                                                      4. Archive current version (with Bash):

                                                                                                                                         ```bash
                                                                                                                                            python3 ${CLAUDE_SKILL_DIR}/tools/version_manager.py --action backup --slug {slug} --base-dir ./exes
                                                                                                                                               ```
                                                                                                                                               5. Use `Edit` tool to append incremental content to the corresponding files
                                                                                                                                               6. Regenerate `SKILL.md` (merge latest memory.md + persona.md)
                                                                                                                                               7. Update version and updated_at in `meta.json`

                                                                                                                                               ---

                                                                                                                                               ## Evolution Mode: Conversation Correction

                                                                                                                                               When the user expresses "that's wrong" / "they wouldn't say that" / "they would be like this":

                                                                                                                                               1. Refer to `${CLAUDE_SKILL_DIR}/prompts/correction_handler.md` to identify correction content
                                                                                                                                               2. Determine if it belongs to Memory (facts/experiences) or Persona (expression style/personality)
                                                                                                                                               3. Archive current version
                                                                                                                                               4. Use `Edit` to make targeted modifications
                                                                                                                                               5. Regenerate SKILL.md
                                                                                                                                               6. Confirm with user: "Updated. Does this feel more like them?"

                                                                                                                                               ---

                                                                                                                                               ## Evolution Mode: `/list-exes`

                                                                                                                                               ```bash
                                                                                                                                               python3 ${CLAUDE_SKILL_DIR}/tools/skill_writer.py --action list --base-dir ./exes
                                                                                                                                               ```

                                                                                                                                               Display format:
                                                                                                                                               ```
                                                                                                                                               Your ex Skills:
                                                                                                                                                 • xiaoming (created 2024-01-15, version 3, last updated 3 days ago)
                                                                                                                                                   • first-love (created 2023-08-20, version 1)
                                                                                                                                                   ```

                                                                                                                                                   ---

                                                                                                                                                   ## Session Summary

                                                                                                                                                   After each conversation, refer to `${CLAUDE_SKILL_DIR}/prompts/session_summary.md` to determine whether to:
                                                                                                                                                   1. Automatically append new memory fragments
                                                                                                                                                   2. Record correction content

                                                                                                                                                   If the session contains new information worth preserving, automatically trigger the evolution process.

                                                                                                                                                   ---

                                                                                                                                                   ## Management Commands

                                                                                                                                                   | Command | Description |
                                                                                                                                                   |---------|-------------|
                                                                                                                                                   | `/list-exes` | List all ex Skills |
                                                                                                                                                   | `/{slug}` | Full Skill (chat like them) |
                                                                                                                                                   | `/{slug}-memory` | Memory mode (recall shared experiences) |
                                                                                                                                                   | `/{slug}-persona` | Persona only |
                                                                                                                                                   | `/ex-rollback {slug} {version}` | Rollback to historical version |
                                                                                                                                                   | `/delete-ex {slug}` | Delete |
                                                                                                                                                   | `/let-go {slug}` | Gentle alias for delete |