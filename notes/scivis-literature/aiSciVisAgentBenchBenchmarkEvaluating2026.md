---
title:
    "SciVisAgentBench: A Benchmark for Evaluating Scientific Data Analysis and
    Visualization Agents"
citekey: "aiSciVisAgentBenchBenchmarkEvaluating2026"
authors:
    "Kuangshi Ai, Haichao Miao, Kaiyuan Tang, Nathaniel Gorski, Jianxin Sun,
    Guoxi Liu, Helgi I. Ingolfsson, David Lenz, Hanqi Guo, Hongfeng Yu, Teja
    Leburu, Michael Molash, Bei Wang, Tom Peterka, Chaoli Wang, Shusen Liu"
year: 2026
tags:
    [
        "FOS: Computer and information sciences",
        "Human-Computer Interaction (cs.HC)",
        "Artificial Intelligence (cs.AI)",
        "Graphics (cs.GR)",
    ]
---

# SciVisAgentBench: A Benchmark for Evaluating Scientific Data Analysis and Visualization Agents

**Zotero Link:** [Zotero Link](zotero://select/library/items/8KKQEVSL) | **PDF
Link:** [PDF](zotero://select/library/items/ISMPHMZY)

---

## Summary & Notes

%% begin notes %% Write your personal notes, summaries, and synthesis here! %%
end notes %%

---

## Annotations

%% begin annotations %% \_Tags: #note_SciVisOpenProblem\_
<mark class="hltr-purple">"the community lacks a principled and reproducible
benchmark for evaluating these emerging SciVis agents in realistic, multi-step
analysis settings"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=8WWUTIV3))
<mark class="hltr-purple">Open problem, although this seems to have closed this
gap. Needs more updates to be truly a solution IMO</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"SciVisAgentBench"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=FF8WU738))
<mark class="hltr-blue">Benchmark suit</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"Our benchmark is grounded in
a structured taxonomy spanning four dimensions: application domain, data type,
complexity level, and visualization operation."</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=YSQ33XQL))
<mark class="hltr-blue">Evaluations to support</mark>

<mark class="hltr-blue">"108 expert-crafted cases covering diverse SciVis
scenarios"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=ZL5V98VG))

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"we introduce a
multimodal outcome-centric evaluation pipeline that combines LLM-based judging
with deterministic evaluators, including image-based metrics, code checkers,
rule-based verifiers, and case-specific evaluators."</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=BYCRW6RQ))
<mark class="hltr-yellow">Using multiple modalities to autonomously analyze
SciVisAgents</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"We also conduct a validity
study with 12 SciVis experts to examine the agreement between human and LLM
judges."</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=8U3W4N8P))
<mark class="hltr-blue">Need to get a hold of these evaluations for ground
truth/ golden exampels</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"AVA"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=Y4IVYAM7))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ChatVis"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=WAZSMGY4))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ParaView-MCP"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=P4EMNHET))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"NLI4VolVis"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=XK9XTUK6))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"VizGenie"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=F4HWMG9U))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"InferA"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=9FIIH4QL))

