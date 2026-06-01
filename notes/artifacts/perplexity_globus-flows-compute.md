# Globus Flows and Globus Compute: Concepts, Comparisons, and Example Projects

## Executive overview

Globus Flows and Globus Compute are complementary services in the Globus
research automation platform: Flows provides managed, long‑running workflow
orchestration, while Compute is a distributed function‑as‑a‑service (FaaS) layer
for executing Python functions on heterogeneous endpoints. Together they fill
roles broadly similar to a combination of AWS Step Functions plus Lambda, or
Google Cloud Workflows plus Cloud Functions, but they are designed specifically
for research cyberinfrastructure spanning supercomputers, campus clusters, and
cloud resources. This report explains both services, maps them to analogs from
AWS, Google Cloud, and Cloudflare, and lists concrete open‑source projects that
use them with links to their source code.[^1][^2][^3][^4][^5][^6]

## Globus Flows: core concepts

Globus Flows is a managed automation and workflow service which lets users
define **flows**: declarative, reusable workflows that orchestrate a sequence of
**action providers** to automate research data and compute tasks. A flow is
defined as a series of actions with ordering, branching, and error‑handling
rules, and each run of a flow is tracked as a separate execution with status,
logs, and controls such as cancel or delete. Flows can call built‑in Globus
services (for example, high‑performance file transfer and sharing) as well as
user‑defined HTTP APIs, so workflows can span storage systems, instruments,
analysis services, and external web services.[^4][^7][^1]

An **action provider** is an HTTP‑accessible service implementing a standard
interface; when invoked it creates an **action** object representing one unit of
work with status, result, and access control enforced by Globus Auth. Flows
orchestrate these actions, tolerate success and failure states, and provide
long‑lived runs without fixed time limits, which makes them suitable for large
data movement and analysis pipelines common in scientific facilities. Notably, a
deployed flow itself implements the action provider interface, so flows can be
composed into higher‑level “sub‑flows,” promoting modular design of complex
automations.[^7][^8][^1]

## Globus Compute: core concepts

Globus Compute (formerly funcX) is a distributed function‑as‑a‑service (FaaS)
platform for remote execution of Python functions on heterogeneous computing
resources. The system consists of a cloud‑hosted control plane and user‑deployed
**endpoints**: lightweight agents installed on laptops, clusters, clouds, or
supercomputers that register with the service and serve as execution backends.
Users register Python functions with the service then invoke them by specifying
the function ID, input arguments, and the target endpoint ID, following a
familiar FaaS pattern but with explicit placement on chosen
resources.[^9][^10][^2][^5][^11]

Globus Compute emphasizes reliability and “fire‑and‑forget” execution: the cloud
service queues tasks, communicates securely with endpoints, and stores results
until the client retrieves them. Unlike commercial cloud FaaS systems that run
only within a single provider, Globus Compute endpoints can run in many
administrative domains, behind firewalls and NAT, and have been deployed
thousands of times on HPC systems worldwide for scientific workloads. A Python
SDK and command‑line tools make it straightforward to register, share, and
execute functions, and the open‑source implementation is available on GitHub and
PyPI.[^10][^5][^12][^13][^14][^8][^15][^9]

## How Flows and Compute work together

Globus Flows and Globus Compute are often used in combination: Flows
orchestrates higher‑level automation across storage and compute systems, while
Compute executes individual compute steps as remote functions. For example, a
flow might transfer data from an instrument to a staging area, invoke a Globus
Compute endpoint to preprocess or analyze the data, then move results to
archival storage and share them with collaborators. In this pattern, Globus
Flows remains a cloud‑hosted, durable coordinator (itself implemented on top of
AWS Step Functions), while Globus Compute bridges to on‑premises or specialized
compute resources.[^16][^2][^5][^17][^8][^7]

