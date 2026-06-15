# Actionable Report: Evaluation-Centric Paradigm for Scientific Visualization Agents

This report synthesizes and structures key insights from the paper _"An
Evaluation-Centric Paradigm for Scientific Visualization Agents"_
([aiEvaluationCentricParadigmScientific2025](file:///home/nicholas/Documents/projects/alcf-viz-2026/notes/scivis-literature/aiEvaluationCentricParadigmScientific2025.md)).
It is organized into clustered themes by literature tags and provides an
actionable blueprint for running and evaluating agentic systems against
scientific visualization (SciVis) benchmarks.

---

## Part 1: Tag-Clustered Synthesis

### 1. Core Concepts & Definitions (`#note_SciVisCore_`)

- **Scientific Visualization (SciVis) Agent**: An AI system that interprets
  human natural language intent and autonomously interacts with the SciVis
  pipeline to produce visualizations satisfying user-specified analysis goals.
- **Core Workflows**: SciVis requires precise sequences of:
    - Sophisticated data transformations
    - Diverse rendering techniques
    - Multi-dimensional parameter mappings (e.g., transfer functions)
    - Careful view/camera selections
- **Execution Paradigms**:
    - _Outcome-Based_: Black-box evaluation focusing on the final
      visualization's quality, correctness, and interpretability.
    - _Process-Based_: White-box evaluation examining the intermediate actions,
      step efficiency, and structural logic of code execution.
    - _Task Complexity_: Divided into single-step atomic actions (e.g., loading
      data, applying filters) and multi-step tasks (requiring backtracking and
      refinement).
- **Evaluation Metrics Framework**:
    - _Accuracy_: Reliability and visual grounding of assessment signals.
    - _Coverage_: Spanning the full range of SciVis tasks and user intents.
    - _Cost-Effectiveness_: Amortizing computational and token overhead to allow
      rapid development iterations.

### 2. Benchmarking Datasets & Prompts (`#note_SciVisDataset_`, `#note_SciVisPrompt_`)

- **Reference Dataset**: The _Bonsai Dataset_ (available from
  [Open SciVis Datasets](http://klacansky.com/open-scivis-datasets/)) serves as
  a primary benchmark for volume visualization.
- **Standard Prompt Template**: An exemplar prompt used in evaluation is:
    > _"Load the Bonsai dataset with given parameters, perform volume rendering,
    > and adjust the transfer function to achieve the target visualization: 'A
    > potted tree with a brown pot, silver branches, and golden leaves.'"_

### 3. Evaluation Taxonomy & Validators (`#note_SciVisEval_`)

To thoroughly evaluate systems, benchmarks must use a three-pronged validation
strategy:

1.  **Multi-Modal LLM Judge**: Assesses overall semantic visualization quality
    (e.g., color matching, view angles, interpretability).
2.  **Hard-Coded State Verifiers**: Inspect the visualization engine's internal
    parameters (e.g., verifying rendering primitives, transfer functions, and
    exact isosurface values).
3.  **System Performance Monitors**: Track process metrics such as step length,
    token consumption, execution latency, and financial cost.

### 4. Running & Verification Methodology (`#note_SciVisMethodology`)

- **Sandbox Environments**: Secure execution environments where agents can run
  direct code or invoke tools through the Model Context Protocol (MCP).
- **Statistical Rigor**: Run experiments with at least 10 repeated trials per
  configuration to capture statistical variance.
- **Hybrid Protocols**:
    - Combine high-level MM-LLM judging with low-level Python scripts via
      `pvpython` that reload saved state files (e.g., ParaView `.pvsm` states)
      to verify configuration matches.
    - Assess code-generating agents (like ChatVis) by comparing generated
      scripts with gold-standard scripts using CodeBERT-based semantic
      similarity.
- **Checkpointing**: Decompose multi-step objectives into smaller, controllable
  checkpoints to pinpoint exactly where an agentic pipeline fails.

### 5. Open Research Problems & System Limitations (`#note_SciVisOpenProblem_`)

- **API Grounding & Tool Fragility**: High error rates in direct code generation
  and API usage (potentially mitigated by highly structured schemas like MCP).
- **Non-Deterministic Outcomes**: Different visualization parameters/angles can
  reveal the same scientific insights, causing ambiguity in strict image
  comparison.
- **Judge Reliability**: Visual grounding limits in standard MLLMs can be
  mitigated using a "council" of judges or visual transformer models.
- **Evaluation Cost & Resource Overhead**: High API and compute cost to run full
  rendering loops (can be mitigated by pre-rendering lookups or offline
  databases of transformations).
- **Latency vs. Reproducibility**: High-latency MCP-based systems offer superior
  repeatability and traceability compared to fast but brittle on-the-fly code
  generators (such as ChatVis).
- **Autonomous Meta-Capabilities**: The open challenge of agents autonomously
  choosing the correct visualization tool for a given dataset/problem.

### 6. Background Literature & Benchmarks (`#note_SciVisBackground_`)

Key systems and baselines to consult:

- _Task-Specific Benchmarks_: VisEval (chart reading), Drawing Pandas (data
  code-gen), MatPlotAgent, AVA, NLI4VolVis, VeriGUI (GUI-state verification).
- _General Agent Benchmarks_: AgentBench, AgentBoard, GAIA, τ-bench,
  VisualWebArena, MMMU.
- _SciVis Baselines_: ChatVis (code-generating, lacks vision), ParaView-MCP
  (tool-driven, stable but high-latency).

---

## Part 2: Actionable Engineering Guide

If you are running agentic systems against SciVis benchmarks, implement the
following end-to-end framework.

```
                  +-----------------------------------------+
                  |         Scientific User Prompt          |
                  +--------------------+--------------------+
                                       |
                                       v
                  +--------------------+--------------------+
                  |    Agentic Loop (planning & execution)  | <---+ (Backtrack)
                  +--------------------+--------------------+     |
                                       |                          |
                                       v                          |
                  +--------------------+--------------------+     |
                  |     Sandbox Render Engine (ParaView)    |     |
                  +---------+--------------------+----------+     |
                            |                    |                |
         (State File)       |                    | (Image Export) |
                            v                    v                |
                  +---------+----------+  +------+----------+     |
                  | State Verifier     |  | MLLM Judge      |     |
                  | (pvpython checks)  |  | (GPT-4o/Claude) |     |
                  +---------+----------+  +------+----------+     |
                            |                    |                |
                            +---------+----------+                |
                                      |                           |
                                      v                           |
                  +-------------------+---------------------+     |
                  | Process-Based Self-Evaluation Feedback  | ----+
                  +-------------------+---------------------+
                                      | (Criteria Met)
                                      v
                  +-------------------+---------------------+
                  |   Final Correctness Score & Performance |
                  +-----------------------------------------+
```

### Step 1: Environment Setup & Sandboxing

1.  **Isolate Execution**: Wrap the visualization engine (e.g., ParaView, VTK)
    in a secure Docker sandbox.
2.  **Define Interface**: Expose pipeline operations either via:
    - **Direct Python Scripting**: High flexibility, high failure rate.
    - **Model Context Protocol (MCP)**: Expose highly structured, hand-crafted
      API tools. This improves reliability and maintains a clean boundary.

### Step 2: Task Decompositions & Test Suites

1.  **Define Atomic Checkpoints**: Rather than prompting the agent to complete a
    whole visualization in one go, structure tasks into explicit checkpoints:
    - `Checkpoint 1`: Load the scientific dataset (`.raw`, `.vti`, etc.).
    - `Checkpoint 2`: Extract a specific technique feature (e.g., Isosurface at
      ISO value $X$).
    - `Checkpoint 3`: Map colors correctly using specified transfer functions.
2.  **Statistical Benchmarking Run**: Run each task across **10 repeated seeds**
    to compute robust success rates, tracking:
    - Average step count until completion.
    - Total tokens used (input, output, cache).
    - Success/failure rates per checkpoint.

### Step 3: Implement the Hybrid Evaluation Pipeline

A robust evaluation cannot rely on visual or state checks alone. You must build
a hybrid evaluation module combining:

#### A. Hard-Coded Engine State Verification

Write Python scripts that execute under `pvpython` to inspect the generated
state directly:

```python
# verify_state.py
from paraview.simple import *

def verify_bonsai_isosurface():
    # Load saved state
    LoadState("output_state.pvsm")

    # Locate target filter
    contour = FindSource("Contour1")
    assert contour is not None, "Error: Contour filter was not applied."

    # Check physical values
    iso_values = contour.Isosurfaces
    assert abs(iso_values[0] - 80.0) < 1e-3, f"Incorrect ISO value: {iso_values[0]}"

    # Check volume representation
    volume = GetRepresentation()
    assert volume.Representation == 'Volume', "Not configured for volume rendering."
    print("Engine state verification passed!")
```

#### B. Multi-Modal LLM Judge Scoring

Feed the exported render image along with the ground-truth image to a
vision-capable model (e.g., Claude 3.5 Sonnet, GPT-4o) using explicit,
structured scoring instructions:

```markdown
You are a scientific visualization judge evaluating an agent's output.

Target Specifications:

- Feature: Potted tree from Bonsai dataset.
- Pot color: Brown.
- Branch color: Silver/grey.
- Leaf color: Gold.

Evaluate the attached agent-generated image against the specifications:

1. Is the target dataset correctly oriented? (Score 0-2)
2. Are the transfer functions correctly applied to resolve the colors (brown
   pot, silver branches, golden leaves)? (Score 0-5)
3. Is there visual noise or occluding artifacts? (Score 0-3)

Output your response in the following JSON format: { "scores": {"orientation":
X, "color_accuracy": Y, "noise": Z}, "total_score": Total, "feedback": "..." }
```

#### C. Code-Level Assessment (For Code-Gen Agents)

Calculate CodeBERT semantic similarity between the generated script and your
reference gold-standard script. If the similarity is high but execution fails,
look for API deprecations or path issues in the sandbox.

### Step 4: Mitigate Known Failures during System Optimization

- **Combatting API Grounding Fragility**: Inject highly structured JSON schemas
  and docstrings directly into the agent's system prompt or MCP definitions.
- **Handling Non-Determinism**: If the agent's camera view differs from the
  ground truth but displays the requested features perfectly, rely on **Engine
  State Verification** (which is camera-invariant) rather than strict
  visual-difference thresholds.
- **In-Loop Self-Correction**: Integrate the MLLM judge and hard-coded state
  checks into the agentic loop itself. Allow the agent to self-inspect the
  rendered frame and state, compare it against the goal, and iteratively refine
  its visualization parameters before presenting the final result.
