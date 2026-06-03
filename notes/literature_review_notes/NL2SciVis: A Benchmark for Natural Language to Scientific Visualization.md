# Annotations

(6/3/2026, 2:04:59 PM)

“NL2SciVis benchmark suite, which focuses on generating atomic scientific
visualization operations in ParaView via Python code. To demonstrate its
utility, we evaluate popular LLMs (Claude Sonnet 4.5, GPT-5, GPT-4o, and
GPT-OSS-120B) on the suite under baseline, prompt modification, and scaffolding
conditions, checking execution and pipeline validity across over 14,000 trials.”
(Mathai et al., 2026, p. 1)

“ParaView” (Mathai et al., 2026, p. 1)

“VisIt” (Mathai et al., 2026, p. 1)

“It targets 3D scientific field data on structured or unstructured grids,”
(Mathai et al., 2026, p. 1)

“D3” (Mathai et al., 2026, p. 1)

“Vega” (Mathai et al., 2026, p. 1)

“Recent LLM-driven SciVis work [MYLP24, PMY∗25, LMB25] also targets ParaView,
placing our benchmark alongside that line of research.” (Mathai et al., 2026,
p. 1)

“We address this issue by limiting the scope of the suite to basic operations.”
(Mathai et al., 2026, p. 1)

“One motivation for this plan is that basic operations are the prerequisite for
complex ones: an LLM that cannot handle basics cannot handle more complex
tasks.” (Mathai et al., 2026, p. 1)

“15 atomic operations across three categories (setup, adaptation, reporting)
with evaluation checking both code execution and visualization correctness. We
demonstrate its utility through three campaigns (baseline, prompt modifications,
scaffolding) comprising over 14,000 trials.” (Mathai et al., 2026, p. 1)

“Early works produced natural language interfaces that parse text into chart
specifications over tabular data [SBT∗16, GDA∗15, NSS21, YS20]. Neural
approaches replaced hand-crafted parsing rules [LTL∗22],” (Mathai et al., 2026,
p. 1)

“multi-step agentic pipelines [Dib23, SLY∗25, YZW∗24, CCA∗25, BIS∗26].” (Mathai
et al., 2026, p. 2)

“nvBench” (Mathai et al., 2026, p. 2)

“VisEval” (Mathai et al., 2026, p. 2)

“Text2Vis” (Mathai et al., 2026, p. 2)

“LLM-driven scientific visualization. Recent systems extend LLM-driven
visualization to scientific data, targeting flow fields [HXHT22, LZT25], volume
rendering [ATW26], cosmological ensembles [TGB∗25], and general ParaView/VTK
pipelines [MYLP24,PMY∗25,LMB25,BTR∗26].” (Mathai et al., 2026, p. 2)

“ChatVis” (Mathai et al., 2026, p. 2)

“end-to-end RAG pipelines” (Mathai et al., 2026, p. 2)

“ParaView-MCP [LMB25] takes a different approach, providing direct tool-use
control of ParaView through a curated API, but validates through case studies
and domain expert feedback rather than systematic benchmarks.” (Mathai et al.,
2026, p. 2)

“Emerging frameworks extract agentic design patterns from visualization systems
[DWL∗25] and propose evaluation-centric paradigms for SciVis agents [AML∗25].”
(Mathai et al., 2026, p. 2)

“HumanEval” (Mathai et al., 2026, p. 2)

“MBPP” (Mathai et al., 2026, p. 2)

“SWE-Bench” (Mathai et al., 2026, p. 2)

“SciCode” (Mathai et al., 2026, p. 2)

“AgentBench” (Mathai et al., 2026, p. 2)

“no benchmark targets NL-driven scientific visualization with deterministic
validation, isolated capability testing, and cross-model comparison under
controlled conditions. NL2SciVis addresses this gap.” (Mathai et al., 2026,
p. 2)

“Scientific visualization workflows involve loading data, applying filters,
adjusting parameters, and extracting results. Rather than assess full multi-step
workflows, we decompose them into atomic operations to pinpoint what agents can
and cannot do.” (Mathai et al., 2026, p. 2)

“operations are validated through ParaView state files (PVSM); reporting
operations are validated against expected numerical ranges.” (Mathai et al.,
2026, p. 2)

“Each operation satisfies four constraints: single intent, strict preconditions,
independent execution, and deterministic defaults” (Mathai et al., 2026, p. 2)

“Multi-step compositions, derived field construction, and qualitative adaptation
goals (e.g., “make the contour more prominent”) are excluded because they break
one or more of these constraints. Future versions may relax them.” (Mathai et
al., 2026, p. 2)

“We validate against PVSM state files rather than rendered images as they
provide direct structural access to the pipeline: filter types, field
assignments, and parameter values can be verified exactly.” (Mathai et al.,
2026, p. 2)

