---
title: "An Evaluation-Centric Paradigm for Scientific Visualization Agents"
citekey: "aiEvaluationCentricParadigmScientific2025"
authors: "Kuangshi Ai, Haichao Miao, Zhimin Li, Chaoli Wang, Shusen Liu"
year: 2025
tags:
    [
        "FOS: Computer and information sciences",
        "Human-Computer Interaction (cs.HC)",
        "Computation and Language (cs.CL)",
        "Graphics (cs.GR)",
    ]
---

# An Evaluation-Centric Paradigm for Scientific Visualization Agents

**Zotero Link:** [Zotero Link](zotero://select/library/items/XILD7SHH) | **PDF
Link:** [PDF](zotero://select/library/items/FTPJFEHM)

---

## Summary & Notes

%% begin notes %%

Write your personal notes, summaries, and synthesis here!

%% end notes %%

---

## Annotations

%% begin annotations %% _Tags: #note_SciVisDataset_
<mark class="hltr-red">"Bonsai dataset"</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=MRFAFGS9))
<mark class="hltr-red">Dataset to benchmark on.
[Link](http://klacansky.com/open-scivis-datasets/)</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-blue">"volume visualization and
adjust the transfer function"</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=JEVNJLZN))
<mark class="hltr-blue">This is something that the agent will be prompted to
do</mark>

_Tags: #note_SciVisPrompt_ <mark class="hltr-green">"A potted tree with a brown
pot, silver branches, and golden leaves."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=7SBXB8C9))
<mark class="hltr-green">Prompt to give to the agent which it will then be
evaluated on</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-blue">"(1) a multi-modal LLM judge
for visualization quality, (2) hard-coded verifiers for correctness of
visualization primitives and techniques, and (3) token usage and execution time
for system performance."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=3F2X3VPC))
<mark class="hltr-blue">Any SciVis agentic system and tooling will have to be
evaluated against these validators. Additi</mark>

_Tags: #note_SciVisMethodology, #note_SciVisOpenProblem_
<mark class="hltr-yellow">"(1) a multi-modal LLM judge for visualization
quality, (2) hard-coded verifiers for correctness of visualization primitives
and techniques,"</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=67M5MGAF))
<mark class="hltr-yellow">1 and 2 describe components that could be incorporated
into the SciVis agent itself to self evaluate its work prior to returning
results to the scientist</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"However, measuring
progress and comparing different agents remains challenging, particularly in
scientific visualization (SciVis), due to the absence of comprehensive,
large-scale benchmarks for evaluating real-world capabilities."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=HG5LY9QQ))
<mark class="hltr-purple">Are there datasets to enable these benchmarks? These
datasets would both need the prompts + the scientific data and the ground truth
code.</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"We define a SciVis agent
as: an AI system that interprets human users’ natural language intent,
autonomously interacts with the SciVis pipeline to produce visualizations that
meet userspecified analysis goals"</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=GV5F44PX))
<mark class="hltr-magenta">Critical definition</mark>

_Tags: #note_SciVisMethodology, #note_SciVisOpenProblem_
<mark class="hltr-yellow">"Importantly, we focus on fully autonomous execution
scenarios where agents must complete tasks without additional human intervention
beyond the initial instruction, allowing for consistent and repeatable
benchmarking."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=A4Q6KUWG))
<mark class="hltr-yellow">While necessary for the MVP, testing a separate system
that first plans, ask questions as needed, and then executes would be most
beneficial</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Importantly, we focus on
fully autonomous execution scenarios where agents must complete tasks without
additional human intervention beyond the initial instruction, allowing for
consistent and repeatable benchmarking."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=A9VXLHGB))
<mark class="hltr-magenta">Core requirements of existing SciVis agentic
systems</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"Existing benchmarks focus primarily on simple
plotting tasks [7, 35, 12] or general data science workflows [17, 14]"</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=8C6NCUXH))
<mark class="hltr-orange">Benchmarks to review</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"SciVis workflows require
sophisticated data transformations, diverse rendering techniques,
multi-dimensional parameter mappings, and careful view selections, all of which
must be applied in precise sequences to produce meaningful scientific
insights."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=K2KQWM7P))
<mark class="hltr-magenta">Core requirements of workflows</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"difficulties in
visual perception of visual outputs [15, 19] to the fragility of tool-use
mechanisms that underpin LLM agents [36, 31]. The absence of comprehensive
evaluation frameworks not only hinders progress in the field but also makes it
impossible to reliably deploy these agents in critical scientific applications
where accuracy and reproducibility are paramount [20, 18]."</mark>
([Page 1](zotero://open-pdf/library/items/FTPJFEHM?page=1&annotation=KAZIHS9S))
<mark class="hltr-purple">These are fairly broad gaps in the literature and
existing capabilities in evaluating these systems. Honestly, after reading this
paper and others in this collection, deployment and reproducibility are
challenges that we could tackle</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-red">"task complexity (from simple
parameter adjustment to complex multi-step pipelines), domain coverage (from
experimental data to computational simulation), and evaluation methodology (from
output quality to process efficiency)"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=YR5QX42G))
<mark class="hltr-red">Any future work on evaluations will have to address these
components</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"VisEval"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=WZ6X7DUU))
<mark class="hltr-orange">Chart reading system</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"Drawing Pandas"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=24MWIDGY))
<mark class="hltr-orange">Code generation and execution</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"MatPlotAgent"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=YFTIVBZU))
<mark class="hltr-orange">Code + chart reading?</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"AVA’s"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=AU7UERH5))
<mark class="hltr-orange">Iteration based visualization improvements?</mark>

