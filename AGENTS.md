# AGENTS.md

Notes and planning repo for the **ALCF 2026 summer project** (agentic
orchestration of scientific visualization on DOE HPC). The repo is
**Markdown-only**; no application code lives here. Code dependencies are pulled
in as git submodules and should not be edited from this repo.

## Repo shape

- [`notes/MM-DD-YYYY.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes)
  — daily journal. New entries follow this exact filename pattern.
- [`notes/artifacts/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts)
  — longer-lived references (project charter, setup guides, perplexity dumps).
  Linked from daily notes via relative paths.
- [`notes/scivis-literature/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/scivis-literature)
  — paper notes **exported from Zotero** using
  [`notes/note-templates/Zotero Note Import.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/note-templates/Zotero%20Note%20Import.md).
  Do not hand-edit the `%% begin annotations %% … %% end annotations %%` blocks
  or the YAML frontmatter — they get clobbered on the next Zotero re-import.
  Personal synthesis goes in the `%% begin notes %%` block or in daily notes /
  `report.md`.
- [`report.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/report.md)
  — top-level synthesis derived from the literature notes; safe to edit
  directly.
- Three git submodules, all owned upstream by NicholasSynovic — **do not commit
  changes inside them from this repo**:
    - [`paraview_mcp/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/paraview_mcp)
      (custom ParaView MCP server)
    - [`argo-opencode-integration/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/argo-opencode-integration)
      (Argo proxy + Claude/OpenCode launcher; supersedes the older standalone
      `argo-proxy` setup mentioned in some daily notes).
    - [`chatvis/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/chatvis)
      (ChatVis migration/reimplementation — the NL-to-ParaView code path).

    After cloning, run `git submodule update --init --recursive`.

## Formatting (non-default, enforced by pre-commit)

All Markdown / JS / TS / CSS / HTML / JSON / YAML is formatted by **`prettier`**
via
[`.pre-commit-config.yaml`](file:///home/nicholas/Documents/projects/alcf-viz-2026/.pre-commit-config.yaml)
(`language: system` — it runs whichever `prettier` is on `PATH`; install via
`bun add -g prettier`, `npm i -g prettier`, etc.). Settings differ from prettier
defaults — match them or the hook will rewrite your edits:

- `--tab-width 4` (4 spaces, **not** 2 — matches
  [`.editorconfig`](file:///home/nicholas/Documents/projects/alcf-viz-2026/.editorconfig)
  `indent_size = 4`)
- `--print-width 80` (hard wrap at 80;
  [`.prettierrc`](file:///home/nicholas/Documents/projects/alcf-viz-2026/.prettierrc)
  sets `proseWrap: always` so prose gets re-wrapped — expect your paragraphs to
  be rewrapped)
- `--trailing-comma es5`
- `--end-of-line lf`, `--use-tabs false`, `--insert-pragma false`
- `trim_trailing_whitespace = true`, final newline required

Format before committing (either invocation works):

```bash
prettier --write --ignore-unknown --end-of-line lf \
  --insert-pragma false --trailing-comma es5 --tab-width 4 \
  --use-tabs false --print-width 80 <files>

# or, if pre-commit is installed:
pre-commit run --all-files
```

## Writing daily notes

Existing daily notes use a consistent structure worth preserving:

- `## Homework from <prev-date>` — checklist items copied forward with `[ x ]` /
  `[ ]` (note the spaces inside brackets, used inconsistently across files —
  match the surrounding file's style rather than normalizing).
- `## Meeting with …` sections for each meeting.
- `## Weekly Task Breakdown` blocks repeat across consecutive daily files as the
  plan evolves. When updating the plan, edit the **latest** daily note rather
  than past ones.

The current plan-of-record is the week-by-week milestone list in
[`notes/artifacts/Task List.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts/Task%20List.md)
(the project charter; the older `week1a`/`week1b_deliverable.md` drafts have
been folded into this file). If a daily note conflicts with the Task List, the
more recent one wins — daily notes track reality, the Task List lags. As of the
latest notes, actual work sits around Week 6–7 but Task List Weeks 4–10 are
still unrevised. `notes/artifacts/deliverables/` exists but is currently empty.

## Project context (so suggestions stay in scope)

- **Stack**: ParaView + a custom ParaView MCP server, agent framework TBD
  (SmolAgents first, LangChain/LangGraph fallback), Argo Gateway API for LLMs,
  OpenCode as the dev-side client.
- **Primary compute**: Crux (access pending as of latest notes).
  Polaris/Sophia/Argo API are also in scope.
- **Out of scope** (per the 06-02 scope-down): INRs, MFAs, KANs, homomorphic
  data representations, neural rendering research. The 06-02 meeting narrowed
  focus toward **ParaView Docs MCP vs. ChatVis RAG benchmarking**.
- OpenCode is wired to Argo via a local `argo-proxy` on port `52675` — full
  setup is in
  [`notes/artifacts/opencode.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts/opencode.md).
  Reference that file before suggesting alternate LLM access patterns.

## Commits

Repo style is short, imperative, sentence-case subjects
(`Update tasks and add week 1 deliverable`, `Fix excessive MD formatting`). No
conventional-commits prefix. Match it.
