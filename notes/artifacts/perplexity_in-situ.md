<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# I want to learn more about HPC in-situ visualization and workflows. Currently, I am aware of Decaf, PyCOMPSs, Pegasus, Wilkins, and Ascent. However, I do not have academic references for these software packages. Can you please identify the academic artifacts, summarize what each tool is capable of, and compare and contrast each of these tools.

Here are the main academic references for each system, what they actually do,
and how they differ in an HPC in‑situ/workflow context.[^1][^2][^3][^4][^5]

---

## Key academic references

### Decaf

- M. Dreher and T. Peterka, “Decaf: Decoupled Dataflows for In Situ
  High‑Performance Workflows,” Argonne National Laboratory technical report
  (2017).[^6][^7]
- O. Yildiz et al., “LowFive: In Situ Data Transport for High‑Performance
  Workflows,” in _In Situ Visualization for Computational Science_, Springer,
  2022 – cites and summarizes Decaf and related work.[^8]
- T. Peterka, “Decaf: Decoupled Dataflows for In Situ Workflows,” chapter in _In
  Situ Visualization for Computational Science_ (Mathematics and Visualization,
  Springer).[^9][^8]

### PyCOMPSs

- E. Tejedor et al., “PyCOMPSs: Parallel computational workflows in Python,”
  _International Journal of High Performance Computing Applications_,
  31(1):66–82, 2017, DOI 10.1177/1094342015594678.[^2][^10][^11]
- PyCOMPSs/COMPSs overview and tutorial material (HPC‑AI Society slides)
  describing the task‑based programming model and runtime.[^12]
- PRACE “Development of sample application in PyCOMPSs/COMPSs” training
  material.[^13]

### Pegasus

- E. Deelman et al., “Pegasus, a workflow management system for science
  automation,” _Future Generation Computer Systems_, 46:17–35, 2015, DOI
  10.1016/j.future.2014.10.008.[^14][^15]
- Pegasus project descriptions and usage reports (e.g., New Frontiers Initiative
  seminar and official GitHub docs).[^16][^17][^3]

### Wilkins

- O. Yildiz et al., “Wilkins: HPC In Situ Workflows Made Easy,” _Frontiers in
  High Performance Computing_, 2, 2024, DOI
  10.3389/fhpcp.2024.1472719.[^18][^4][^19]
- The Wilkins paper builds directly on “LowFive: In Situ Data Transport for
  High‑Performance Workflows,” which describes the underlying HDF5‑based
  transport.[^8]

### Ascent

- Ascent was first presented at the ISAV 2017 Workshop (in situ visualization
  workshop at SC17), as cited in the official Ascent documentation.[^5]
- The Ascent infrastructure is described in detail in a chapter in _In Situ
  Visualization for Computational Science_ (Mathematics and Visualization,
  Springer; editors Childs, Bennett, Garth), as referenced by the Ascent
  docs.[^20][^5]
- Multiple LLNL/ATPESC tutorial slide decks: “Ascent: Flyweight In Situ
  Visualization and Analysis for HPC Simulations” (2018–2025
  series).[^21][^22][^23][^24][^25][^26]

---

## Capabilities by system

### Decaf

Decaf is a dataflow system focused on parallel communication and coordination of
coupled tasks in in‑situ HPC workflows.[^1][^9] It represents an in‑situ
workflow as a directed graph of tasks connected by parallel message‑passing
channels over MPI, and it can perform arbitrary data transformations (from
simple forwarding to complex redistributions) inside the dataflow.[^9][^1]

Key capabilities:

- **Heterogeneous coupling layer.** Decaf lets you interconnect independently
  developed components that may use different programming models (e.g., MPI
  simulation, DIY analysis, external visualization tools) via a common dataflow,
  without forcing everything into a single runtime.[^1][^9][^8]
- **Message‑driven, parallel execution.** The runtime is fully message‑driven:
  tasks fire when their input messages arrive, enabling efficient parallelism
  and even cyclic task dependencies for computational steering.[^6][^9][^1]
- **Library + Python workflow API.** It provides a C++ library and a simple
  Python API to describe the workflow graph, allocate resources, and plug in
  custom dataflow operators while using MPI for high‑performance
  communication.[^6][^9][^1]

