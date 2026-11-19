# Content Authoring Tools — Study

## The question

> Which content-authoring tools treat **Markdown (and adjacent open
> formats) as first-class citizens** in their data model — such that
> an AI agent can read from and write into the same store the human
> uses, without going through an app-specific cloud API?

Two adjacent questions stay in scope:

1. Where does the tool actually *write* the file? (local FS, Git, a sync
   service that syncs files, a database that hides files, a pure cloud API)
2. What's the smallest delta a tool would need to add to be
   "agent-friendly" without becoming agent-native? (a watch-folder hook,
   a CLI export, a typed schema for blocks)

The study covers second brains / PKM, team wikis, Markdown editors, and
notebooks whose file format is Markdown or plain source code (the notebook
form of the same question: can an agent edit the notebook as a text file?).

Kickoff and full candidate list (including negative exemplars):
[`ai-labs/studies/context-v/explorations/Create-Study-of-Content-Authoring-Tools.md`](https://github.com/lossless-group/lossless-ai-labs/blob/main/studies/context-v/explorations/Create-Study-of-Content-Authoring-Tools.md).

## Pin criterion

- **(a) Open artifact model.** Plain files on disk are ideal; a local-first
  store with an open programmatic interface is acceptable when the source
  is available.
- **(b) Bidirectional reach.** An agent can both read and write the same
  store the human uses, and the tool treats those writes as first-class.
- **(c) Live ecosystem.** Active maintenance and real users.

## What we are looking at, repo by repo

Working checklist for each entry:

- **Artifact on disk.** What does a vault / workspace / notebook look like
  on disk? Could a non-AI program parse it cleanly?
- **Block model.** Page, block, object, cell, or row? How are links and
  references encoded?
- **Agent surface.** Files, local API, SDK, MCP, plugin API?
- **Sync & collaboration.** File sync, CRDT, server, P2P — and what that
  does to the "plain file" promise.
- **License shape.** Open source, open core, or source-available? It
  decides what we may build on.

### Second brains / personal knowledge management

| Bet | Entry | License |
|---|---|---|
| Plain `.md` on disk + real-time CRDT collaboration + built-in MCP endpoint | [Baalda](./baalda) | Apache-2.0 |
| Outliner (every line is a block), local Markdown / org-mode files | [Logseq](./logseq) | AGPL-3.0 |
| Block outliner storing `.sy` JSON on disk, with a local HTTP API | [SiYuan](./siyuan) | AGPL-3.0 |
| Local-first encrypted object graph with P2P sync; Markdown export | [Anytype](./anytype-ts) | Source-available (Any Source Available License 1.0) |
| Docs + whiteboard + database on a CRDT store | [AFFiNE](./affine) | Open core (MIT client, EE-licensed backend) |
| Local-first "Notion alternative" (Rust + Flutter), optional self-hosted sync | [AppFlowy](./appflowy) | AGPL-3.0 |
| Markdown notes, end-to-end encrypted sync | [Joplin](./joplin) | Open core (AGPL-3.0 apps, personal-use-licensed server) |
| End-to-end encrypted notes — the "agent can't read it" counterpoint | [Notesnook](./notesnook) | GPL-3.0 |
| Hierarchical notes in SQLite, reachable via ETAPI | [Trilium](./trilium) | AGPL-3.0 |
| Browser-based Markdown "power tool"; pages are Markdown files on a server | [SilverBullet](./silverbullet) | MIT |
| AI-first second brain: an agent that reads and searches *your* notes | [Khoj](./khoj) | AGPL-3.0 |

### Team wikis & docs

| Bet | Entry | License |
|---|---|---|
| Team wiki storing Markdown-shaped docs, with a public API | [Outline](./outline) | Source-available (BSL 1.1) |
| Open-source Notion / Confluence alternative | [Docmost](./docmost) | Open core (AGPL-3.0 + `ee/` directories) |

### Markdown editors & editor frameworks

| Bet | Entry | License |
|---|---|---|
| WYSIWYG desktop Markdown editor | [MarkText](./marktext) | MIT |
| Academic Markdown editor with Zettelkasten linking and citations | [Zettlr](./zettlr) | GPL-3.0 |
| Markdown note editor (Qt) with notebook folders on disk | [VNote](./vnote) | LGPL-3.0 |
| Plugin-driven WYSIWYG Markdown editor *framework* — how editors round-trip Markdown | [Milkdown](./milkdown) | MIT |

### Notebooks whose file is Markdown or plain source

| Bet | Entry | License |
|---|---|---|
| Elixir notebooks saved as Markdown (`.livemd`) | [Livebook](./livebook) | Apache-2.0 |
| Reactive Julia notebooks saved as plain `.jl` files | [Pluto](./pluto) | MIT |
| Deepnote's open-sourced notebook format and tooling | [Deepnote](./deepnote) | Apache-2.0 |
| MyST: a Markdown dialect for executable, citable documents | [mystmd](./mystmd) | MIT |
| Observable's notebook format, saved as plain HTML files | [Notebook Kit](./notebook-kit) | ISC |
| Markdown + SQL rendered into reports | [Evidence](./evidence) | MIT |

### Why each first-round pin is here

- **[Baalda](https://github.com/naveedharri/baalda)** — maintained by
  Naveed Harri. Tauri v2 desktop app (Rust core, TypeScript UI). Every note
  is a plain `.md` file on disk, *and* notes are co-edited in real time. Its
  README frames the core tension this study cares about: AI-editable notes
  need loose Markdown as source of truth, while real-time collaboration is
  usually built on CRDTs whose state is an opaque blob. Here because it
  claims to bridge the two, and ships an MCP endpoint for cloud agents.

- **[Logseq](https://github.com/logseq/logseq)** — maintained by the
  Logseq team. Outliner over local Markdown or org-mode files. Very actively
  maintained. Here as the block-outline archetype: how does a block-first
  model serialize to plain files, and what happens as the project moves
  toward a database-backed version?

- **[Anytype](https://github.com/anyproto/anytype-ts)** — maintained by
  Any Association. TypeScript desktop client; the core lives in
  `anyproto/anytype-heart` (Go). Local-first, encrypted, P2P sync. Not
  Markdown on disk, and source-available rather than open source — here as
  the worked example of an object-graph store an agent can drive locally.

- **[AppFlowy](https://github.com/AppFlowy-IO/AppFlowy)** — maintained by
  AppFlowy-IO. Docs, databases, kanbans, wikis; local-first with optional
  self-hosted sync. Here as the head-to-head with Anytype and AFFiNE.

- **[Trilium](https://github.com/TriliumNext/Trilium)** — maintained by
  the TriliumNext community (canonical successor to `zadam/trilium`).
  SQLite-backed tree with attributes and relations; agents reach it via
  ETAPI or the DB directly.

- **[SilverBullet](https://github.com/silverbulletmd/silverbullet)** —
  maintained by Zef Hemel. Server-run, browser-based; pages are Markdown
  files on disk, extended with queries and scripting. Here as the
  "Markdown files, but programmable" end of the spectrum.

## Not pinned (yet)

- **Obsidian** (closed-source app, open file format) is the de-facto
  reference point; covered via the `everything-as-code` study (JSONCanvas,
  Bases). **Quarto** lives there too.
- **Jupyter / marimo / Jupytext / Runme** were candidates for the notebook
  section and are not pinned yet.
- Other kickoff categories — memos, HedgeDoc, static-site pipelines,
  long-form, wikis — are not pinned until their scope is decided.
- Archived or stale: Reor (archived), Athens (no pushes since 2023),
  Dendron (no pushes in a year).

## Reading checklist

- [ ] For each entry, find where a note/page/notebook is written and dump a
      sample artifact.
- [ ] Compare how links/backlinks are encoded across the PKM entries.
- [ ] Baalda vs. AFFiNE: plain files + CRDT vs. CRDT as the source of truth.
      What does Baalda's MCP endpoint expose?
- [ ] Logseq vs. SiYuan: file-graph vs. JSON-on-disk vs. DB-graph — what
      changes for an agent?
- [ ] Anytype vs. AppFlowy vs. AFFiNE: what local API / SDK does each expose?
- [ ] Notebooks: which formats let an agent edit a cell with a plain text
      diff, and which need a format-aware tool?
- [ ] License shape per entry: what's open source, what's open core, what's
      source-available.
