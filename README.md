# Second Brain PWA

A local-first, installable personal knowledge app inspired by the progressive “five levels” model described in [Yarchi’s X post](https://x.com/undefinedKi/status/2068779566479679800) and by [GBrain](https://github.com/garrytan/gbrain).

The aim is not to reproduce GBrain immediately. It is to build the smallest useful second brain first, then add retrieval and automation only when they solve a demonstrated problem.

## Original inspiration and credit

This project’s starting point and five-level framing come from Yarchi’s original article, [“How to Build an AI Second Brain With Claude and Obsidian That Gets Smarter Every Day (Full Guide)”](https://x.com/i/article/2067725011880697856), and the [companion X post](https://x.com/undefinedKi/status/2068779566479679800). Full credit for that guide and its progression from simple routing to an autonomous brain belongs to [Yarchi (`@undefinedKi`)](https://x.com/undefinedKi).

[GBrain](https://github.com/garrytan/gbrain), created by Garry Tan, is credited separately as the open-source implementation examined by the article and as a source of architectural ideas for later stages of this project.

## Product principles

- **Local first:** notes remain usable without a network connection.
- **Portable:** Markdown is the durable interchange format; import and export should work with Obsidian-style vaults.
- **Progressive:** users can stop at the simplest level that meets their needs.
- **Private by default:** no note content leaves the device without an explicit choice.
- **Evidence over magic:** generated answers should link back to their source notes and disclose missing or stale context.

## The five levels

1. **Routing** — folders, Markdown, metadata, and an index that tells the assistant where knowledge lives.
2. **Linked wiki** — wikilinks, backlinks, indexes, and navigable trails between notes.
3. **Semantic search** — retrieval by meaning when filenames and exact words are insufficient.
4. **Knowledge graph** — typed relationships for questions that require tracing people, projects, organisations, and events.
5. **Autonomous brain** — opt-in ingestion, enrichment, consolidation, and maintenance jobs.

The first release will target Levels 1 and 2. Levels 3–5 remain later, independently valuable layers rather than prerequisites.

## Why a PWA?

A Progressive Web App can provide an installable, cross-platform shell, offline reading and editing, cached application assets, notifications, and a fast path from web prototype to desktop/mobile use.

There are important constraints:

- Browser filesystem access is inconsistent, especially on iOS.
- Reliable background processing is restricted by mobile operating systems.
- Local AI models and large vector indexes may exceed practical browser resource limits.

The initial design will therefore store data locally in the browser, support explicit Markdown import/export, and keep the storage layer replaceable. Native wrappers or a small optional sync/AI service can be evaluated later without abandoning the PWA.

## Proposed technical direction

- TypeScript
- React with Vite
- PWA manifest and service worker
- IndexedDB for local application data
- Markdown as the portable source format
- A storage adapter boundary for browser storage, filesystem access, and future sync
- Web Worker-based indexing so search does not block the interface
- Optional, provider-agnostic AI adapters introduced only after the core note experience works

These are starting hypotheses, not irreversible commitments. The first milestone includes technical spikes to validate storage, offline behaviour, and Markdown round-tripping.

## First useful release

The first release should let someone:

1. Install the app.
2. Create, edit, link, and find Markdown notes while offline.
3. Navigate wikilinks and backlinks.
4. Import a small Obsidian vault without losing note content.
5. Export the complete knowledge base as readable Markdown.
6. Recover safely from an interrupted update or failed import.

## Project status

Planning. See [PLAN.md](./PLAN.md) for milestones, decisions, risks, and acceptance criteria.

## References

- [Yarchi’s original “How to Build an AI Second Brain…” article](https://x.com/i/article/2067725011880697856)
- [The companion X post framing the five progressive levels](https://x.com/undefinedKi/status/2068779566479679800)
- [GBrain repository](https://github.com/garrytan/gbrain)
- [Progressive Web Apps on MDN](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
- [Obsidian-flavoured Markdown](https://help.obsidian.md/obsidian-flavored-markdown)

## Licence

No licence has been selected yet. Until one is added, the repository is not offered under an open-source licence.