In practice, Decaf is usually embedded alongside existing simulation and
analysis codes to build tightly or loosely coupled in‑situ workflows without
rewriting those codes into a new framework.[^9][^8][^1]

---

### PyCOMPSs

PyCOMPSs is a task‑based programming model and runtime that parallelizes Python
(and other language) applications by turning annotated functions into
distributed tasks executed on clusters, clouds, or grids.[^13][^12][^2] The
runtime automatically builds a data‑dependency task graph from the
directionality of function arguments and schedules tasks and data transfers
accordingly.[^12][^2][^13]

Key capabilities:

- **Task‑based programming model.** Developers annotate Python, Java, or C/C++
  functions/methods as tasks, and the runtime infers dependencies between tasks
  from “in/out/inout” parameter annotations, building a dynamic task
  graph.[^2][^13][^12]
- **Distributed execution.** PyCOMPSs executes tasks on distributed resources
  (nodes in a cluster, cloud VMs, etc.) under a master‑worker scheme, handling
  scheduling, data movement, and fault management.[^13][^12]
- **Integration with Big Data backends.** It can treat data stored in backends
  like Cassandra (Hecuba) or persistent object stores (dataClay) as “persistent
  objects”, letting workflows span HPC and Big Data storage.[^2][^13]
- **Workflows of external codes.** PyCOMPSs can orchestrate workflows composed
  of external binaries, including MPI simulations, by wrapping them as tasks, so
  you can combine simulations, analyses, and preprocessing/postprocessing stages
  in a single task graph.[^12][^2]

PyCOMPSs itself is not a visualization library; instead, it is used to express
and execute complex computational workflows that may include simulation,
analysis, and external in‑situ or post‑hoc visualization tasks.[^13][^12][^2]

---

### Pegasus

Pegasus is a workflow management system (WMS) that maps abstract scientific
workflows, expressed as DAGs, onto a wide range of distributed and HPC
infrastructures.[^27][^17][^3] It is widely used in data‑intensive scientific
projects (such as LIGO and SCEC) to orchestrate large, complex workflows with
hundreds of thousands to millions of tasks.[^17][^3][^16]

Key capabilities:

- **Abstract DAG workflows.** Users describe workflows at an abstract level as
  directed acyclic graphs (DAGs), independent of specific execution sites, via
  APIs in Python, Java, R, or Jupyter.[^16][^27][^17]
- **Automated mapping and data management.** Pegasus maps abstract workflows to
  executable workflows for target platforms (HTCondor pools, HPC clusters,
  grids, clouds), automatically locating input data, planning data transfers,
  and inserting auxiliary jobs for staging and cleanup.[^3][^27][^17]
- **Scalability and reliability.** It has been used to run workflows with up to
  roughly one million tasks and tens of terabytes of data, with features like
  task clustering, retries, and provenance capture to ensure reliable
  large‑scale execution.[^15][^17][^3]
- **Provenance and reuse.** Pegasus records data locations, software and
  parameter configurations, and execution metadata, enabling reproducibility and
  partial re‑runs of only the remaining work.[^17][^3]

Pegasus is primarily a system‑level workflow engine; in HPC in‑situ contexts it
typically orchestrates the overall pipeline (multiple simulations, analysis
codes, and perhaps in‑situ hooks) rather than providing in‑memory visualization
capabilities itself.[^27][^16][^17]

---

### Wilkins

Wilkins is an in‑situ workflow system designed to make in‑situ workflows easier
to specify and run while still supporting scalable, efficient execution of
workflow tasks.[^4][^19][^18] It builds on LowFive, an HDF5‑based in‑situ data
transport layer, to couple tasks that already use HDF5 with minimal or no code
changes.[^19][^4][^8]

Key capabilities:

- **Flexible workflow description.** Wilkins provides a flexible interface for
  describing in‑situ workflows, targeting scientists who need to couple
  simulations, analyses, and visualization codes at runtime.[^4][^19]
- **HDF5‑based transport via LowFive.** Its data transport layer uses the HDF5
  data model so that executables using HDF5 can communicate in situ (in‑memory
  and via MPI) and/or via traditional HDF5 files without changing their I/O
  calls.[^19][^4][^8]
