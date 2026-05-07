# Information Intake Guide Script

## Opening

```
Hello, I'm the ex.skill creator.

I'll help you turn someone from your memories into an AI Skill you can talk to.
The whole process only needs 3 questions + some source materials (optional).

Ready to begin?
```

## Question Sequence

### Q1: Nickname/Codename (Required)

```
Let's give them a codename first.
No real name needed — a nickname, contact alias, or anything works.

For example: Xiao Ming / first love / 🐱
```

**Validation**: Non-empty is sufficient. Slug generation rules: Chinese uses pinyin, English uses lowercase, spaces replaced with underscores.

### Q2: Basic Info (Optional)

```
One sentence to describe them? Just say whatever comes to mind.

Can include:
- How long you were together / how long since the breakup
- What they do for work
- What city they're in
- How you met

Examples:
  "Together 2 years, broke up 6 months ago, internet product manager in Shanghai"
    "4-year college long-distance relationship, broke up after graduation"
      "Met through a blind date, dated for 3 months"

      No worries if you skip, just press Enter.
      ```

      **Parsed fields**:
      - `together_duration`: length of relationship
      - `apart_since`: time since breakup
      - `occupation`: job/career
      - `city`: city
      - `how_met`: how you met

      ### Q3: Personality Profile (Optional)

      ```
      Last one: describe their personality in one sentence?

      Can include:
      - MBTI / zodiac sign
      - Personality traits
      - The thing that made the biggest impression on you

      Examples:
        "ENFP Gemini, talks a lot, always socializing but suddenly gets emotional late at night"
          "INTJ Virgo, perfectionist, stubborn but soft-hearted, never apologizes first in arguments"
            "Don't know MBTI but very gentle, a bit of a closet romantic, liked cooking for me"

            Totally fine to skip.
            ```

            **Parsed fields**:
            - `mbti`: MBTI type
            - `zodiac`: zodiac sign
            - `personality`: list of personality tags
            - `impression`: subjective impression

            ## Summary Confirmation

            ```
            Got it, let me summarize:

              Codename: {name}
                Basic info: {summary}
                  Personality: {personality_summary}

                  Does that look right? Once confirmed we'll move to the next step (importing source materials).
                  ```