Some of the official example flows explicitly use a **compute action** that
calls Globus Compute; these examples demonstrate steps such as creating a tar
archive on a compute endpoint and then transferring or sharing the resulting
file via Globus Transfer. Tutorials for research software engineers emphasize
this pairing, teaching how to wire data‑management flows with Globus Flows and
run Python code on remote HPC systems with Globus Compute.[^17][^8][^16]

## Mapping to AWS, Google, and Cloudflare services

### High‑level analogies

At a high level, Globus Flows plays a role similar to AWS Step Functions, Google
Cloud Workflows, or Cloudflare Workflows, while Globus Compute is akin to AWS
Lambda, Azure Functions, or Google Cloud Functions/Cloud Run for functions. The
key difference is that Globus targets research cyberinfrastructure and federated
HPC environments rather than a single public cloud, and it integrates deeply
with Globus data transfer, sharing, and identity
services.[^2][^3][^5][^18][^19][^20][^4]

The table below summarizes the closest managed analogs and some distinguishing
characteristics.

| Capability                          | Globus service | Rough commercial analogs                                         | Key distinguishing traits                                                                                                                                                                                |
| ----------------------------------- | -------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Workflow orchestration / automation | Globus Flows   | AWS Step Functions, Google Cloud Workflows, Cloudflare Workflows | Designed for research data management; integrates with Globus Transfer and Auth; flows can run arbitrarily long; implemented on AWS Step Functions under the hood.[^1][^4][^7][^8][^18][^21][^6]         |
| Function execution (FaaS)           | Globus Compute | AWS Lambda, Azure Functions, Google Cloud Functions / Cloud Run  | Executes Python functions on user‑managed endpoints (laptops, clusters, supercomputers); supports federated HPC environments; emphasizes high throughput and scientific workloads.[^9][^3][^5][^12][^14] |

### Globus Flows vs AWS Step Functions

Globus Flows provides secure, managed automation of complex workflows, with
flows defined as ordered series of actions that can handle simple chores such as
file replication or complex conditional analysis and distribution tasks. AWS
Step Functions is likewise a serverless orchestrator for multi‑step workflows
that can integrate many AWS services and custom Lambda functions, with built‑in
error handling and state management. However, Globus Flows is tightly coupled to
Globus Auth and Globus Transfer, with flows commonly used to move and share
scientific data across institutional boundaries and storage systems, whereas
Step Functions is constrained to AWS services and AWS‑accessible
endpoints.[^22][^23][^24][^2][^4][^7]

Implementation‑wise, Globus Flows itself is built on AWS Step Functions and
exposes a domain‑specific API and tooling, including a Python SDK, CLI, and a
browser‑based “Flows IDE” for defining and validating flow specifications. From
a user’s perspective, Flows hides the Step Functions details and provides
research‑oriented action providers and access‑control policies suitable for
scientific collaborations.[^8][^1][^4][^7]

### Globus Compute vs AWS Lambda and other FaaS

Globus Compute’s model closely resembles mainstream FaaS offerings: users
register functions once and then invoke them with arguments, with the service
handling scaling, scheduling, and result storage. AWS Lambda, Azure Functions,
and Google Cloud Functions/Cloud Run follow the same basic idea, but they
execute functions only within their respective cloud regions and impose limits
on runtime, memory, and package size that are tuned for web and event‑driven
workloads rather than HPC. Globus Compute instead routes calls to user‑deployed
endpoints, which can be configured to launch MPI jobs or other HPC applications
via tools such as Parsl, Balsam, or local schedulers once the Python wrapper
function starts.[^3][^5][^12][^14][^25][^9][^8]

Scientific reviews describe Globus Compute as a **serverless framework that
supports remote execution across federated endpoints such as cloud machines, HPC
clusters, edge nodes, and workstations**, emphasizing that it uses cloud storage
(Redis and S3) for task queues and results, and enforces payload size limits to
manage costs. This makes it closer to an HPC‑oriented FaaS fabric than a general
web application engine, and many research frameworks (for example, libEnsemble,
FLoX, and Flight) integrate with it for orchestrating scientific
tasks.[^12][^26][^14][^25][^27]

