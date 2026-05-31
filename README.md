# personal-context-system

**`personal-context-system` is the public, ASK-origin scaffold for building a tool-agnostic, durable personal context system. It does NOT contain anyone's private personal context.**

When you run the setup prompt, the generated system is written into your own private local folder — by default `personal-<YOUR-INITIALS>`, or any name you choose — separate from this scaffold. **Never commit your private context back to this repo.**

---

## Scaffold vs. your private system (read this first)

This repo and the system you build from it are two different things, and they live in two different places:

| | `personal-context-system` (this repo) | Your private system |
|---|---|---|
| **What it is** | The public scaffold: architecture, templates, and the setup prompt. | Your actual life-context: identity, voice, domains. |
| **Who owns the content** | Apex Solar Kiss (the method artifact). | You. |
| **Where it lives** | A clone/fetch of this repo — installer source, disposable, updatable. | A **separate** local folder you own (e.g. `~/Context/personal-<initials>`). |
| **Commit to this repo?** | Yes — it's public source. | **Never.** It is private and lives outside this repo. |

The clone is the installer. Your context goes somewhere else. The setup prompt enforces this split: it asks for two paths and refuses to write your private content into the scaffold clone.

---

## What this is

A way to give any AI tool — Claude, ChatGPT, whatever comes next — a consistent, persistent understanding of you (your work, your voice, your context, what to surface, what to handle carefully) without re-establishing it in every conversation.

The core idea: **you are not building "memory" for one AI tool. You are building durable context that you own, and AI tools are rendering environments that consume it.** Tools come and go; your files persist. Drop your files into any tool, paste one short instruction, and it understands you immediately.

The mechanism is a small set of Markdown files plus a "bootstrap" pattern that makes the same files work reliably across tools — including tools that only fetch files on demand. The full rationale is in [`templates/context-architecture-decisions.template.md`](templates/context-architecture-decisions.template.md) (the architecture decision record).

---

## How to use it

1. **Clone or fetch this repo** somewhere disposable (the installer source).
2. **Run the setup prompt** — [`SETUP-PROMPT.md`](SETUP-PROMPT.md) — in your AI tool:
   - **Claude Code (or any filesystem-capable agent):** point it at `SETUP-PROMPT.md`. It can fetch this public repo and write your generated system directly into your private folder.
   - **ChatGPT (or any chat-only tool):** paste the contents of `SETUP-PROMPT.md`. It will run the interview and generate your file contents for you to save manually.
3. The prompt **interviews you**, then **generates your private system** into a folder you choose — *not* into the clone.
4. It also generates the short paste-in instruction (see [`templates/project-instructions.template.md`](templates/project-instructions.template.md)) and **guides you** to install/upload the files into each AI tool's project.

This is a public repo, so no GitHub account or connector is needed — a raw fetch or clone is enough.

---

## What's in here

```text
README.md            // this file — public orientation
SETUP-PROMPT.md      // the drop-in setup prompt (the deliverable)
templates/           // the genericized payload (.template suffix kept in the repo)
  context-architecture-decisions.template.md   // the ADR — why the system is shaped this way
  _BOOTSTRAP.template.md                        // AI-facing entry point (read-first)
  _INDEX.template.md                            // master file map + retrieval protocol
  project-instructions.template.md              // paste-in for each tool's instructions field
  identity-and-voice.template.md                // the one always-read file (portable "memory")
  domain-file.template.md                       // copyable skeleton for any life domain
  how-to-use-this-system.template.md            // owner-facing operating manual
```

The setup flow writes **clean final filenames** (no `.template`) into your private folder. The `.template` suffix stays here in the scaffold.

---

## The boundary that matters

A durable-context system is only safe if the public part and the private part never mix:

- **Public (this repo):** generic templates and a setup prompt. No real names, no private specifics.
- **Private (your folder):** your actual context. Lives in its own folder, never committed back here.

The setup prompt is built to keep that line structural, not just a good intention — separate paths, a refusal to write private content into the clone, and no automatic commits of your private folder. If you only remember one thing: **your context is yours and lives in your folder; this repo is just the installer.**

---

## Provenance + License

This scaffold is published by **apex solar kiss** — <https://github.com/apexSolarKiss/personal-context-system>. The name is a generic literal — it names the artifact class, legible on sight; apex solar kiss / ASK origin is carried by the `apexSolarKiss/` owner namespace and the ADR provenance frontmatter, not by the repo name. The repo carries the *method*; your generated system carries your *content* and links back here only by provenance, not by name.

Generated systems stamp this lineage into their ADR frontmatter (`source-repo`, `template-version`, `template-commit`, `generated`) so a future tool — or future you — can trace where the architecture came from.

**This release:** `v0.1.0` — initial commit `4c004ff`.

---

Copyright 2026 Andrew S Klug // ASK

Licensed under the Apache License 2.0 // see [`LICENSE`](LICENSE)
