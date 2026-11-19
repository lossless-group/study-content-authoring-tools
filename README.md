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

Kickoff and full candidate list (including negative exemplars):
[`ai-labs/studies/context-v/explorations/Create-Study-of-Content-Authoring-Tools.md`](https://github.com/lossless-group/ai-labs/blob/main/studies/context-v/explorations/Create-Study-of-Content-Authoring-Tools.md).

## Pin criterion

- **(a) Open artifact model.** Plain files on disk are ideal; a local-first
  store with an open programmatic interface is acceptable when the project
  is open source.
- **(b) Bidirectional reach.** An agent can both read and write the same
  store the human uses, and the tool treats those writes as first-class.
- **(c) Live ecosystem.** Active maintenance and real users.

## What we are looking at, repo by repo

Working checklist for each entry:

- **Artifact on disk.** What does a vault / workspace look like on disk?
  Could a non-AI program parse it cleanly?
- **Block model.** Page, block, object, or row? How are links and
  references encoded?
- **Agent surface.** Files, local API, SDK, MCP, plugin API?
- **Sync & collaboration.** File sync, CRDT, server, P2P — and what that
  does to the "plain file" promise.

### Personal / team knowledge management (PKM, "second brains")

| Bet | Entry |
|---|---|
| Plain `.md` on disk + real-time CRDT collaboration + built-in MCP endpoint | [Baalda](./baalda) |
| Outliner (every line is a block), local Markdown / org-mode files | [Logseq](./logseq) |
| Local-first encrypted object graph with P2P sync; Markdown export | [Anytype](./anytype-ts) |
| Local-first "Notion alternative" (Rust + Flutter), optional self-hosted sync | [AppFlowy](./appflowy) |
| Hierarchical notes in SQLite, reachable via ETAPI | [Trilium](./trilium) |
| Browser-based Markdown "power tool"; pages are Markdown files on a server | [SilverBullet](./silverbullet) |

- **[Baalda](https://github.com/naveedharri/baalda)** — maintained by
  Naveed Harri. Tauri v2 desktop app (Rust core, TypeScript UI),
  Apache-2.0. Every note is a plain `.md` file on disk, *and* notes are
  co-edited in real time. Its README frames the core tension this study
  cares about: AI-editable notes need loose Markdown as source of truth,
  while real-time collaboration is usually built on CRDTs whose state is
  an opaque blob. Here because it claims to bridge the two, and ships an
  MCP endpoint for cloud agents.

- **[Logseq](https://github.com/logseq/logseq)** — maintained by the
  Logseq team. Open-source outliner over local Markdown or org-mode
  files. Very actively maintained. Here as the block-outline archetype:
  how does a block-first model serialize to plain files, and what happens
  to that as the project moves toward a database-backed version?

- **[Anytype](https://github.com/anyproto/anytype-ts)** — maintained by
  Any Association. TypeScript desktop client; the core lives in
  `anyproto/anytype-heart` (Go). Local-first, encrypted, P2P sync. Not
  Markdown on disk — here as the worked example of the broadened
  criterion: an open object-graph store an agent can drive locally.

- **[AppFlowy](https://github.com/AppFlowy-IO/AppFlowy)** — maintained by
  AppFlowy-IO. Docs, databases, kanbans, wikis; local-first with optional
  self-hosted sync. Here as the head-to-head with Anytype: the strongest
  Notion-shaped candidate that keeps data under the user's control.

- **[Trilium](https://github.com/TriliumNext/Trilium)** — maintained by
  the TriliumNext community (canonical successor to `zadam/trilium`).
  Hierarchical notes in an SQLite-backed tree with attributes and
  relations; agents reach it via ETAPI or the DB directly. Here as
  Anytype's cousin: open data model that isn't plain Markdown files.

- **[SilverBullet](https://github.com/silverbulletmd/silverbullet)** —
  maintained by Zef Hemel. Server-run, browser-based; pages are Markdown
  files on disk, extended with queries and scripting. Here as the
  "Markdown files, but programmable" end of the spectrum.

## Not pinned (yet)

Obsidian (closed-source app, open file format) is the de-facto reference
point and is covered via the `everything-as-code` study (JSONCanvas,
Bases). Other clusters in the kickoff — memos, collaborative editors
(HedgeDoc, Outline), static-site pipelines, long-form, wikis, editors —
are not pinned until their scope is decided.

## Reading checklist

- [ ] For each entry, find where a note/page is written and dump a sample
      artifact.
- [ ] Compare how links/backlinks are encoded across all six.
- [ ] Baalda: how does it reconcile CRDT state with the `.md` file on disk?
      What does the MCP endpoint expose?
- [ ] Logseq: file-graph vs. DB-graph — what changes for an agent?
- [ ] Anytype vs. AppFlowy: what local API / SDK does each expose?
