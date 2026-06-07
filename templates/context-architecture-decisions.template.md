---
file: context-architecture-decisions.md
type: canonical-reference
generated-from: personal-context-system
source-repo: https://github.com/apexSolarKiss/personal-context-system
template-version: {{TEMPLATE_VERSION}}
template-commit: {{TEMPLATE_COMMIT}}
generated: {{DATE}}
local-system-name: {{SYSTEM_NAME}}
owner-chosen-name: {{OWNER_CHOSEN_NAME}}
---

*Last updated: {{DATE}}*

# Context Architecture // decisions + rationale

<!--
TEMPLATE — generic, tool-agnostic durable-context system.
Placeholders in {{DOUBLE_BRACES}} are filled during setup (by you or the setup interview):
  {{SYSTEM_NAME}}       = the name of YOUR system / folder. Default: personal-<YOUR-INITIALS>
                          (e.g. personal-JD). Override to anything: personal-context, my-context.
                          NOTE: this is YOUR private system. It is NOT "personal-context-system" — that is the
                          public upstream scaffold this was generated from. Don't name your private
                          system personal-context-system unless you deliberately choose to.
  {{NAME}}              = your name or handle
  {{DATE}}              = today's date, YYYY-MM-DD
  {{TEMPLATE_VERSION}}  = the upstream scaffold release tag this was generated from (e.g. v0.4.2)
  {{TEMPLATE_COMMIT}}   = the upstream scaffold commit SHA this was generated from
  {{OWNER_CHOSEN_NAME}} = whatever you decided to call your system
Lines in [square-bracket italics] are illustrative examples — replace or delete them.
This file is the ADR: it records WHY the system is shaped this way, so a future AI (or future you)
can read it instead of re-deriving the reasoning. Keep it; it is part of the payload.
-->

## Provenance

This context system was generated from the public **`personal-context-system`** scaffold by apex solar kiss:
<https://github.com/apexSolarKiss/personal-context-system>

The upstream repo provides the architecture, templates, and setup interview. **This folder is your private implementation** — its content is yours and lives only here. Keep your private context in your own folder (`{{SYSTEM_NAME}}`), separate from any clone of the public scaffold, and **never commit private content back to the upstream repo.**

Clean model: `personal-context-system` is the method artifact; `{{SYSTEM_NAME}}` is your private implementation; this provenance is the lineage bridge between them.

*Architecture Decision Record (ADR) for a durable personal-context system you own. It explains the storage tiers, the file conventions, the cross-tool bootstrap pattern, and the public/private boundary. Any AI tool reading your context should read this to understand the structure.*

---

## The principle behind all of this

You are not building "memory" for an AI tool. You are building **durable context that you own** — and AI tools (Claude, ChatGPT, whatever comes next) are rendering environments that consume it.

Tools come and go; memory features change; your files persist. The system is designed so the substance is yours and any tool can be plugged in or unplugged without losing what's been built.

**Two-year test:** if a new tool emerges and you can't drop your files into it, paste a short instruction, and have it understand you immediately — the architecture has failed.

---

## Three-tier storage model

Durable context lives in three tiers with different reliability properties across tools:

| Tier | Mechanism | Role |
|---|---|---|
| **1. Always-on preferences** | The tool's built-in preferences / memory feature, where it has one. Tool-specific; not all tools have it. | A few things that should apply in *every* conversation: tone, response style, your name, formatting preferences. Small and lean. |
| **2. Context files** | Markdown files in the tool's project/sources + an offline copy you own. Portable across tools. | The substantive durable content, organized by domain. **This is the load-bearing tier.** |
| **3. Past-conversation search** | The tool's history-search, where available. Lossy, best-effort. | Backup recall only. Never a primary store. |

**Rule:** if something matters across conversations, put it in a **file** (tier 2). Only keep something as an always-on preference (tier 1) if it is about *how the AI should behave* and you'd want it applied in literally every conversation. Don't trust thread context to survive, and don't rely on a tool's built-in preferences when the same content is needed in another tool — bias toward files.

**Quick test:** *would I want the AI to apply this in every conversation, even one about cooking or code?* If no, it's a file, not an always-on preference.