_Tags: #note_SciVisOpenProblem, #note_SciVisCore, #note_SciVisBackground_
<mark class="hltr-orange">"ChatVis"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=MRGH4G3T))
<mark class="hltr-orange">Core related work for my project. GPT 4 based, no
agentic framework. Lots of room to explore this option</mark>

_Tags: #note_SciVisOpenProblem, #note_SciVisCore, #note_SciVisBackground_
<mark class="hltr-orange">"ParaView-MCP"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=U9TYFLXH))
<mark class="hltr-orange">Core tooling for my project. Leverages hand crafted
tooling. Potentially less capable that the options provided to ChatVis</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"Magentic-UI"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=8EXJ368Q))
<mark class="hltr-orange">UI driven visualization workflow?</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"NLI4VolVis"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=EBYYKVB2))
<mark class="hltr-orange">Interacting with volumes via natural language</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"AgentBench"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=IXN8EUNI))
<mark class="hltr-orange">Eval to review</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"AgentBoard"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=DKVRT7S6))
<mark class="hltr-orange">Eval to review</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"GAIA"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=3FYW6SXD))
<mark class="hltr-orange">Eval to review</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"τ-bench"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=6D2QKPZV))
<mark class="hltr-orange">Eval to review</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"VisualWebArena"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=9AIZF8A7))
<mark class="hltr-orange">Eval to review</mark>

_Tags: #note_SciVisEval, #note_SciVisBackground_
<mark class="hltr-orange">"MMMU"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=G987BIWF))
<mark class="hltr-orange">Eval to review</mark>

_Tags: #note_SciVisOpenProblem, #note_SciVisBackground_
<mark class="hltr-purple">"Tool-use studies also surface fragility in API
grounding [31]."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=FW7JA9AE))
<mark class="hltr-purple">I wonder if this can be addressed via MCP
tooling?</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"“LLM-as-a-judge”
correlates reasonably with human preference but has known limits in visual
grounding and stability [38, 13, 34]."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=ACPJVFKR))
<mark class="hltr-purple">How can we get more accuracy out of our LLM judges?
Potentially a "council" of LLMs or ViTs?</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"known limits in visual
grounding and stability [38, 13, 34]."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=AV2XYQLT))
<mark class="hltr-orange">Review limitations these limitations</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-blue">"motivates hybrid protocols
that combine LLM judging with engine-state verification."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=VBUUIFBX))
<mark class="hltr-blue">Make sure that any evals use both of these.</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"motivates hybrid
protocols that combine LLM judging with engine-state verification"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=IQABQM2D))
<mark class="hltr-yellow">Hybrid verification can also be included during the
agentic loop, assuming that engine state access is trivial</mark>

