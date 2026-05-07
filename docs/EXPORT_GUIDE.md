# Chat History Import Guide

ex-skill accepts chat history in plain text format. You don't need any specialized export tools — here are several ways to obtain chat text.

---

## Method 1: Direct Copy-Paste (Simplest)

Open the chat window with your ex, manually select messages, copy, and paste into a txt file.

Both WeChat and QQ desktop clients support selecting multiple messages in the chat window for copying. On mobile, you can long-press a message → multi-select → copy, or use "Merge Forward" to send to your desktop client and copy from there.

The format doesn't need to be precise. As long as you can tell who said what, like:

```
Me: What are you up to
Them: Just got off work, exhausted
Me: Want to grab dinner?
Them: Nah, don't want to move
```

That level is enough. Claude can handle it.

---

## Method 2: Screenshots + Verbal Description

If the chat history is too long to copy, you can directly take screenshots and upload them. ex-skill supports image input, and Claude will extract conversation content from the screenshots.

You can also provide nothing at all, relying purely on verbal description: describe how your ex talked, their personality traits, and the story between you two. A Skill can be generated from description alone, though accuracy won't be as high as with real records.

---

## Method 3: Use Platform Built-in Backup Features

Both WeChat and QQ have official chat history backup/migration features that can sync phone records to desktop:

**WeChat:** Mobile WeChat → Settings → Chat → Chat History Migration & Backup → Migrate to WeChat Desktop

**QQ:** Mobile QQ can use "Merge Forward" to send messages to "My Computer", then copy text from desktop client after receiving

After syncing to desktop, select messages in the chat window and copy.

---

## About Third-Party Export Tools

WeChat stores chat history in locally encrypted databases. There used to be many open-source tools on GitHub that could decrypt and batch-export these, but since WeChat frequently updates its encryption methods and issues warnings against such tools, these projects generally have short lifespans.

**This project does not recommend, bundle, or include any third-party chat history decryption/export tools.** If you have the technical ability and understand the risks, you can search GitHub yourself for currently available solutions, but note:

- These tools may stop working at any time
- Using such tools may violate platform terms of service
- This project makes no guarantees about the safety or legality of third-party tools

---

## What Content is Most Valuable?

Regardless of which method you use, prioritize providing this content (in order of value):

1. **Late-night conversations** — best at revealing true personality
2. **Arguments/conflict records** — reactions during conflict are more authentic than everyday chat
3. **Conversations around the breakup** — highest emotional intensity
4. **Casual everyday chat** — accumulates habitual expressions and rhythms
5. **Voice message transcriptions** — if you have them