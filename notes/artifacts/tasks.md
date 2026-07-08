## About

This is a list of tasks that I need to complete in order to prove to my advisors
(Silvio and George) that I have had a productive summer at Argonne National
Labs. These tasks also provide the framework and scaffolding necessary to create
posters for submission to the SuperComputing poster session and an academic
workshop.

## Weekly Task List

> Created in collaboration with LLMs

#### Week 1 — Project Scoping & Alignment

> **Objective:** Define a concrete, demonstrable project targeting agentic
> tooling improvements for scientific visualization workflows.

> [**Deliverable:**](artifacts/week1b_deliverable.md) A one-page project charter
> shared with the team, including a diagram showing the agent -> visualization
> pipeline -> HPC system interaction.

- [x] M1.1 Meet with the thrust lead and relevant team members to select the
      target science domain for the prototype (cosmology, X-ray science, or
      fusion flow).
    - Primarily going to target synthetic datasets. The datasets come from prior
      work and a synthetically generated CFD simulation hosted on Aurora
- [x] M1.2 Define the assistant's input/output contract:
    - Input: Natural language queries from a scientist (e.g., "Generate a
      contour plot of dark matter density at timestep 400 with a threshold above
      1e3")
        - This is realistically going to be non-intuitive and non-specific. A
          better example would be "Generate an isosurface of this data file in
          ParaView"
        - The synthetic CFD dataset comes with example prompts, although these
          are fairly specific and may need to be generalized
        - Prior work also lists example works that we can use
            - ChatVis 2024, ChatVis 2025, ParaView MCP, SciVisAgentBench,
              SciVisAgentSkills
    - Output: An orchestrated visualization artifact (rendered image,
      interactive session URL, or ParaView state file) plus a provenance log of
      all actions taken.
        - These are functional requirements that the user will need to be able
          to work with.
            - Images come from all prior work
            - NL2SciVis benchmark uses paraview state files
            - Session URL comes from the ParaView MCP work. Although this may
              not be feasible as statefulness in MCP servers is difficult to
              implement
- [x] M1.3 Draft a one-page project charter specifying:
    - Which visualization backend(s) to target (ParaView/Catalyst, Ascent, VTK,
      matplotlib as fallback).
        - Nope, only focus on ParaView
    - Which agent framework to use (SmolAgents, LangChain, or custom).
        - We are going to use the OpenCode coding harness
    - Which LLM backends to evaluate (proprietary and open-source - see M2.5).
        - GPT, Anthropic, Open Models
    - Which compute target (Polaris, Sophia, Crux).
        - Crux
    - Success criteria for the summer deliverable.
        -
- [x] M1.4 Map the project charter to relevant project milestones, annotating
      which goals this work advances.

#### Week 2 — Technical Landscape Review & Environment Setup

> **Objective:** Understand the existing codebase, survey agentic visualization
> literature, establish a working development environment, and begin scoping
> model selection.

> **Deliverable:** A technical memo (~2 pages) summarizing the landscape review
> and candidate model list, a screenshot showing a test render from the sample
> dataset on ALCF hardware, and an annotated architecture diagram showing the
> proposed integration point.

- [ ] M2.1 Review existing team artifacts:
    - ChatVis implementation and architecture.
    - Genius tool for AI-assisted scientific reasoning.
    - Any existing Globus Flows/Compute integration prototypes.
    - Wilkins/Ascent in situ integration code.
- [ ] M2.2 Conduct a focused literature review (8-12 papers) on:
    - LLM-driven visualization generation (e.g., ChatVis, LIDA, Data Formulator,
      NL4DV).
    - Agentic orchestration patterns for scientific workflows (A2A, MCP
      protocols).
    - Multi-agent architectures for task decomposition in visualization
      contexts.
- [ ] M2.3 Obtain access to:
    - Source code repositories (GitHub) for ChatVis, Genius, Wilkins, Ascent.
    - ALCF machines (Polaris/Sophia/Crux) with appropriate allocations.
    - Argo or ALCF Inference Service for hosted LLM access.
    - A sample scientific dataset from the target domain (e.g., a small HACC
      snapshot, sample XPCS g2 curves, or a NekRS fusion output).
- [ ] M2.4 Build and validate the software stack on the target machine:
    - Install ParaView (headless/pvpython), Ascent, or VTK.
    - Verify that a simple Python script can load the sample dataset and produce
      a rendered visualization.
    - Verify connectivity to the ALCF Inference Service or deploy a local model
      endpoint.
- [ ] M2.5 Identify candidate LLM backends for evaluation throughout the
      project:
    - One large proprietary model (e.g., GPT-4o, Claude Sonnet).
    - One large open model (e.g., Llama 3.1 70B via ALCF Inference Service).
    - One small open model (e.g., Llama 3.1 8B, Qwen 2.5 7B).
    - Document selection rationale and access method for each.
- [ ] M2.6 Identify specific tooling options that are novel and have the
      potential to build off of existing systems.

#### Week 3 — Minimum Viable Agent: Single-Task Visualization Orchestration

> **Objective:** Build a minimal agent that accepts a natural language prompt
> and produces a single scientific visualization artifact.

> **Deliverable:** A live demo (screen recording or Jupyter notebook) showing
> the agent responding to three distinct natural language prompts and producing
> correct scientific visualizations from the sample dataset. Include a brief
> comparison note on the two LLM backends tested. The MCP server should be
> queryable from a separate terminal.

- [ ] M3.1 Reimplement the ChatViz agent loop using SmolAgents, LangChain, or a
      lightweight custom harness:
    - The agent receives a natural language query.
    - It invokes a tool (a Python function) that executes a visualization
      script.
    - It returns the result (image path, status message).
- [ ] M3.2 Implement at least three visualization tools as callable functions:
    - `load_dataset(path, format)` - loads a scientific dataset into memory.
    - `render_volume(dataset, variable, colormap, camera_position)` - produces a
      volume rendering or slice via ParaView/VTK.
    - `render_plot(dataset, variable, plot_type)` - produces a 2D analytical
      plot (e.g., histogram, line plot, contour plot).
- [ ] M3.3a Wrap these tools behind an interface that enables us to plug in
      additional, different, or completely new technologies in its place
- [ ] M3.3b MCP server so that external agents or clients can discover and
      invoke them programmatically:
    - Define the MCP tool schema (name, description, input JSON schema, output
      schema).
    - Verify that a generic MCP client can list tools and call them.
- [ ] M3.4 Ensure the agent integration is non-blocking to any existing pipeline
      components:
    - The agent operates as a sidecar process or microservice.
    - It reads data from a shared filesystem or data stream; it does not modify
      upstream outputs.
- [ ] M3.5 Test the MVP against at least two LLM backends from the candidate
      list (Week 2, M2.5):
    - Verify that the agent produces correct tool calls with both a large and a
      small model.
    - Note qualitative differences in tool selection accuracy and argument
      formatting.
- [ ] M3.6 Demonstrate end-to-end: user types a prompt -> agent selects tool ->
      visualization is produced -> image is returned.

#### Week 4 — Multi-Agent Coordination & Workflow Orchestration

> NOTE: I have not updated weeks 4 - 10 as of June 4th, 2026

- **Objective:** Extend the single agent into a multi-agent system capable of
  decomposing complex visualization requests.
- **Tasks:**
    - M4.1 Decompose the monolithic agent into specialized sub-agents:
        - Data Agent: Handles dataset discovery, loading, filtering, and
          metadata extraction.
        - Visualization Agent: Handles rendering, colormap selection, camera
          control, and annotation.
        - Workflow Agent: Handles sequencing, error recovery, and provenance
          logging.
    - M4.2 Integrate an agent coordination layer:
        - Evaluate and select a coordination mechanism (e.g., a simple
          orchestrator agent, CrewAI, AutoGen, or a custom A2A dispatcher).
        - Implement message passing between agents using A2A-style task cards or
          a shared blackboard.
    - M4.3 Wrap additional existing visualization tools or scripts behind
      MCP/A2A services:
        - Example: wrap an existing halo-finder script as a tool the Data Agent
          can invoke.
        - Example: wrap a ParaView macro for time-series animation as a
          Visualization Agent tool.
    - M4.4 Enable support for multiple LLM backends at the system level:
        - Configure the system to route requests to different backends (Argo,
          ALCF Inference Service, proprietary API) based on a configuration flag
          or per-agent assignment.
        - Test assigning different models to different sub-agents (e.g., large
          model for the Workflow Agent, small model for the Data Agent).
    - M4.5 Demonstrate a multi-step visualization workflow triggered by a single
      complex prompt:
        - Example: "Load the simulation snapshot at z=0, filter halos with
          mass > 1e14 solar masses, render a volume visualization of the density
          field centered on the most massive halo, and save the result."
        - The orchestrator decomposes this into: load -> filter -> identify
          target -> set camera -> render -> save.
- **Deliverable:** An architecture diagram of the multi-agent system with
  protocol annotations (MCP/A2A). A demo showing the complex multi-step prompt
  being decomposed, executed, and producing a final scientific visualization
  with a logged provenance trace (e.g., a JSON file recording each agent's
  actions and decisions). Include a note on which LLM backend was used for each
  sub-agent.

#### Week 5 — Small-Scale Benchmarking: Correctness & Responsiveness

- **Objective:** Establish quantitative baselines for the agent system's
  visualization performance, including a systematic comparison across LLM
  backends.
- **Tasks:**
    - M5.1 Define a benchmark suite of 10-15 natural language visualization
      prompts spanning:
        - Simple queries (single variable, single timestep rendering).
        - Moderate queries (filtering + rendering a derived quantity).
        - Complex queries (multi-step visualization workflows, comparative
          views).
        - Adversarial/ambiguous queries (to test robustness and clarification
          behavior).
    - M5.2 Define evaluation metrics:
        - Correctness: Does the produced visualization match a ground-truth
          reference? (Manual scoring on a 1-5 scale, or automated pixel-level
          comparison for deterministic renders.)
        - Task completion rate: What fraction of prompts result in a valid
          visualization output without human intervention?
        - Time to insight: Wall-clock time from prompt submission to
          visualization delivery.
        - Tool call accuracy: Does the agent select the correct tool(s) and pass
          valid arguments?
        - Provenance completeness: Does the log capture all intermediate steps?
    - M5.3 Implement a benchmarking harness that:
        - Iterates over the prompt suite.
        - Records all metrics automatically.
        - Supports swapping LLM backends via a configuration flag.
        - Outputs a structured results table (CSV/JSON).
    - M5.4 Run the full benchmark suite against all candidate LLM backends (from
      M2.5):
        - Large proprietary, large open, and small open models.
        - Record per-model metrics for direct comparison.
    - M5.5 Identify tunable parameters that affect visualization output quality:
        - System prompt / context window content.
        - Temperature and sampling parameters.
        - Tool description verbosity.
        - Number of agent reasoning steps allowed.
    - M5.6 Run a parameter sweep and freeze an optimal configuration per model.
    - M5.7 Select and document the recommended model configuration with
      justification based on the accuracy/latency/cost tradeoff.
- **Deliverable:** A benchmark results table comparing performance across the
  prompt suite and across all LLM backends. Include a model comparison chart
  (accuracy, latency, task completion rate). A one-page recommendation memo on
  the selected model configuration. Share results in a short slide deck (5-8
  slides) for the team.

#### Week 6 — Large-Scale & Stress Benchmarking

- **Objective:** Push the system to its limits with larger scientific datasets,
  more complex visualization queries, and concurrent usage patterns.
- **Tasks:**
    - M6.1 Identify stress-test cases:
        - Prompts requiring visualization of datasets that exceed single-node
          memory (requiring distributed rendering or out-of-core access).
        - Prompts requiring sequential visualization of many timesteps
          (animation generation).
        - Concurrent prompt submission (simulating multiple users or a batch of
          visualization queries).
    - M6.2 Scale the test environment:
        - If using Polaris, request a multi-node allocation and test distributed
          ParaView rendering triggered by the agent.
        - If using Globus Compute, test remote function execution for
          visualization tasks.
    - M6.3 Execute the stress benchmarks and record:
        - Throughput (visualizations per minute).
        - Latency distribution (p50, p95, p99).
        - Failure modes (timeouts, OOM errors, hallucinated tool calls,
          malformed visualization parameters).
        - Resource utilization (GPU memory, CPU, network I/O).
    - M6.4 Perform comparative analysis against the "frozen" parameters from
      Week 5:
        - Do optimal parameters from small-scale testing hold at larger scale?
        - Where are the bottlenecks (LLM inference, data I/O, rendering)?
    - M6.5 Document failure modes and propose mitigations (e.g., retry logic,
      fallback to simpler rendering, chunked data loading).
- **Deliverable:** A performance report with latency/throughput charts, a table
  of failure modes and mitigations, and an updated architecture diagram
  annotating bottlenecks. A side-by-side comparison table of small-scale vs.
  large-scale results.

#### Week 7 — Model Optimization & Targeted Refinement

- **Objective:** Using the empirical evidence from Weeks 5-6, optimize the
  system's weakest components and explore techniques to close identified
  performance gaps.
- **Tasks:**
    - M7.1 Triage Week 5/6 results to identify the top 3 failure categories
      (e.g., incorrect tool selection, malformed arguments, poor multi-step
      decomposition, latency spikes) and rank them by impact on task completion
      rate.
    - M7.2 For each failure category, implement a targeted mitigation:
        - Incorrect tool selection: Refine tool descriptions, add few-shot
          examples to the system prompt, or implement a tool-selection
          verification step where the agent confirms its plan before execution.
        - Malformed arguments: Add Pydantic or JSON Schema validation at the
          tool boundary with automatic retry and error feedback to the agent.
        - Poor multi-step decomposition: Introduce explicit chain-of-thought
          planning prompts or a dedicated planning agent that generates a
          step-by-step plan before execution begins.
        - Latency spikes: Profile the pipeline end-to-end, identify whether the
          bottleneck is LLM inference, data I/O, or rendering, and apply
          targeted fixes (e.g., caching repeated data loads, batching tool
          calls, switching to a faster model for simple sub-tasks).
    - M7.3 If the small open model underperformed significantly in Weeks 5-6,
      explore parameter-efficient fine-tuning (PEFT):
        - Curate a training dataset of 50-100 (prompt, correct tool call
          sequence) pairs derived from the benchmark suite and manual
          corrections.
        - Apply QLoRA/LoRA fine-tuning on the small model.
        - Re-run the benchmark suite and compare against the pre-tuned baseline.
    - M7.4 If fine-tuning is not feasible or not impactful, explore
      distillation:
        - Use the large model's outputs (tool call traces from successful
          benchmark runs) as training signal for the small model.
        - Measure latency and accuracy improvements.
    - M7.5 Implement RAG over visualization documentation to reduce tool call
      errors:
        - Index ParaView Python API docs, VTK class references, and
          domain-specific dataset schemas into a vector store.
        - Wire the RAG retriever into the agent's tool-selection pipeline so
          that the agent can look up correct API usage before generating tool
          calls.
        - Measure the impact on tool call accuracy by re-running a subset of the
          Week 5 benchmark suite with and without RAG.
    - M7.6 Re-run the full benchmark suite with all Week 7 enhancements enabled
      and produce a before/after comparison:
        - Task completion rate delta.
        - Tool call accuracy delta.
        - Latency delta.
        - Qualitative assessment of multi-step workflow reliability.
    - M7.7 Freeze the final system configuration (model selection, prompt
      templates, RAG settings, validation layers) as the release candidate for
      documentation and demonstration.