### Globus Flows vs Google Cloud Workflows and Cloudflare Workflows

Google Cloud Workflows is a fully managed orchestration platform that executes
workflows composed of steps defined in YAML or JSON and can call any HTTP‑based
API, including Cloud Functions, Cloud Run, BigQuery, and external services.
Cloudflare Workflows is a durable execution engine built on Cloudflare Workers
that lets developers build long‑running, multi‑step applications with persisted
state, automatic retries, and the ability to sleep or wait for external events
for extended periods. Globus Flows plays a similar orchestration role but is
oriented around data‑centric research workflows, integrating deeply with Globus
identity and data services and supporting long‑running flows without fixed
timeouts.[^28][^18][^21][^19][^20][^6][^1][^4][^7]

While Cloudflare Workflows and Google Cloud Workflows primarily orchestrate
cloud‑native HTTP services in their respective ecosystems, Globus Flows commonly
orchestrates data movement between HPC storage, campus storage, and cloud
buckets (for example, Amazon S3) and can include manual approval steps or
human‑in‑the‑loop interactions tailored to scientific facilities. In practice, a
research institution might use Globus Flows to automate data ingestion from an
instrument, controlled transfers to analysis clusters, and eventual archiving,
whereas a SaaS company might use Cloudflare or Google workflows for user
lifecycle emails or microservice orchestration.[^23][^2][^7][^8]

## Example projects using Globus Flows

### globus/globus-flows-trigger-examples

The **globus-flows-trigger-examples** repository provides sample flows and
trigger scripts that show how to deploy and invoke Globus Flows in response to
filesystem events and other conditions. It includes flows that perform actions
such as: creating a tar archive on a Globus Compute endpoint, transferring the
archive to another collection, and sharing it with collaborators; pure
transfer‑and‑share flows; and examples of using the Python `watchdog` library to
trigger flows when files appear in a directory. The repository demonstrates
end‑to‑end patterns for defining a flow (JSON definition and input schema),
deploying it with the Globus CLI, and wiring triggers.[^29][^30][^16][^8]

- GitHub: https://github.com/globus/globus-flows-trigger-examples[^16]

### stanford-rc/globus-example-flow

The **globus-example-flow** project from Stanford Research Computing shows an
automated pipeline where the source data store, compute system, and results
store are all in different locations, orchestrated via Globus. The example
illustrates how Globus can coordinate data movement and computation across
heterogeneous environments, such as transferring data from one cluster to
another, launching remote computation, and placing results in a user‑accessible
location. It serves as a concrete prototype for research groups wanting to adopt
Globus flows for cross‑site workflows.[^31][^32][^33]

- GitHub: https://github.com/stanford-rc/globus-example-flow[^31]

### Facility examples and slides

Documentation and presentations from facilities such as the Argonne Leadership
Computing Facility (ALCF) include example flow definitions that combine Globus
Compute tasks with data transfers. One ALCF webinar on remote workflows shows a
“transfer‑compute” flow in which users register Python functions with Globus
Compute, start endpoints on systems like Polaris, and then create a flow that
first moves data, then runs compute tasks via Globus Compute actions, and
finally performs follow‑up transfers. These materials provide realistic
templates for production‑scale flows, though the flow JSON itself is embedded in
slides rather than a standalone GitHub repository.[^8]

- ALCF Remote Workflows slides (contains example flow link): Remote Workflows at
  ALCF PDF[^8]

## Example projects using Globus Compute

### globus/globus-compute (core project)

The main Globus Compute implementation is itself open‑source and hosted under
the `globus` GitHub organization. This repository contains the core
cloud‑service client, endpoint code, and examples of registering and invoking
functions, as well as integration tests and configuration examples for clusters
and supercomputers. Accompanying packages such as `globus-compute-common` and
`globus-compute-endpoint` factor out shared utilities and endpoint management
logic.[^34][^13][^9][^10]

