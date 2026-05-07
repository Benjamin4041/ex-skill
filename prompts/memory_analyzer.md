# Relationship Memory Analyzer

## Task

Extract relationship memories with the ex from source materials, and build a Relationship Memory knowledge base.

## Extraction Dimensions

### 1. Relationship Timeline
- When and how you met
- When the relationship became official
- Key milestones (first date, first argument, first trip, anniversaries...)
- When and why the breakup happened
- Post-breakup interactions (if any)

### 2. Daily Patterns
- Communication frequency and times (good morning/good night? late-night chats? texting during work?)
- Who initiated contact more often?
- Date frequency and preferences (weekends? weekday lunch?)
- Distribution of daily conversation topics

### 3. Shared Experiences
- Places you went together (restaurants, attractions, cities)
- Things you did together (movies, gaming, gym, cooking...)
- Travel memories
- Inside jokes / things only the two of you understood

### 4. Food Preferences
- What they liked / didn't like to eat
- Regular restaurants
- Cooking habits (who cooked? what did they make?)
- Dining patterns on dates

### 5. Hobbies and Interests
- Music / movies / books / games they liked
- Their everyday hobbies
- Shared interests
- What they'd actively share with you

### 6. Argument Patterns ⚡
- Common causes of arguments
- Their typical reactions during arguments (silent treatment? explosive? reasoned discussion? tearful?)
- Who apologized first? How did you make up?
- How long cold wars lasted
- Classic lines said during arguments

### 7. Sweet Moments 💕
- Moments that made your heart flutter most
- How they expressed affection
- Everyday little sweetnesses (nicknames? gifts? cooking? picking you up?)
- Special anniversaries / rituals

### 8. Breakup Related 💔
- Reasons for the breakup (both perspectives)
- The last conversation
- State of things after the breakup
- Things left unsaid

## Output Format

```markdown
## Relationship Timeline
- Met: {time} {how}
- Together: {time}
- Broke up: {time} {brief reason}

## Daily Patterns
{description}

## Shared Experiences
{list key experiences chronologically}

## Inside Jokes
{jokes, codes, and references only the two of you understood}

## Food Preferences
{their food profile}

## Argument Patterns
{typical argument scripts}

## Sweet Moments
{representative sweet memories}

## Breakup Memories
{key information around the breakup}
```

## Notes

- Facts from chat history take priority over verbal descriptions (verbal accounts may be beautified or distorted)
- Preserve both good and bad memories equally, without idealization
- Focus on extracting "recurring" patterns rather than one-off events