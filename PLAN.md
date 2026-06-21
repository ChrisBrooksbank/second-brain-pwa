# Second Brain PWA — Delivery Plan

## Objective

Build a private, local-first PWA that begins as a dependable Markdown and linked-wiki tool, while leaving deliberate extension points for semantic retrieval, a typed knowledge graph, and opt-in automation.

## Scope strategy

The project follows the five-level model from [Yarchi’s post](https://x.com/undefinedKi/status/2068779566479679800): ship the lowest useful level first and advance only when user evidence justifies the added machinery.

The architecture may borrow ideas from [GBrain](https://github.com/garrytan/gbrain)—particularly source-backed synthesis, gap reporting, hybrid retrieval, and typed relationships—but will not assume GBrain’s database, autonomous agents, or operational complexity are necessary for the initial product.

## Phase 0 — Feasibility and product decisions

**Goal:** retire the PWA-specific risks before building the product shell.

- Test installability and offline startup on current Chrome, Edge, Safari, iOS, and Android.
- Prototype durable browser storage with IndexedDB.
- Round-trip representative Obsidian Markdown, frontmatter, attachments, and wikilinks.
- Test File System Access API enhancement where supported and document the fallback.
- Measure import, search, and startup behaviour with 100, 1,000, and 10,000 notes.
- Define the threat model, backup expectations, and data-loss recovery path.

**Exit criteria**

- A written decision record for storage and import/export.
- No known path where an app update silently destroys user notes.
- A supported-platform matrix with clearly stated limitations.

## Phase 1 — Level 1: local-first Markdown

**Goal:** create an installable offline notebook that is trustworthy without AI.

- Scaffold the TypeScript application, test setup, and PWA shell.
- Add install manifest, service worker, offline shell, and update handling.
- Implement note CRUD, folders, titles, tags, and basic frontmatter.
- Add fast exact-text, filename, and metadata search.
- Add Markdown import/export and a complete backup flow.
- Add migration versioning and automated recovery tests.

**Exit criteria**

- The app installs and launches offline.
- Notes survive refreshes, browser restarts, and application updates.
- A complete export can be opened as ordinary Markdown outside the app.

## Phase 2 — Level 2: linked wiki

**Goal:** make knowledge navigable rather than merely stored.

- Parse and render `[[wikilinks]]` without corrupting source Markdown.
- Provide backlinks, unresolved-link views, and rename assistance.
- Add index/map-of-content notes and relationship navigation.
- Introduce optional daily notes and lightweight templates.
- Test import compatibility against representative Obsidian vaults.

**Exit criteria**

- Links and backlinks remain correct through note renames and exports.
- Users can trace a topic through multiple related notes without search.
- Unsupported Obsidian syntax is preserved even if it cannot be rendered.

## Phase 3 — Level 3: semantic retrieval

**Goal:** find relevant notes when the query and note use different words.

- Establish a retrieval benchmark from realistic questions and expected notes.
- Compare in-browser embeddings with an explicit opt-in remote provider.
- Run indexing outside the main UI thread and make it resumable.
- Combine lexical and semantic results with explainable ranking.
- Add citations that open the exact source note or passage.

**Promotion rule:** do not ship semantic search unless it beats lexical search on the benchmark enough to justify its cost, complexity, and privacy implications.

## Phase 4 — Level 4: typed knowledge graph

**Goal:** answer relationship questions that search alone handles poorly.

- Define a small, user-editable entity and relationship schema.
- Derive edges from explicit links and metadata before attempting AI extraction.
- Add graph inspection, correction, and provenance.
- Support bounded multi-hop questions with source citations.
- Measure graph-assisted retrieval against the Phase 3 benchmark.

**Promotion rule:** every derived edge must be inspectable, attributable, and reversible.

## Phase 5 — Level 5: opt-in automation

**Goal:** reduce maintenance without reducing user control.

- Add an inbox and explicit capture workflows first.
- Prototype scheduled deduplication, stale-note detection, and link suggestions.
- Require review queues for destructive or meaning-changing operations.
- Add audit logs, retry safety, resource budgets, and pause controls.
- Evaluate a companion service or native wrapper for work browsers cannot run reliably in the background.

**Promotion rule:** automation may suggest freely but must not silently rewrite the user’s knowledge base.

## Cross-cutting work

### Privacy and security

- Keep local data local by default.
- Encrypt sync and remote AI traffic when those options exist.
- Never place provider secrets in shipped client code.
- Make each external data transfer visible and revocable.

### Quality

- Unit tests for Markdown parsing, link resolution, migrations, and ranking.
- Browser tests for offline startup, updates, imports, and exports.
- Fixture vaults covering filenames, Unicode, attachments, frontmatter, and broken links.
- Performance budgets for startup, editing latency, search, and index size.

### Accessibility

- Keyboard-complete navigation and editing.
- Semantic controls, visible focus, and screen-reader labels.
- Respect reduced-motion and system colour preferences.

## Initial backlog

1. Create architecture decision records for framework, storage, and Markdown parsing.
2. Build the PWA/installability spike.
3. Build the Markdown round-trip and vault-import spike.
4. Benchmark IndexedDB with representative vault sizes.
5. Select the Phase 1 architecture from the spike results.
6. Scaffold the tested application shell.

## Open decisions

- Is browser-only storage sufficient for the intended vault size?
- Should filesystem access be a progressive enhancement or a desktop-wrapper feature?
- Which subset of Obsidian syntax must render in the first release?
- Is multi-device sync part of the product, or should external file sync remain the user’s choice?
- Which semantic-search modes can preserve acceptable privacy and cost?
- Should future GBrain interoperability use Markdown exchange, its CLI, or MCP?

## Definition of success

The project succeeds when the Level 1–2 product is useful and trustworthy on its own. Higher levels are successful only if they measurably improve retrieval or reduce maintenance while keeping sources, uncertainty, privacy, and user control visible.