\_Tags: #note_SciVisCore\_ <mark class="hltr-magenta">"how should progress in
SciVis agents be measured in a principled, reproducible, and scalable
way?"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=GWR3VRQA))
<mark class="hltr-magenta">Core question to answer for longitudinal
analysis</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"NL4DV"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=5NAJF95I))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"VisEval"</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=KDWINYMK))

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"heir scope remains limited.
These benchmarks typically focus on short-horizon tasks, 2D charts, or
declarative plotting, and do not capture the defining characteristics of SciVis:
high-dimensional data, view-dependent semantics, complex pipelines composed of
multiple operations, and exploratory workflows that rely on expert
judgment."</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=VEQ2FTPD))
<mark class="hltr-blue">It would be nice to also use these benchmarks when
comparing against agentic solutions</mark>

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"Consequently,
existing evaluations fall short of providing a reliable benchmark for measuring
agent capability in scientific data analysis and visualization."</mark>
([Page 1](zotero://open-pdf/library/items/ISMPHMZY?page=1&annotation=7KLK6V2R))
<mark class="hltr-purple">Open problem in benchmarking</mark>

\_Tags: #note_SciVisCore\_ <mark class="hltr-magenta">"First, meaningful SciVis
tasks frequently require multi-step workflows involving data loading, filtering,
parameter tuning, rendering choices, and view manipulation, rather than
single-shot plot generation. Second, visualization tasks often admit multiple
valid outcomes, making the specification of ground truth inherently difficult.
Third, the notion of “correctness” is often entangled with subjective judgment
and domain expertise, complicating objective evaluation."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=UIBJXMQB))
<mark class="hltr-magenta">Core features and problems of Scientific
Agents</mark>

\_Tags: #note_SciVisEval, #note_SciVisCore\_
<mark class="hltr-blue">"SciVisAgentBench, a comprehensive and extensible
Benchmark for evaluating Scientific data analysis and Visualization
Agents."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=3ANBY75P))
<mark class="hltr-blue">Core evaluation suite</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"We begin by
assessing the capability of our LLM judge by having it evaluate agent-generated
visualizations against expert-defined ground truths using structured,
expert-authored rubrics."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=6QWQV3BQ))
<mark class="hltr-yellow">Methodology for autonomous reviews</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"We conduct a human-LLM
alignment study, in which SciVis experts and an MLLM judge independently
evaluate visualization outcomes, enabling us to quantify agreement and
reliability."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=QSW4X3U9))
<mark class="hltr-blue">Human evaluations critical for correctness</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"To further stress-test the
evaluation process, we examine the robustness of the LLM judge across variations
in prompts and presentation, as well as its limitations in multimodal
understanding."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=UWCFVNR6))
<mark class="hltr-blue">Multiple prompts and data representations</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"AgentBench"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=4TQZL5XW))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"AgentBoard"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=2ATN63PX))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"Kapoor et al. [30]
critiqued current evaluation practices, advocating for joint optimization of
accuracy and cost metrics rather than focusing solely on task completion
rates."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=26I8YFWG))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"GAIA"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=86MV7L7I))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"τ-bench"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=V8U8V4A6))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"WebArena"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=RE3MPCWT))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ToolLLM"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=CB39NVNH))

\_Tags: #note_SciVisBackground\_
<mark class="hltr-orange">"MultiAgentBench"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=VRY2IFD6))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"Holistic evaluation
frameworks [8] and agent architecture surveys [68] provide high-level guidance
but require substantial domain-specific adaptation for visualization-centric
systems."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=VVTYUHQ9))

\_Tags: #note_SciVisBackground\_
<mark class="hltr-orange">"VisualWebArena"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=QNMDUGKD))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"MMMU"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=GQVX6LHC))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"Windows Agent
Arena"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=JDZDBTIH))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"LLM Evaluate"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=PLGZ3KFC))

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"Yehudai et al. [62]
synthesize open problems in LLM-based agent evaluation, emphasizing
reproducibility, generalization, and task diversity."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=V4GTAAYY))
<mark class="hltr-purple">Open problems in the field</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Zhu et al. [72]
show that many existing agentic benchmarks suffer from validity issues in task
design and outcome evaluation, and propose best practices for constructing
rigorous benchmarks."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=X3AGY4FA))
<mark class="hltr-yellow">Best practices for evaluating SciVisAgents</mark>

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"Empirical studies
[28, 54] further demonstrate that LLMs continue to struggle with visualization
generation and understanding, underscoring the need for domain-specific,
carefully constructed evaluation frameworks."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=EKTN8IS4))
<mark class="hltr-purple">Open problem</mark>

<mark class="hltr-blue">"Dhanoa et al. [13] framed this shift as agentic
visualization,"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=WJPMJBYL))

<mark class="hltr-red">"defining design patterns that highlight the balance
between autonomous actions and analyst control."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=7HMLARRW))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"VOICE"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=K6Q5EGIA))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"IntuiTF"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=HMJKT47C))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"CoDA"</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=NFGAHLZF))

