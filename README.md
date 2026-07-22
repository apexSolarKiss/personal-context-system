# personal-context-system

![personal-context-system banner](personal-context-system-banner.jpeg)

**`personal-context-system` is the public, ASK-origin scaffold for building a tool-agnostic, durable personal context system. It does NOT contain anyone's private personal context.**

When you provide the setup prompt to your AI tool, your generated context system lands in a private folder you own — by default `personal-<YOUR-INITIALS>`, or any name you choose — separate from this scaffold. **Never commit your private context back to this repo.**

---

## Just want to try it?

Paste this into ChatGPT, Claude, or any AI chat — that is the whole start. No GitHub account, no install, no terminal:

```
Fetch this file and follow it:
https://raw.githubusercontent.com/apexSolarKiss/personal-context-system/stable/SETUP-PROMPT.md
If you can't open URLs, tell me and I'll paste the file in instead.
```

If the tool can't open links (e.g. ChatGPT without browsing), download [`SETUP-PROMPT.md`](SETUP-PROMPT.md) and upload that file to the chat instead — it carries everything inline.

*Want to understand what it is before you run it? Keep reading.*

---

## Start here: provide the setup prompt

A single entry action works across tools: **provide the setup prompt.** The prompt detects the environment, chooses the right path, and guides the setup from there.

You do not need to understand GitHub, clone a repo, or choose a tool-specific workflow before starting. The setup prompt carries every template it needs inline, so one file is enough.

**Universal start**

1. Download [`SETUP-PROMPT.md`](SETUP-PROMPT.md).
2. Attach or upload the file to your AI tool.
3. If file upload is not available, open the file and paste its full contents into the prompt composer.

**Concretely, in ChatGPT:** start a new chat, click the attach button, upload `SETUP-PROMPT.md`, and send a short message like “follow this.” No GitHub account, terminal, or clone required — uploading the one file is the whole start.

If a tool rejects `.md`, rename a copy to `SETUP-PROMPT.txt` and upload that instead. The content is plain text.

For URL-capable tools, use [`BOOTSTRAP-PROMPT.md`](BOOTSTRAP-PROMPT.md). It contains the pinned setup URL and tells the tool what to do if URL access fails.

The prompt then interviews you, generates your private context files, and guides installation into the AI tools you choose.

---

## What each tool does with it

The entry action is the same across tools: provide the setup prompt. What differs is how the prompt can continue once it has the file.

| Tool | User action | What the prompt does |
|---|---|---|
| **ChatGPT** / chat-only tools | Attach/upload `SETUP-PROMPT.md`, or paste the full contents if upload is unavailable | Interviews you and returns generated files as downloads or one labeled file at a time |
| **Claude.ai / Grok** | Attach/upload `SETUP-PROMPT.md`, or use `BOOTSTRAP-PROMPT.md` if URL fetch works | Fetches the pinned setup prompt when possible; otherwise asks for upload/paste |
| **Claude Code / Codex** | Start a session in a safe workspace folder and provide `SETUP-PROMPT.md` or `BOOTSTRAP-PROMPT.md` | Detects the working folder, clones the scaffold only if useful, keeps scaffold and private folders separate, and writes files to disk |
| **Connector-capable chat/project tools** (a Dropbox/Drive connector on your plan) | Same entry as above, then *optionally* keep canonicals in cloud storage and give the project just `_BOOTSTRAP.md`, which carries the exact `_INDEX.md` locator | Sets up the bootstrap with the index locator; the tool fetches the index and canonicals live through the connector, and asks for upload/paste if connector access fails |

Attach/upload of the one self-contained `SETUP-PROMPT.md` is the supported floor everywhere; URL fetch and clone are conveniences on top, never prerequisites. In standard ChatGPT setup in particular, do not depend on URL fetching, repo traversal, or a GitHub connector.

---

## Connector-backed canonical folder (optional)

If your AI tool can connect to cloud storage such as Dropbox or Google Drive, you can keep your context files in that cloud folder; the AI project keeps only `_BOOTSTRAP.md`, which carries the exact locator for the live `_INDEX.md` map.

