# AGENTS.md

Notes and planning repo for the **ALCF 2026 summer project** (agentic
orchestration of scientific visualization on DOE HPC). **No application code
lives here yet** — only Markdown notes under
[`notes/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes).

## Repo shape

- [`notes/MM-DD-YYYY.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes)
  — daily journal. New entries follow this exact filename pattern.
- [`notes/artifacts/`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts)
  — longer-lived references (project charter, setup guides, perplexity dumps).
  Linked from daily notes via relative paths.
- A `paraview_mcp` git submodule existed and was **intentionally removed**
  (commit `cddbe85`). Do not re-add it; the upstream is tracked separately.

## Formatting (non-default, enforced by pre-commit)

All Markdown / JS / TS / CSS / HTML / JSON / YAML is formatted by
**`bunx prettier`** via
[`.pre-commit-config.yaml`](file:///home/nicholas/Documents/projects/alcf-viz-2026/.pre-commit-config.yaml).
The settings differ from prettier defaults — match them or the hook will rewrite
your edits:

- `--tab-width 4` (4 spaces, **not** 2 — matches
  [`.editorconfig`](file:///home/nicholas/Documents/projects/alcf-viz-2026/.editorconfig)
  `indent_size = 4`)
- `--print-width 80` (hard wrap at 80;
  [`.prettierrc`](file:///home/nicholas/Documents/projects/alcf-viz-2026/.prettierrc)
  sets `proseWrap: always` so prose gets re-wrapped)
- `--trailing-comma es5`
- `--end-of-line lf`, `--use-tabs false`, `--insert-pragma false`
- `trim_trailing_whitespace = true`, final newline required

`bun` must be installed locally for the hook to run. If you don't have `bun`,
run `prettier` manually with the flags above before committing.

Format before committing:

```bash
bunx prettier --write --ignore-unknown --end-of-line lf \
  --insert-pragma false --trailing-comma es5 --tab-width 4 \
  --use-tabs false --print-width 80 <files>
```

Or, if `pre-commit` is installed: `pre-commit run --all-files`.

## Writing daily notes

Existing daily notes use a consistent structure worth preserving:

- `## Homework from <prev-date>` — checklist items copied forward with `[ x ]` /
  `[ ]` (note the spaces inside brackets, used inconsistently across files —
  match the surrounding file's style rather than normalizing).
- `## Meeting with …` sections for each meeting.
- `## Weekly Task Breakdown` blocks repeat across consecutive daily files as the
  plan evolves. When updating the plan, edit the **latest** daily note rather
  than past ones.

The current plan-of-record is in the **most recent** `notes/MM-DD-YYYY.md` and
in
[`notes/artifacts/week1_deliverable.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts/week1_deliverable.md)
(the project charter). If a daily note conflicts with an older artifact, the
daily note wins.

## Project context (so suggestions stay in scope)

- **Stack**: ParaView + a custom ParaView MCP server, agent framework TBD
  (SmolAgents first, LangChain/LangGraph fallback), Argo Gateway API for LLMs,
  OpenCode as the dev-side client.
- **Primary compute**: Crux (access pending as of latest notes).
  Polaris/Sophia/Argo API are also in scope.
- **Out of scope** (per
  [`week1_deliverable.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts/week1_deliverable.md)
  and the 06-02 scope-down): INRs, MFAs, KANs, homomorphic data representations,
  neural rendering research. The 06-02 meeting narrowed focus toward **ParaView
  Docs MCP vs. ChatVis RAG benchmarking**.
- OpenCode is wired to Argo via a local `argo-proxy` on port `52675` — full
  setup is in
  [`notes/artifacts/opencode.md`](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/artifacts/opencode.md).
  Reference that file before suggesting alternate LLM access patterns.

## Commits

Repo style is short, imperative, sentence-case subjects
(`Update tasks and add week 1 deliverable`, `Fix excessive MD formatting`). No
conventional-commits prefix. Match it.
