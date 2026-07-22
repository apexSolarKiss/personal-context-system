# How to use this system

*This doc is for you, the owner — not for the AI. Keep it wherever you keep your notes. If future-you forgets how the system works, re-read this.*

---

## What this is

A way to give any AI tool a consistent, persistent understanding of you — your work, your voice, your context, what to surface, what to handle carefully — without re-establishing it in every conversation.

Four layers:

1. **Context files** in an offline folder you own (durable backup) and uploaded into each AI tool's project (where the AI reads them).
2. **A bootstrap file** (`_BOOTSTRAP.md`) the AI reads first in every conversation — it directs the read order.
3. **The Project Instructions block** (from `chat-tool-settings.md`) pasted into a tool's **project** instructions field — or supplied as chat-local invocation where the tool has no projects — telling the AI to read the bootstrap (works around tools that don't auto-load files). This is project invocation, not account-wide personalization.
4. **Optional account-level behavior blocks** (from `chat-tool-settings.md`) installed in a tool's account-wide custom-instructions/preferences field for cross-tool behavioral consistency — **behavior only, no life facts**, and kept lean. Where a tool has no such field, the `identity-and-voice.md` context file carries the same behavioral load.

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

If your AI tool can connect to your cloud storage, you have a cleaner option than uploading copies into every project. Keep the real files — including `_INDEX.md` — in a Dropbox or Google Drive folder you own, and give each AI project only `_BOOTSTRAP.md`, which carries the exact `_INDEX.md` locator. The AI fetches the index live, then the canonicals it names, so your files never go stale inside a project — keep only the bootstrap in the project; fetch the index and canonicals live.

If your tool has **no** connector (or it isn't on your plan), nothing changes: upload the relevant files into the project or chat as usual. Those uploads are copies — after any approved change, update the canonical folder so the copies don't drift. Connector mode is optional; the upload floor always works.

## One-time setup

1. **Create your private folder** (cloud-synced is fine), e.g. `{{SYSTEM_NAME}}`, separate from the scaffold clone. This is the durable home and canonical source of your context.
2. **Fill the files.** Start small: `identity-and-voice.md`, plus a domain file for each part of your life you want held. Use the templates; replace the placeholders.
3. **Per tool:** create a project, upload the context files (including `_BOOTSTRAP.md`, `_INDEX.md`, `context-architecture-decisions.md`), and paste the **Project Instructions** block from `chat-tool-settings.md` into the project's instructions field. (Optionally install an account-level block too — see *Chat-tool settings: which block goes where* below.)

Repeat step 3 for each tool you use. The files are identical across tools.

---

## Chat-tool settings: which block goes where

`chat-tool-settings.md` holds the exact strings you paste into tools' settings fields, split across **three distinct surfaces**. They are not interchangeable — installing the wrong block in the wrong field is how project invocation and account-wide personalization get silently collapsed. It is a **deployment-only** reference, **not a standing project source** — don't mount it as a context file (it isn't read during conversations); `_INDEX.md` lists it under deployment-only.

| Surface | Scope | Canonical block |
|---|---|---|
| ChatGPT Personalization | account-wide | `ChatGPT // Personalization // Custom Instructions` |
| Claude Chat Instructions | account-wide | `Claude Chat Settings // Instructions` |
| ChatGPT / Claude Project Instructions | project only | `Project Instructions // ChatGPT + Claude Projects` |

- **Which block goes where:** the *Project Instructions* block goes in a project's instructions field and is what invokes your context system. The two account-level blocks go in the tool's account-wide personalization/instructions field and set behavior everywhere in that tool.
- **Never paste the whole file into one field.** Install only the block named for that surface.
- **Installation is manual, and it is yours to do.** No setup tool can reach into a tool's settings UI and install these for you — it generates the strings; you paste them.
- **Verify parity yourself.** After pasting, confirm the field's contents match the block in `chat-tool-settings.md`. Parity is user-visible or user-attested — a setup tool cannot confirm a UI it can't see.
- **Account-level personalization is optional.** The account-level blocks are an extra — install them only if you want them. The system runs without them: project-mode operation needs the *Project Instructions* block plus the relevant context sources; no-Projects operation needs the supplied context plus chat-local invocation.
- **Two failure legs are separate.** "The AI is generically-worded *everywhere*" is an account-level behavior problem (check the Personalization / Instructions block); "the AI doesn't know my context *in this project*" is a project-retrieval problem (check the Project Instructions block + `_BOOTSTRAP.md` in the project). Diagnose them separately.

---

## Optional add-ons

Two things you can layer on later — both optional, neither required for the system to work:

- **Import existing context.** If you already have useful context about yourself in another AI tool, an old chat, an exported memory, or a document, you can fold it in instead of starting from scratch. Point the setup (or any later "update my context" conversation) at **one or two high-signal sources**; it will help you extract and consolidate them. Treat whatever comes out as a **draft** — you review and approve what actually lands in your files. Your files are canonical only after you've okayed the content. Agreement across sources is evidence, not proof — your review is the validation step (*synthesis is not validation*).
- **Global behavior preferences.** The project instructions make a tool behave right *inside your project*. If you also want it to treat you consistently *everywhere* in that tool, install the account-level block for that surface — `Claude Chat Settings // Instructions` or `ChatGPT // Personalization // Custom Instructions` from `chat-tool-settings.md` — into the tool's account-wide custom-instructions/preferences area. These are **behavior only — no life facts** (facts stay in your files). They are generated from your `identity-and-voice.md` preferences, but their exact deployed strings are owned durably by `chat-tool-settings.md` — change one there on purpose, then re-paste (see *Chat-tool settings: which block goes where*). The setup guide generates these blocks for you; installing them is optional.

---

## Load only what a project needs (every upload is a sharing decision)

You do not need to load every file into every AI project. For a specialized project, upload only the files that project needs. Example: a work project might need `identity-and-voice.md` and `work.md`, but not `family.md` or `health.md`.

Treat every upload as a sharing decision. If a file contains context that does not belong in that project, leave it out.

---

## Daily use

Start a new conversation in any tool's **project**. The bootstrap runs automatically — the AI reads `_BOOTSTRAP.md` → `_INDEX.md` → whatever topic files are relevant, and you don't paste anything at the start. **In no-Projects / chat-local mode there is no project to hold the invocation**, so you supply the relevant context and paste the *Project Instructions* block at the start of each chat where you want the system active.

**Is it working? — two failure legs are separate.** If the AI **doesn't know your context in a project** (generic on your specifics, wrong domain), that's a *project-retrieval* problem — most likely the *Project Instructions* block is missing from the project's instructions field, or `_BOOTSTRAP.md` isn't in the project. If instead the AI's **tone/behavior is off everywhere** (across every tool and topic), that's an *account-level behavior* problem — check the account-level block in the tool's Personalization / Instructions field. Diagnose them separately.

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

First **classify the new tool's persistent field(s)** as account-level, project-level, or chat-local — the label "Custom Instructions" alone doesn't tell you which. Then map the blocks: copy the context files into the tool's project (or supply them chat-locally), paste the *Project Instructions* block into a **project** field or use it chat-locally, and — only if you want it — paste an **account-level** behavior block into an account-wide field. Verify each pasted field matches its block. The bootstrap pattern is the trick that makes the same files work in any tool. If you ever *can't* map these surfaces at all, the architecture has failed its purpose; the substance is yours, and tools are just rendering environments.