- **Deliverable:** A short optimization report (~2 pages) documenting: (1) the
  top failure categories identified, (2) the mitigation implemented for each,
  (3) before/after benchmark comparison tables, and (4) the frozen final
  configuration. If PEFT or distillation was attempted, include a learning curve
  plot and accuracy comparison. If RAG was integrated, include a with/without
  comparison on tool call accuracy.

#### Week 8 — "Learning on the Lawn" Poster Draft & Narrative Synthesis

- **Objective:** Synthesize all findings into a compelling visual narrative for
  the poster session.
- **Tasks:**
    - M8.1 Outline the poster structure:
        - Motivation: The gap between scientific data generation and discovery
          at extreme scale.
        - Approach: Multi-agent LLM architecture for visualization workflow
          orchestration (architecture diagram).
        - Demo: Annotated screenshot sequence showing a complex prompt ->
          decomposition -> scientific visualization output.
        - Results: Key benchmark metrics (task completion rate, time to insight,
          model comparison, optimization impact).
        - Impact: How this work advances agentic scientific visualization on
          HPC.
    - M8.2 Create high-quality figures:
        - System architecture diagram (agents, tools, MCP/A2A protocols, HPC
          backend).
        - Example visualization outputs from the science domain.
        - Benchmark result charts (including Week 7 optimization improvements).
    - M8.3 Write concise poster text (aim for <= 800 words total on the poster).
    - M8.4 Circulate the draft to the team and mentor for feedback.