- **Flow control for disparate data rates.** Wilkins includes mechanisms to
  handle tasks with very different data production/consumption rates, providing
  flow control so fast producers do not overwhelm slower consumers and vice
  versa.[^4][^19]
- **Minimal code modification.** Because it aligns with the HDF5 API and data
  model, in‑situ coupling often requires no or minimal source changes for
  applications that already use HDF5, easing adoption in existing HPC
  codes.[^19][^8][^4]

The Wilkins paper demonstrates these properties using synthetic benchmarks and
real use cases in materials science and cosmology, highlighting scalability and
efficiency of its in‑situ task execution.[^4][^19]

---

### Ascent

Ascent is a “flyweight” in‑situ visualization and analysis library designed for
multi‑physics simulations on many‑core HPC architectures, including large
GPU‑accelerated systems like Sierra.[^28][^25][^21][^5] It focuses on minimizing
dependencies and memory footprint while still providing a broad set of
visualization and analysis operations suitable for in‑situ use.[^29][^21][^5]

Key capabilities:

- **In‑memory vis/analysis library.** Ascent couples visualization and analysis
  routines directly with simulation codes so data can be processed as it is
  generated, avoiding or greatly reducing filesystem I/O.[^21][^5][^28]
- **Many‑core and GPU support.** It uses VTK‑m for node‑level parallelism,
  enabling efficient execution on many‑core CPUs and GPUs, and has been
  demonstrated scaling in situ filtering and ray tracing across 16 384 GPUs on
  LLNL’s Sierra.[^25][^28][^21]
- **Flexible “Actions” interface.** Users specify analysis and visualization
  pipelines via an Actions API (C++, Fortran, Python, or YAML), built around
  five composable concepts: Scenes (render pictures), Pipelines (transform
  data), Extracts (capture data), Queries (ask questions), and Triggers (adapt
  actions based on data).[^26][^5][^21]
- **Conduit data model.** Ascent uses Conduit and its Mesh Blueprint schema as
  the in‑memory representation of simulation meshes, providing a clean,
  language‑agnostic way to describe hierarchical mesh data.[^30][^5][^25]
- **Ecosystem integration.** It can work with ParaView (e.g., ParaView‑based
  in‑situ visualization workflows), Jupyter, and Trame for interactive steering,
  enabling both batch and interactive in‑situ workflows.[^31][^32][^33][^30]

Ascent is therefore a direct answer to in‑situ visualization and analysis
requirements on modern heterogeneous supercomputers, complementing more general
workflow or coupling frameworks.[^5][^28][^25]

---

## How they differ conceptually

At a high level:

- **Ascent** is an in‑situ visualization and analysis _library_ tightly embedded
  in simulation codes.
- **Decaf** and **Wilkins** are primarily _workflow coupling / data transport
  layers_ for in‑situ workflows, focusing on how components exchange data at
  runtime.
- **PyCOMPSs** and **Pegasus** are more general _workflow/programming systems_
  that orchestrate tasks and jobs across distributed resources, not specialized
  visualization engines.

### Design focus and abstraction level

- **Ascent** gives you direct visualization and analysis primitives (filters,
  rendering, queries) and a declarative way to run them in situ, but it assumes
  something else (e.g., the batch system, a workflow engine, or the user)
  decides _when_ to run the simulation and how to integrate with larger
  workflows.[^26][^21][^5]
- **Decaf** focuses on representing and executing an in‑situ workflow as a
  dataflow graph between existing HPC components, handling MPI‑based
  communication and data redistribution among them.[^8][^1][^9]
- **Wilkins** similarly focuses on connecting existing HDF5‑based tasks and
  providing flow‑controlled in‑situ data movement, but uses the HDF5 data model
  and LowFive transport as its core abstraction.[^19][^8][^4]
- **PyCOMPSs** raises the abstraction to the level of task‑based parallel
  programming: you write (mostly) sequential Python code, annotate tasks, and
  let the runtime discover concurrency and schedule across a cluster or
  cloud.[^12][^2][^13]
- **Pegasus** goes higher still, treating workflows as large DAGs of jobs (often
  separate executables) that must be mapped, staged, and executed across
  heterogeneous infrastructures with strong emphasis on data management and
  provenance.[^3][^27][^17]

