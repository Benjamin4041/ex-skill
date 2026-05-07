# Detailed Installation Guide

## Claude Code Installation

### Project Installation

Run from your git repository root directory:

```bash
mkdir -p .claude/skills
git clone https://github.com/therealXiaomanChu/ex-skill .claude/skills/create-ex
```

### Global Installation

```bash
git clone https://github.com/therealXiaomanChu/ex-skill ~/.claude/skills/create-ex
```

### OpenClaw Installation

```bash
git clone https://github.com/therealXiaomanChu/ex-skill ~/.openclaw/workspace/skills/create-ex
```

---

## Dependency Installation

### Basic Dependencies (Optional)

```bash
cd .claude/skills/create-ex  # or your installation path
pip3 install -r requirements.txt
```

The only optional dependency is `Pillow`, used to read photo EXIF information. You can skip this if you don't need photo analysis.

---

## WeChat Chat History Export Guide
- Export format: txt / html / csv
- Usage: Download and install → Log into WeChat desktop → Select contact → Export

### Manual Copy

If none of the above tools are convenient, you can also:
1. Open the chat window with your ex in WeChat
2. Manually select and copy key conversations
3. Paste into a txt file
4. Use method D (upload file) when running `/create-ex`

---

## QQ Chat History Export Guide

1. Open QQ → Click ≡ in the bottom left → Settings
2. General → Chat History → Export Chat History
3. Select contact → Export as txt format
4. QQ chat history can also be directly copied and pasted

---

## FAQ

### Q: Will my data be uploaded to the cloud?
A: No. All data is stored on your local file system and will not be uploaded to any server.

### Q: Can I create Skills for multiple exes at the same time?
A: Yes. Each ex uses a different slug (alias/codename), and they are stored separately in the `exes/{slug}/` directory.

### Q: What if the WeChat export fails?
A: Try the manual copy method, or directly describe your memories of your ex to Claude.

### Q: How do I delete a created Skill?
A: Delete the corresponding `exes/{slug}/` directory.