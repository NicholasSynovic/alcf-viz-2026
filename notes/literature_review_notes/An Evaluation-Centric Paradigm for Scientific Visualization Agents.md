# Annotations

(6/3/2026, 2:04:55 PM)

“SciVis agents” (Ai et al., 2025, p. 1) Is this a subset of agents? Potentially
ViTs which would be useful to include

“Bonsai dataset” (Ai et al., 2025, p. 1) Dataset to benchmark on

“A potted tree with a brown pot, silver branches, and golden leaves.” (Ai et
al., 2025, p. 1) Prompt

“(1) a multi-modal LLM judge for visualization quality, (2) hard-coded verifiers
for correctness of visualization primitives and techniques” (Ai et al., 2025,
p. 1) Methods to include

“(3) token usage and execution time for system performance” (Ai et al., 2025,
p. 1) Benchmark to include

“However, measuring progress and comparing different agents remains challenging,
particularly in scientific visualization (SciVis), due to the absence of
comprehensive, large-scale benchmarks for evaluating real-world capabilities.”
(Ai et al., 2025, p. 1) Are there datasets to enable these benchmarks?

“We define a SciVis agent as: an AI system that interprets human users’ natural
language intent, autonomously interacts with the SciVis pipeline to produce
visualizations that meet userspecified analysis goals” (Ai et al., 2025, p. 1)
Critical definition

“Importantly, we focus on fully autonomous execution scenarios where agents must
complete tasks without additional human intervention beyond the initial
instruction, allowing for consistent and repeatable benchmarking.” (Ai et al.,
2025, p. 1) While necessary for the MVP, testing a separate system that first
plans, ask questions as needed, and then executes would be most beneficial

“Existing benchmarks focus primarily on simple plotting tasks [7, 35, 12] or
general data science workflows [17, 14]” (Ai et al., 2025, p. 1) Benchmarks to
review

“SciVis workflows require sophisticated data transformations, diverse rendering
techniques, multi-dimensional parameter mappings, and careful view selections,
all of which must be applied in precise sequences to produce meaningful
scientific insights.” (Ai et al., 2025, p. 1)

“difficulties in visual perception of visual outputs [15, 19] to the fragility
of tool-use mechanisms that underpin LLM agents [36, 31]. The absence of
comprehensive evaluation frameworks not only hinders progress in the field but
also makes it impossible to reliably deploy these agents in critical scientific
applications where accuracy and reproducibility are paramount [20, 18].” (Ai et
al., 2025, p. 1)

“dresses multiple dimensions: task complexity (from simple parameter adjustment
to complex multi-step pipelines), domain coverage (from experimental data to
computational simulation), and evaluation methodology (from output quality to
process efficiency)” (Ai et al., 2025, p. 2)

“VisEval” (Ai et al., 2025, p. 2)

“Drawing Pandas” (Ai et al., 2025, p. 2)

“MatPlotAgent” (Ai et al., 2025, p. 2)

“AVA’s” (Ai et al., 2025, p. 2)

“ChatVis” (Ai et al., 2025, p. 2)

“ParaView-MCP” (Ai et al., 2025, p. 2)

“Magentic-UI” (Ai et al., 2025, p. 2)

“NLI4VolVis” (Ai et al., 2025, p. 2)

“AgentBench” (Ai et al., 2025, p. 2)

“AgentBoard” (Ai et al., 2025, p. 2)

“GAIA” (Ai et al., 2025, p. 2)

“τ-bench” (Ai et al., 2025, p. 2)

“VisualWebArena” (Ai et al., 2025, p. 2)

“MMMU” (Ai et al., 2025, p. 2)

“Tool-use studies also surface fragility in API grounding [31].” (Ai et al.,
2025, p. 2)

““LLM-as-a-judge” correlates reasonably with human preference but has known
limits in visual grounding and stability [38, 13, 34].” (Ai et al., 2025, p. 2)

“motivates hybrid protocols that combine LLM judging with engine-state
verification.” (Ai et al., 2025, p. 2)

“reproducibility remains a cross-cutting concern in visualization and systems
evaluation, reinforcing the need for transparent frameworks and benchmarks [18,
20], which we propose in this position paper for visualization agents.” (Ai et
al., 2025, p. 2)

“Outcome-based evaluation focuses exclusively on the relationship between input
data/specifications and final outputs, treating the agent as a black box” (Ai et
al., 2025, p. 2)

“from those that generate executable code [28] to those that directly manipulate
tool interfaces [25]” (Ai et al., 2025, p. 2)

