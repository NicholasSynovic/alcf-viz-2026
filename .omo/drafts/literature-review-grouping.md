<!--
Organized grouping of the three literature review notes in
notes/literature_review_notes/. Paste the block below (starting at the
"## Literature Review" heading content) into notes/06-03-2026.md under
the existing empty "## Literature Review" heading.

Source notes:
- An Evaluation-Centric Paradigm for Scientific Visualization Agents
  (Ai et al., 2025)            → cited below as [Evaluation-Centric, 2025]
- NL2SciVis: A Benchmark for Natural Language to Scientific Visualization
  (Mathai et al., 2026)        → cited below as [NL2SciVis, 2026]
- SciVisAgentBench: A Benchmark for Evaluating Scientific Data Analysis
  and Visualization Agents
  (Ai et al., 2026)            → cited below as [SciVisAgentBench, 2026]
-->

### 1. Methodologies for implementing a similar benchmarking tool

Concrete techniques and protocols we can reuse when building our own
prompt-engineering vs. context-management benchmark.

- **Hybrid LLM-judge + deterministic verifier protocol.** Combine a multi-modal
  LLM judge for visualization _quality_ with hard-coded verifiers (case-specific
  Python / `pvpython` scripts) that inspect the ParaView engine's internal state
  for _correctness_ of primitives and techniques. Track token usage and
  execution time as the system-perf axis. [Evaluation-Centric, 2025]
- **Two-gate deterministic scoring (Execution Gate → Technique Gate).** Gate 1:
  did the agent produce a valid PVSM state file? Gate 2: are the filter type,
  field assignment, and parameter values correct? Primary metric is pass rate
  with **Wilson 95% CIs**, **Cohen's h** for pairwise effect size, and
  **chi-squared + Bonferroni** for significance across the 15 tasks. Secondary
  metrics: lines of code, output tokens, latency. [NL2SciVis, 2026]
- **Validate against ParaView state files (PVSM), not rendered images.** PVSM
  gives direct structural access to the pipeline (filter types, field
  assignments, parameter values) and avoids the fragility of pixel-level
  comparison for non-image properties. [NL2SciVis, 2026]
- **Atomic-operation decomposition with four constraints.** Each benchmark item
  is single-intent, has strict preconditions, executes independently, and uses
  deterministic defaults. Excludes multi-step composition, derived fields, and
  qualitative goals (e.g., "make the contour more prominent"). [NL2SciVis, 2026]
- **Three-campaign experimental design.** Baseline → Prompt Enhancement →
  Scaffolding, with a **concurrent control group** during scaffolding to avoid
  cross-batch confounds. Prompt-enhancement conditions tested: documentation
  reference, job-stakes framing, threat-stakes framing, negative-reward framing.
  [NL2SciVis, 2026]
- **Outcome / Process / Efficiency tri-axis evaluation.** Outcome = black-box
  input→output; Process = action sequence, tool use, intermediate decisions;
  Efficiency = time, steps, tokens, $$. [Evaluation-Centric, 2025;
  SciVisAgentBench, 2026]
- **Multimodal outcome pipeline.** Layer five evaluator types: (1) MLLM judge
  against expert rubrics on a 0–10 scale; (2) image metrics PSNR / SSIM / LPIPS
  for tasks with controlled camera/lighting; (3) code checkers (script
  generation + execution success); (4) rule-based verifiers for multiple-choice
  / yes-no outputs; (5) case-specific evaluators. [SciVisAgentBench, 2026]
- **Rubric shuffling to mitigate LLM-judge ordering bias.** Randomly permute
  rubric order across trials; pair with a human–LLM alignment study and a
  prompt/presentation robustness study to quantify judge reliability.
  [SciVisAgentBench, 2026]
- **Checkpoint decomposition of long-horizon workflows.** Break complex
  workflows into smaller verifiable checkpoints with explicit intermediate
  outcomes, so outcome-based evaluation stays reliable even when end-to-end
  completion is fragile. [SciVisAgentBench, 2026; Evaluation-Centric, 2025]
