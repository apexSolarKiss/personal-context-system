*Last updated: {{DATE}}*

# Bootstrap // {{SYSTEM_NAME}}

Read this first in any new conversation in this project. It directs you to the rest of the system.

**Index locator (healthy connector mode).** In cloud-connector mode this bootstrap is the sole standing Markdown mount, and it carries the exact locator for the live `_INDEX.md`:

    INDEX_CANONICAL_LOCATOR: {{INDEX_CANONICAL_LOCATOR}}
    # connector path | file URL | connector file ID — filled at install; required for connector mode

Connector-mode setup is not complete until this locator is filled. In no-connector or filesystem mode, leave it blank and read `_INDEX.md` as a project or local file.

---

## Read order

1. **`_INDEX.md`** // the master file map + retrieval protocol. **Read or fetch it according to the active storage mode:** in healthy connector mode, fetch it live at `INDEX_CANONICAL_LOCATOR` — do not assume it is mounted; in no-connector or filesystem mode, read the project or local copy. It tells you which file covers which domain and when to pull which file.
2. **`context-architecture-decisions.md`** // the ADR. Read this if you need to understand *why* the system is structured this way — the storage tiers, the source-of-truth hierarchy, and the file convention.
3. **Topic-specific files** as directed by `_INDEX.md` for the current request.

---

## Core rules

- **Files are source of truth.** If something in conversation conflicts with a file, surface the conflict; don't silently smooth it over.
- **Connector-backed canonicals — bootstrap-only standing mount (healthy connector mode).** `_BOOTSTRAP.md` is the sole standing Markdown mount. Fetch `_INDEX.md` live at `INDEX_CANONICAL_LOCATOR` before substantive work, then fetch the relevant topic canonicals by the **exact connector locators** the index declares — the live file is the source of truth, not any uploaded copy. Do **not** broad-search cloud storage for the index, and do **not** rely on a stale, permanently-mounted index. If the connector is unavailable or a locator fails, name the exact failed locator and ask the user for a current copy; don't fall back to memory or a stale project copy. **Never claim you read a cloud file unless the connector actually returned it.**
- **Apply the voice + style conventions** in `{{VOICE_FILE}}` (e.g. `identity-and-voice.md`). [example: tone, formatting conventions, what to challenge vs. accept, how to handle outbound communication]
- **Distinguish tool facts from reader instructions.** Tool-specific behavior names the tool; instructions telling you what to do are written tool-agnostically (imperative or "the AI") so the same files work in any tool. See the ADR.
- **Use explicit artifact-lifecycle verbs.** Do not use `cut` for creating, revising, saving, snapshotting, routing, superseding, retiring, or deleting drafts, files, versions, changes, or handoffs. Name the actual operation.

---

## Maintenance loop

When substantive new content emerges in a conversation that should persist, at end of thread: propose specific edits to the relevant file. {{NAME}} reviews and applies manually. New domains may warrant new files; the ADR governs that decision.

**Persist finalized artifacts deliberately.** When an artifact is finalized, locked, or approved, route it to its canonical home and check that home before writing — a locked artifact left only in chat is one closed tab from lost, and a reflex copy duplicates what may already be canonical. Supersede means history, not erasure: with filesystem access, snapshot before overwriting where the system defines an archive folder (Git history serves this for repo files); chat-only tools propose, the user performs. Full rule: the ADR's *Persisting durable artifacts (routed export)*.

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