<mark class="hltr-red">"treats visualization more broadly as a collaborative
multi-agent workflow in which specialized agents negotiate specification,
refinement, and validation."</mark>
([Page 2](zotero://open-pdf/library/items/ISMPHMZY?page=2&annotation=SQ4ZHXNU))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"TexGS-VolVis"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=I5KB7ZGG))

<mark class="hltr-yellow">"Zhang et al. [67] advance semantic mapping for flow
visualization"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=EZP6U9TF))
<mark class="hltr-yellow">Methodology advancement</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"Drawing
Pandas"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=7G374Y5T))

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Wu et al. [59]
introduced a principled comparison against hypothetical rational agents,
offering insight into the actual contribution of visualization to analytical
outcomes."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=VMM2PSCX))
<mark class="hltr-yellow">Methodology</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"MatPlotAgent"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=GVXCSUM9))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"LIDA"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=XGG6JKVY))

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"introduces
visualization-specific metrics such as visualization error rate (VER) and
self-evaluated visualization quality (SEVQ), accounting for both correctness and
perceptual quality."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=I2LZJYSI))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"PlotGen"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=ND6SK9CE))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"nvAgent"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=RGWXC8X3))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ChartLlama"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=JK4YPHLW))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"neural machine
translation for visualization [39],"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=RVDENYNQ))

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"NL2VIS benchmarks"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=Q9F92GQS))
<mark class="hltr-blue">Evaluation</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"NL2SQL"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=R6CDFE6I))

<mark class="hltr-blue">"DA-Code"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=JQBVP99X))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ThinkGeo"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=LG37PRS3))

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"SVLAT"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=9EF3J8QI))

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Ai et al. [2]
called for an evaluation-centric paradigm for SciVis agents, arguing that the
absence of systematic, reproducible benchmarks fundamentally constrains progress
in agentic visualization."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=IIT7SXGJ))
<mark class="hltr-yellow">Methodology improvement</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ParaView [1], napari
[51], VMD [26]"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=7PZHETZE))

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"Multidimensional evaluation.
We consider three dimensions: outcome quality, process behavior, and efficiency
for benchmark assessment. Outcome correctness serves as the primary evaluation
axis in the current release, while process-level analysis remains future work
due to reproducibility and stability challenges in trajectory assessment.
Efficiency is quantified through execution cost, including time and token usage,
as well as benchmark-level computational tractability, ensuring that evaluations
can be run repeatedly without excessive overhead"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=LI9ED2IZ))
<mark class="hltr-blue">Evaluations to consider in my paper</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Reproducibility is
a central design requirement."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=R4GHC7DA))

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Where full
determinism is infeasible due to stochastic model behavior, repeated trials and
consistency measures are incorporated to quantify variability and
robustness."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=BXNLCUSU))
<mark class="hltr-yellow">Repeated trials. Potentially thousands of times if
possible</mark>

\_Tags: #note_SciVisDataset\_ <mark class="hltr-red">"Expert-contributed cases
are hosted through a public Hugging Face repository to facilitate versioning,
access, and reproducibility. In parallel, we actively coordinate with
collaborators across national laboratories and universities through recurring
meetings that support case development and benchmark expansion."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=S3RG3QRN))
<mark class="hltr-red">Dataset link:
https://huggingface.co/datasets/SciVisAgentBench/SciVisAgentBench-tasks</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"Datasets are selected to
represent major field structures in SciVis, including scalar, vector, and tensor
fields, as well as multivariate and time-varying data."</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=7TBNQCG4))
<mark class="hltr-blue">Evaluation data</mark>

