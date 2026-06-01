# personal-context-system

![personal-context-system banner](personal-context-system-banner.jpeg)

**`personal-context-system` is the public, ASK-origin scaffold for building a tool-agnostic, durable personal context system. It does NOT contain anyone's private personal context.**

When you run the setup prompt, the generated system is written into your own private local folder — by default `personal-<YOUR-INITIALS>`, or any name you choose — separate from this scaffold. **Never commit your private context back to this repo.**

---

## Start here: run the setup prompt

You don't fetch this whole repo to use the system. You run **one self-contained file** — [`SETUP-PROMPT.md`](SETUP-PROMPT.md) — and it does the rest: it interviews you, then generates your private context files. The prompt carries every template it needs inline (in its Template Appendix), so it works even in a tool that can't browse a repo.

**Best universal path (works in almost any AI tool):**

1. Download or open [`SETUP-PROMPT.md`](SETUP-PROMPT.md).
2. **Paste its full contents into your AI tool — or upload it as a file.**
3. The prompt interviews you and generates your private files, one labeled file at a time.

**If your tool can fetch URLs:** instead of pasting, paste the raw pinned `SETUP-PROMPT.md` URL and let the tool fetch it. (The pinned URL lives in [`BOOTSTRAP-PROMPT.md`](BOOTSTRAP-PROMPT.md) — a tiny hand-deliverable you can text to someone.)

**If your tool is filesystem-capable (Claude Code, Codex):** clone this repo and run `SETUP-PROMPT.md` from the clone. It writes your generated files directly to disk.

> The supported floor is **paste or upload of the one self-contained `SETUP-PROMPT.md` file.** Everything else (URL fetch, repo clone) is a convenience on top of that floor — not a requirement.

---

## Which path fits your tool

| Your tool | Do this | Why |
|---|---|---|
| **ChatGPT** (chat-only) | **Upload or paste** the self-contained `SETUP-PROMPT.md`. | Reliable floor — needs no URL fetching and no repo traversal. In standard ChatGPT setup, do not depend on URL fetching, repo traversal, or a GitHub connector; paste/upload is the supported floor. |
| **Claude.ai / Grok** | Paste the **raw pinned `SETUP-PROMPT.md` URL**; fall back to upload/paste if the fetch doesn't land. | These can usually fetch a raw URL, but upload/paste always works as the fallback. |
| **Claude Code / Codex** (filesystem-capable) | **Clone the repo**, run `SETUP-PROMPT.md`. | The agent reads the local templates and **writes your files directly** into your private folder. |

The one file is enough on its own. The URL and the clone are conveniences layered on top — not prerequisites.

---

## Scaffold vs. your private system (read this first)

This repo and the system you build from it are two different things, and they live in two different places:

| | `personal-context-system` (this repo) | Your private system |
|---|---|---|
| **What it is** | The public scaffold: architecture, templates, and the setup prompt. | Your actual life-context: identity, voice, domains. |
| **Who owns the content** | Apex Solar Kiss (the method artifact). | You. |
| **Where it lives** | A clone of this repo, or the single `SETUP-PROMPT.md` file — installer source, disposable, updatable. | A **separate** place you own: a local folder (e.g. `~/Context/personal-<initials>`) for filesystem tools, or wherever you save the generated files for chat-only tools. |
| **Commit to this repo?** | Yes — it's public source. | **Never.** It is private and lives outside this repo. |

For filesystem agents, the clone is the installer and your context goes somewhere else — the setup prompt asks for two paths and refuses to write your private content into the scaffold clone. For chat-only tools there is no clone at all: you just pick a private system name/folder label and a place to save the generated files.

---

## What this is

A way to give any AI tool — Claude, ChatGPT, whatever comes next — a consistent, persistent understanding of you (your work, your voice, your context, what to surface, what to handle carefully) without re-establishing it in every conversation.

The core idea: **you are not building "memory" for one AI tool. You are building durable context that you own, and AI tools are rendering environments that consume it.** Tools come and go; your files persist. Drop your files into any tool, paste one short instruction, and it understands you immediately.

The mechanism is a small set of Markdown files plus a "bootstrap" pattern that makes the same files work reliably across tools. The full rationale is in [`templates/context-architecture-decisions.template.md`](templates/context-architecture-decisions.template.md) (the architecture decision record).

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

<!-- maintainer: on merge, cut tag `v0.2.0` on the merge commit so the bootstrap URL resolves. -->
**This release:** `v0.2.0` — the self-contained setup flow (one-file `SETUP-PROMPT.md` + `BOOTSTRAP-PROMPT.md`). The `v0.2.0` tag is cut on this release's merge commit, and the bootstrap pins to it.

---

Copyright 2026 Andrew S Klug // ASK

Licensed under the Apache License 2.0 // see [`LICENSE`](LICENSE)