“Validation happens in two stages: first, we verify that a valid PVSM file was
produced; second, we confirm that (1) a Contour filter exists in the pipeline,
(2) it operates on the correct field, and (3) the isovalue matches the requested
value.” (Mathai et al., 2026, p. 2)

“Two sequential gates deterministically assess each trial: Execution Gate checks
whether the agent produced a valid state file” (Mathai et al., 2026, p. 2)

“Technique Gate checks whether the visualization method, field, and parameters
are correct.” (Mathai et al., 2026, p. 3)

“Our primary metric is pass rate: the proportion of trials where both execution
and technique gates pass. We report 95% Wilson score confidence intervals, which
provide better coverage than Wald intervals for proportions near 0 or 1 –
relevant since some model-task combinations achieve 0% or 100% pass rates. For
pairwise comparisons, we compute Cohen’s h as the effect size to quantify
practical significance independent of sample size. Following standard
conventions: |h| < 0.2 is negligible, 0.2–0.5 is small, 0.50.8 is medium, and >
0.8 is large. For significance testing, we use chi-squared tests for
independence to assess whether observed differences exceed chance variation. For
multiple comparisons across 15 tasks, we apply Bonferroni correction (α =
0.05/15) and report both raw and corrected p-values. As secondary metrics, we
record lines of code generated, output token count, and execution latency for
each trial to characterize generation cost and enable efficiency comparisons
across models” (Mathai et al., 2026, p. 3)

“Dataset: The benchmark uses a synthetic wavelet dataset with scalar and
gradient-derived vector fields suitable for all 15 operations. The dataset comes
from VTK’s vtkRTAnalyticSource, a deterministic source that produces a
wavelet-shaped RTData scalar field, instantiated as a 40×40×40 grid. We add a
vector field computed from the scalar field’s gradient, with a localized swirl
term for non-zero vorticity. This synthetic choice ensures reproducibility but
may limit generalization.” (Mathai et al., 2026, p. 3)

“Future versions may add public scientific datasets to test broader coverage.”
(Mathai et al., 2026, p. 3)

“Visualization tool: The operation taxonomy is tool-neutral. The evaluation
protocol is ParaView-specific but portable to other scriptable applications
(e.g., VisIt)” (Mathai et al., 2026, p. 3)

“Sonnet 4.5 (Anthropic), GPT5 and GPT-4o (OpenAI), and GPT-OSS-120B,” (Mathai et
al., 2026, p. 3)

“All models receive identical system prompts instructing them to generate a
self-contained Python function that performs the requested operation.” (Mathai
et al., 2026, p. 3)

“To illustrate the utility of the benchmark suite, we performed three campaigns
with over 14,000 trials: Baseline (LLM performance on the 15 operations), Prompt
Enhancement (effects of prompt modifications), and Scaffolding (effects of code
templates).” (Mathai et al., 2026, p. 3)

“Baseline Campaign: The baseline campaign establishes fundamental performance
levels for each model. Each model executes all 15 tasks with a minimal system
prompt containing only format instructions. We collected 30 runs per task (fixed
prompt) per model, yielding 450 trials per model and 1,800 total baseline
trials. Cross-run variation reflects model stochasticity at temperature 0.2.”
(Mathai et al., 2026, p. 3)

“Performance by Category and Operation: Breaking down by operation category
(Table 2), two patterns emerge: reporting operations are the most difficult,
requiring data-extraction APIs that differ from filter-creation patterns and are
likely underrepresented in training data, while adaptation operations are
easiest, involving simpler API calls with fewer dependencies.” (Mathai et al.,
2026, p. 3)

“Prompt Enhancement Campaign: The prompt enhancement campaign tests whether
specific prompt modifications affect pass rates. We append one of four
conditions to the baseline prompt: (1) Documentation: “Please consult the
ParaView v5.13 Python API documentation, when needed” (testing whether explicit
documentation references help); (2) Job stakes: “Your performance on this task
will directly affect my job offer” (testing emotional manipulation effects); (3)
Threat stakes: “Your performance is time-sensitive and affects an urgent
situation” (testing urgency framing); (4) Negative reward: “You start with $100
and lose it all if wrong” (testing loss aversion framing).” (Mathai et al.,
2026, p. 4)

“Scaffolding Campaign: The scaffolding campaign provides a minimal code template
showing the expected function format, filter creation pattern, and state-saving
call. This campaign includes a concurrent control group to avoid cross-batch
confounds.” (Mathai et al., 2026, p. 4)

“We scope evaluation to a single platform (ParaView), a synthetic wavelet
dataset, and single-turn atomic operations.” (Mathai et al., 2026, p. 4)

“We leave cross-tool generalization to future work. The 96% pass rate of the
strongest model signals that future iterations need harder operations to retain
discriminative power.” (Mathai et al., 2026, p. 4)