- GitHub: https://github.com/globus/globus-compute[^13]

### globus-labs/globus-compute-golf-demo

The **globus-compute-golf-demo** repository is a demonstration of executing
simulations at scale using Globus Compute. It models a synthetic scientific
application by simulating golf balls dropping onto a procedurally generated golf
green using PyBullet, and uses Globus Compute to run many such simulations
concurrently on a configured endpoint. The repository provides setup
instructions, including creating a virtual environment, installing dependencies,
configuring a Globus Compute endpoint (local or remote), and running the demo to
launch large ensembles of simulation tasks.[^35]

- GitHub: https://github.com/globus-labs/globus-compute-golf-demo[^35]

### Federated learning frameworks: FLoX and Flight

The **FLoX-prototype** project (Federated Learning on funcX) is a Python library
that uses Globus Compute (under its former name funcX) to run federated learning
experiments in a serverless manner. FLoX lets users describe a federated
learning network (for example, aggregators and workers associated with different
Globus Compute endpoints) and then launch training jobs that execute on
endpoints while the framework orchestrates parameter aggregation. This design
allows FL experiments to span devices and HPC nodes without exposing data,
aligning with privacy‑preserving learning patterns.[^36][^37]

- GitHub: https://github.com/globus-labs/FLoX-prototype[^36]

**Flight**, a newer federated learning framework, builds directly on Globus
Compute as a FaaS substrate for hierarchical and asynchronous federated
learning. Flight’s `GlobusComputeLauncher` uses the Globus Compute Python SDK
and executor interface to submit aggregator and worker tasks to remote
endpoints, leveraging the same client–endpoint model. This framework is
open‑source and intended for real‑device deployment across the computing
continuum, from edge devices to HPC resources.[^26][^38][^39]

- GitHub: https://github.com/globus-labs/flight[^39]

### Ensemble and workflow frameworks: libEnsemble and EMEWS

The **libEnsemble** toolkit supports dynamic ensembles of simulations and can
offload simulator or generator functions to Globus Compute endpoints for remote
execution, enabling ensembles to span machines and heterogeneous resources. The
documentation describes a `globus_compute_endpoint` configuration option that
lets libEnsemble workers launch user functions on remote systems via Globus
Compute, while still using local executors to submit MPI applications on those
systems. This pattern helps isolate heavy simulation work from the main
coordinating process and exploits Globus Compute’s cross‑site
execution.[^25][^40]

- Docs (includes example code): libEnsemble platforms documentation[^25]

The **EMEWS** (Extreme‑scale Model Exploration with Swift) framework also
integrates with Globus Compute through a decoupled architecture called EMEWS DB,
using Globus Compute to coordinate tasks across federated HPC resources.
Literature describing these integrations emphasizes that Globus Compute provides
secure access to heterogeneous resources and that EMEWS creates local task
queues inside each HPC facility’s security boundary, backed by Globus Compute
for remote function execution.[^41][^12]

- Example project (ParSocial OSPREY example, uses EMEWS DB / Globus Compute
  concepts): https://github.com/RESUME-Epi/2023_ParSocial_OSPREY_example[^41]

### Other research systems built on Globus Compute

Several additional research projects and frameworks use Globus Compute as a
plug‑in execution layer:

- **TaPS (Task Performance Suite)**: A benchmarking framework that evaluates
  task execution frameworks and data management systems, with plugins for Dask
  Distributed, Globus Compute, Parsl, Ray, and ProxyStore. Its GitHub repository
  includes applications spanning domains such as linear algebra, drug discovery,
  and molecular design.[^42]
    - GitHub: https://github.com/proxystore/taps[^42]
