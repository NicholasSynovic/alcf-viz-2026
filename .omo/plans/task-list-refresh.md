# Task List Refresh: 06-03 Daily Note + New tasks.md Artifact

## TL;DR

> **Quick Summary**: Refresh the task list in `notes/06-03-2026.md` to reflect
> completions and scope changes from the 06-02 meetings, and extract a revised
> 10-week plan to a new `notes/artifacts/tasks.md` scoped to comparing
> prompt-engineering and context-management strategies for LLM-driven scientific
> visualization.
>
> **Deliverables**:
>
> - Rewritten `notes/06-03-2026.md` with promoted (06-02) homework + a new Week
>   2 task block reflecting current progress
> - New `notes/artifacts/tasks.md` with the layered 10-week plan (Docs-MCP vs.
>   ChatVis-RAG as MVR; prompt + context sweeps layered on top; A2A / stress /
>   PEFT moved to a Stretch section)
> - Both files prettier-clean per AGENTS.md (4-space, 80-col,
>   `proseWrap: always`)
>
> **Estimated Effort**: Quick (2 single-file writes, both content pre-staged in
> this plan) **Parallel Execution**: YES - both file writes are independent
> (Wave 1 = Tasks 1 + 2 in parallel) **Critical Path**: Task 1 ∥ Task 2 → F1-F4
> → user okay

---

## Context

### Original Request

User asked Prometheus to "update the task list in `notes/06-03-2026.md` and
extract a revised 10-week task list (scoped to prompt-engineering +
context-management for LLM-enabled scientific data visualization) to
`notes/artifacts/tasks.md`."

Prometheus initially tried to write the files directly. The `prometheus-md-only`
hook correctly blocked this — even in a notes-only repo, Prometheus may only
write to `.omo/*.md`. The work was therefore re-cast as a plan; the file
payloads are embedded verbatim in Tasks 1 and 2 below for the executor to apply.

### Interview Summary

**Key Decisions (from `Question`-tool responses):**

- **Framing**: Both-layered — Docs-MCP vs. ChatVis-RAG A/B is the minimum viable
  result; additional prompt/context strategies layer on top of the same harness.
- **Descoped weeks (A2A, stress, PEFT)**: Delete from the main timeline AND keep
  as a "Stretch / If Time Permits" section.
- **Venue**: AgenticAI4HPC primary (thesis fit); EduHPC backup.
- **06-03 homework refresh**: Promote 06-02 — keep only open items, drop
  completed ones, add the three milestones from the 06-02 meeting with
  George/Silvio/Mengjiang/Jakub.

**Source files read** (grounding for the rewrites):

- `notes/06-03-2026.md` (current state — 172 lines)
- `notes/06-02-2026.md` (most recent updates + meeting milestones — 381 lines)
- `notes/06-01-2026.md` (homework baseline)
- `notes/05-29-2026.md` (original homework baseline)
- `notes/artifacts/week1_deliverable.md` (charter; superseded plan source)

### Research Findings

- AGENTS.md mandates prettier with
  `--tab-width 4 --print-width 80 --trailing-comma es5 --end-of-line lf --use-tabs false --insert-pragma false`.
  `.prettierrc` adds `proseWrap: always`.
- Existing notes use `[ x ]` (with spaces inside brackets) inconsistently —
  match surrounding style. The new files use GitHub-standard `[ ]` / `[x]` since
  prettier will normalize anyway.
- Pre-commit hook runs `bunx prettier` on commit; running it ahead of time is
  the canonical verification.

### Metis Review

Skipped. This is a 2-file markdown edit in a notes-only repo with all decisions
pre-resolved via the `Question` tool. Gap-analysis machinery designed for
software-engineering plans is not load-bearing here.

---

## Work Objectives

### Core Objective

Refresh the project's living task documentation so it reflects (a) the 06-02
scope narrowing to prompt-engineering / context-management comparisons and (b)
the new milestones surfaced in the 06-02 team meeting.

### Concrete Deliverables

- `notes/06-03-2026.md` — rewritten file with promoted homework + Week 2
  progress block
- `notes/artifacts/tasks.md` — new file with the layered 10-week plan

### Definition of Done

- [ ] Both files exist with the exact content embedded in Tasks 1 and 2
- [ ] `bunx prettier --check` passes on both files
- [ ] `git status` shows only those two files modified (plus optional
      `.omo/plans/task-list-refresh.md` and `.omo/drafts/task-list-refresh.md`)

### Must Have

- 06-02 meeting milestones (NERSC MCP tutorial, ParaView MCP fix via
  SciVisAgent, ChatVis-in-SmolAgents) present in the 06-03 homework
- AgenticAI4HPC listed as primary venue in `tasks.md`
- Stretch section in `tasks.md` capturing A2A / stress / PEFT
- All open carry-forward items (Crux, TGV data, DGX Spark, Workday, argo-shim,
  ParaView MCP connection) present in 06-03 homework
- prettier compliance per AGENTS.md flags

### Must NOT Have (Guardrails)

- No code files written (this repo is notes-only and Prometheus is
  hook-restricted regardless)