“or more intelligent systems (yet to be developed)” (Ai et al., 2025, p. 2)

“By abstracting away implementation details, outcomebased metrics enable direct
comparison between fundamentally different agent designs” (Ai et al., 2025,
p. 2)

“what ultimately matters: the quality and correctness of the visualization
output” (Ai et al., 2025, p. 2)

“different visualization results that reveal the same insights, which creates
ambiguity for outcome-based evaluation.” (Ai et al., 2025, p. 2)

“To make the agent solution specific, we can increase the constraint and
condition to narrow the solution. Alternatively, we can focus on shorter, more
focused tasks with no branching possibilities, or start from a predetermined
intermediate result.” (Ai et al., 2025, p. 2)

“Process-based evaluation examines the agent’s actions and the rationale,
providing insights into how solutions are achieved rather than merely what is
produced. This granular analysis is particularly valuable for identifying
failure modes, understanding generalization capabilities, and guiding iterative
refinement of agent architectures.” (Ai et al., 2025, p. 2)

“Task complexity naturally divides process-based evaluations, i.e., single-step
vs. multi-step tasks. Single-step tasks evaluate atomic operations such as
loading a dataset and applying a specific filter. Multi-step tasks consist of
interdependent single-step tasks spanning dozens or even hundreds of steps,
potentially involving backtracking and iterative refinement.” (Ai et al., 2025,
p. 2)

“VeriGUI dataset [24].” (Ai et al., 2025, p. 3)

“Evaluation can be divided based on targeted tools such as ParaView for general
SciVis, napari for biomedical imaging, VMD for molecular dynamics, etc.” (Ai et
al., 2025, p. 3)

“Advanced agents might demonstrate meta-capabilities by autonomously selecting
the most appropriate tool for a given task, requiring not only the ability to
manipulate and use different tools but also an understanding of each tool’s
strengths and limitations.” (Ai et al., 2025, p. 3)

“Does the agent use more steps than strictly required? Does it do unrelated
tasks concerning the stated goals while stumbling upon the correct solution?
Regarding practical measurement, we can rely indirectly on token usage and time
or step length.” (Ai et al., 2025, p. 3)

“Effectiveness of the evaluation can be examined through three complementary
lenses: accuracy, which concerns the reliability of individual evaluation
results; coverage, which indicate how much of the potential realworld usage
scenarios are covered by the benchmark; and costeffectiveness, which convey the
need to strike a balance between the amount of computational and human efforts
and achieving good accuracy and coverage.” (Ai et al., 2025, p. 3)

“Accuracy requires reducing uncertainty and ensuring robust evaluation signals.”
(Ai et al., 2025, p. 3)

“use MLLM judges, which have shown strong alignment with human preference [38,
13].” (Ai et al., 2025, p. 3)

“However, recent studies [34, 4] reveal that these models still face notable
limitations in visual perception and grounding despite their promise.” (Ai et
al., 2025, p. 3)

“For greater reliability, automated verification against the visualization
engine’s internal state can be used (process-based evaluation). For example, a
case-specific Python script can confirm that a ParaView isosurface has been
generated at the correct value and colored appropriately. Quantitative checks
can be added for code-generating agents such as ChatVis by comparing generated
scripts with goldstandard reference scripts and validating their execution
outcomes.” (Ai et al., 2025, p. 3)

“Human evaluation, though costly, may still be needed for ambiguous or
high-stakes cases.” (Ai et al., 2025, p. 3)

“Coverage concerns whether the evaluation spans the full range of SciVis tasks
and interaction patterns.” (Ai et al., 2025, p. 3)

“Test design should begin with representative user intents mapped to diverse
techniques (e.g., volume rendering, streamline tracing, isosurface extraction).
An outcome-based evaluation specifies only the dataset and task description,
without constraining how agents achieve the goal. This allows fair evaluation of
agents with varying capabilities, whether they generate code to interact with
the visualization engine or directly invoke high-level tools.” (Ai et al., 2025,
p. 3)

“Ensuring evaluation coverage benefits from both top-down alignment with a
taxonomy of visualization tasks and bottom-up analysis of which visualization
primitives, techniques, and interaction modalities are exercised.” (Ai et al.,
2025, p. 3)

“Cost-effectiveness addresses two key practical constraints in SciVis agent
evaluation. First, defining ground truth for exploratory SciVis tasks is
inherently challenging” (Ai et al., 2025, p. 3)

