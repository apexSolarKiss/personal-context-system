*Last updated: {{DATE}}*

# Project Index // {{SYSTEM_NAME}}

Read this after `_BOOTSTRAP.md` directs you here. This file is the master file map + retrieval protocol. Drill into the relevant file before substantive work.

---

## File convention (short)

- **Naming:** canonical + mounted copies use clean names; copies in transit carry a `YYYY-MM-DD_` prefix, stripped on landing. Full rule in `context-architecture-decisions.md`.
- **Headers:** every file carries a date stamp. Reference files use `*Last updated: YYYY-MM-DD*`; workstream/archival files use the metadata block.
- **Source of truth:** if a fact in the tool's built-in memory/preferences conflicts with a fact in a file, **the file wins.**

---

## Canonical storage mode

Where your canonical files actually live — one of these is true for you:

- **Local-folder canonical** — the files live in a folder you own on disk; a filesystem-capable tool reads them there directly.
- **Cloud-connector canonical** — the files live in Dropbox, Google Drive, or another service your AI tool can connect to. The locators in the file list below are the **canonical locators** (a path, file URL, or file ID, depending on the connector), and the tool reads the live files through the connector. The AI project then holds only the map (`_BOOTSTRAP.md` + `_INDEX.md`), not full copies.
- **Project-file mirror** — the files uploaded into the AI project are **copies**. If a local or cloud canonical also exists, the canonical wins and the upload is a fallback that can go stale.

This is optional. With no connector and no separate canonical folder, the uploaded project files simply *are* your working copy — the universal floor. Connector mode is an upgrade, not a requirement.

## Connector read protocol

Applies only in **cloud-connector** mode:

1. **Read the exact connector locators** named in the file list. Do **not** broad-search the user's cloud storage unless they explicitly ask.
2. **Fetch the relevant live files through the connector** before substantive work — the same read order the bootstrap directs, sourced live.
3. **If a locator fails** (connector unavailable, blocked, not on the user's plan), say **which locator failed** and ask the user to upload or paste that file. Do not reconstruct its contents from memory.
4. **The connector canonical wins over a stale project copy.** If an uploaded copy conflicts with the live file the connector returned, the live file is authoritative.
5. **A connector read is verification, not write authority.** Propose edits back through the maintenance loop; only write through a connector if the tool explicitly supports it *and* the user asks.

---

## Files

<!--
This is a STARTER set. Keep only the files that apply to you; the setup interview can
delete the rest. Add new files (and categories) as your context grows. One line each:
  **`<name>.md`** // <type> // <one-line description + when to pull it>
In cloud-connector mode, add the canonical locator so the AI fetches the right live file:
  **`<name>.md`** // <type> // canonical: `<connector path / file URL / file ID>` // <when to pull it>
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

This system can live in more than one tool (e.g. a Claude project and a ChatGPT project) at once. Files are identical across tools — when you update one, update the others. The bootstrap pattern + the pasted instruction (see `project-instructions.md`) is what guarantees the system invokes itself in each tool. Your offline folder is the durable backup and the canonical source the tools re-sync from. In cloud-connector mode there is less to re-sync: the tools read the one live canonical through the connector, so an approved edit to the cloud file is visible everywhere at once (uploaded copies, if any, are fallbacks to refresh).