\_Tags: #note_SciVisCore\_ <mark class="hltr-magenta">"Complexity levels. The
complexity of cases is categorized into three tiers: operations, tasks, or
workflows based on the highest-level procedural scope. An operation is a defined
procedure with explicit inputs and outputs. A task is a structured sequence of
operations performed to accomplish a clearly defined goal. A workflow is a
structured, potentially multi-stage process composed of multiple interrelated
tasks"</mark>
([Page 3](zotero://open-pdf/library/items/ISMPHMZY?page=3&annotation=EQQQWVLV))
<mark class="hltr-magenta">Core definitions of the scientific visualization
pipeline</mark>

<mark class="hltr-red">"ParaView visualization,"</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=5BY692Q2))

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"Only task-level and
workflowlevel entries are reported as benchmark cases, while operations serve as
compositional building blocks within these higher-level tiers."</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=XJ8SUHUN))
<mark class="hltr-purple">Workflows have yet to be evaluated leaving an open
problem for the field</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"First, the
benchmark supports tool-using agents that directly manipulate SciVis software
through APIs or protocol-based interfaces, such as MCP-style tool invocation.
These agents operate over visualization environments and maintain state across
multi-step interactions. Second, code-generating agents are supported, where
agents produce executable visualization scripts or pipelines (e.g., PvPython
scripts) that are subsequently run by external tools to generate visualization
outcomes. Third, the benchmark supports the evaluation of humanlike interface
agents that interact with visualization software in the same way as human users,
using screenshots, mouse clicks, keyboard input, scrolling, and other GUI-level
interactions rather than structured APIs or code execution. In addition, the
benchmark accommodates multimodal and multi-agent systems that combine natural
language, vision, and tool feedback, including architectures in which multiple
agents collaborate or specialize across different subtasks."</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=RD9HAQJ9))
<mark class="hltr-yellow">Support tool usage, code generation, human review,
multimodal, and multi-agent systems both for generation and review</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"We organize evaluation along
three complementary dimensions: outcome, process, and efficiency."</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=SZWFR3EI))
<mark class="hltr-blue">Evaluations to consider</mark>

\_Tags: #note_SciVisEval, #note_SciVisCore\_
<mark class="hltr-blue">"Outcome-based evaluation. Outcome-based evaluation
examines the relationship between task specifications and visualization outputs,
treating the agent as a black box. This approach enables direct comparison
across diverse agent designs (such as script-generating agents, tool-using
agents, and multimodal multi-agent systems) without requiring access to internal
states or reasoning traces."</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=7EYB4JIH))
<mark class="hltr-blue">Evaluation definition</mark>