_Tags: #note_SciVisBackground_ <mark class="hltr-orange">"reproducibility
remains a cross-cutting concern in visualization and systems evaluation,
reinforcing the need for transparent frameworks and benchmarks [18, 20],"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=ZMQQFYYP))
<mark class="hltr-orange">Review these arguments</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-blue">"We organize evaluation tasks
into two primary categories: outcome-based and process-based."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=Y8H88I6E))
<mark class="hltr-blue">Given all of the evals listed in this paper, can we
categorize them into these two buckets? Is this taxonomy robust?</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Outcome-based evaluation
focuses exclusively on the relationship between input data/specifications and
final outputs, treating the agent as a black box"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=SBLPRK7H))
<mark class="hltr-magenta">Core definition</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"from those that
generate executable code [28] to those that directly manipulate tool interfaces
[25]"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=W5C6XZDE))
<mark class="hltr-yellow">These are separate tasks, but can be used in parallel
in agentic systems. For example, you may tool call to get the relevant
documentation for a task, and generate code from these docs.</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"or more intelligent
systems (yet to be developed)"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=E3CPNCL5))
<mark class="hltr-purple">Everything in this paper assumes that there is a
single agent operating on the data. Multi-agent systems are possible. Having an
agent work with multiple tools is possible. There are many open directions just
based on this work</mark>

