*Last updated: {{DATE}}*

# Project Index // {{SYSTEM_NAME}}

Read this after `_BOOTSTRAP.md` directs you here. This file is the master file map + retrieval protocol. Drill into the relevant file before substantive work.

---

## File convention (short)

- **Naming:** canonical + mounted copies use clean names; copies in transit carry a `YYYY-MM-DD_` prefix, stripped on landing. Full rule in `context-architecture-decisions.md`.
- **Headers:** every file carries a date stamp. Reference files use `*Last updated: YYYY-MM-DD*`; workstream/archival files use the metadata block.
- **Source of truth:** if a fact in the tool's built-in memory/preferences conflicts with a fact in a file, **the file wins.**

---

## Files

<!--
This is a STARTER set. Keep only the files that apply to you; the setup interview can
delete the rest. Add new files (and categories) as your context grows. One line each:
  **`<name>.md`** // <type> // <one-line description + when to pull it>
-->

### Bootstrap (read-first)

- **`_BOOTSTRAP.md`** // AI-facing entry point. Directs the read order: `_BOOTSTRAP.md` → `_INDEX.md` → topic files.

### Identity + voice

- **`identity-and-voice.md`** // reference // who you are at a glance + how the AI should talk to you (tone, formatting, what to challenge, comms conventions). *Read in every conversation.*

### Life domains (starter set — keep only what applies)

- **`life-admin.md`** // reference // housing, logistics, recurring practicalities. *Pull for day-to-day planning.*
- **`family.md`** // reference // the people close to you the AI should know about.
- **`work.md`** // reference // what you do, current focus, working context.
- **`projects.md`** // reference // active projects worth tracking across conversations.
- **`health.md`** // reference // health context you want considered — keep it high-level (see the safety note in `how-to-use-this-system.md`).

### Meta

- **`context-architecture-decisions.md`** // the ADR. Read to understand *why* the system is structured this way. Also carries the public/private boundary if external tools touch this context.

---

## Retrieval protocol

1. If a request touches anything in the file list above, read the relevant file before substantive work.
2. For multi-domain requests, pull every relevant file together.
3. When something changes in a domain, update that file directly + bump its `Last updated` date.
4. Always-on preferences hold only behavior/tone + this index pointer. New substantive content goes into files.

---

## Cross-tool deployment

This system can live in more than one tool (e.g. a Claude project and a ChatGPT project) at once. Files are identical across tools — when you update one, update the others. The bootstrap pattern + the pasted instruction (see `project-instructions.md`) is what guarantees the system invokes itself in each tool. Your offline folder is the durable backup and the canonical source the tools re-sync from.