In that mode the AI project doesn't store the index or any canonical as an uploaded copy. It keeps only `_BOOTSTRAP.md`, which carries the exact `_INDEX.md` locator; at the start of a conversation the AI reads `_BOOTSTRAP.md`, fetches `_INDEX.md` live by that locator, then fetches the relevant canonicals live through the connector. Neither the index nor the canonicals go stale inside a project — **keep only the bootstrap in the project; fetch the index and canonicals live.**

If the connector is unavailable, blocked, or missing from your tool or plan, fall back to uploading the relevant files (or the self-contained setup prompt). Don't let the AI guess from memory. **Connector mode is optional; the upload floor above always works.**

---

## Scaffold vs. your private system (read this first)

This repo and the system you build from it are two different things, and they live in two different places:

| | `personal-context-system` (this repo) | Your private system |
|---|---|---|
| **What it is** | The public scaffold: architecture, templates, and the setup prompt. | Your actual life-context: identity, voice, domains. |
| **Who owns the content** | Apex Solar Kiss (the method artifact). | You. |
| **Where it lives** | A clone of this repo, or the single `SETUP-PROMPT.md` file — installer source, disposable, updatable. | A **separate** place you own: a local folder (e.g. `~/Context/personal-<initials>`) for filesystem tools, or wherever you save the generated files for chat-only tools. |
| **Commit to this repo?** | Yes — it's public source. | **Never.** It is private and lives outside this repo. |

For filesystem agents, any scaffold clone is installer source, not the private destination. If the setup flow uses a clone, it asks for a separate private path and refuses to write private content into the scaffold clone. If no clone is used, the self-contained setup prompt is still enough. For chat-only tools there is no clone at all: you just pick a private system name/folder label and a place to save the generated files.

---

## What this is

A way to give any AI tool — Claude, ChatGPT, whatever comes next — a consistent, persistent understanding of you (your work, your voice, your context, what to surface, what to handle carefully) without re-establishing it in every conversation.

The core idea: **you are not building "memory" for one AI tool. You are building durable context that you own, and AI tools are rendering environments that consume it.** Tools come and go; your files persist. Drop your files into any tool, paste one short instruction, and it understands you immediately.

The mechanism is a small set of Markdown files plus a "bootstrap" pattern that makes the same files work reliably across tools. The full rationale is in [`templates/context-architecture-decisions.template.md`](templates/context-architecture-decisions.template.md) (the architecture decision record).

The **architecture** is the design logic, documented in the ADR. The **system** is what the setup prompt generates. The **repo** is the scaffold that delivers both.

---

## What's in here

```text
README.md            // this file — public orientation
SETUP-PROMPT.md      // the one self-contained deliverable: full setup flow + all templates inlined
BOOTSTRAP-PROMPT.md  // tiny hand-deliverable: a stable-aliased URL + fetch instruction you can text to someone
SHARE-KIT.md         // ready-made three-bubble chat share — the real first-touch surface
templates/           // the genericized payload (.template suffix kept in the repo)
  context-architecture-decisions.template.md   // the ADR — why the system is shaped this way
  _BOOTSTRAP.template.md                        // AI-facing entry point (read-first)
  _INDEX.template.md                            // master file map + retrieval protocol
  chat-tool-settings.template.md                // canonical paste-ins: project + two account-level surfaces
  identity-and-voice.template.md                // the one always-read file (portable "memory")
  domain-file.template.md                       // copyable skeleton for any life domain
  how-to-use-this-system.template.md            // owner-facing operating manual
```

`SETUP-PROMPT.md` inlines all its templates in its **Template Appendix**, so a paste or upload of that one file carries the entire payload. The `templates/` directory is the modular maintainer / filesystem-agent source. The setup flow writes **clean final filenames** (no `.template`) into your private folder or output. The `.template` suffix stays here in the scaffold.

---

## The boundary that matters

A durable-context system is only safe if the public part and the private part never mix:

- **Public (this repo):** generic templates and a setup prompt. No real names, no private specifics.
- **Private (your folder / your saved files):** your actual context. Lives in its own place, never committed back here.