- **Green‑ACCESS / core-hours-artifact**: A system for incentivizing
  energy‑aware computing that uses Globus Compute as the FaaS platform to
  execute Python functions on HPC systems, with an open‑source artifact
  repository. The framework registers machines by deploying Globus Compute
  endpoints that monitor energy and performance metrics, and it forwards user
  jobs through Globus Compute while pricing them based on environmental
  impact.[^27]
- **ProxyStore‑based applications**: ProxyStore is a data management library
  that can leverage Globus Transfer and Globus Compute to decouple control and
  data paths in distributed applications, including federated learning
  frameworks like Flight.[^14][^43][^44]

## Putting Globus Flows and Compute in context

From a cloud‑architecture perspective, Globus Flows and Globus Compute can be
thought of as **research‑centric analogs** of commercial orchestration and
serverless compute, optimized for cross‑institutional data and compute
integration rather than single‑cloud microservices. Where AWS Step Functions,
Google Cloud Workflows, and Cloudflare Workflows primarily orchestrate
cloud‑native APIs, Globus Flows is typically used to automate research data
lifecycles: instrument data capture, replication across storage tiers,
invocation of HPC analysis, and compliant sharing of results. Where Lambda and
similar services run in a provider’s data center, Globus Compute allows users to
run Python code on the specific HPC, campus, or edge systems where data or
specialized hardware resides, while still exposing a serverless‑like
interface.[^5][^6][^9][^23][^2][^3][^7][^14][^8]

For teams already comfortable with AWS or Google Cloud, the mental model carries
over: think of **Globus Flows ≈ Step Functions / Workflows** and **Globus
Compute ≈ Lambda / Cloud Functions**, but with execution targets that are your
own clusters and supercomputers and with identity and sharing semantics tuned
for research collaborations. The open‑source projects listed here provide
concrete starting points and reference implementations for building real systems
on top of these services.

---

## References

