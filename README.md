# personal-context-system

![personal-context-system banner](personal-context-system-banner.jpeg)

**`personal-context-system` is the public, ASK-origin scaffold for building a tool-agnostic, durable personal context system. It does NOT contain anyone's private personal context.**

When you provide the setup prompt to your AI tool, your generated context system lands in a private folder you own — by default `personal-<YOUR-INITIALS>`, or any name you choose — separate from this scaffold. **Never commit your private context back to this repo.**

---

## Start here: provide the setup prompt

A single entry action works across tools: **provide the setup prompt.** The prompt detects the environment, chooses the right path, and guides the setup from there.

You do not need to understand GitHub, clone a repo, or choose a tool-specific workflow before starting. The setup prompt carries every template it needs inline, so one file is enough.

**Universal start**

1. Download [`SETUP-PROMPT.md`](SETUP-PROMPT.md).
2. Attach or upload the file to your AI tool.
3. If file upload is not available, open the file and paste its full contents into the prompt composer.

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

Attach/upload of the one self-contained `SETUP-PROMPT.md` is the supported floor everywhere; URL fetch and clone are conveniences on top, never prerequisites. In standard ChatGPT setup in particular, do not depend on URL fetching, repo traversal, or a GitHub connector.

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

Three words for three things, kept distinct: the **architecture** is the design logic, documented in the ADR; the **system** is the working thing the setup prompt generates for you; the **repo** is the scaffold that delivers both. That is why it is named `personal-context-system` — the deliverable is a working system, not a static design specification.

---

## What's in here

```text
README.md            // this file — public orientation
SETUP-PROMPT.md      // the one self-contained deliverable: full setup flow + all 7 templates inlined
BOOTSTRAP-PROMPT.md  // tiny hand-deliverable: a pinned URL + fetch instruction you can text to someone
templates/           // the genericized payload (.template suffix kept in the repo)
  context-architecture-decisions.template.md   // the ADR — why the system is shaped this way
  _BOOTSTRAP.template.md                        // AI-facing entry point (read-first)
  _INDEX.template.md                            // master file map + retrieval protocol
  project-instructions.template.md              // paste-in for each tool's instructions field
  identity-and-voice.template.md                // the one always-read file (portable "memory")
  domain-file.template.md                       // copyable skeleton for any life domain
  how-to-use-this-system.template.md            // owner-facing operating manual
```

`SETUP-PROMPT.md` inlines all seven templates in its **Template Appendix**, so a paste or upload of that one file carries the entire payload. The `templates/` directory is the modular maintainer / filesystem-agent source. The setup flow writes **clean final filenames** (no `.template`) into your private folder or output. The `.template` suffix stays here in the scaffold.

---

## The boundary that matters

A durable-context system is only safe if the public part and the private part never mix:

- **Public (this repo):** generic templates and a setup prompt. No real names, no private specifics.
- **Private (your folder / your saved files):** your actual context. Lives in its own place, never committed back here.

The setup prompt is built to keep that line structural, not just a good intention — for filesystem agents, separate paths, a refusal to write private content into the clone, and no automatic commits of your private folder; for chat-only tools, a private system name and a save destination that is never this repo. If you only remember one thing: **your context is yours and lives with you; this repo is just the installer.**

---

## Provenance + License

This scaffold is published by **apex solar kiss** — <https://github.com/apexSolarKiss/personal-context-system>. The name is a generic literal — it names the artifact class, legible on sight; apex solar kiss / ASK origin is carried by the `apexSolarKiss/` owner namespace and the ADR provenance frontmatter, not by the repo name. The repo carries the *method*; your generated system carries your *content* and links back here only by provenance, not by name.

Generated systems stamp this lineage into their ADR frontmatter (`source-repo`, `template-version`, `template-commit`, `generated`) so a future tool — or future you — can trace where the architecture came from.

<!-- maintainer: on merge, cut tag `v0.3.1` on the merge commit so the bootstrap URL + the in-prompt clone command resolve. -->
**This release:** `v0.3.1` — language + UX-precision patch over v0.3.0: README diction elevated to a clean product surface, attach/upload made the universal first path (paste as fallback), the URL path routed through `BOOTSTRAP-PROMPT.md`, and the system / architecture / scaffold distinction made explicit. The `v0.3.1` tag is cut on this release's merge commit; the bootstrap and the in-prompt clone command pin to it.

---

Copyright 2026 Andrew S Klug // ASK

Licensed under the Apache License 2.0 // see [`LICENSE`](LICENSE)