- **Tool-agnostic agent abstraction.** Support tool-using agents (MCP-style
  APIs), code-generating agents (PvPython scripts), GUI / human-like interface
  agents (screenshots + clicks), and multi-agent / multimodal systems behind one
  evaluator interface. [SciVisAgentBench, 2026]
- **Reproducibility scaffolding.** Sandboxed execution (MCP or direct code
  execution), repeated trials (≥10–30 per cell) to quantify stochastic variance,
  serialize tasks + rubrics in YAML compatible with promptfoo.
  [Evaluation-Centric, 2025; NL2SciVis, 2026; SciVisAgentBench, 2026]
- **Code-similarity scoring caveat.** CodeBERT-style similarity between
  generated scripts and gold references was tried and **dropped** in
  SciVisAgentBench because functionally correct and incorrect scripts scored
  similarly. Use it only as a supplementary signal, not a primary metric.
  [SciVisAgentBench, 2026; Evaluation-Centric, 2025]

### 2. Background reading

Prior work, related benchmarks, and tools cited across the three papers that we
should be aware of before designing our own protocol.

**Operational definition of a SciVis agent.** "An AI system that interprets
human users' natural language intent, autonomously interacts with the SciVis
pipeline to produce visualizations that meet user-specified analysis goals."
[Evaluation-Centric, 2025]

**SciVis agent systems** (the field we are benchmarking):

- **ChatVis** — RAG-style code-generation agent for ParaView; baseline in both
  benchmarks. [Evaluation-Centric, 2025; NL2SciVis, 2026; SciVisAgentBench,
  2026]
- **ParaView-MCP** — direct MCP tool-use over a curated ParaView API; validated
  previously via case studies + expert feedback rather than systematic
  benchmarks. [Evaluation-Centric, 2025; NL2SciVis, 2026; SciVisAgentBench,
  2026]
- **AVA, NLI4VolVis, VizGenie, InferA, TexGS-VolVis, IntuiTF, VOICE, CoDA** —
  other SciVis / volume-vis agent systems. [Evaluation-Centric, 2025;
  SciVisAgentBench, 2026]
- **Magentic-UI** — agentic UI work. [Evaluation-Centric, 2025]

**General-vis / NL2VIS benchmarks** (mostly 2D / tabular, not SciVis):

- VisEval, Drawing Pandas, MatPlotAgent, nvBench, Text2Vis, NL4DV, LIDA,
  PlotGen, nvAgent, ChartLlama, NL2SQL, DA-Code, ThinkGeo, SVLAT.
  [Evaluation-Centric, 2025; NL2SciVis, 2026; SciVisAgentBench, 2026]

**General agent / code benchmarks** (methodology references):

- AgentBench, AgentBoard, GAIA, τ-bench, VisualWebArena, WebArena, Windows Agent
  Arena, MMMU, ToolLLM, MultiAgentBench, HumanEval, MBPP, SWE-Bench, SciCode,
  VeriGUI, LLM Evaluate. [Evaluation-Centric, 2025; NL2SciVis, 2026;
  SciVisAgentBench, 2026]

**Visualization tooling targeted:**

- **ParaView** (primary), **VisIt**, **napari** (biomedical imaging), **VMD**
  (molecular dynamics), **D3**, **Vega**. The NL2SciVis operation taxonomy is
  tool-neutral; the evaluation protocol is ParaView-specific but portable.
  [Evaluation-Centric, 2025; NL2SciVis, 2026]

**Models evaluated across the papers:**

- GPT-5, GPT-4.1, GPT-4o, Claude Sonnet 4.5, GPT-OSS-120B; LLaMA, Qwen, Claude
  families also referenced. [Evaluation-Centric, 2025; NL2SciVis, 2026]