<mark class="hltr-yellow">"By abstracting away implementation details,
outcomebased metrics enable direct comparison between fundamentally different
agent designs"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=MBH36J4U))

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"what ultimately matters:
the quality and correctness of the visualization output"</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=DGBXTSTW))
<mark class="hltr-magenta">Core non-functional requirement</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"different
visualization results that reveal the same insights, which creates ambiguity for
outcome-based evaluation."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=EEUBEPSC))
<mark class="hltr-purple">How can we enable reproducibility within our agents
given the same input?</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"To make the agent
solution specific, we can increase the constraint and condition to narrow the
solution. Alternatively, we can focus on shorter, more focused tasks with no
branching possibilities, or start from a predetermined intermediate
result."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=C97L6LG6))
<mark class="hltr-yellow">Methodologies to try to replicate and evaluate</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-red">"Process-based evaluation
examines the agent’s actions and the rationale, providing insights into how
solutions are achieved rather than merely what is produced."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=N4F5NYKW))
<mark class="hltr-red">Core definition. Given that SciVis agents generate code
as an intermediate step before visualizing, code process evals are going to be
critical</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-blue">"This granular analysis is
particularly valuable for identifying failure modes, understanding
generalization capabilities, and guiding iterative refinement of agent
architectures."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=JW4GJ4N3))
<mark class="hltr-blue">Evaluation definition</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Task complexity naturally
divides process-based evaluations, i.e., single-step vs. multi-step tasks.
Single-step tasks evaluate atomic operations such as loading a dataset and
applying a specific filter. Multi-step tasks consist of interdependent
single-step tasks spanning dozens or even hundreds of steps, potentially
involving backtracking and iterative refinement."</mark>
([Page 2](zotero://open-pdf/library/items/FTPJFEHM?page=2&annotation=3UTTSVZF))
<mark class="hltr-magenta">Core definitions</mark>

_Tags: #note_SciVisBackground, #note_ <mark class="hltr-orange">"VeriGUI dataset
[24]."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=NSM2GAN9))
<mark class="hltr-orange">Review this eval</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"Advanced agents might
demonstrate meta-capabilities by autonomously selecting the most appropriate
tool for a given task, requiring not only the ability to manipulate and use
different tools but also an understanding of each tool’s strengths and
limitations."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=R7TKV48T))
<mark class="hltr-purple">No SciVis agent that I'm aware of accomplishes this
yet. Most likely this a greater goal of Project IDEAS</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-blue">"Does the agent use more steps
than strictly required? Does it do unrelated tasks concerning the stated goals
while stumbling upon the correct solution? Regarding practical measurement, we
can rely indirectly on token usage and time or step length."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=XAEEGUHL))
<mark class="hltr-blue">Process evals for SciVis agents</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Effectiveness of the
evaluation can be examined through three complementary lenses: accuracy, which
concerns the reliability of individual evaluation results; coverage, which
indicate how much of the potential realworld usage scenarios are covered by the
benchmark; and costeffectiveness, which convey the need to strike a balance
between the amount of computational and human efforts and achieving good
accuracy and coverage."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=6NLLYIEB))
<mark class="hltr-magenta">Core components of effectiveness</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Accuracy requires reducing
uncertainty and ensuring robust evaluation signals."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=PBIYTY69))
<mark class="hltr-magenta">Core definition of accuracy</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"use MLLM judges,
which have shown strong alignment with human preference [38, 13]."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=TW79JFWQ))
<mark class="hltr-yellow">Methodology to test for evaluating accuracy</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"For greater
reliability, automated verification against the visualization engine’s internal
state can be used (process-based evaluation). For example, a case-specific
Python script can confirm that a ParaView isosurface has been generated at the
correct value and colored appropriately. Quantitative checks can be added for
code-generating agents such as ChatVis by comparing generated scripts with
goldstandard reference scripts and validating their execution outcomes."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=Q7C7FLR5))
<mark class="hltr-yellow">Methodology for evaluating the accuracy of the process
in which the SciVis agent generated the code for the final visualization</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"Human evaluation,
though costly, may still be needed for ambiguous or high-stakes cases."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=GZJPLUIV))
<mark class="hltr-purple">Is there a dataset of human reviewed SciVis agent
generated figures?</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Coverage concerns whether
the evaluation spans the full range of SciVis tasks and interaction
patterns."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=HR3XYI5Y))
<mark class="hltr-magenta">Core definition of coverage</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"Test design should
begin with representative user intents mapped to diverse techniques (e.g.,
volume rendering, streamline tracing, isosurface extraction). An outcome-based
evaluation specifies only the dataset and task description, without constraining
how agents achieve the goal. This allows fair evaluation of agents with varying
capabilities, whether they generate code to interact with the visualization
engine or directly invoke high-level tools."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=ENTZTSML))
<mark class="hltr-yellow">Requirements for eval design</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"defining ground truth
for exploratory SciVis tasks is inherently challenging: unlike deterministic
operations, these tasks often allow multiple equally valid visualizations,
viewpoints, or parameter settings."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=99RZ52EG))
<mark class="hltr-purple">How do you define the ground truth given these
different settings? What enables a "human friendly" view?</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"Second, running
comprehensive evaluations—spanning diverse datasets, visualization techniques,
and agent configurations—demands substantial computational resources."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=GB9SLSWS))
<mark class="hltr-purple">It's expensive to run these agents, so how do we
amortize these costs? Can we create a dataset of generated visualizations and
their transformations and pull these in during eval to reduce cost?</mark>

_Tags: #note_SciVisCore_ <mark class="hltr-magenta">"Benchmarks must strike a
balance, delivering actionable and representative evaluation while minimizing
overhead to support rapid, iterative development cycles."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=5298LNPL))
<mark class="hltr-magenta">Core benchmark definition</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"Tasks are decomposed
into smaller, controllable checkpoints to pinpoint points of failure, and agents
operate in a controlled sandbox via either model context protocol (MCP) [2] or
direct code execution. For outcome quality, the focus is on whether the final
visualization meets the intended goals in terms of accuracy, semantic
correctness, and interpretability. Factors such as colormap selection,
viewpoint, and use of appropriate visualization primitives are assessed. We
employ instruction-tuned multi-modal LLM judges aligned with human preferences
in our implementation. These models are prompted with domain-specific evaluation
criteria, the ground-truth visualization, and the agent’s output, then asked to
assign quality scores. For process verification, the emphasis is on whether the
agent’s intermediate actions and applied techniques satisfy explicit task
requirements. This includes verifying the correct use of visualization
primitives (e.g., isosurfaces) and techniques (e.g., volume rendering) via
case-specific hard-coded verifiers that inspect the visualization engine’s
internal state. For code-generating agents, additional checks compare the
generated scripts to gold-standard references and validate their execution
outcomes. For system efficiency, we track runtime, token usage, and monetary
cost for each run. These measures complement accuracy-based metrics, providing
insight into scalability, cost-effectiveness, and the real-world deployability
of agentic visualization systems."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=X3RIS9IR))
<mark class="hltr-yellow">Implement this methodology to start, then iterate upon
it</mark>

_Tags: #note_SciVisEval_ <mark class="hltr-yellow">"GPT series, i.e., GPT-5,
GPT-4.1, and GPT-4o, as their backbone LLM."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=TN6UZBEH))
<mark class="hltr-yellow">Evaluate these models</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"Each experiment is
repeated 10 times for statistical robustness. The agents are instructed to load
the Bonsai dataset with given parameters, perform volume rendering, and adjust
the transfer function to achieve the target visualization: “A potted tree with a
brown pot, silver branches, and golden leaves.” The resulting ParaView state is
saved for subsequent evaluation. Upon task completion, overall visualization
quality is assessed using an instruction-tuned multi-modal LLM judge (e.g.,
GPT4o), presented with both the ground-truth images and the agentgenerated
results. The judge evaluates outputs against explicit criteria: whether the
overall goal is met, whether the pot is brown, the branches are silver, and the
leaves are gold. These scores form part of the final evaluation metric. To
enhance robustness of the assessment, the LLM-based evaluation is supplemented
with hard-coded verification scripts executed via pvpython. The saved ParaView
state is reloaded to confirm the correct volume rendering configuration and
accurate colormap settings. For code-generating agents such as ChatVis, we
additionally compute the CodeBERT-based [11] similarity between the generated
and gold-standard reference scripts. While these casespecific checks
substantially improve reliability, they require additional manual effort to
design and maintain. Performance metrics, including token usage, monetary cost,
and task completion time, are recorded as they directly reflect user-perceived
latency and the practical feasibility of deploying such agents. Each metric is
assigned a point value, and the sum of these points constitutes the final
evaluation score (see Figure 1)."</mark>
([Page 3](zotero://open-pdf/library/items/FTPJFEHM?page=3&annotation=EVHWUM5F))
<mark class="hltr-yellow">Evaluation methodology. Implement this first to
evaluate agent performance</mark>

_Tags: #note_SciVisOpenProblem_ <mark class="hltr-purple">"Table 1 shows that
while the MCP-based agent delivers stable, high-quality results, its reliance on
complex toolchains leads to high latency, limiting real-world deployment. In
contrast, ChatVis—lacking vision capabilities and generating code on the
fly—typically completes tasks more quickly but incurs increased token usage and
reduced visualization quality."</mark>
([Page 4](zotero://open-pdf/library/items/FTPJFEHM?page=4&annotation=JLE3HSUX))
<mark class="hltr-purple">I disagree with this. The MCP server enables
reproducibility and while latency is an issue, the traceability and
understanding of the system's process exceeds the latency issues (which was
never an explicit goal of a SciVis agent to begin with either)</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"Claude, LLaMA, and
Qwen"</mark>
([Page 4](zotero://open-pdf/library/items/FTPJFEHM?page=4&annotation=UDQ3ZSER))
<mark class="hltr-yellow">Evaluate these models</mark>

_Tags: #note_SciVisMethodology_ <mark class="hltr-yellow">"smaller language
models (SLMs)"</mark>
([Page 4](zotero://open-pdf/library/items/FTPJFEHM?page=4&annotation=PEYVUDUW))
<mark class="hltr-yellow">Evaluate a subset of these models</mark>

%% end annotations %%

%% Import Date: 2026-06-04T11:22:06.458-05:00 %%