\_Tags: #note_SciVisEval, #note_SciVisCore\_
<mark class="hltr-blue">"Process-based evaluation. Process-based evaluation
examines how an agent reaches a solution, including its action sequence, tool
usage, and intermediate decisions. It is useful for diagnosing failures,
assessing generalization, and distinguishing systematic reasoning from
trial-and-error behavior."</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=EXR4TK8G))
<mark class="hltr-blue">Evaluation definition</mark>

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"Although
conceptually central for understanding SciVis agent behavior, process-based
evaluation is not fully realized in the current SciVisAgentBench."</mark>
([Page 4](zotero://open-pdf/library/items/ISMPHMZY?page=4&annotation=U2QSRZQM))
<mark class="hltr-purple">PRIME usage is an open problem</mark>

\_Tags: #note_SciVisBackground\_ <mark class="hltr-orange">"ground truth [37],
constrained-prompt executions as references [63], or LLM-based evaluators to
judge trajectories directly [57]."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=MEHF9UJ6))
<mark class="hltr-orange">MCP implementations to review</mark>

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"These methods
assume a largely unique or outcome-insensitive action sequence. This assumption
rarely holds in SciVis: multiple sequences can produce the same visualization,
while early tool or parameter choices can dramatically affect results."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=2FNE7RI8))
<mark class="hltr-purple">Potential shortcoming of MCP approaches</mark>

\_Tags: #note_SciVisEval, #note_SciVisCore\_
<mark class="hltr-magenta">"Efficiency-aware evaluation. Efficiency is evaluated
from two complementary perspectives. At the agent level, efficiency captures
practical resource usage such as execution time, number of interaction steps,
and token consumption, reflecting the cost of deploying agents in scientific
workflows. At the benchmark level, efficiency constrains the evaluation
framework itself: SciVisAgentBench is designed to remain computationally
tractable, avoiding excessive evaluation time, tool invocations, or evaluator
overhead."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=VSMYSJQ7))
<mark class="hltr-magenta">Evaluation defintion</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Each task is paired
with a naturallanguage SciVis description, authored and refined by visualization
experts, that specifies a concrete analysis or visualization goal. To ensure
evaluability and reproducibility, all tasks included in the benchmark are
carefully curated to admit a single, explicit visualization outcome. Each task
is anchored by a mandatory ground-truth artifact, typically a reference
visualization image."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=XCBU7APR))
<mark class="hltr-yellow">Ensure that we are are only getting one vis
output</mark>

\_Tags: #note_SciVisDataset\_ <mark class="hltr-red">"For assessment, every task
includes expert-authored evaluation rubrics that describe the required
properties of a desirable visualization outcome. These rubrics are used to score
outcome quality, while efficiency metrics capture token usage and execution
time."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=2IQTVV7H))
<mark class="hltr-red">Human dataset of golden results</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Task specifications
and rubrics are serialized in a structured YAML format compatible with existing
evaluation frameworks such as promptfoo [47], enabling rapid text-based
testing."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=B7WE7RHB))
<mark class="hltr-yellow">Leverage promptfoo to iterate through prompts</mark>

\_Tags: #note_SciVisMethodology, #note_SciVisEval\_
<mark class="hltr-yellow">"The LLM judge scores each rubric on a 0-10 scale
based on how well the agent output satisfies the specified criteria. Prior work
has shown that LLM-based judges can be sensitive to prompt formulation and
rubric ordering [33]. To mitigate ordering bias, we adopt a rubric shuffling
strategy that randomly permutes the order of evaluation criteria across trials.
In addition, MLLM judgments may not always align with human preferences in
domains with limited training data [22, 58, 69], such as SciVis. To assess the
reliability of this evaluation strategy, we conduct dedicated validation
studies, including a human-LLM alignment analysis and a prompt and presentation
robustness study, reported in Section 6.2."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=BPZCKBBY))
<mark class="hltr-yellow">Multimodal eval methodology</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"Image-based metrics. For
tasks whose ground-truth visualizations are rendered under controlled conditions
(e.g., fixed camera pose, lighting, and background), the benchmark supports
quantitative evaluation of image-based similarity between agent-generated
outputs and groundtruth visualizations. We consider pixel-level and perceptual
metrics, including PSNR for measuring reconstruction fidelity, SSIM for
assessing structural similarity [56], and LPIPS for capturing perceptual
alignment [66]."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=VIZB4FFL))
<mark class="hltr-blue">Image evals</mark>

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"Evaluation proceeds by
verifying correct script generation and placement, executing the agent-generated
code, and checking for successful visualization output. We also explore
measuring similarity between reference and generated scripts using CodeBERT
[18]."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=UURWF79I))
<mark class="hltr-blue">Code gen checkers</mark>

<mark class="hltr-green">"However, in practice, this signal proved unreliable
for SciVis workflows: functionally correct and incorrect scripts often received
similar similarity scores, and the metric failed to capture nuanced but critical
differences. Therefore, we do not incorporate CodeBERT similarity into the final
scoring."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=NZSMLFNY))
<mark class="hltr-green">Static analysis would be simpler solutiu</mark>

<mark class="hltr-red">"Rule-based verifiers. Besides visualization-centric
tasks, SciVisAgentBench includes tasks with discrete outputs, such as
multiplechoice and binary (yes/no) questions."</mark>
([Page 5](zotero://open-pdf/library/items/ISMPHMZY?page=5&annotation=NDRYKD9F))

\_Tags: #note_SciVisEval\_ <mark class="hltr-blue">"Following Zhu et al. [72],
we examine two key aspects of benchmark validity: task validity and outcome
validity."</mark>
([Page 6](zotero://open-pdf/library/items/ISMPHMZY?page=6&annotation=MGHD4SLQ))
<mark class="hltr-blue">Evaluation</mark>

<mark class="hltr-red">"• Accuracy and agreement: The judge should demonstrate
strong accuracy, self-consistency, and agreement with human experts. •
Robustness: The judge should remain stable under prompt and presentation
variations."</mark>
([Page 7](zotero://open-pdf/library/items/ISMPHMZY?page=7&annotation=N2FV8AI2))

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"All three models
exhibit strong positive correlation with human judgments, indicating that
LLM-based judges can approximate expert evaluations of visualization quality.
Gemini-3.1-Pro achieves the highest correlation with human scores, while
Claude-Opus-4.6 yields the lowest RMSE and the closest score distribution to
human ratings."</mark>
([Page 7](zotero://open-pdf/library/items/ISMPHMZY?page=7&annotation=975KXMRP))
<mark class="hltr-yellow">Humans are not needed</mark>

\_Tags: #note_SciVisMetrics\_ <mark class="hltr-gray">"We quantified robustness
using a judge stability metric that measures score consistency across repeated
trials and perturbations. For each case, we computed the normalized standard
deviation of the judge scores across all experimental conditions and aggregated
the results across cases. Formally, the stability score is defined as Sstable =
1 − (∑N i=1 σi/R)/N, where σi is the standard deviation of the judge scores for
case i across perturbations, R = 11 is the scoring range (0–10), and N is the
number of evaluated cases. Higher values indicate more consistent judgments and,
therefore, greater robustness of the evaluation signal. Table 3 reports
stability across models. All LLM judges show high stability (Sstable > 0.92),
with Claude-Opus-4.6 achieving the highest score."</mark>
([Page 7](zotero://open-pdf/library/items/ISMPHMZY?page=7&annotation=AZPAJYUZ))
<mark class="hltr-gray">Judge evaluation. Use this to identify candidate judges
in multi-agent systems</mark>

\_Tags: #note_SciVisOpenProblem\_ <mark class="hltr-purple">"For ParaView
visualization tasks, we evaluated ChatVis [46] and ParaView-MCP [34]."</mark>
([Page 7](zotero://open-pdf/library/items/ISMPHMZY?page=7&annotation=YYEYFJ2W))
<mark class="hltr-purple">Focus future work on improving these results</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"All agents were
tested with two backbone LLMs, GPT-5.2 and Claude-Claude-Sonnet-4.5."</mark>
([Page 7](zotero://open-pdf/library/items/ISMPHMZY?page=7&annotation=5YSC5THV))
<mark class="hltr-yellow">Standardize on these LLMs</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"Claude Code [5] and
Codex [44], under a minimal-tool setting. Specifically, both agents had access
only to the underlying visualization engines (ParaView, napari, VMD, and TTK,
pre-installed in a conda environment)."</mark>
([Page 7](zotero://open-pdf/library/items/ISMPHMZY?page=7&annotation=YDIZ5I4K))
<mark class="hltr-yellow">Include these coding agents in these environments or
use a more constrained environment</mark>

\_Tags: #note_SciVisMetrics\_ <mark class="hltr-gray">"Table 5: Image-based
evaluation metrics on ParaView visualization tasks. Values are reported as
mean±std across three repeated trials. Setting PSNRscaled ↑ SSIMscaled ↑
LPIPSscaled ↓ ChatVis+GPT-5.2 9.63±0.67 0.44±0.01 0.57±0.01
ChatVis+Claude-Sonnet-4.5 10.50±0.97 0.50±0.04 0.50±0.04 ParaView-MCP+GPT-5.2
9.36±1.27 0.46±0.06 0.57±0.05 ParaView-MCP+Claude-Sonnet-4.5 12.00±2.96
0.54±0.14 0.49±0.14 Claude-Code+Claude-Sonnet-4.5 20.99±0.68 0.92±0.02 0.10±0.02
Codex+GPT-5.2 21.27±1.02 0.92±0.02 0.10±0.03"</mark>
([Page 8](zotero://open-pdf/library/items/ISMPHMZY?page=8&annotation=L5DMULTC))
<mark class="hltr-gray">Results to compare against</mark>

<mark class="hltr-purple">"SciVis agent across different backbone models,
Claude-Sonnet-4.5 generally performs better than GPT-5.2. However, improved
agentic performance often comes at the cost of higher token usage and longer
execution time, as shown in Table 6."</mark>
([Page 8](zotero://open-pdf/library/items/ISMPHMZY?page=8&annotation=U4NVATI2))
<mark class="hltr-purple">Focus on reducing token usage and faster execution
time</mark>

\_Tags: #note_SciVisMetrics\_ <mark class="hltr-gray">"Table 6: Token usage
across all five task suites of SciVisAgentBench. Input and output tokens are
reported as mean±std across three repeated trials. Token counts are shown using
K (thousands) and M (millions) for readability. Cached tokens are counted as
regular input tokens for consistent accounting and comparison across settings.
Task Suite Setting Input Tokens ↓ Output Tokens ↓ ParaView Visualization
ChatVis+GPT-5.2 156.64K±8.02K 180.56K±8.84K ChatVis+Claude-Sonnet-4.5
116.83K±7.59K 152.70K±6.88K ParaView-MCP+GPT-5.2 5.71M±0.61M 33.30K±1.99K
ParaView-MCP+Claude-Sonnet-4.5 28.51M±3.30M 380.30K±42.53K
Claude-Code+Claude-Sonnet-4.5 39.49M±6.62M 425.32K±55.52K Codex+GPT-5.2
45.57M±9.47M 396.60K±23.27K Molecular Visualization GMX-VMD-MCP+GPT-5.2
1.56M±0.17M 28.27K±6.57K GMX-VMD-MCP+Claude-Sonnet-4.5 5.89M±1.00M 82.90K±12.53K
Claude-Code+Claude-Sonnet-4.5 5.07M±0.12M 81.73K±3.45K Codex+GPT-5.2 8.63M±1.81M
112.28K±17.22K Bioimage Visualization BioImage-Agent+GPT-5.2 931.66K±186.31K
6.26K±1.47K BioImage-Agent+Claude-Sonnet-4.5 1.58M±0.02M 18.47K±1.28K
Claude-Code+Claude-Sonnet-4.5 8.60M±0.17M 125.66K±2.43K Codex+GPT-5.2
10.36M±3.76M 104.83K±25.78K Topology Visualization TopoPilot+GPT-5.2
394.00K±6.06K 2.89K±0.17K TopoPilot+Claude-Sonnet-4.5 3.74M±3.67M 57.93K±32.35K
Claude-Code+Claude-Sonnet-4.5 17.26M±1.87M 172.37K±18.51K Codex+GPT-5.2
46.04M±4.48M 193.58K±27.62K Object Identification ParaView-MCP+GPT-5.2
4.12M±0.39M 24.58K±1.20K ParaView-MCP+Claude-Sonnet-4.5 11.42M±0.49M
119.24K±4.65K Claude-Code+Claude-Sonnet-4.5 16.83M±0.28M 273.90K±22.71K
Codex+GPT-5.2 38.43M±3.55M 344.27K±14.95K"</mark>
([Page 8](zotero://open-pdf/library/items/ISMPHMZY?page=8&annotation=XRVKD4C4))
<mark class="hltr-gray">Token usages to compare against</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-purple">"They may also
misuse visualization APIs or capture incorrect outputs (e.g., Codex takes
screenshots of the entire napari GUI instead of the visualization viewport),
which increases interaction overhead and can lead to low-quality
results."</mark>
([Page 8](zotero://open-pdf/library/items/ISMPHMZY?page=8&annotation=F22CQFDU))
<mark class="hltr-purple">Make sure that we configure OpenCode/ coding agents to
support images</mark>

\_Tags: #note_SciVisMethodology\_ <mark class="hltr-yellow">"In contrast,
MCP-based agents emphasize efficiency and reliability through predefined tool
pipelines. They remain valuable in scenarios where tasks are well-defined and
predictable. In such settings, MCP pipelines provide reliable and reusable
solutions with minimal token usage."</mark>
([Page 9](zotero://open-pdf/library/items/ISMPHMZY?page=9&annotation=W8ENWM3I))
<mark class="hltr-yellow">Benefit of MCP</mark>

%% end annotations %%

%% Import Date: 2026-06-09T11:13:28.942-05:00 %%