The setup prompt is built to keep that line structural, not just a good intention — for filesystem agents, separate paths, a refusal to write private content into the clone, and no automatic commits of your private folder; for chat-only tools, a private system name and a save destination that is never this repo. If you only remember one thing: **your context is yours and lives with you; this repo is just the installer.**

---

## Upgrading an existing system (v0.6.0 → v0.7.0)

Systems generated from v0.6.0 and earlier remain valid — nothing you built is broken, and the account-level split is **opt-in**. Account-wide personalization is never turned on for you automatically; upgrading is a set of choices you make, not a migration done to you. To adopt the new three-surface settings model in an existing system:

1. **Create `chat-tool-settings.md`** in your private folder — or ask any tool that already has your context to *"update my context: add chat-tool-settings"*.
2. **Carry your existing bootstrap paste-in forward** as the *Project Instructions* block — it is unchanged.
3. **Generate the two account-level blocks** (Claude account instructions; ChatGPT Personalization) from your confirmed `identity-and-voice.md` preferences — **behavior only, no life facts**. Confirm the exact strings before you treat the file as final.
4. **Reconcile your existing meta files:** add the deployment-only entry for `chat-tool-settings.md` to your `_INDEX.md`, and add the surface map to your owner manual (`how-to-use-this-system.md`) where appropriate.
5. **Disposition any bootstrap text already installed account-wide.** v0.6.0 let no-Projects users paste the bootstrap invocation into an account-wide Custom Instructions field. If yours is there: move it to a **project** instructions field or use it chat-locally where those surfaces exist; **remove it from the account-wide behavior field** when you adopt the canonical mapping; retain it globally only through an explicit single-field fallback you mark as noncanonical.
6. **Install only the surfaces you choose.** Account-level personalization stays optional; the system runs without it — project-mode needs the *Project Instructions* block plus your context sources, no-Projects mode needs supplied context plus chat-local invocation.
7. **Verify parity** between each pasted settings field and its block.
8. **Keep any old `project-instructions.md` as history** — don't rewrite it to look current; it is lineage.

---

## Provenance + License

This scaffold is published by **apex solar kiss** — <https://github.com/apexSolarKiss/personal-context-system>. The name is a generic literal — it names the artifact class, legible on sight; apex solar kiss / ASK origin is carried by the `apexSolarKiss/` owner namespace and the ADR provenance frontmatter, not by the repo name. The repo carries the *method*; your generated system carries your *content* and links back here only by provenance, not by name.

Generated systems stamp this lineage into their ADR frontmatter (`source-repo`, `template-version`, `template-commit`, `generated`) so a future tool — or future you — can trace where the architecture came from.

For the rationale and the trust-boundary story behind this scaffold, read [*Crossing the Wall*](https://atomicspacekitten.substack.com/p/crossing-the-wall).

**This release:** `v0.7.0` — chat-tool-settings authority split (minor; backward-compatible — systems generated from v0.6.0 and earlier remain valid, see *Upgrading an existing system* above). The single `project-instructions` paste-in is replaced by a deployment canonical, `chat-tool-settings.md`, that separates four previously-collapsed concerns — semantic behavior, account-level personalization, project-level invocation, and the exact deployed strings — across **three distinct surfaces** (project instructions; Claude account instructions; ChatGPT Personalization). The template `project-instructions.template.md` is renamed to `chat-tool-settings.template.md`; the generated bundle now delivers `chat-tool-settings.md` (all three blocks) as a required file; setup gains an explicit deployment-string confirmation gate before finalizing that file, and account-level personalization is generated but installed only when the user chooses. The ADR (deployment-string authority; the no-durable-owner derivation doctrine retired), the owner manual (surface map), `_INDEX` (deployment-only entry), the setup flow, and the self-contained `SETUP-PROMPT.md` (with its inlined Template Appendix) are reconciled to match. The `v0.7.0` tag is created on this release's merge commit and `stable` is fast-forwarded to it; pin to a version tag explicitly for reproducible use.

---

Copyright 2026 Andrew S Klug // ASK

Licensed under the Apache License 2.0 // see [`LICENSE`](LICENSE)