### Workflow structure and coupling style

- **Decaf** supports message‑driven execution with potential cyclic dependencies
  in the task graph, which is useful for computational steering and feedback
  loops in in‑situ workflows (e.g., analysis driving simulation parameter
  changes).[^1][^6][^9]
- **Wilkins** supports multi‑producer/multi‑consumer communication and
  redistribution of datasets between $n$ producer processes and $m$ consumers
  via LowFive, addressing common fan‑in/fan‑out patterns in in‑situ
  workflows.[^8][^4]
- **PyCOMPSs** builds a dynamic dependency graph of tasks based on runtime data
  dependencies, but it conceptually fits more in the “many‑task” / dataflow
  programming space rather than explicit in‑situ data transport; simulations and
  visualization codes would be wrapped as tasks or external binaries.[^2][^12]
- **Pegasus** insists on DAG workflows (no cycles) and focuses on offline or
  loosely coupled orchestration of large pipelines; any in‑situ elements are
  typically encapsulated within jobs rather than modeled as fine‑grain streaming
  edges in the Pegasus graph.[^27][^17][^3]
- **Ascent** lives “inside” a simulation process (or tightly coupled processes)
  and operates at the in‑memory mesh/field level, not as a system‑level workflow
  engine; it can, however, participate in broader workflows through its Extracts
  (e.g., writing data or invoking scripts) or by being driven via
  Jupyter/Trame.[^32][^21][^5][^26]

### Data model and transport

- **Ascent**: in‑memory mesh data via Conduit Mesh Blueprint; operations
  implemented with VTK‑m, plus optional extract mechanisms to files or
  streaming.[^29][^25][^5]
- **Decaf**: user‑defined data types transported via MPI; the workflow graph can
  include data transformation nodes for redistribution or
  reformatting.[^6][^9][^1]
- **Wilkins**: HDF5 data model via LowFive; communication can be purely in
  memory, purely file‑based, or hybrid, with deep or shallow copies selectable
  per dataset.[^4][^19][^8]
- **PyCOMPSs**: treats data mainly as task arguments and persistent objects;
  data location is abstracted by the runtime and underlying storage systems
  (e.g., Hecuba, dataClay, files).[^13][^2]
- **Pegasus**: treats data as files and datasets managed via catalogs; it plans
  data staging, replica selection, and cleanup across storage systems and
  compute sites.[^15][^17][^3]

### Ecosystem, maturity, and typical use

- **Ascent** is part of the ALPINE project and is being integrated into a number
  of DOE ECP applications and tutorials; it is specifically aimed at
  next‑generation GPU‑heavy supercomputers.[^28][^30][^25]
- **Decaf** has been used in research demonstrations coupling, for example,
  molecular dynamics with visualization via other workflow systems, and
  cosmology codes with analysis tools, showing heterogeneous coupling of
  components.[^9][^1]
- **Wilkins** is newer (2024), with initial evaluations on synthetic workloads
  and two domain science use cases, emphasizing ease of adoption for existing
  HDF5‑based codes.[^19][^4]
- **PyCOMPSs** has a longer history as part of the COMPSs ecosystem and has been
  applied to both HPC and Big Data infrastructures, including machine‑learning
  workflows.[^12][^2]
- **Pegasus** is mature and widely deployed across many scientific domains for
  large‑scale production workflows on HTC and HPC infrastructures, especially
  where complex data management and provenance are important.[^16][^17][^3]

---

## Side‑by‑side view

### Role of each tool in an HPC in‑situ context