- **Deliverable:** A complete poster draft (PDF or PowerPoint) ready for review.

#### Week 9 — Final Submission & Documentation

- **Objective:** Finalize all deliverables and ensure reproducibility.
- **Tasks:**
    - M9.1 Incorporate feedback and finalize the "Learning on the Lawn" poster
      for submission.
    - M9.2 Write a comprehensive final report (8-12 pages) covering:
        - Problem statement and relationship to project milestones.
        - System architecture and design decisions.
        - Implementation details (frameworks, models, tools, infrastructure).
        - Benchmark methodology and results (Weeks 5-7).
        - Optimization strategies and their impact (Week 7).
        - Lessons learned and future work.
    - M9.3 Package the codebase for handoff:
        - Clean repository with README, installation instructions, and usage
          examples.
        - Configuration files for all tested model/parameter combinations.
        - Benchmark suite and evaluation harness.
        - Sample datasets or pointers to them.
    - M9.4 Record a 5-minute demo video of the system in action.
- **Deliverable:** Submitted poster, final report PDF, clean GitHub repository,
  and demo video.

#### Week 10 — Conference/Workshop Paper Preparation

- **Objective:** Distill the work into a submission-ready workshop paper aligned
  with an SC-affiliated venue.
- **Tasks:**
    - M10.1 Identify and prioritize target venues
    - M10.2 Select a primary venue and one backup venue based on fit, deadline,
      and page limits.
    - M10.3 Reformat the final report into the selected venue’s paper template
      and page constraints.
    - M10.4 Sharpen the contributions section to emphasize novelty:
        - Integration of MCP/A2A-style protocols for scientific workflow and
          visualization orchestration on HPC.
        - Empirical comparison of LLM backbones for agentic scientific computing
          and visualization tasks.
        - Benchmark suite for evaluating AI-assisted scientific
          workflow/visualization assistants.
        - Systematic optimization methodology (failure triage -> targeted
          mitigation -> validation).
    - M10.5 Tailor framing to the selected venue:
        - For **AI on HPC**: emphasize AI-enhanced HPC workflows and scientific
          application relevance.
        - For **WORKS**: emphasize workflow composition, orchestration, and
          large-scale science execution.
        - For **AI4S**: emphasize generative AI for scientific discovery and
          development workflows.
        - For **AgenticAI4HPC**: emphasize agentic orchestration, intelligent
          coordination, and coupled simulation/data/AI workflows.
    - M10.6 Circulate to co-authors for review and finalize.
- **Deliverable:** A submission-ready workshop paper formatted for the primary
  target venue, with a backup version plan for an alternate SC workshop if
  needed.

#### Summary: Week-by-Week Focus

| Week | Focus                                    | Key Output                                            |
| ---- | ---------------------------------------- | ----------------------------------------------------- |
| 1    | Scoping                                  | Project charter                                       |
| 2    | Review, Setup & Model Candidates         | Technical memo, working environment                   |
| 3    | MVP Agent + MCP + Multi-Model Test       | End-to-end demo, MCP server                           |
| 4    | Multi-Agent + A2A + Backend Routing      | Multi-step workflow demo, architecture diagram        |
| 5    | Small Benchmarks + Model Comparison      | Benchmark results, model recommendation               |
| 6    | Large-Scale Stress Benchmarks            | Performance report, failure mode analysis             |
| 7    | Model Optimization & Targeted Refinement | Optimization report, frozen final configuration       |
| 8    | Poster Draft                             | Poster PDF                                            |
| 9    | Report & Submission                      | Final report, code repository, demo video             |
| 10   | Paper                                    | Submission-ready workshop paper for selected SC venue |