**Conceptual / methodology references worth pulling:**

- "Agentic visualization" framing balancing autonomy vs. analyst control (Dhanoa
  et al.). [SciVisAgentBench, 2026]
- Wu et al. — comparison against hypothetical rational agents to isolate the
  contribution of visualization itself. [SciVisAgentBench, 2026]
- Kapoor et al. — joint optimization of accuracy AND cost, not just completion
  rate. [SciVisAgentBench, 2026]
- Yehudai et al. — open problems in LLM-agent eval (reproducibility,
  generalization, task diversity). [SciVisAgentBench, 2026]
- Zhu et al. — validity issues in agentic benchmarks; best practices for
  rigorous construction. [SciVisAgentBench, 2026]
- LLM-as-a-judge limits in visual grounding / stability — motivates hybrid
  protocols. [Evaluation-Centric, 2025; SciVisAgentBench, 2026]

### 3. Open problems / future work

Gaps explicitly flagged by the three papers — natural targets for our
contribution.

- **No comprehensive, large-scale SciVis-agent benchmark exists.** Existing
  benchmarks focus on simple plotting or general data-science workflows, not the
  3D / multi-step / view-dependent reality of SciVis. [Evaluation-Centric, 2025;
  SciVisAgentBench, 2026]
- **Plan-then-ask-then-execute agents are untested.** Current benchmarks assume
  fully autonomous execution after a single instruction; a system that first
  plans, asks clarifying questions, then executes is an open evaluation target.
  [Evaluation-Centric, 2025]
- **Process-based evaluation is not yet realized.** SciVisAgentBench's current
  release intentionally excludes process-level scoring because multiple action
  sequences can produce the same visualization and agents fail long-horizon
  workflows, making reference trajectories unstable. [SciVisAgentBench, 2026;
  Evaluation-Centric, 2025]
- **Cross-tool generalization is open.** NL2SciVis is single-platform (ParaView)
  and uses one synthetic wavelet dataset. Future versions should add real public
  scientific datasets and other scriptable tools (e.g., VisIt). [NL2SciVis,
  2026]
- **Discriminative power is decaying.** The strongest model already hits 96%
  pass rate on NL2SciVis baseline — harder operations are needed to keep the
  benchmark informative. [NL2SciVis, 2026]