| System   | Primary role in HPC stack                                                     | Typical granularity                                                      | In‑situ focus                                                                                                                | Data model / transport                                                                  | Where you program                                                                                           |
| :------- | :---------------------------------------------------------------------------- | :----------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| Decaf    | Dataflow library for in‑situ workflows and coupling[^1][^9]                   | Components (sim, analysis, viz processes) connected via dataflow[^1][^9] | Yes, explicit support for in‑situ workflows and steering[^1][^9]                                                             | MPI messages, user data types; internal dataflow operators for redistribution[^1][^6]   | Python (workflow spec), C++ (components, operators)[^1][^9]                                                 |
| PyCOMPSs | Task‑based programming model and runtime for parallel workflows[^13][^12][^2] | Fine‑ to medium‑grain tasks, possibly wrapping entire MPI jobs[^12][^2]  | Indirect; can orchestrate in‑situ components as tasks, but not a vis library itself[^12][^2]                                 | Task arguments, files, persistent objects over storage backends[^2][^13]                | Python, plus Java/C/C++ bindings for COMPSs[^13][^12][^2]                                                   |
| Pegasus  | Science workflow management system and DAG engine[^27][^17][^3]               | Jobs (executables) and large pipelines (10³–10⁶ tasks)[^17][^3]          | Indirect; orchestrates jobs that may include in‑situ codes, but focuses on global workflow \& data management[^16][^27][^17] | Files and datasets via catalogs, data staging and cleanup[^17][^3]                      | Workflow description via APIs (Python, Java, R, Jupyter) and configuration files[^27][^17]                  |
| Wilkins  | In‑situ workflow system with HDF5‑based data transport[^4][^19]               | Executables/tasks using HDF5, connected by LowFive[^4][^8]               | Yes, explicit in‑situ workflows with flow control and minimal code changes[^4][^19]                                          | HDF5 data model via LowFive; in‑memory and file‑based transport[^4][^19][^8]            | Workflow descriptions plus minor HDF5‑related configuration in applications[^4][^19]                        |
| Ascent   | Flyweight in‑situ visualization and analysis library[^21][^5][^25]            | Visualization/analysis operations inside simulation time steps[^21][^26] | Yes, directly embedded in the simulation for in‑memory vis/analysis[^21][^5]                                                 | Conduit Mesh Blueprint in memory; VTK‑m for algorithms; optional extracts[^5][^29][^25] | C, C++, Fortran, Python APIs; actions in code or YAML; optional Jupyter/Trame front ends[^5][^25][^32][^33] |

---

## How to think about using them together

In practical HPC work:

- You might use **Ascent** inside each simulation process to do in‑situ
  visualization and analysis, driven either by YAML actions or Jupyter/Trame for
  interactive steering.[^33][^32][^21][^5][^26]
- You could use **Decaf** or **Wilkins** as the coupling layer to connect that
  simulation (and Ascent) to other concurrent components such as additional
  analysis codes, downsampling filters, or I/O services, with Decaf giving you a
  custom MPI‑based dataflow and Wilkins giving you an HDF5/LowFive‑based
  transport.[^1][^9][^8][^4][^19]
- At a higher level, **PyCOMPSs** can orchestrate the execution of multiple
  simulations, analysis pipelines, and data management tasks in a task graph,
  wrapping simulations that contain Ascent or Wilkins/Decaf integration as
  tasks.[^2][^13][^12]
- Above that, **Pegasus** can be used to manage full experimental campaigns or
  large analysis pipelines involving many workflows, data products, and compute
  sites, where each job may internally rely on in‑situ workflows handled by
  Ascent, Decaf, Wilkins, or PyCOMPSs.[^17][^3][^16][^27]

If you share a bit about the kinds of simulations and resources you’re targeting
(e.g., GPU‑heavy codes, existing HDF5 I/O, need for steering vs. pure batch), I
can sketch concrete workflow patterns involving these tools (e.g., “Ascent +
Wilkins + Pegasus” vs. “Decaf + PyCOMPSs”).
<span style="display:none">[^34][^35][^36][^37][^38][^39][^40][^41][^42][^43][^44][^45]</span>

<div align="center">⁂</div>

[^1]: https://www.osti.gov/biblio/1372113

[^2]:
    https://www.semanticscholar.org/paper/PyCOMPSs:-Parallel-computational-workflows-in-Tejedor-Becerra/e988006284b8305c41b8f99f23e66be67a576f10

[^3]:
    https://impact.ornl.gov/en/publications/pegasus-a-workflow-management-system-for-science-automation/

[^4]: https://arxiv.org/abs/2404.03591

[^5]: https://ascent.readthedocs.io/en/latest/Overview.html

[^6]: https://www.osti.gov/servlets/purl/1372113

[^7]: https://dl.acm.org/doi/10.1145/3364228.3364234

[^8]: https://mrzv.org/publications/lowfive/ipdps/