“Second, running comprehensive evaluations—spanning diverse datasets,
visualization techniques, and agent configurations—demands substantial
computational resources.” (Ai et al., 2025, p. 3)

“Benchmarks must strike a balance, delivering actionable and representative
evaluation while minimizing overhead to support rapid, iterative development
cycles.” (Ai et al., 2025, p. 3)

“Tasks are decomposed into smaller, controllable checkpoints to pinpoint points
of failure, and agents operate in a controlled sandbox via either model context
protocol (MCP) [2] or direct code execution.” (Ai et al., 2025, p. 3)

“For outcome quality, the focus is on whether the final visualization meets the
intended goals in terms of accuracy, semantic correctness, and interpretability.
Factors such as colormap selection, viewpoint, and use of appropriate
visualization primitives are assessed.” (Ai et al., 2025, p. 3)

“We employ instruction-tuned multi-modal LLM judges aligned with human
preferences in our implementation. These models are prompted with
domain-specific evaluation criteria, the ground-truth visualization, and the
agent’s output, then asked to assign quality scores.” (Ai et al., 2025, p. 3)

“For process verification, the emphasis is on whether the agent’s intermediate
actions and applied techniques satisfy explicit task requirements.” (Ai et al.,
2025, p. 3)

“his includes verifying the correct use of visualization primitives (e.g.,
isosurfaces) and techniques (e.g., volume rendering) via case-specific
hard-coded verifiers that inspect the visualization engine’s internal state. For
code-generating agents, additional checks compare the generated scripts to
gold-standard references and validate their execution outcomes.” (Ai et al.,
2025, p. 3)

“For system efficiency, we track runtime, token usage, and monetary cost for
each run. These measures complement accuracy-based metrics, providing insight
into scalability, cost-effectiveness, and the real-world deployability of
agentic visualization systems.” (Ai et al., 2025, p. 3)

“Bonsai dataset” (Ai et al., 2025, p. 3)

“ParaView” (Ai et al., 2025, p. 3)

“ChatVis” (Ai et al., 2025, p. 3)

“ParaView-MCP” (Ai et al., 2025, p. 3)

“GPT series, i.e., GPT-5, GPT-4.1, and GPT-4o, as their backbone LLM.” (Ai et
al., 2025, p. 3)

“Each experiment is repeated 10 times for statistical robustness. The agents are
instructed to load the Bonsai dataset with given parameters, perform volume
rendering, and adjust the transfer function to achieve the target visualization:
“A potted tree with a brown pot, silver branches, and golden leaves.” The
resulting ParaView state is saved for subsequent evaluation.” (Ai et al., 2025,
p. 3)

“Upon task completion, overall visualization quality is assessed using an
instruction-tuned multi-modal LLM judge (e.g., GPT4o), presented with both the
ground-truth images and the agentgenerated results. The judge evaluates outputs
against explicit criteria: whether the overall goal is met, whether the pot is
brown, the branches are silver, and the leaves are gold. These scores form part
of the final evaluation metric.” (Ai et al., 2025, p. 3)

“To enhance robustness of the assessment, the LLM-based evaluation is
supplemented with hard-coded verification scripts executed via pvpython. The
saved ParaView state is reloaded to confirm the correct volume rendering
configuration and accurate colormap settings. For code-generating agents such as
ChatVis, we additionally compute the CodeBERT-based [11] similarity between the
generated and gold-standard reference scripts. While these casespecific checks
substantially improve reliability, they require additional manual effort to
design and maintain.” (Ai et al., 2025, p. 4)

“Performance metrics, including token usage, monetary cost, and task completion
time, are recorded as they directly reflect user-perceived latency and the
practical feasibility of deploying such agents” (Ai et al., 2025, p. 4)

“Each metric is assigned a point value, and the sum of these points constitutes
the final evaluation score (see Figure 1).” (Ai et al., 2025, p. 4)

“Table 1 shows that while the MCP-based agent delivers stable, high-quality
results, its reliance on complex toolchains leads to high latency, limiting
real-world deployment. In contrast, ChatVis—lacking vision capabilities and
generating code on the fly—typically completes tasks more quickly but incurs
increased token usage and reduced visualization quality.” (Ai et al., 2025,
p. 4)

“Claude, LLaMA, and Qwen” (Ai et al., 2025, p. 4)

“smaller language models (SLMs)” (Ai et al., 2025, p. 4)

“This position paper serves as an open invitation for collaboration on building
this evaluation benchmark as a community.” (Ai et al., 2025, p. 4)
