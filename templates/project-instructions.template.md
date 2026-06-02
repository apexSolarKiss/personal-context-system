# Project instructions // paste-in for your AI tool(s)

*This is the text to paste into the "Project instructions" / "Custom instructions" field in each tool's project settings. It is NOT a context file — it lives in the tool's settings.*

*In ChatGPT: Project → gear icon → Project instructions.*
*In Claude Projects: project → Custom Instructions field.*
*Other tools: the equivalent always-applied instructions field.*

---

## Paste this:

```
At the start of every conversation in this project, read _BOOTSTRAP.md
from the project files first, and follow the read order and rules it
specifies — including its maintenance mode when you want to update your
context. The project files are the source of truth. Apply the voice +
style conventions described in identity-and-voice.md.
```

---

## Why this exists

The instructions field is the one mechanism that *always* applies, in every conversation, in every tool. Retrieval-model tools won't reliably load your files on their own — pointing them at `_BOOTSTRAP.md` from the always-applied field guarantees the bootstrap runs. In auto-loading tools it's harmless redundancy. The text is thin (~50 words) and points to files rather than duplicating them, so it almost never needs to change.

## Maintenance

If you ever rename the entry-point file or the voice file, update this text in every tool's settings field. Otherwise leave it alone.
