*Last updated: {{DATE}}*

# Chat tool settings // canonical paste-ins

<!--
TEMPLATE — the deployment canonical for the exact strings that get pasted into AI tools' settings fields.

This file is NOT a standing project source (don't mount it as context). It is the durable owner of the
compressed, exact deployment strings for three distinct surfaces. It is generated once during setup and
updated deliberately thereafter — a live UI edit is not canonical until it is recorded back here.

Fill the blocks below during setup:
  - The Project Instructions block is near-fixed (the bootstrap invocation); keep it thin.
  - The two account-level blocks are GENERATED from the user's CONFIRMED identity-and-voice preferences.
    Behavior only — NO life facts, names, household/health/financial/relationship/identity payload.
Delete these TEMPLATE comments and any [square-bracket italics] that don't apply when you emit the real file.
-->

*The exact strings to paste into your AI tools' settings fields. This file is a **deployment canonical**, not a context file — do not mount it as a project source. Install only the block named for each surface; never paste the whole file into one field. Account-level personalization is **optional** — generating these blocks does not install them, and you can decline either one.*

## Authority split

- **`_BOOTSTRAP.md`** — owns project invocation + the operating protocol the AI follows each conversation.
- **`identity-and-voice.md`** — owns the fuller semantic behavior: voice, formatting, pushback, communication preferences.
- **this file (`chat-tool-settings.md`)** — owns the deliberately-compressed, exact deployment strings below.
- **the live ChatGPT / Claude UI fields** — are manually-installed **deployment mirrors**. A UI edit is not canonical until it is recorded back here.

A change to your semantic behavior (`identity-and-voice.md`) does not silently rewrite these strings. Deciding to change a deployment string is a separate, explicit decision (see **Maintenance**).

---

## Project Instructions // ChatGPT + Claude Projects

*Project-scoped invocation. Paste into: **ChatGPT** Project → gear icon → Project instructions; **Claude** Project → Custom Instructions field. This is the block that makes the system invoke itself — it is not account-level personalization.*

```
At the start of every conversation in this project, read _BOOTSTRAP.md from the project files first, and follow the read order and rules it specifies — including its maintenance mode when you want to update your context. The context files named by _INDEX.md are the source of truth: they may be uploaded project files, local files, or connector-backed canonicals. Apply the voice + style conventions described in identity-and-voice.md.
```

**Cloud-connector mode — add this line only** if your canonicals live in Dropbox/Drive and this tool has a connector to them:

```
Follow the exact _INDEX.md locator that _BOOTSTRAP.md declares: fetch _INDEX.md live by that locator (do not assume the index is already mounted), then read the live canonicals it names by exact locator before substantive work; if the connector fails or a locator is missing, say which one and ask me to upload or paste that file — don't guess from memory.
```

---

## Claude Chat Settings // Instructions

*Account-level, **optional**. Paste into: **Claude** → Settings → your account instructions field. Applies across all of Claude, not just one project. **Behavior only — no life facts** (those live in your files). Generated from your confirmed `identity-and-voice.md` preferences.*

```
<!-- TEMPLATE: generate this behavior-only block from the user's CONFIRMED identity-and-voice preferences. No life facts. Cover the dimensions below; drop any the user didn't supply. -->
[Interaction mode / tone — e.g. how direct, how much hedging, register.]
[What to challenge vs. accept — where the user wants pushback and where they don't.]
[Formatting conventions — default typography / structure preferences.]
[Outbound communication default — how to handle drafting messages on their behalf.]
[Uncertainty + load-bearing-assumption handling — when supplied.]
Source of truth: durable facts live in my context files; if memory conflicts with a file, the file wins.
```

---

## ChatGPT // Personalization // Custom Instructions

*Account-level, **optional**. Paste into: **ChatGPT** → Settings → Personalization → Custom instructions. Applies across all of ChatGPT, not just one project. **Behavior only — no life facts.** A compact form of the same confirmed preferences above.*

```
<!-- TEMPLATE: generate a COMPACT behavior-only block from the SAME confirmed preferences as the Claude block. No life facts. -->
[Compact interaction mode / tone + what to challenge vs. accept + formatting + outbound default.]
Source of truth: durable facts live in my context files; if memory conflicts with a file, the file wins.
```

---

## Maintenance

The authority chain, in order — do not skip a link:

```text
semantic behavior decision (identity-and-voice.md)
  → explicit deployment-string decision (decide the string change on purpose)
  → update this file (chat-tool-settings.md) — the canonical
  → preserve the prior version under your system's snapshot conventions
  → manually paste the changed block into its named UI field
  → verify UI-to-canonical parity (the field now matches this file)
```

- A change to `identity-and-voice.md` does **not** silently rewrite these strings — decide the deployment-string change explicitly.
- A live UI edit is **not** canonical until it is recorded back into this file.
- **Supersede = history, not erasure.** When you change a deployed string, preserve the prior version under your system's snapshot conventions before overwriting — don't silently erase what was deployed.
- Never reconstruct the current strings from memory, `_BOOTSTRAP.md`, `identity-and-voice.md`, an old conversation, or a historical snapshot — this file is the record.
- Install only the block named for each surface. **Never paste the whole file into one field.**
- Account-level personalization stays **optional**. Generating a block is not installing it; declining to install either account-level block leaves your context system fully functional — project-mode operation needs the *Project Instructions* block plus the relevant context sources, and no-Projects operation needs the supplied context plus chat-local invocation.