[^9]: https://web.cels.anl.gov/~tpeterka/papers/2022/yildiz-isvfcs22-chapter.pdf

[^10]: https://dl.acm.org/doi/10.1145/3149869.3149870

[^11]: https://journals.sagepub.com/doi/abs/10.1177/1094342015594678

[^12]: https://hpcsociety.org/wp-content/uploads/2020/05/Badia_Houston_v0.3.pdf

[^13]:
    https://summerofhpc.prace-ri.eu/development-of-sample-application-in-pycompsscompss/

[^14]: https://www.sciencedirect.com/science/article/pii/S0167739X14002015

[^15]: https://www.osti.gov/biblio/1245675

[^16]:
    https://newfrontiers.illinois.edu/news-and-events/pegasus-workflow-management-system/

[^17]: https://github.com/pegasus-isi/pegasus

[^18]:
    https://www.frontiersin.org/journals/high-performance-computing/articles/10.3389/fhpcp.2024.1472719/full

[^19]: https://www.bnicolae.net/publications

[^20]:
    https://www.informatik.rwth-aachen.de/cms/informatik/forschung/publikationen/bibliographie-komplett-/~lolj/details/?file=783269\&lidx=1

[^21]: https://www.olcf.ornl.gov/wp-content/uploads/Ascent_Tutorial_Sep2023.pdf

[^22]:
    https://www.exascaleproject.org/wp-content/uploads/2020/11/ascent-201217-slides.pdf

[^23]:
    https://extremecomputingtraining.anl.gov/wp-content/uploads/sites/96/2025/08/Ascent-Flyweight-In-Situ-Visualization-and-Analysis-for-HPC-Simulations_ATPESC-2025.pdf

[^24]: https://www.ascent-dav.org/tutorial/2025_07_22_ascent_tutorial.pdf

[^25]:
    https://extremecomputingtraining.anl.gov/wp-content/uploads/sites/96/2022/11/ATPESC-2022-Track-4-Talk-4-Harrison-Jupyter.pdf

[^26]: https://www.ascent-dav.org/tutorial/2023_08_22_ascent_intro.pdf

[^27]: https://en.wikipedia.org/wiki/Pegasus_(workflow_management)

[^28]:
    https://www.exascaleproject.org/demonstrating-in-situ-computer-simulation-visualization-and-analysis-on-the-sierra-supercomputer/

[^29]: https://ascent.readthedocs.io

[^30]:
    https://www.cscs.ch/publications/news/2023/course-in-situ-analysis-and-visualization-with-paraview-catalyst-and-ascent

[^31]: https://www.kitware.com/insitu-visualization-using-ascent-and-paraview/

[^32]: https://dl.acm.org/doi/10.1145/3364228.3364232

[^33]: https://ieeexplore.ieee.org/document/11181507/

[^34]:
    https://www.kitware.com/accelerating-hpc-innovation-with-interactive-visual-workflows/

[^35]: https://www.cs.uoregon.edu/Reports/AREA-201703-Kress.pdf

[^36]: https://www.sciencedirect.com/science/article/abs/pii/S1877750320305573

[^37]:
    https://wordpress.cels.anl.gov/atpesc/wp-content/uploads/sites/96/2021/08/ATPESC2021_Track-4-Talk-1b-InsleyRizzi.In-SituVisualizationAnalysispdf-1.pdf

[^38]: https://cdux.cs.uoregon.edu/pubs/MalonyParco.pdf

[^39]:
    https://sc18.supercomputing.org/proceedings/workshops/workshop_files/ws_isav116s3-file1.pdf

[^40]:
    https://www.ixpug.org/images/docs/SDVis_Workshop_2018/harrison_IXPUG_insitu_vis_Alpine_2018.pdf

[^41]:
    https://www.cottoncreekcapital.com/cotton-creek-capital-announces-the-formation-of-alpine-infrastructure-partners-llc

[^42]:
    https://www.rferl.org/a/azerbaijan_first_family_build_eurovision_arena/24575761.html

[^43]: https://warpx.readthedocs.io/en/19.10/visualization/ascent.html

[^44]: https://nerdnomads.com/alpine-route-japan

[^45]:
    https://assets.fis-ski.com/f/252177/x/bb48be94c5/coc-rules-2425_25-06-2024_final.pdf