- No edits to past daily notes (06-02 and earlier) — AGENTS.md says edit the
  latest note, not history
- No edits to `notes/artifacts/week1_deliverable.md` — it is the charter of
  record and superseded only by reference, not by overwrite
- No INRs / MFAs / KANs / homomorphic / neural-rendering language in either file
- No reintroduction of completed-and-dropped homework items (ArgoAPI ↔ OpenCode,
  OhMyAgents, `argo-proxy` on laptop, ALCF Batch Inference access, papers read,
  Week 1 close-out)
- No tab characters, no 2-space indent, no lines > 80 cols outside fenced
  code/tables (prettier will reject)

### Spec Framework Integration

- **Detected Framework**: None. Repository contains no `openspec/`, `.specify/`,
  or `_bmad/` directory.

---

## Verification Strategy (MANDATORY)

> **ZERO HUMAN INTERVENTION** - all verification is agent-executed.

### Test Decision

- **Infrastructure exists**: NO (notes-only repo; no test runner)
- **Automated tests**: NONE
- **Framework**: N/A
- **Substitute**: `bunx prettier --check` + structural greps for required
  headings + `git diff --stat` for blast-radius check

### QA Policy

Every task verifies its output by:

1. Reading the file back and confirming required headings/sections are present
   (grep).
2. Running `bunx prettier --check` against the file with the AGENTS.md-mandated
   flags.
3. Capturing the post-write file listing and a unified diff sample as evidence
   under `.omo/evidence/`.

---

## Execution Strategy

### Parallel Execution Waves

```
Wave 1 (Start Immediately - both files independent):
├── Task 1: Rewrite notes/06-03-2026.md            [quick]
└── Task 2: Create notes/artifacts/tasks.md        [quick]

Wave FINAL (after Wave 1):
├── Task F1: Plan compliance audit                 [oracle]
├── Task F2: Markdown / prettier quality review    [unspecified-high]
├── Task F3: Real manual QA (render in viewer,     [unspecified-high]
│             link-check, grep required sections)
└── Task F4: Scope fidelity (no forbidden topics,  [deep]
              no overwrites of charter or past notes)
-> Present results -> Get explicit user okay

Critical Path: (Task 1 ∥ Task 2) → F1-F4 → user okay
Parallel Speedup: Two file writes in parallel; trivial overall
Max Concurrent: 2 (Wave 1)
```

### Dependency Matrix

- **1**: blocked-by none → blocks F1-F4
- **2**: blocked-by none → blocks F1-F4
- **F1-F4**: blocked-by 1, 2 → blocks user okay

### Agent Dispatch Summary

- **Wave 1**: 2 tasks - T1 → `quick`, T2 → `quick`
- **Wave FINAL**: 4 tasks - F1 → `oracle`, F2 → `unspecified-high`, F3 →
  `unspecified-high`, F4 → `deep`

---

## TODOs