1. [Overview - Globus Docs](https://docs.globus.org/api/flows/overview/) - The
   Globus automation platform provides tools and services which can be used to
   create reliable, eas...

2. [What We Do - Globus](https://www.globus.org/what-we-do) - Compute from
   anywhere: The Globus Compute platform enables you to execute functions on
   diverse remot...

3. [A Systematic Literature Review on Serverless for HPC, AI, and Big ...](https://arxiv.org/html/2601.09334v1) -
   As previously stated, serverless computing was first popularized by Amazon in
   2014 with AWS Lambda, ...

4. [Globus Flows](https://docs.globus.org/api/flows/) - Globus Flows provides
   secure, managed automation of complex workflows at scale. These automations,
   c...

5. [Computing with Globus](https://www.globus.org/compute) - The Globus compute
   platform enables you to execute functions on diverse remote systems, from
   laptops...

6. [Workflows - Google Cloud](https://cloud.google.com/workflows) - Orchestrate
   work of any Google Cloud product without worrying about authentication. Use a
   proper ser...

7. [Globus Flows service](https://www.globus.org/globus-flows-service) - Globus
   Flows is a foundational service for defining and executing secure, reliable
   automated data fl...

8. [[PDF] Remote Workflows at ALCF](https://www.alcf.anl.gov/sites/default/files/2024-12/RemoteWorkflowsWebinarDec2024.pdf) -
   Example flows:
   https://github.com/globus/globus-flows-trigger-examples/tree/main. 17.
   Page 20. Flow ...

9. [Globus Compute 4.11.0 documentation - Read the Docs](https://globus-compute.readthedocs.io/en/stable/) -
   Globus Compute is a distributed Function as a Service (FaaS) platform that
   enables flexible, scalabl...

10. [globus-compute-endpoint - PyPI](https://pypi.org/project/globus-compute-endpoint/) -
    Globus Compute is a distributed Function as a Service (FaaS) platform that
    enables flexible, scalabl...

11. [The Globus Compute Client - Globus Compute 2.23.0 documentation](https://globus-compute.readthedocs.io/en/2.23.0/reference/client.html) -
    Register a function code with the Globus Compute service. Parameters:
    function (Python Function) – T...

12. [DISTRIBUTED MODEL EXPLORATION WITH EMEWS - PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11939112/) -
    The Globus Compute task queue uses Globus Compute (Chard et al. 2020),
    formerly known as funcX, to e...

13. [Globus Compute: High Performance Function Serving for Science](https://github.com/globus/globus-compute) -
    Globus Compute (formerly funcX) is a high-performance function-as-a-service
    (FaaS) platform that ena...

14. [[PDF] Accelerating Communications in Federated Applications with ...](https://gregpauloski.com/publications/pauloski2023proxystore-preprint.pdf) -
    Our application is implemented using FLoX [36], a FL frame- work which uses
    Globus Compute to orches...

15. [[PDF] Globus Compute Multi-User Endpoints - Parsl](https://parsl-project.org/parslfest/2024/mello-reid_pf24-presentation.pdf) -
    Globus Compute Web App. 16. Page 17. Any questions? Docs:
    https://globus-compute.readthedocs.io/en/l...

16. [Examples of Triggers for Globus Flows - GitHub](https://github.com/globus/globus-flows-trigger-examples) -
    We provide examples of triggering flows with the following actions: Tar and
    Transfer: A flow that cr...

17. [Tutorials - US-RSE](https://us-rse.org/usrse24/program/tutorials/) - This
    tutorial equips Research Software Engineers (RSEs) to automate research data
    processes using Gl...

18. [Workflows overview - Google Cloud Documentation](https://docs.cloud.google.com/workflows/docs/overview) -
    Workflows is a fully managed orchestration platform that executes services
    in an order that you defi...

19. [Cloudflare Workflows - Durable Execution Engine](https://www.cloudflare.com/products/workflows/) -
    Workflows is an execution engine built on Cloudflare Workers — to build
    applications that can automa...

20. [Overview · Cloudflare Workflows docs](https://developers.cloudflare.com/workflows/) -
    Workflows give you: Durable multi-step execution without timeouts; The
    ability to pause for external...

21. [Cloudflare Workflows is now GA: production-ready durable execution](https://blog.cloudflare.com/workflows-ga-production-ready-durable-execution/) -
    Workflows is a durable execution engine built on Cloudflare Workers that
    allows you to build resilie...

22. [Airflow versus AWS Step Functions for workflow - Stack Overflow](https://stackoverflow.com/questions/64016869/airflow-versus-aws-step-functions-for-workflow) -
    Overall, I see more advantages of using AWS Step Functions. You will have to
    consider maintenance co...

23. [Globus and Amazon S3](https://globus.stanford.edu/cloud/s3.html) - For
    users who want to upload data into a different storage class (that is not S3
    Standard), we sugge...

24. [Why use AWS Step Functions? - Reddit](https://www.reddit.com/r/aws/comments/pmc1o2/why_use_aws_step_functions/) -
    Step Functions reduces the amount of function code you need to
    write/maintain. It also offers native...

25. [Running on HPC Systems - libEnsemble - Read the Docs](https://libensemble.readthedocs.io/en/main/platforms/platforms_index.html) -
    Therefore the second option is to use Globus Compute to isolate this work
    from the workers. Globus C...

26. [A FaaS-Based Framework for Complex and Hierarchical Federated ...](https://arxiv.org/html/2409.16495v1) -
    Flight's GlobusComputeLauncher uses Globus Compute's Python SDK and executor
    interface to submit tas...

27. [[PDF] Core Hours and Carbon Credits: Incentivizing Sustainability in HPC](https://www.research-collection.ethz.ch/bitstreams/95a59139-ec62-47cf-89c4-e7c5df3062a8/download) -
    2 Green-ACCESS uses Globus Compute as the FaaS platform to run ...
    github.com/AK2000/core-hours-arti...

28. [Automate and Orchestrate: Harnessing the Power of Google Cloud ...](https://www.workloadautomation-community.com/blogs/automate-and-orchestrate-harnessing-the-power-of-google-cloud-workflows) -
    Google Cloud Workflows is a fully managed service that allows users to
    orchestrate and automate work...

29. [globus-flows-trigger-examples/deploy_flow.py at main - GitHub](https://github.com/globus/globus-flows-trigger-examples/blob/main/deploy_flow.py) -
    Sample code for triggering Globus Flows using the Python watchdog library. -
    globus-flows-trigger-ex...

30. [globus-flows-trigger-examples/user.py at main - GitHub](https://github.com/globus/globus-flows-trigger-examples/blob/main/user.py) -
    Sample code for triggering Globus Flows using the Python watchdog library. -
    globus-flows-trigger-ex...

31. [stanford-rc/globus-example-flow: An example pipeline ... - GitHub](https://github.com/stanford-rc/globus-example-flow) -
    An example pipeline showing how to use Globus when your source data store,
    compute, and results stor...

32. [states-language · GitHub Topics](https://github.com/topics/states-language) -
    stanford-rc / globus-example-flow · Star 6 · Code · Issues · Pull requests.
    An example pipeline show...

33. [schema.json - stanford-rc/globus-example-flow · GitHub](https://github.com/stanford-rc/globus-example-flow/blob/flow/schema.json) -
    ... source data store, compute, and results store are all in different
    locations - globus-example-fl...

34. [globus-compute-common - GitHub](https://github.com/globus/globus-compute-common) -
    This package contains common utilities for use across various Globus Compute
    projects. For example, ...

35. [globus-labs/globus-compute-golf-demo: Executing ... - GitHub](https://github.com/globus-labs/globus-compute-golf-demo) -
    Clone the repository and navigate to the project directory: git clone
    https://github.com/globus-labs...

36. [globus-labs/FLoX-prototype - Federated Learning on funcX - GitHub](https://github.com/globus-labs/FLoX-prototype) -
    FLoX (Federated Learning on funcX) is a Python library for serverless
    Federated Learning experiments...

37. [Hierarchical Federated Learning on Globus Compute using Flox](https://www.youtube.com/watch?v=uKE_uvPNcus) -
    Hierarchical Federated Learning on Globus Compute using Flox. 86 views · 2
    years ago ...more. Parsl ...

38. [[PDF] A FaaS-Based Framework for Complex and Hierarchical Federated ...](https://arxiv.org/pdf/2409.16495.pdf) -
    Flight's GlobusComputeLauncher uses Globus Compute's. Python SDK ... URL:
    https://github.com/Lightni...

39. [globus-labs/flight: Flight (Federated Learning In General ... - GitHub](https://github.com/globus-labs/flight) -
    Flight is a modular, easy-to-use federated learning framework built on top
    of Globus Compute, a fede...

40. [libEnsemble - NERSC Documentation](https://docs.nersc.gov/jobs/workflow/libensemble/) -
    libEnsemble is a complete Python toolkit for steering dynamic ensembles of
    calculations. Workflows a...

41. [2023_ParSocial_OSPREY_example/README.md at main ... - GitHub](https://github.com/RESUME-Epi/2023_ParSocial_OSPREY_example/blob/main/README.md) -
    The Extreme-scale Model Exploration with Swift (EMEWS) framework enables the
    direct integration of m...

42. [proxystore/taps - Task Performance Suite - GitHub](https://github.com/proxystore/taps) -
    yml · Add physics app based on Globus Compute golf demo. 2 years ago.
    pyproject.toml · pyproject.tom...

43. [ProxyStore - Globus Labs](https://labs.globus.org/projects/proxystore.html) -
    ProxyStore provides a unique interface to object stores through transparent
    object proxies that is d...

44. [proxystore - PyPI](https://pypi.org/project/proxystore/) - ProxyStore can
    leverage many popular mediated data transfer and storage systems: DAOS,
    Globus Transf...
