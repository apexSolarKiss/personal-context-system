# How to use this system

*This doc is for you, the owner — not for the AI. Keep it wherever you keep your notes. If future-you forgets how the system works, re-read this.*

---

## What this is

A way to give any AI tool a consistent, persistent understanding of you — your work, your voice, your context, what to surface, what to handle carefully — without re-establishing it in every conversation.

Four layers:

1. **Context files** in an offline folder you own (durable backup) and uploaded into each AI tool's project (where the AI reads them).
2. **A bootstrap file** (`_BOOTSTRAP.md`) the AI reads first in every conversation — it directs the read order.
3. **A short instruction** pasted into each tool's settings field that tells the AI to read the bootstrap (works around tools that don't auto-load files).
4. **Behavioral memory** (only in tools that have it) for cross-context behavioral patterns — kept lean. Where a tool has no reliable memory, the `identity-and-voice.md` file carries the same load.

The complexity is in setting it up once; using it is just "start a new conversation and the AI already knows you."

---

## Safety — what to put here (and what not to)

Assume **anything you put in these files may be surfaced by an AI tool you upload them to.** Do not store passwords, full account numbers, private keys, or anything you would not want included in a generated answer.

**This is not a vault.** It is not a password manager, legal archive, medical-record vault, or financial ledger — it's a *context layer* for helping AI tools understand you. Store sensitive source records elsewhere and reference them here only at the level of detail actually needed (e.g. "lease renews each spring," not the full document; "primary checking at [bank]," not the account number).

---

## Where things live (read this first)

Two roles to keep separate:

- **The public scaffold / setup source** — either the self-contained `SETUP-PROMPT.md`, a fetched bootstrap URL, or a local clone of `apexSolarKiss/personal-context-system`. Installer source only: disposable, updatable, public.
- **Your private context system** — a *separate* folder or saved-file location you own. Example: `~/Context/{{SYSTEM_NAME}}`. Default name `personal-<YOUR-INITIALS>` (e.g. `personal-JD`); override to anything you like (`personal-context`, `my-context`). It is **not** called `personal-context-system` unless you choose that — that's the public scaffold, not your private system.

If you use a filesystem-capable tool, setup may write your generated files directly into your private folder. If you use a chat-only tool, the AI generates the files and you save them there yourself.

**Never fill private context inside a scaffold clone, and never commit private content back to the public repo.** This avoids the obvious failure mode: accidentally committing your private life-context into a Git repo.

### Optional: cloud-connector mode (Dropbox / Google Drive)

If your AI tool can connect to your cloud storage, you have a cleaner option than uploading copies into every project. Keep the real files in a Dropbox or Google Drive folder you own, and give each AI project only the map — `_BOOTSTRAP.md` and `_INDEX.md`, with the canonical locators filled into the index. The AI reads the live files through the connector when a conversation needs them, so your canonicals never go stale inside a project.

If your tool has **no** connector (or it isn't on your plan), nothing changes: upload the relevant files into the project or chat as usual. Those uploads are copies — after any approved change, update the canonical folder so the copies don't drift. Connector mode is optional; the upload floor always works.

## One-time setup

1. **Create your private folder** (cloud-synced is fine), e.g. `{{SYSTEM_NAME}}`, separate from the scaffold clone. This is the durable home and canonical source of your context.
2. **Fill the files.** Start small: `identity-and-voice.md`, plus a domain file for each part of your life you want held. Use the templates; replace the placeholders.
3. **Per tool:** create a project, upload the context files (including `_BOOTSTRAP.md`, `_INDEX.md`, `context-architecture-decisions.md`), and paste the text from `project-instructions.md` into the project's instructions field.

Repeat step 3 for each tool you use. The files are identical across tools.

---

## Optional add-ons

Two things you can layer on later — both optional, neither required for the system to work:

- **Import existing context.** If you already have useful context about yourself in another AI tool, an old chat, an exported memory, or a document, you can fold it in instead of starting from scratch. Point the setup (or any later "update my context" conversation) at **one or two high-signal sources**; it will help you extract and consolidate them. Treat whatever comes out as a **draft** — you review and approve what actually lands in your files. Your files are canonical only after you've okayed the content.
- **Global behavior preferences.** The project instructions make a tool behave right *inside your project*. If you also want it to treat you consistently *everywhere* in that tool, paste a short **behavior-only** block — tone, formatting, pushback style, outbound-comms default, and *files win over memory* — into the tool's global custom-instructions/preferences area. Derive it from `identity-and-voice.md` and regenerate it when that file changes; **keep life facts out of it** (facts stay in your files). The setup guide can produce this block for you.

---

## Load only what a project needs (every upload is a sharing decision)

You do not need to load every file into every AI project. For a specialized project, upload only the files that project needs. Example: a work project might need `identity-and-voice.md` and `work.md`, but not `family.md` or `health.md`.

Treat every upload as a sharing decision. If a file contains context that does not belong in that project, leave it out.

---

## Daily use

Start a new conversation in any tool's project. The bootstrap runs automatically — the AI reads `_BOOTSTRAP.md` → `_INDEX.md` → whatever topic files are relevant. You don't paste anything at the start of conversations.

**Is it working?** The AI knows your name and basics, applies your voice conventions without being asked, and pulls the right context for the topic. If it's being generic, the system isn't loading — most likely the instructions paste-in is missing from the settings field, or `_BOOTSTRAP.md` isn't in the project.

---

## Keeping this system current

This system is not finished after setup. When something durable changes, start any conversation in a tool that has these files and say:

"Update my context."

The AI should interview you lightly, identify the file that should change, and propose the exact update. You review and save the file. The files remain the source of truth; the conversation is just the editing surface.

---

## End-of-thread maintenance (the habit most easily skipped)

At the end of a substantive conversation, ask: *"What new content from this conversation should be added to which file? Propose specific edits."* Then:

1. Review the proposed edits — you are the source of truth, not the AI's wording.
2. Apply them to the file in your offline folder.
3. Bump the `Last updated:` date.
4. Re-sync: re-upload the changed file to each tool (delete old, upload new).

Skip this and files go stale; stale content is worse than missing content.

---

## When something new emerges

A conversation produces content that fits no existing file → usually the answer is **a new file**, not stuffing it into an old one. Save it offline, upload to each tool, and add a one-line entry to `_INDEX.md` under the right category.

---

## When a new tool appears

Copy the context files into the new tool's project, paste the instructions text into its settings field — done. The bootstrap pattern is the trick that makes the same files work in any tool. If you ever *can't* do that, the architecture has failed its purpose; the substance is yours, and tools are just rendering environments.
