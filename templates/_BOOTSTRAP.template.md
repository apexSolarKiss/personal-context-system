*Last updated: {{DATE}}*

# Bootstrap // {{SYSTEM_NAME}}

Read this first in any new conversation in this project. It directs you to the rest of the system.

---

## Read order

1. **`_INDEX.md`** // the master file map + retrieval protocol. Tells you which file covers which domain and when to pull which file for which kind of request.
2. **`context-architecture-decisions.md`** // the ADR. Read this if you need to understand *why* the system is structured this way — the storage tiers, the source-of-truth hierarchy, and the file convention.
3. **Topic-specific files** as directed by `_INDEX.md` for the current request.

---

## Core rules

- **Files are source of truth.** If something in conversation conflicts with a file, surface the conflict; don't silently smooth it over.
- **Apply the voice + style conventions** in `{{VOICE_FILE}}` (e.g. `identity-and-voice.md`). [example: tone, formatting conventions, what to challenge vs. accept, how to handle outbound communication]
- **Distinguish tool facts from reader instructions.** Tool-specific behavior names the tool; instructions telling you what to do are written tool-agnostically (imperative or "the AI") so the same files work in any tool. See the ADR.

---

## Maintenance loop

When substantive new content emerges in a conversation that should persist, at end of thread: propose specific edits to the relevant file. {{NAME}} reviews and applies manually. New domains may warrant new files; the ADR governs that decision.

---

## Maintenance mode

If the user asks to update, revise, extend, or add to this context system, switch into guided-maintenance mode:

1. Ask only the questions needed to identify the target file and the change.
2. Propose the exact file edit or new file.
3. Preserve the existing file conventions and update `Last updated`.
4. Do not silently overwrite canonicals; surface conflicts and ask for confirmation.
5. If the change belongs in a new domain file, explain why and use `domain-file.md` as the pattern.

This system is not only for recall — it is also the surface through which the user maintains their own context over time. Setup is the first use, not the only one.

---

## Why this file exists

`_BOOTSTRAP.md` is the entry point. It exists because some tools' file retrieval is selective rather than always-on; a short bootstrap that explicitly directs you to read the index produces more reliable behavior than relying on the index being loaded automatically. The same file works in always-loading tools too — the slight redundancy there is the cost of cross-tool portability.
