# Data and Privacy Compliance

## Data Handling

All data processing in this project is done locally on the user's device. Specifically:

- Chat history is exported by the user themselves; the project provides no remote data extraction capabilities
- Exported chat history is parsed locally by Claude Code, without passing through any third-party servers
- Generated ex Skill files (persona.md, memory.md) are saved to the user's local `exes/` directory, which is excluded by `.gitignore` and will not be committed to the Git repository
- The project itself contains no data upload, remote storage, or telemetry features

The only network interaction is the conversation requests between Claude Code and the Anthropic API, which are governed by the [Anthropic Usage Policy](https://www.anthropic.com/policies).

## Legal Boundaries

**Permitted uses:**

- Extracting chat history from conversations you participated in, for personal reflection and emotional healing
- Generating AI personas based on your own memory descriptions, for personal use only

**Prohibited uses:**

- Sharing generated AI personas or conversation content publicly without the other person's knowledge or consent
- Using generated AI personas for harassment, stalking, impersonation, or fraud
- Using this project to generate any content involving minors
- Using chat history or generated content for commercial purposes or distribution

## Legal Nature of Chat History

Chat history from platforms like WeChat and QQ constitutes the user's personal data. Users have the right to export and back up conversation content they participated in. However, note that:

- Chat history contains messages from the other party, who retains corresponding rights to their messages
- Different jurisdictions have different levels of personal data protection; please comply with local laws
- This project provides technical tools only and does not constitute legal advice

## Mental Health Notice

The original intent of this project is to help users digitally archive emotional memories, not to replace real human relationships. If during use you find that you:

- Cannot stop conversing with the AI persona, affecting normal life
- Experience strong urges to contact your ex
- Feel persistently low mood or have thoughts of self-harm

Please pause use and consider seeking professional psychological counseling.

---

*This document last updated: April 2026*