- **Multi-step compositions, derived fields, and qualitative goals** ("make the
  contour more prominent") are excluded from NL2SciVis on purpose; future
  versions should relax these constraints. [NL2SciVis, 2026]
- **Meta-tool-selection agents** that choose between ParaView / napari / VMD per
  task have not been benchmarked. [Evaluation-Centric, 2025]
- **MLLM judges have known visual-grounding and stability limits** in SciVis
  specifically (limited training data in domain); reliability studies are
  ongoing. [Evaluation-Centric, 2025; SciVisAgentBench, 2026]
- **CodeBERT-style script similarity is unreliable** for SciVis and was dropped
  — a better code-equivalence signal is open work. [SciVisAgentBench, 2026]
- **Data sampling / resolution control operations** are deliberately excluded
  from the current SciVisAgentBench release because they need large-scale
  datasets and are influenced by external algorithms (e.g., INRs) — a future
  axis. [SciVisAgentBench, 2026]
- **Smaller language models (SLMs)** as cost-effective backbones are flagged as
  worth evaluating but not yet covered. [Evaluation-Centric, 2025]
- **Living-benchmark sustainability.** Both Ai et al. papers explicitly invite
  community contribution of new datasets / tasks / evaluators; long-term
  governance and contribution workflow are open. [Evaluation-Centric, 2025;
  SciVisAgentBench, 2026]

### 4. Benchmarking requirements

Constraints and required properties our benchmark must satisfy to be defensible.

**Coverage**

- Span the canonical SciVis task taxonomy along four axes: application domain,
  data type, complexity level, visualization operation. [SciVisAgentBench, 2026]
- Include representative user intents mapped to diverse techniques — volume
  rendering, streamline tracing, isosurface extraction. [Evaluation-Centric,
  2025]
- Datasets should cover scalar, vector, tensor, multivariate, and time-varying
  fields (downsample for cost as long as analytical character is preserved).
  [SciVisAgentBench, 2026]
- Three complexity tiers must be supported even if not all reported: **operation
  → task → workflow**. Report task-level and workflow-level cases; treat
  operations as compositional building blocks. [SciVisAgentBench, 2026]

**Accuracy of evaluation signal**

- MLLM judges must be paired with engine-state verifiers, not used alone.
  [Evaluation-Centric, 2025]
- LLM-judge protocols must include rubric shuffling and a documented human–LLM
  alignment study. [SciVisAgentBench, 2026]
- Human evaluation must remain available for ambiguous / high-stakes cases.
  [Evaluation-Centric, 2025]
- Deterministic evaluators (image metrics, rule-based verifiers, code execution
  gates) take precedence over LLM judges wherever a single correct outcome is
  specifiable. [SciVisAgentBench, 2026]

**Reproducibility**

- All cases must be expert-authored / expert-reviewed and serialized in a
  structured format (YAML, promptfoo-compatible). [SciVisAgentBench, 2026]
- Agents must run in a controlled sandbox (MCP or direct code execution); the
  agent interface must be abstracted so heterogeneous agents (tool-use /
  code-gen / GUI / multi-agent) are evaluated consistently. [Evaluation-Centric,
  2025; SciVisAgentBench, 2026]
- Where full determinism is infeasible, run repeated trials and quantify
  variance (≥10 in Evaluation-Centric, ≥30 per task per model in NL2SciVis
  baseline). [Evaluation-Centric, 2025; NL2SciVis, 2026]
- Cases versioned in a public repo (Hugging Face is the cited host) with
  explicit ground-truth artifacts (typically a reference image and an
  expert-authored rubric). [SciVisAgentBench, 2026]

**Task validity**

- Each task must admit a single explicit visualization outcome to be
  benchmark-eligible, OR be decomposed into checkpoints that each do.
  [SciVisAgentBench, 2026]
- Each atomic operation must satisfy: single intent, strict preconditions,
  independent execution, deterministic defaults. [NL2SciVis, 2026]
- Benchmark must be **agnostic to how** an agent reaches the solution (code
  generation vs. tool invocation vs. GUI). [SciVisAgentBench, 2026;
  Evaluation-Centric, 2025]

**Efficiency & cost**

- Per-trial cost telemetry is mandatory: execution time, interaction step count,
  token consumption, monetary cost. [Evaluation-Centric, 2025; SciVisAgentBench,
  2026; NL2SciVis, 2026]
- The benchmark itself must remain computationally tractable for iterative
  development; avoid blowing up evaluator overhead. [SciVisAgentBench, 2026;
  Evaluation-Centric, 2025]
- Report joint accuracy + cost (per Kapoor et al.), not pass rate in isolation.
  [SciVisAgentBench, 2026]

**Statistical rigor**

- Report **Wilson 95% CIs** for pass-rate proportions (handles 0% / 100% cells
  better than Wald).
- Report **Cohen's h** for pairwise effect size.
- Use **chi-squared** with **Bonferroni correction** for multi-task comparisons;
  report both raw and corrected p-values.
- Use a **concurrent control group** when testing scaffolding /
  prompt-modification interventions to avoid cross-batch confounds. [all four
  bullets: NL2SciVis, 2026]

**Extensibility**

- Modular task specs, evaluator interfaces, and agent abstractions so new agents
  / datasets / metrics can be added without restructuring the benchmark.
  [SciVisAgentBench, 2026]
- Explicit contribution path for the community (HF repo + recurring collaborator
  meetings is the model used). [SciVisAgentBench, 2026; Evaluation-Centric,
  2025]