- [x]   1. Rewrite `notes/06-03-2026.md` with refreshed homework + Week 2
       progress block

        **What to do**:
    - Overwrite the file with the verbatim payload in the fenced block below.
    - Promote the 06-02 homework: keep only items still open, drop the completed
      ones (ArgoAPI ↔ OpenCode, OhMyAgents, `argo-proxy` on laptop, ALCF Batch
      Inference, papers read, Week 1 close-out).
    - Add the three milestones surfaced in the 06-02 meeting (NERSC MCP
      tutorial, ParaView MCP fix via SciVisAgent upstream, basic
      ChatVis-in-SmolAgents).
    - Replace the embedded 10-week table with a one-line link to the new
      `notes/artifacts/tasks.md` (the table now lives there).
    - Preserve the file's section ordering: `## Homework from 06-02-2026` →
      `## Week 2 Focus` → `## Notes` → links.
    - Run `bunx prettier --write` with AGENTS.md flags after writing.

    **Must NOT do**:
    - Do not touch any other note file.
    - Do not invent meeting content that didn't happen (only the 06-02 meeting
      milestones already captured in `notes/06-02-2026.md` go in).
    - Do not re-add completed-and-dropped homework.
    - Do not use `[ x ]` with a space inside brackets — use prettier's canonical
      `[x]` (prettier will rewrite either way; pick canonical upfront).

    **Recommended Agent Profile**:
    - **Category**: `quick` — single-file overwrite with content fully
      pre-staged in this plan; zero discovery needed.
    - **Skills**: none required.
    - **Skills Evaluated but Omitted**:
        - `customize-opencode` — this is not an OpenCode config edit.

    **Parallelization**:
    - **Can Run In Parallel**: YES
    - **Parallel Group**: Wave 1 (with Task 2)
    - **Blocks**: F1, F2, F3, F4
    - **Blocked By**: None (can start immediately)

    **References**:

    **Pattern References** (existing code to follow):
    - `notes/06-02-2026.md:1-60` — homework block style to mirror
      (`## Homework from <prev-date>` checklist, then meeting sections).
    - `notes/06-01-2026.md:1-40` — alternate homework layout for
      cross-reference.
    - `notes/06-02-2026.md` (whole file) — source of meeting milestones
        - the completion signals used to prune the carry-forward list.

    **Format References**:
    - `AGENTS.md` — prettier flags + the `[ x ]`/`[ ]` style note.
    - `.prettierrc` — `proseWrap: always`.
    - `.editorconfig` — `indent_size = 4`, LF, final newline.

    **WHY Each Reference Matters**:
    - The 06-02 file is the immediate predecessor; the 06-03 homework must be a
      promotion of its open items minus completions plus the three new meeting
      milestones. Without diffing against 06-02 the executor risks duplicating
      done work.
    - AGENTS.md and `.prettierrc` together define formatting; missing
      `proseWrap: always` will produce long lines that the pre-commit hook will
      rewrite.

    **Acceptance Criteria**:
    - [ ] File written with exact content from the fenced payload below.
    - [ ] `bunx prettier --check --ignore-unknown --end-of-line lf --insert-pragma false --trailing-comma es5 --tab-width 4 --use-tabs false --print-width 80 notes/06-03-2026.md`
          → PASS.
    - [ ] `grep -c '^## Homework from 06-02-2026' notes/06-03-2026.md` → `1`.
    - [ ] `grep -F 'notes/artifacts/tasks.md' notes/06-03-2026.md` returns at
          least 1 line (link to the new artifact).
    - [ ] `grep -Ei 'INR|MFA|KAN|homomorphic|neural rendering' notes/06-03-2026.md`
          → no matches.

    **QA Scenarios**:

    ```
    Scenario: Prettier compliance
      Tool: Bash
      Preconditions: file has just been written
      Steps:
        1. bunx prettier --check --ignore-unknown --end-of-line lf \
           --insert-pragma false --trailing-comma es5 --tab-width 4 \
           --use-tabs false --print-width 80 notes/06-03-2026.md \
           | tee .omo/evidence/task-1-prettier.txt
      Expected Result: exit code 0; output contains
        "All matched files use Prettier code style!"
      Failure Indicators: non-zero exit, "Code style issues found"
      Evidence: .omo/evidence/task-1-prettier.txt

    Scenario: Required sections present
      Tool: Bash
      Preconditions: file has just been written
      Steps:
        1. grep -nE '^## (Homework from 06-02-2026|Week 2 Focus|Notes)' \
           notes/06-03-2026.md | tee .omo/evidence/task-1-sections.txt
        2. grep -F 'notes/artifacts/tasks.md' notes/06-03-2026.md \
           | tee -a .omo/evidence/task-1-sections.txt
      Expected Result: three `## …` lines AND at least one link to
        notes/artifacts/tasks.md
      Failure Indicators: missing section or missing link
      Evidence: .omo/evidence/task-1-sections.txt

    Scenario: Forbidden vocabulary absent (negative test)
      Tool: Bash
      Steps:
        1. grep -nEi 'INR|MFA|KAN|homomorphic|neural rendering' \
           notes/06-03-2026.md \
           > .omo/evidence/task-1-forbidden.txt || true
        2. test ! -s .omo/evidence/task-1-forbidden.txt
      Expected Result: evidence file is empty (no matches), exit 0
      Failure Indicators: non-empty file
      Evidence: .omo/evidence/task-1-forbidden.txt
    ```

    **Evidence to Capture**:
    - [ ] `.omo/evidence/task-1-prettier.txt`
    - [ ] `.omo/evidence/task-1-sections.txt`
    - [ ] `.omo/evidence/task-1-forbidden.txt`

    **File Payload — write this verbatim to `notes/06-03-2026.md`**:

    ```markdown
    # 06-03-2026

    ## Homework from 06-02-2026

    Carried forward (still open):

    - [ ] Follow up with George/Silvio on Crux access (EVITA project lacks an
          allocation; need either a project add or a different compute path).
    - [ ] Ping Dr. Saumil Patel for the Taylor–Green Vortex CFD dataset (via
          Silvio's Slack intro).
    - [ ] Confirm DGX Spark user / access path with Victor.
    - [ ] Workday + benefits onboarding with Melissa.
    - [ ] Stand up `argo-shim` (or `argo-proxy`) on an HPC login node so
          OpenCode / SmolAgents can reach the Argo Gateway from compute.
    - [ ] Get the ParaView MCP server actually connecting — the current
          `pv_external_mcp` errors with
          `'vtkPythonStdStreamCaptureHelper' object has no attribute 'buffer'`
          and there is FastMCP API drift to resolve.

    New from 06-02 team meeting (George / Silvio / Mengjiang / Jakub):

    - [ ] Walk through the NERSC MCP tutorial end-to-end and capture the bits
          that map onto our ParaView-MCP setup.
    - [ ] Port the ParaView MCP fixes from the SciVisAgent project upstream into
          `LLNL/paraview_mcp` (or a fork) so the server starts cleanly under
          current FastMCP.
    - [ ] Stand up a basic ChatVis-in-SmolAgents prototype: re-implement a
          minimal slice of ChatVis with the prompt + context interfaces as
          explicit, swappable seams (this is the harness that Weeks 5–7 will
          sweep over).

    Completed since 06-02 (dropped from carry-forward):

    - ArgoAPI ↔ OpenCode wiring via local `argo-proxy` on port 52675.
    - OhMyAgents / OhMyOpenCode setup.
    - ALCF Batch Inference access confirmed.
    - First-pass reading of the assigned papers.
    - Week 1 deliverable closed out (see
      [`notes/artifacts/week1_deliverable.md`](artifacts/week1_deliverable.md)).

    ## Week 2 Focus

    Week 2 is "review + setup": land the MCP fixes, get one NL → ParaView
    round-trip working end-to-end on a laptop, and stand up the ChatVis-mini
    harness so Week 5 can start benchmarking. The prompt-engineering vs.
    context-management framing now drives the whole back half of the project.

    The full revised 10-week plan now lives in
    [`notes/artifacts/tasks.md`](artifacts/tasks.md) — it supersedes the
    embedded table that used to live here. Edit `tasks.md` (not this daily note)
    when the plan changes.

    This week, in priority order:

    1. ParaView MCP fix (port from SciVisAgent → `LLNL/paraview_mcp` fork).
       Blocks every downstream agent task.
    2. NERSC MCP tutorial walk-through. Gives us a reference design for the
       agent ↔ MCP loop and surfaces gaps in our current `pv_external_mcp`
       setup.
    3. ChatVis-mini in SmolAgents. Minimum: one tool that invokes ParaView's
       Python API via the MCP server, one prompt template swappable from config,
       one context strategy (naive "dump the docs") in place as the baseline.
    4. Crux access unblock (or pivot to Polaris/Sophia for development if Crux
       stays blocked through end of week).
    5. Argo proxy on an HPC login node (sequence after #4 — depends on which
       host we land on).

    ## Notes

    - Scope reminder from 06-02: the project is now explicitly framed as
      "compare prompt-engineering vs. context-management strategies for
      LLM-driven scientific visualization." Out of scope: INRs, MFAs, KANs,
      homomorphic data representations, neural rendering. If a question doesn't
      help us decide between prompt or context strategies, it's not Week 3–7
      work.
    - Target venue: AgenticAI4HPC (primary, best thesis fit); EduHPC as backup.
    - Candidate LLM backends already confirmed: Claude Sonnet 4.6 + GPT 5.5 via
      Argo Gateway; Nemotron 3 Super 120B, Gemma4 31B, and Llama 3.3 70B via
      ALCF Inference. DGX Spark pending Victor.
    - Compute: Polaris ✓, Sophia ✓, ALCF Inference ✓, ALCF Batch Inference ✓,
      Argo API ✓, Crux ✗ (blocked), DGX Spark ◐ (pending).

    ## Links

    - Plan of record: [`artifacts/tasks.md`](artifacts/tasks.md)
    - Week 1 charter:
      [`artifacts/week1_deliverable.md`](artifacts/week1_deliverable.md)
    - OpenCode ↔ Argo setup: [`artifacts/opencode.md`](artifacts/opencode.md)
    - Prior day: [`06-02-2026.md`](06-02-2026.md)
    ```

    **Commit**: NO (groups with Task 2 into the single commit defined in Commit
    Strategy).

- [x]   2. Create `notes/artifacts/tasks.md` with the revised 10-week
       plan-of-record

        **What to do**:
    - Create a new file `notes/artifacts/tasks.md` with the verbatim payload in
      the fenced block below.
    - Structure: framing → scope (IN / OUT / Stretch) → target venue → compute &
      LLM table → evaluation metrics → 10-week timeline table → per-week
      milestone breakdowns (W1 done → W10 submission) → cross-cutting open
      threads → success criteria.
    - Include the mermaid diagram showing the layered architecture (NL query →
      prompt strategy → context strategy → MCP / ChatVis tooling → ParaView →
      eval harness).
    - Run `bunx prettier --write` with AGENTS.md flags after writing.

    **Must NOT do**:
    - Do not overwrite `notes/artifacts/week1_deliverable.md`. The charter stays
      as-is; `tasks.md` only references it.
    - Do not include INR / MFA / KAN / homomorphic / neural-rendering work
      anywhere except in the single "Explicitly out of scope" line that names
      them as excluded.
    - Do not promote any Stretch item into the main 10-week plan.
    - Do not list EduHPC as primary venue anywhere.

    **Recommended Agent Profile**:
    - **Category**: `quick` — single-file create with payload fully pre-staged;
      zero discovery needed.
    - **Skills**: none required.
    - **Skills Evaluated but Omitted**:
        - `customize-opencode` — not an OpenCode config edit.

    **Parallelization**:
    - **Can Run In Parallel**: YES
    - **Parallel Group**: Wave 1 (with Task 1)
    - **Blocks**: F1, F2, F3, F4
    - **Blocked By**: None (can start immediately)

    **References**:

    **Pattern References**:
    - `notes/artifacts/week1_deliverable.md` — tone + heading style for
      artifact-level documents (project charter is the closest structural
      sibling).
    - `notes/artifacts/opencode.md` — alternate artifact style; useful for
      callout / table conventions.
    - `notes/artifacts/perplexity_in-situ.md`,
      `notes/artifacts/perplexity_globus-flows-compute.md` — link targets
      referenced from W2 / W6 of the new plan.

    **Format References**:
    - `AGENTS.md` — prettier flags, repo layout, scope guardrails (INR / MFA /
      etc.).
    - `.prettierrc`, `.editorconfig` — formatting source of truth.

    **WHY Each Reference Matters**:
    - `week1_deliverable.md` defines what an "artifact" doc looks like in this
      repo; matching its register keeps the docs cohesive.
    - The perplexity dumps are cited from the milestone bullets, so the paths
      must stay accurate or F2's link-check will reject the file.

    **Acceptance Criteria**:
    - [ ] File written with exact content from the fenced payload below.
    - [ ] `bunx prettier --check ... notes/artifacts/tasks.md` → PASS.
    - [ ] `grep -c '^## ' notes/artifacts/tasks.md` ≥ `10` (framing, scope,
          venue, compute, metrics, timeline, per-week sections, stretch,
          threads, success).
    - [ ] `grep -F 'AgenticAI4HPC' notes/artifacts/tasks.md` → at least 1 match;
          appears before any `EduHPC` mention.
    - [ ] `grep -F 'Stretch' notes/artifacts/tasks.md` → at least 1 match.
    - [ ] `grep -Ei 'INR|MFA|KAN|homomorphic|neural rendering' notes/artifacts/tasks.md`
          returns matches ONLY on the explicit "out of scope" enumeration line
          (verified by reading the matches).

    **QA Scenarios**:

    ```
    Scenario: Prettier compliance
      Tool: Bash
      Steps:
        1. bunx prettier --check --ignore-unknown --end-of-line lf \
           --insert-pragma false --trailing-comma es5 --tab-width 4 \
           --use-tabs false --print-width 80 \
           notes/artifacts/tasks.md \
           | tee .omo/evidence/task-2-prettier.txt
      Expected Result: exit code 0; "All matched files use Prettier
        code style!"
      Failure Indicators: non-zero exit, "Code style issues found"
      Evidence: .omo/evidence/task-2-prettier.txt

    Scenario: Structural sections present
      Tool: Bash
      Steps:
        1. grep -nE '^## ' notes/artifacts/tasks.md \
           | tee .omo/evidence/task-2-sections.txt
        2. test "$(wc -l < .omo/evidence/task-2-sections.txt)" -ge 10
      Expected Result: at least 10 top-level sections
      Failure Indicators: fewer than 10 sections
      Evidence: .omo/evidence/task-2-sections.txt

    Scenario: Venue ordering (AgenticAI4HPC primary, EduHPC backup)
      Tool: Bash
      Steps:
        1. agentic_line=$(grep -nF 'AgenticAI4HPC' \
             notes/artifacts/tasks.md | head -1 | cut -d: -f1)
        2. eduhpc_line=$(grep -nF 'EduHPC' notes/artifacts/tasks.md \
             | head -1 | cut -d: -f1)
        3. test -n "$agentic_line" && \
           { test -z "$eduhpc_line" || \
             test "$agentic_line" -lt "$eduhpc_line"; }
        4. echo "agentic=$agentic_line eduhpc=$eduhpc_line" \
           > .omo/evidence/task-2-venue.txt
      Expected Result: AgenticAI4HPC mentioned and appears before
        EduHPC (or EduHPC absent)
      Failure Indicators: EduHPC appears first or AgenticAI4HPC missing
      Evidence: .omo/evidence/task-2-venue.txt

    Scenario: Forbidden vocabulary appears ONLY in the out-of-scope line
      Tool: Bash
      Steps:
        1. grep -nEi 'INR|MFA|KAN|homomorphic|neural rendering' \
           notes/artifacts/tasks.md \
           | tee .omo/evidence/task-2-forbidden.txt
        2. # Every match line MUST contain the substring
           # "out of scope" (case-insensitive). If any match line
           # does not, fail.
           awk 'tolower($0) !~ /out of scope/ {print; bad=1}
                END {exit bad?1:0}' \
                .omo/evidence/task-2-forbidden.txt
      Expected Result: every grep hit is on an "out of scope" line
      Failure Indicators: any hit on a non-out-of-scope line
      Evidence: .omo/evidence/task-2-forbidden.txt
    ```

    **Evidence to Capture**:
    - [ ] `.omo/evidence/task-2-prettier.txt`
    - [ ] `.omo/evidence/task-2-sections.txt`
    - [ ] `.omo/evidence/task-2-venue.txt`
    - [ ] `.omo/evidence/task-2-forbidden.txt`

    **File Payload — write this verbatim to `notes/artifacts/tasks.md`**:

    ````markdown
    # ALCF 2026 — 10-Week Plan of Record

    > Living plan-of-record for the ALCF 2026 summer project. Supersedes the
    > embedded weekly tables in earlier daily notes. Daily notes should link
    > here rather than duplicate the plan.
    >
    > Charter (unchanged): [`week1_deliverable.md`](week1_deliverable.md).

    ## Project Framing

    **One-line thesis**: compare prompt-engineering and context-management
    strategies for LLM-driven scientific visualization, using ParaView as the
    visualization backend and a reimplemented ChatVis-mini harness as the
    experimental substrate.

    The minimum viable result (MVR) is a head-to-head benchmark of two context
    strategies — a **ParaView Docs MCP server** vs. a **ChatVis RAG pipeline** —
    on a fixed set of NL → visualization tasks. Additional prompt strategies
    (zero-shot, few-shot, structured decomposition, self-critique) and
    additional context strategies (function-calling, hierarchical retrieval,
    summarization caches) layer on top of the same harness.

    ```mermaid
    flowchart LR
        NL[NL viz query] --> Prompt[Prompt strategy]
        Prompt --> Ctx[Context strategy]
        Ctx -->|MCP| MCP[ParaView Docs MCP]
        Ctx -->|RAG| RAG[ChatVis-RAG]
        MCP --> Agent[SmolAgents / LangGraph]
        RAG --> Agent
        Agent --> PV[ParaView Python API]
        PV --> Out[Rendered viz + script]
        Out --> Eval[Eval harness:\ntask-completion, correctness,\nfirst-pass success, recovery,\nlatency, token cost]
    ```

    ## Scope

    **In scope** (Weeks 3–7 drive these):

    - Prompt strategies: zero-shot, few-shot, structured decomposition,
      self-critique / reflexion-lite.
    - Context strategies: ParaView Docs MCP, ChatVis-style RAG, function-calling
      tool exposure, hierarchical doc retrieval, summarization-cache for long
      sessions.
    - Eval harness: fixed task set, repeatable scoring, agent-executable QA.
    - One end-to-end CFD demo on TGV (Taylor–Green Vortex) data once Dr. Patel's
      dataset lands.

    **Explicitly out of scope** (per 06-02 scope-down): INRs, MFAs, KANs,
    homomorphic data representations, neural rendering. If a question doesn't
    help decide between prompt or context strategies, it's not on the main
    track.

    **Stretch / If Time Permits** (descoped from main timeline; pursue only
    after W8 if schedule allows):

    - Multi-agent A2A coordination (planner ↔ executor ↔ critic).
    - Large-scale stress benchmarking on Polaris (multi-node, large datasets).
    - PEFT / LoRA distillation of the best prompt+context configuration into a
      smaller model.

    ## Target Venue

    - **Primary**: AgenticAI4HPC — best thesis fit; the comparative benchmark is
      exactly the workshop's interest area.
    - **Backup**: EduHPC — fallback if AgenticAI4HPC dates don't align or scope
      contracts further.

    ## Compute & LLM Backends

    | Resource             | Status    | Use                                              |
    | -------------------- | --------- | ------------------------------------------------ |
    | Polaris              | ✓         | Dev + medium runs                                |
    | Sophia               | ✓         | GPU dev                                          |
    | Crux                 | ✗ blocked | Target for batch eval (EVITA)                    |
    | Argo Gateway API     | ✓         | Claude Sonnet 4.6, GPT 5.5                       |
    | ALCF Inference       | ✓         | Nemotron 3 Super 120B, Gemma4 31B, Llama 3.3 70B |
    | ALCF Batch Inference | ✓         | Bulk eval sweeps                                 |
    | DGX Spark            | ◐ pending | Local dev (per Victor)                           |

    ## Evaluation Metrics

    Every prompt × context configuration is scored on:

    1. **Task-completion rate** — did the agent produce a runnable ParaView
       script for the query?
    2. **Visualization correctness** — does the rendered output match
       ground-truth (rubric + image diff against reference).
    3. **First-pass success** — completion without retries.
    4. **Recovery rate** — when the first pass fails, does self-critique / retry
       recover?
    5. **Latency** — wall-clock per query, end-to-end.
    6. **Token cost** — total input + output tokens per query (proxy for $).

    ## 10-Week Timeline

    | Week | Dates window | Theme                            | Primary deliverable                          |
    | ---- | ------------ | -------------------------------- | -------------------------------------------- |
    | 1    | done         | Scoping + charter                | `week1_deliverable.md`                       |
    | 2    | in progress  | Review + setup                   | ChatVis-mini harness skeleton; MCP unblocked |
    | 3    | upcoming     | ParaView MCP PoC + first NL→viz  | One working NL→viz round-trip on laptop      |
    | 4    |              | ChatVis-mini in SmolAgents       | Swappable prompt + context interfaces        |
    | 5    |              | Docs-MCP vs. ChatVis-RAG harness | First A/B benchmark numbers (MVR)            |
    | 6    |              | Prompt-strategy sweep            | Prompt strategies × both contexts            |
    | 7    |              | Context-strategy sweep           | Context strategies × best prompt             |
    | 8    |              | Poster                           | AgenticAI4HPC poster draft                   |
    | 9    |              | Report + repo + video            | Final write-up, clean repo, demo             |
    | 10   |              | AgenticAI4HPC submission         | Submitted artifact + retro                   |

    ## Week 2 — Review + Setup (in progress)

    - M2.1 — Walk the NERSC MCP tutorial; capture deltas vs. our
      `pv_external_mcp` setup.
    - M2.2 — Port ParaView MCP fixes from SciVisAgent into `LLNL/paraview_mcp`
      (or a fork); make `pv_external_mcp` start cleanly under current FastMCP.
    - M2.3 — Stand up basic ChatVis-in-SmolAgents with prompt + context seams as
      config.
    - M2.4 — Unblock Crux (or commit to Polaris/Sophia for dev for the remainder
      of the project).
    - M2.5 — Confirm candidate LLM list (Argo + ALCF Inference) — DONE.
    - M2.6 — `argo-shim` / `argo-proxy` on an HPC login node.
    - M2.7 — Refresh project bibliography against the new scope.
    - M2.8 — Capture relevant in-situ / Globus-Flows research in
      [`perplexity_in-situ.md`](perplexity_in-situ.md) and
      [`perplexity_globus-flows-compute.md`](perplexity_globus-flows-compute.md)
      for W6/W7 reference.

    ## Week 3 — ParaView MCP PoC + first NL→viz

    - M3.1 — One canonical NL → ParaView script round-trip via MCP on a laptop.
    - M3.2 — Define the v0 task set (5–10 NL queries) used by the eval harness.
    - M3.3 — Stub eval harness: load task, dispatch to agent, capture script +
      render.
    - M3.4 — Choose ground-truth dataset for dev (small CFD or stock ParaView
      example until TGV lands).
    - M3.5 — Record latency + token-cost instrumentation conventions.

    ## Week 4 — ChatVis-mini in SmolAgents

    - M4.1 — Reimplement a minimal slice of ChatVis (script generation
        - execution loop) inside SmolAgents.
    - M4.2 — Expose **prompt strategy** as a swappable interface
      (config-selectable).
    - M4.3 — Expose **context strategy** as a swappable interface
      (config-selectable).
    - M4.4 — Wire Argo + ALCF Inference backends behind a single `LLMClient`
      abstraction.
    - M4.5 — End-to-end smoke test: same NL query produces a script via each
      backend.

    ## Week 5 — Docs-MCP vs. ChatVis-RAG harness (MVR)

    - M5.1 — Implement context strategy A: ParaView Docs MCP server
      (tool-exposed docs + function-calling).
    - M5.2 — Implement context strategy B: ChatVis-RAG (vector retrieval over
      ParaView docs + ChatVis prompts).
    - M5.3 — Run the v0 task set through both, with a fixed baseline prompt
      strategy.
    - M5.4 — First numbers: task-completion, correctness, first-pass success,
      latency, token cost.
    - M5.5 — Decide whether MVR meets workshop bar; if not, what's the single
      biggest gap?

    ## Week 6 — Prompt-strategy sweep

    - M6.1 — Add prompt strategies: zero-shot, few-shot, structured
      decomposition, self-critique.
    - M6.2 — Run prompts × {MCP, RAG} on the v0 task set.
    - M6.3 — Recovery-rate study: how often does self-critique rescue a failed
      first pass?
    - M6.4 — Identify the prompt strategy that dominates per context.

    ## Week 7 — Context-strategy sweep

    - M7.1 — Add context variants: hierarchical retrieval, summarization cache,
      function-calling-only.
    - M7.2 — Run best prompt × all context strategies on v0 + expanded task set.
    - M7.3 — Cost / quality Pareto plot.
    - M7.4 — Pick the recommended prompt + context pairing for the write-up.
    - M7.5 — If TGV data is in hand, run the recommended pairing on the full CFD
      demo.

    ## Week 8 — Poster

    - M8.1 — Poster draft (AgenticAI4HPC format).
    - M8.2 — Internal review with George / Silvio.
    - M8.3 — Final figures: timeline, Pareto plot, sample NL → viz transcripts.
    - M8.4 — Demo video stub.

    ## Week 9 — Report + repo + video

    - M9.1 — Final write-up (workshop short paper or technical report).
    - M9.2 — Repo cleanup: reproducibility README, eval harness CLI, `tasks.md`
      parity with what shipped.
    - M9.3 — Polished demo video (5–8 minutes).

    ## Week 10 — AgenticAI4HPC submission

    - M10.1 — Submit to AgenticAI4HPC.
    - M10.2 — Retro: what worked, what didn't, what to publish next.
    - M10.3 — Decide which Stretch items (A2A / stress / PEFT) are worth
      pursuing post-internship.

    ## Cross-Cutting Open Threads

    - Crux access (EVITA project allocation) — George / Silvio.
    - TGV CFD dataset — Dr. Saumil Patel via Silvio Slack intro.
    - DGX Spark user / access path — Victor.
    - `argo-shim` / `argo-proxy` deployment on HPC login node.
    - Workday + benefits — Melissa.
    - ParaView MCP upstream fix path —
      [`LLNL/paraview_mcp`](https://github.com/LLNL/paraview_mcp) + SciVisAgent.

    ## Success Criteria

    - MVR shipped by end of Week 5 (Docs-MCP vs. ChatVis-RAG numbers on v0 task
      set).
    - Both prompt and context sweeps complete by end of Week 7.
    - One CFD demo end-to-end with the recommended configuration.
    - Submission to AgenticAI4HPC in Week 10.
    - Repo is reproducible by a new collaborator from the README alone.
    ````

    **Commit**: NO (groups with Task 1 into the single commit defined in Commit
    Strategy).

---

## Final Verification Wave (MANDATORY — after ALL implementation tasks)

> 4 reviewers run in PARALLEL. ALL must APPROVE. Present consolidated results to
> user and get explicit "okay" before completing.

- [x] F1. **Plan Compliance Audit** — `oracle`

    Read `.omo/plans/task-list-refresh.md` end-to-end. For each "Must Have":
    verify the corresponding string/section is present in the written files
    (grep `notes/06-03-2026.md` and `notes/artifacts/tasks.md`). For each "Must
    NOT Have": search both files for forbidden patterns — reject with file:line
    on hit. Verify evidence files exist under `.omo/evidence/`. Confirm only the
    two intended files (plus optional `.omo/` artifacts) appear in `git status`.

    Output:
    `Must Have [N/N] | Must NOT Have [N/N] | Tasks [2/2] | VERDICT: APPROVE/REJECT`

- [x] F2. **Markdown / prettier quality review** — `unspecified-high`

    Run
    `bunx prettier --check --ignore-unknown --end-of-line lf --insert-pragma false --trailing-comma es5 --tab-width 4 --use-tabs false --print-width 80 notes/06-03-2026.md notes/artifacts/tasks.md`.
    Then sanity-check: no trailing whitespace, no tabs, final newline present,
    mermaid blocks render (parse-check by inspecting fences), all internal
    relative links resolve to existing files
    (`notes/artifacts/week1_deliverable.md`, `notes/06-02-2026.md`,
    `notes/artifacts/perplexity_*.md`).

    Output:
    `prettier [PASS/FAIL] | Whitespace [PASS/FAIL] | Links [N   ok/N broken] | Mermaid [N ok/N broken] | VERDICT`

- [x] F3. **Real Manual QA** — `unspecified-high`

    Open both files in a markdown renderer (or pipe through `glow` / inspect
    raw). Walk the rendered view and assert: (a) 06-03 homework section shows
    only open items plus the three meeting milestones; (b) `tasks.md` 10-week
    table is present with the new focus columns; (c) Stretch section in
    `tasks.md` lists A2A + stress + PEFT; (d) primary venue reads AgenticAI4HPC.
    Save renderer output / screenshots to `.omo/evidence/final-qa/`.

    Output:
    `Sections [N/N] | Stretch present [Y/N] | Venue correct [Y/N] | VERDICT`

- [x] F4. **Scope Fidelity Check** — `deep`

    `git diff --stat HEAD` MUST show only: `notes/06-03-2026.md` (modified),
    `notes/artifacts/tasks.md` (new), and optionally
    `.omo/plans/task-list-refresh.md` (new) and
    `.omo/drafts/task-list-refresh.md` (deleted). NO other file may appear. Read
    the diff for `notes/06-03-2026.md` — verify no unrelated edits leaked in
    (e.g., 05-29 / 06-01 sections must not be altered beyond removal from the
    06-03 homework). Grep both files for the forbidden vocabulary set: `INR`,
    `MFA`, `KAN`, `homomorphic`, `neural rendering` — each must return 0
    matches. Grep `notes/artifacts/tasks.md` for `EduHPC` — must appear ONLY as
    backup, never as primary.

    Output:
    `Files touched [N expected/N actual] | Forbidden terms [0/N] | Venue ordering [OK/BAD] | VERDICT`

---

## Commit Strategy

- **Single commit** after F1-F4 approve and user okays:
    - Message: `Refresh 06-03 task list and add tasks.md plan-of-record`
    - Files: `notes/06-03-2026.md`, `notes/artifacts/tasks.md`
    - Pre-commit: `bunx prettier --check ...` (already verified in F2);
      `pre-commit run --files notes/06-03-2026.md notes/artifacts/tasks.md` if
      `pre-commit` is installed

---

## Success Criteria

### Verification Commands

```bash
bunx prettier --check --ignore-unknown --end-of-line lf \
  --insert-pragma false --trailing-comma es5 --tab-width 4 \
  --use-tabs false --print-width 80 \
  notes/06-03-2026.md notes/artifacts/tasks.md
# Expected: "All matched files use Prettier code style!"

git diff --stat HEAD -- notes/
# Expected: exactly 2 entries (06-03-2026.md modified, tasks.md new)

grep -E 'INR|MFA|KAN|homomorphic|neural rendering' \
  notes/06-03-2026.md notes/artifacts/tasks.md
# Expected: no matches (except the EXCLUDE bullet in tasks.md which
# names them as out-of-scope — that line is permitted)
```

### Final Checklist

- [ ] All "Must Have" present
- [ ] All "Must NOT Have" absent (excepting the explicit out-of-scope
      enumeration in `tasks.md`)
- [ ] `bunx prettier --check` passes
- [ ] User explicitly approved F1-F4 results