*(Advanced: in tools with a dedicated memory API — e.g. Claude's `memory_user_edits` — tier 1 maps onto that feature.)*

---

## File convention

### Naming

- **Canonical / mounted copies are clean** — no date, no decoration (e.g. `family.md`). Their *location* (your folder, or a tool's project) establishes what they are.
- **Copies in transit carry a date prefix** — `YYYY-MM-DD_<name>.md` — so a file that has lost its folder context (in Downloads, being passed between tools) carries its own provenance. Strip the date prefix on landing.

### Headers

Every file carries a date stamp at the top so staleness is visible.

- **Reference files** (low-churn, "what is true") — single line:
  ```
  *Last updated: YYYY-MM-DD*
  ```
- **Workstream / archival files** (versioned, "what's happening" / "what happened") — a small metadata block:
  ```
  ---
  file: <name>.md
  type: <reference | workstream | archival>
  version: <n or 'final'>
  updated: YYYY-MM-DD
  ---
  ```

The date tracks "I've recently confirmed this is current," not only "first written." Bump it when you re-confirm a file, even if little changed. **Stale content is worse than missing content** — it actively misleads.

---

## Bootstrap pattern (this is what makes it tool-agnostic)

Tools differ in how they load project files:
- Some auto-load every source into every conversation.
- Some use a *retrieval* model — files are available but only fetched on relevance or explicit direction, so your index may not get read automatically.

Writing one version per tool would destroy the single-source-of-truth property. The bootstrap pattern solves it instead with three thin components:

1. **A tool-side instruction field** (the "project instructions" / "custom instructions" box) — the one mechanism guaranteed to apply every conversation. ~2 sentences: *"At the start of every conversation, read `_BOOTSTRAP.md` first and follow it."*
2. **`_BOOTSTRAP.md`** (a context file) — directs the read order: `_BOOTSTRAP.md` → `_INDEX.md` → topic files. Identical across every tool.
3. **`_INDEX.md` + topic files** — the substantive system. The bootstrap just guarantees they get read.

The redundancy in auto-loading tools is a small, harmless cost; the reliability gain in retrieval tools is the value. The same files now work in any tool, present or future.

---

## Tool-agnostic writing rule

Files load into multiple tools, so they must read cleanly regardless of which AI is reading. The split:

- **Tool fact** (about a real product's UI / constraint): name the tool. *"Tool X's memory has a fixed slot cap."* These don't generalize, so accuracy needs the proper noun.
- **Reader instruction** (telling the AI what to do): generalize. Use the **imperative** (*"Read this first."*) or **"the AI"** (*"the header is what the AI reads"*). Avoid binding an instruction to one specific model name.

This keeps a file from reading as "Tool X does this" when Tool Y is the one loading it.

---

## Public / private boundary (only if external tools will touch your context)

If you let a capability-bearing tool (a coding agent, a builder, anything that can write files / push to a remote / call external services) work near your context, separate what it may inherit from what it must never reach.

- **Shareable layer** — "conform-to" material only: naming + file conventions, style preferences, project instructions, this ADR, and any identity/voice details *you have deliberately marked as safe to share*. Don't assume identity is automatically safe — share only what you've decided is. A builder tool reads this *by reference* (to conform; never copying it wholesale into its own artifacts).
- **Private layer** — everything personal: household, finances, family, health, plans, records, and any identity details you haven't cleared for sharing. Never read by or depended on by builder tooling.

**Make the boundary structural, not just a rule.** Put the inheritable layer in its own subfolder and grant a tool *only that subfolder*:

```text
{{SYSTEM_NAME}}/
  inheritable/   <- identity + voice + naming conventions + this ADR.
                    The ONLY subtree a capability-bearing tool is granted.
  ...private files... (root)   <- never granted
```

A grant scoped to `inheritable/` exposes zero private files because they live one level up, outside the grant. This replaces a behavioral wall (a tool *choosing* not to read private files) with a structural one (it *cannot* reach them). The grant boundary equals the content boundary.

> Note: this also means **anything published more widely than that trusted tool** (e.g. a public repo) must be a *genericized template*, not your live files — even inheritable files can carry personal specifics in their examples. Sanitize before publishing.
>
> And keep your private system in **its own folder**, separate from any clone of a public scaffold you generated it from. A scaffold clone is disposable installer source; your private context lives elsewhere and is **never committed back** to it.

---

## Source-of-truth hierarchy

When memory, files, and conversation disagree:

1. **A file wins over always-on preferences.** Files are your maintained source of truth; built-in preferences/memory are lossy behavioral compression.
2. **The most recent dated copy wins.** If two copies drift, the newer timestamp is authoritative.
3. **The in-file header wins over the filename.** The header is what the AI reads.

---

## Retrieval protocol (default AI behavior)

1. Read `_INDEX.md` first in any new conversation.
2. Read the relevant topic file before doing substantive work in its domain.
3. For multi-domain requests, pull every relevant file.
4. When something changes in a domain, update that file directly + bump its `Last updated` date.
5. Always-on preferences hold only behavior/tone + the index pointer. New substantive content goes into **files**.
6. **"Remember this" guard.** Any request to remember/save a *substantive* fact (about people, finances, plans, records — not a behavioral instruction) requires reading the relevant file *first*. If the fact is already there, say so and stop. Saving substantive facts to a tool's built-in memory is the exception; the file is the destination.

---

## Maintenance discipline

When new information arrives, ask:

1. **Behavioral or substantive?** Behavioral (how to engage, write, decide) → always-on-preference candidate. Substantive (facts, decisions, plans, records) → file candidate.
2. **If substantive: does a file already exist for this domain?** Yes → update it + bump the date. No → create a new file and add it to `_INDEX.md`.
3. **If behavioral: would I want this in *every* conversation across all contexts?** Yes → an always-on preference (if your tool supports them). No → reconsider; it probably doesn't belong there.
4. **If unsure → default to a file.** Always-on preferences are the more limited resource.

**End-of-thread habit:** at the end of a substantive conversation, ask the AI *"what new content should be added to which file? Propose specific edits."* Review (you are the source of truth), apply offline, bump the date, re-sync to each tool. Skipping this is how files go stale and thread thinking gets lost.

---

## Persisting durable artifacts (routed export)

When an artifact is **finalized, locked, or approved**, persist it deliberately — don't leave it living only as chat text, and don't dump a reflex copy somewhere arbitrary.

- **Conversation is not storage.** A locked artifact that exists only in a chat is one closed tab from lost.
- **Finalization triggers the review — not every output.** The trigger is a *finalized, durable* artifact; ephemeral one-offs are not filed.
- **Persist = route to its canonical home**, not "dump to a scratch/outputs folder":
  - a **repo deliverable** lives in its repo;
  - a **context edit** becomes a transit copy for loading into the relevant project;
  - a **loose durable artifact** with no repo home goes to the system's scratch / outputs location;
  - an **ephemeral one-off** is not filed.
- **Check the home before writing.** Inspect what's already there; decide update vs. no-op vs. new artifact — so you don't duplicate something already versioned.
- **Supersede means history, not erasure.** Where the acting tool has filesystem write access, check-before-write carries a snapshot obligation: if the system defines an archive/snapshot folder, write a dated snapshot there before (or alongside) any canonical overwrite — unless a current byte-identical snapshot already exists. If the artifact belongs to a Git repo, Git history *is* the snapshot. A chat-only tool proposes the edit; the user performs the file/snapshot step. Prior snapshots are not deleted as ordinary update work.

---

## Safety — what not to store here

Assume **anything in these files can be surfaced by any AI tool you upload them to.** Don't store passwords, full account numbers, private keys, or anything you wouldn't want appearing in a generated answer. This system is a *context layer* for helping AI tools understand you — **not** a password manager, legal archive, medical-record vault, or financial ledger. Keep sensitive source records elsewhere and reference them here only at the level of detail actually needed (e.g. "lease renews each spring," not the document; "primary checking at [bank]," not the account number).

---

## Keep it simple to start

Start with the smallest structure that captures you: an identity/voice file, plus a handful of domain files for the parts of your life you actually want the AI to hold. Add files only when a conversation produces content that fits nowhere. A system you maintain beats an elaborate one you abandon.
