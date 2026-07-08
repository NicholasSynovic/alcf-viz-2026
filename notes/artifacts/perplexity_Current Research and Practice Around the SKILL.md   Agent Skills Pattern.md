# Current Research and Practice Around the SKILL.md / Agent Skills Pattern

## Executive overview

The SKILL.md "agent skills" pattern is now a de‑facto open standard for
packaging reusable, task‑specific capabilities for AI coding and general-purpose
agents. It centers on directories that contain a SKILL.md file with YAML
frontmatter metadata plus markdown instructions, optionally accompanied by
scripts and reference documents that are loaded via progressive disclosure only
when a skill is activated. Recent work spans (1) architectural descriptions and
standardization, (2) ecosystem tooling and registries, (3) security and
supply‑chain risk analysis, and (4) operational guidance for authoring,
maintaining, and routing skills in production
systems.[^1][^2][^3][^4][^5][^6][^7][^8][^9][^10]

## Origins and specification of SKILL.md

### Initial design and open standardization

Agent Skills originated at Anthropic as a format for Claude Code, where a skill
is a folder containing a SKILL.md file that defines metadata and instructions,
with optional scripts, references, and assets. The format has since been
formalized as an open standard under the "Agent Skills" banner and is supported
by multiple vendors and tools, including Anthropic, OpenAI Codex/Codex CLI,
Google Gemini CLI, GitHub Copilot, Cursor, and other coding
agents.[^2][^11][^4][^12][^10][^1]

The core specification defines that each skill directory must contain a SKILL.md
file whose YAML frontmatter minimally includes a `name` and `description`, while
the markdown body provides the procedural instructions the agent should follow
when the skill is invoked. Many implementations also recognize conventional
subdirectories such as `scripts/` for executable helpers, `references/` for
long-form documentation, and `assets/` for templates or other resources
referenced by the instructions.[^3][^11][^4][^12][^10][^1][^2]

### Progressive disclosure and context management

A key design feature repeatedly emphasized in both documentation and research is
progressive disclosure: only minimal metadata is loaded into the system prompt
at startup, with full instructions and resources pulled in lazily when a skill
matches the current task. In practice, agents pre-load the `name` and
`description` fields of all available skills (roughly 100 tokens per skill) so
they can decide which ones might apply, while the full SKILL.md body (up to a
few thousand tokens) and any referenced files are loaded only when the agent
activates that skill.[^13][^4][^12][^9][^1][^2][^3]

This approach allows agents to maintain large skill libraries with minimal
baseline context overhead, in contrast to monolithic configuration files like
AGENTS.md/CLAUDE.md that remain in context for every turn. Multiple sources
point out that this design improves scalability while preserving the ability to
encode rich, workflow-level guidance when needed.[^4][^8][^9][^1][^2][^3][^13]

## Relationship to AGENTS.md and other instruction formats

### Role separation: identity vs capability

Ecosystem guidance stresses that AGENTS.md (or CLAUDE.md) and SKILL.md serve
complementary roles: the former captures persistent project- or agent-level
identity and global behavior, while the latter defines discrete, activatable
capabilities. Commentary aimed at practitioners highlights that many teams
initially "dump everything into one file" and are encouraged instead to move
task-specific workflows into skills while keeping AGENTS.md short and
general.[^14][^15][^8][^2]

Industry analyses argue that AGENTS.md and SKILL.md together form a layered
instruction architecture: AGENTS.md provides always-on context such as project
norms and coding style, whereas skills encapsulate workflows, domain procedures,
and tool usage that should only be loaded when relevant. Empirical work cited by
practitioners suggests that long always-on context files can degrade agent
performance, reinforcing the pattern of keeping global instructions under
roughly 60–100 lines and pushing depth into skills.[^8][^1][^2][^13][^4]

### Router–skill–reference triad

Documentation from tools such as Atmos and OpenAI Codex describes a three-tier
structure: a router file (often AGENTS.md or similar) that maps tasks to skills,
the SKILL.md file that holds task-specific instructions, and deeper reference
files in a `references/` directory. This triad separates high-level routing
logic, operational workflows, and detailed specifications or schemas, allowing
agents to selectively read only the information they need.[^12][^2][^13][^8]

## Ecosystem tooling, registries, and preprints

### Skill registries and package managers

A growing ecosystem of skill registries and package managers has emerged to
support discovery, installation, and governance of SKILL.md-based skills.
Skilldex is a research prototype described in a 2026 arXiv preprint that acts as
a package manager and registry focused on format conformance and skillset-level
bundling. It introduces compiler-style validation of SKILL.md files against the
Anthropic specification, scoring aspects such as description specificity and
frontmatter validity, and proposes "skillsets"—bundles of related skills sharing
assets to enforce cross-skill behavioral coherence.[^16][^17][^18][^3]

Community-facing registries such as SkillsLLM catalog skills with metadata like
supported agents, languages, repository links, and security scan results,
positioning themselves as hubs for sharing SKILL.md-based capabilities across
agents. Forum posts and project announcements describe additional open
registries with versioning and integrated security checks, where each published
skill version is immutable and subjected to automatic scans for prompt injection
and other vulnerabilities before listing.[^17][^19][^18][^16]

### Academic surveys of agent skills

A substantial survey paper, "Agent Skills for Large Language Models:
Architecture, Acquisition, and Governance," systematically analyzes the SKILL.md
specification, its progressive disclosure architecture, and its place in the
broader agent stack (including MCP and computer-use agents). This work frames
skills as structured natural-language instruction bundles, discusses how agents
discover and load them, and reviews research on acquiring skills via
reinforcement learning, autonomous discovery, and compositional synthesis.[^9]

The survey also synthesizes security findings from other academic work,
including large-scale scans of community skills and concrete exploitation case
studies, and argues for a more explicit governance architecture that accounts
for the attack surface created by progressive disclosure and trust in SKILL.md
files.[^6][^7][^9]

### Other ecosystem and practice-focused writings

Blogs, vendor docs, and practitioner write-ups describe how different tools
implement and extend skills—GitHub Copilot via Agent Skills in VS Code, OpenAI
Codex plugins built on skills, Google codelabs using agents.md plus skills
directories, and product-specific skill authoring guidance (for example,
GitBook’s instructions on writing a skill.md that translates product features
into agent-readable workflows). These sources collectively document an emerging
consensus on folder layout, frontmatter fields, and best practices for authoring
SKILL.md files that portable agents can consume.[^11][^20][^10][^2][^13][^12]

## Usage patterns and authoring guidance

### Conceptual model: skills as workflows

Practitioner guidance consistently emphasizes that skills should encode
workflows—"how to do something"—rather than static reference knowledge. Articles
aimed at developers distinguish skills from ordinary documentation by describing
SKILL.md as operational guidance for agents, containing structured instructions,
task sequencing, decision rules, and guardrails instead of marketing copy or
user-facing docs.[^15][^20][^1][^8]

Well-written SKILL.md files are expected to:

- Define clear activation criteria and boundaries, including when not to use the
  skill.
- Provide a structural overview of relevant entities and configuration.
- Document task-oriented workflows step by step.
- Include simple if/then decision rules for branching behaviors.
- Specify constraints, unsupported operations, and common pitfalls.

These recommendations appear across multiple sources, including skill-writing
guides by GitBook, Agensi, and vendor docs, reflecting shared experience with
what LLM agents reliably follow.[^20][^10][^1][^8]

### Routing and description design

Several sources highlight the importance of the `description` field in YAML
frontmatter as the primary routing signal the model uses to decide whether to
activate a skill. Guidance suggests writing descriptions not as human-friendly
summaries but as routing predicates that specify what the skill does, when to
use it, and when not to use it, often including negative examples to avoid
accidental triggers.[^1][^2][^12][^8]

Empirical reports from industry experiments (for example, Vercel’s internal
evaluations and Dometrain/HumanLayer studies cited by consultants) indicate that
precise, narrowly scoped descriptions lead to more reliable triggering, while
vague or overly broad descriptions cause skills to be activated in inappropriate
contexts. As a result, best practices recommend iteratively testing skill
descriptions against representative prompts and adjusting them until the routing
behavior matches expectations.[^21][^8][^1]

### Examples of domain-specific skill libraries

Public skill libraries demonstrate how the pattern is used in specific
domains—academic writing, scientific workflows, production readiness checks, and
more. For example, "academic-paper-skills" packages planning and drafting
workflows into separate skills (strategist and composer) with quality
checkpoints, providing agents with a systematic process for turning research
ideas into submission-ready manuscripts. Scientific-agent skill repositories and
production-readiness skill sets combine SKILL.md instructions with scripts that
interface with external systems, giving agents reproducible pipelines for
technical work.[^22][^18][^16][^15]

## Maintenance, evolution, and governance

### Skills as code: version control and review

Industry guidance increasingly urges teams to treat skills like code rather than
passive documentation, placing SKILL.md files and associated resources under
version control and subjecting them to code review and change-management
processes. Articles on production-grade agent systems argue that changes to
architecture, APIs, deployment pipelines, or test frameworks should trigger
systematic review of all skills that reference those components to prevent drift
and failures in automated workflows.[^7][^3][^8]

The Skilldex preprint explicitly identifies the lack of formal spec versioning
as an open problem and proposes spec-aware validation tooling that tracks the
Anthropic SKILL.md creator guide over time and scores skills against the current
format. Community registry posts describe per-version publication with immutable
histories, so that upgrades create new versions rather than overwriting existing
ones, which enables rollback and provenance tracking.[^3][^17]

### Drift, evals, and robust operation

Practice-oriented analyses warn that agents fail when skills drift out of sync
with underlying systems, leading to brittle behavior and subtle errors.
Recommended mitigations include running evaluation suites against skills
themselves (not just against agents), using deterministic checks and
rubric-based scoring to validate that skills still implement the intended
workflows and adhere to updated constraints.[^8][^21]

Vendor and community content also describe automated harnesses and test harness
engineering as complementary to skills: while skills encode what the agent
should do, harnesses enforce deterministic phases, state management, and
validation, thus compensating for the non-determinism and brittleness of
skill-driven agents in complex pipelines. This reflects a broader trend of
combining SKILL.md-based guidance with programmatic control and monitoring to
achieve production reliability.[^23][^21][^8]

### Registry governance and organizational controls

Security-oriented blogs and whitepapers highlight governance issues in skill
ecosystems, including limited visibility into which skills are installed, lack
of mandatory security reviews in public registries, and insufficient version
pinning. Recommended organizational practices include building internal approved
catalogs of vetted skills, auditing installed skills across environments, and
implementing policies that treat community skills as untrusted by default unless
explicitly reviewed.[^19][^17][^7][^9]

These sources also emphasize the need for runtime observability—tracking which
skills are invoked, what resources they access, and how they interact with
sensitive data—to detect misuse or unexpected behavior arising from skill
updates or supply-chain compromise.[^5][^7][^9]

## Security, safety, and supply‑chain risks

### Prompt injection and instruction trust

A central theme in recent academic and industry work is that trust in SKILL.md
files creates a distinct prompt-injection attack surface. Because every line in
a skill file is intended as instructions to be followed, malicious authors can
embed harmful directives that the agent will treat as authoritative once the
skill is loaded. Case studies demonstrate realistic attacks where skills
exfiltrate files or passwords, bypass user approvals, or subvert system-level
guardrails by smuggling instructions through long skill files and referenced
scripts.[^24][^6][^7][^9]

Analyses show that this vulnerability is more acute than ordinary prompt
injection in user data or websites because skills are pre-trusted, often long,
and may be reused across many environments, making manual review difficult and
increasing blast radius. Researchers argue that naive approaches like
regex-based skill scanners are insufficient, since many dangerous patterns are
semantic and context-dependent, and that model-level defenses alone cannot fully
mitigate the risks.[^5][^6][^7][^9][^24]

### Large-scale empirical security studies

Recent preprints and industry research report large-scale scans of community
skill repositories, finding significant rates of vulnerabilities and confirmed
malicious skills. One study analyzed tens of thousands of skills with a
multi-stage framework (SkillScan), combining static analysis with LLM-based
semantic classification, and found that roughly a quarter of skills contained at
least one vulnerability across categories such as prompt injection, data
exfiltration, privilege escalation, and supply-chain attacks.[^7][^9][^5]

Follow-on work constructed a behaviorally verified ground-truth dataset of
malicious skills from community registries, identifying archetypes such as "Data
Thieves" that silently exfiltrate environment variables and credentials, and
"Agent Hijackers" that alter agent behavior via hidden instructions in SKILL.md.
These studies show that a small number of industrialized actors can mass-produce
malicious skills via templated brand impersonation, underscoring the need for
stronger registry governance and ecosystem-wide defenses.[^9][^7]

### Unicode and obfuscation-based attacks

Security blogs explore more advanced obfuscation techniques in skills, including
hidden Unicode tag instructions that models still interpret, enabling malicious
behavior that is hard for humans or simple scanners to detect. Proof-of-concept
exploits demonstrate that such hidden instructions can be embedded in skill
files or related resources and successfully executed by agents using popular
models, with mitigations inconsistent across platforms.[^24]

These findings highlight that SKILL.md files can carry not only explicit
natural-language instructions but also non-obvious encodings and steganographic
content, complicating security analysis and reinforcing calls for sandboxing and
strict permission controls when executing skill-associated scripts or shell
commands.[^25][^7][^24]

### Security guidance and mitigations

Multiple vendors and security-focused organizations have published practical
guidance for securing SKILL.md ecosystems, emphasizing both code-level and
operational controls. Recommended measures include:[^26][^25][^19][^7][^24]

- Restricting filesystem permissions on skills directories and files by default,
  and requiring signed skills with signature verification before use in
  high-assurance environments.
- Applying standard secure development practices (code review, SAST/DAST,
  fuzzing, vulnerability management) to any scripts bundled with skills.
- Executing skill scripts in isolated environments such as containers or
  sandboxes, with restricted egress networking.
- Limiting agent permissions to the minimum required and avoiding embedding
  credentials directly in skills; instead, using secure secret stores and
  automated secret-scanning tools to catch hardcoded secrets.
- Treating third-party or community skills as untrusted and using checklists
  that include repository provenance, SKILL.md behavior review, dependency
  scanning, network behavior inspection, license review, and sandboxed trial
  runs before granting access to real systems.

Vendor docs for Agent Skills and Claude API also explicitly encourage thorough
auditing of SKILL.md contents and bundled resources, and warn that installing
skills from untrusted sources poses significant risk without these
mitigations.[^25][^19][^26][^7]

## Evaluation, reliability, and limitations

### Impact on agent performance and failure modes

Empirical evaluations referenced by practitioners indicate that while skills can
significantly improve task completion rates and adherence to desired workflows,
there remain substantial gaps between current performance and the reliability
required for fully autonomous production use. Video analyses and blog posts
document that adding well-crafted skills improves benchmark pass rates but still
leaves overall success rates below what businesses typically need without human
oversight.[^23][^1][^8]

Common failure modes include incorrect skill selection due to ambiguous
descriptions, partial adherence to instructions when context windows are
crowded, and brittleness when underlying tools or APIs change without
corresponding skill updates. These limitations motivate the use of evaluation
suites, harness engineering, and layered guardrails to monitor and correct agent
behavior rather than relying solely on static SKILL.md
files.[^21][^1][^23][^8][^9]

### Testing and eval methodologies for skills

Practitioner content outlines emerging methodologies for testing and evaluating
skills directly. Suggested practices include defining explicit success criteria
for each skill, constructing controlled prompt sets that exercise intended
workflows, running repeated trials to capture variability, and scoring outputs
using deterministic or rubric-based checks, sometimes assisted by LLM judges.
When misbehavior is observed, teams iteratively refine both SKILL.md
instructions and frontmatter descriptions, and re-run evaluations to ensure
regressions are caught before deploying updated skills broadly.[^1][^8][^21]

These methods are often integrated into CI pipelines or dedicated evaluation
harnesses, aligning skills with standard software engineering practice and
enabling safer evolution as models or environments change.[^3][^8][^21]

## Open problems and research directions

### Specification versioning and interoperability

Current research identifies specification versioning as a gap: Anthropic’s skill
format has evolved without an explicitly versioned artifact, requiring tools
like Skilldex to track changes manually and score conformance against a moving
target. Formalizing spec versions, deprecation policies, and capability
annotations would help skills remain interoperable across tools and models as
the ecosystem matures.[^10][^9][^3]

Interoperability across agents remains an active area, as different platforms
layer additional metadata or behaviors on top of the common SKILL.md core (for
example, Codex’s plugin packaging or Copilot’s workspace vs user skills),
raising questions about how far the standard can stretch without
fragmentation.[^11][^12][^10][^9]

### Security models and trust frameworks

Security research argues that the implicit trust currently granted to SKILL.md
files is untenable, given empirical vulnerability rates and observed malicious
activity. Proposed directions include multi-layer trust frameworks that combine
spec-level validation, static and dynamic analysis, reputation systems, signed
skills with supply-chain attestations, and runtime policy engines that mediate
what skills are allowed to do based on environment and risk
tolerance.[^6][^19][^5][^25][^7][^9][^3]

There is also interest in model-level approaches that can distinguish benign
from malicious skill instructions and resist prompt injection even when skills
are treated as authoritative, though current work suggests this is challenging
and must be supplemented with external guardrails and
sandboxing.[^5][^6][^9][^24]

### Automated skill acquisition and maintenance

Surveyed research on skill acquisition explores reinforcement learning over
skill libraries, autonomous discovery of new skills from task distributions, and
compositional synthesis of higher-level skills from existing ones. This raises
questions about how to automatically generate SKILL.md files that are both
effective and secure, how to manage their lifecycle, and how to ensure that
autonomously generated skills comply with organizational policies and do not
introduce new vulnerabilities.[^9][^3][^5]

On the maintenance side, there is ongoing work on detecting skill drift,
automatically updating skills in response to upstream changes (for example, API
evolution), and integrating skills with monitoring systems that can trigger
retraining or rewrites when error patterns emerge.[^7][^8][^3][^9]

## Summary of key themes

Across the literature and practice, several themes recur:

- **Standardization and portability:** SKILL.md has become a widely adopted
  standard for portable agent skills across multiple vendors and
  tools.[^2][^4][^12][^10][^11]
- **Progressive disclosure:** Skills rely on progressive context loading to
  scale to large libraries while preserving rich instructions when
  needed.[^4][^12][^2][^1][^3][^9]
- **Workflows over documents:** Effective skills encode procedural workflows,
  decision rules, and guardrails rather than mere reference material, and use
  carefully designed descriptions as routing logic.[^15][^20][^8][^1]
- **Code-like governance:** Maintaining SKILL.md ecosystems requires treating
  skills like code—version-controlled, reviewed, evaluated, and monitored, not
  static docs.[^8][^21][^3][^7]
- **Security and supply chain risk:** High vulnerability rates and observed
  malicious skills make security a central concern, driving research into
  scanning, sandboxing, signatures, and governance
  frameworks.[^19][^6][^24][^5][^7][^9]
- **Reliability limits:** Skills materially improve agent performance but are
  insufficient alone for high-assurance autonomy, prompting integration with
  harnesses, evals, and external guardrails.[^23][^21][^8][^9]

Together, these threads define the current state of research and practice around
the SKILL.md coding agent pattern and highlight where further work is most
needed.

---

## References

1. [Implementing Claude Code Skills from Scratch - Designing with AI](https://newsletter.victordibia.com/p/implementing-claude-code-skills-from) -
   The Arc of Agent Action from Code to Tools and Back to Code - And Why
   Anthropic's SKILLS.md is Not N...

2. [AI Agent Skills | atmos](https://atmos.tools/ai/agent-skills) - Agent skills
   are structured knowledge files that teach AI coding assistants how to work
   with specifi...

3. [Skilldex: A Package Manager and Registry for Agent Skill ... - arXiv](https://arxiv.org/html/2604.16911v1) -
   LLM-powered agents are increasingly extended via skills: structured
   natural-language documents that ...

4. [Agent Skills Overview - Agent Skills](https://agentskills.io/home) - What
   are Agent Skills? Agent Skills are a lightweight, open format for extending
   AI agent capabiliti...

5. [Why Your “Skill Scanner” Is Just False Security (and Maybe Malware](https://snyk.io/blog/skill-scanner-false-security/) -
   Why Regex can't scan SKILL.md for malicious intent · Case study: We pitted
   community scanners agains...

6. [Agent Skills Enable a New Class of Realistic and Trivially Simple ...](https://aisagroup.substack.com/p/agent-skills-enable-a-new-class-of) -
   TLDR: Agent Skills is a feature that loads instructions from markdown files
   to give agents task-spec...

7. [Agent Skills: Real Power, Real Risk - Mondoo](https://mondoo.com/blog/agent-skills-real-power-real-risk) -
   No mandatory registry security review. Every major platform warns users to
   install skills only from ...

8. [Skills vs Documents: Your Agent Is Only as Good as Its ... - Forte Group](https://www.fortegrp.com/insights/skills-vs-documents-your-agent-is-only-as-good-as-its-last-skill-update) -
   AI agents fail when skills drift out of sync. Learn how SKILL.md and
   AGENTS.md maintenance impacts p...

9. [Agent Skills for Large Language Models: Architecture, Acquisition ...](https://arxiv.org/html/2602.12430v3) -
   A systematic analysis of the Agent Skills architecture, including progressive
   disclosure, the SKILL....

10. [SKILL.md: The Open Standard for AI Agent Skills - Agensi](https://www.agensi.io/learn/agent-skills-open-standard) -
    SKILL.md is the open standard adopted by Anthropic, OpenAI, Google,
    Microsoft, and Cursor. One skill...

11. [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills) -
    Select the location and enter a name for the skill. Complete the SKILL.md
    file by filling in the YAM...

12. [Agent Skills – Codex | OpenAI Developers](https://developers.openai.com/codex/skills) -
    Codex loads the full SKILL.md instructions only when it decides to use a
    skill. Codex includes an in...

13. [Build Autonomous Developer Pipelines using agents.md and skills ...](https://codelabs.developers.google.com/autonomous-ai-developer-pipelines-antigravity) -
    Skills and skills.md: A dedicated directory where you define robust
    technical abilities and artifact...

14. [AGENTS.md vs SKILL.md - stop mixing these up Most people dump ...](https://www.instagram.com/p/DXrnUC_CONR/) -
    AGENTS.md vs SKILL.md - stop mixing these up. Most people dump everything
    into one file! Hope this h...

15. [Agent Skills Explained for Developers! - LinkedIn](https://www.linkedin.com/pulse/agent-skills-explained-developers-pavan-belagatti-83csc) -
    The example skill is built around a production readiness workflow and uses
    three main files. 1. skil...

16. [academic-paper-skills - AI Agents on GitHub | SkillsLLM](https://skillsllm.com/skill/academic-paper-skills) -
    These skills transform your research ideas into submission-ready manuscripts
    through structured work...

17. [built an open registry for agent skills — with versioning ... - Reddit](https://www.reddit.com/r/ClaudeCode/comments/1r8tv4v/built_an_open_registry_for_agent_skills_with/) -
    versioning — every skill has a proper version history. when you publish an
    update, it's a new versio...

18. [SciAgent-Skills - AI Agents on GitHub | SkillsLLM](https://skillsllm.com/skill/sciagent-skills) -
    SciAgent-Skills works with any AI agent that can read project files. Clone
    the repo into your projec...

19. [Are Claude Code Skills Safe? How to Vet an AI Skill Before You ...](https://skillsllm.com/blog/how-to-vet-ai-skill-security) -
    Here is a practical 7-point security checklist for vetting any Claude Code
    skill, MCP server, or SKI...

20. [skill.md explained: How to structure your product for AI agents](https://www.gitbook.com/blog/skill-md) -
    A good skill.md file includes things like structured instructions, in-depth
    explanations of features...

21. [How to Evaluate and Test Agent Skills - YouTube](https://www.youtube.com/watch?v=XUzUf_HCgvk) -
    Agent skill eval workflow · Deterministic and rubric checks · Prompt sets
    for regression testing.

22. [K-Dense-AI/scientific-agent-skills - GitHub](https://github.com/K-Dense-AI/scientific-agent-skills) -
    Autonomous optimization: Arbor (Hypothesis Tree Refinement — iteratively
    improve a code ... For comp...

23. [Andrej Karpathy's Math Proves Agent Skills Will Fail. Here's What to ...](https://www.youtube.com/watch?v=I2K81s0OQto) -
    ... skills. Tech stack: Python backend / React frontend; Supabase (state
    management and harness runs...

24. [Scary Agent Skills: Hidden Unicode Instructions in Skills ...And How ...](https://embracethered.com/blog/posts/2026/scary-agent-skills/) -
    Skills introduce common threats, like prompt injection, supply chain
    attacks, RCE, data exfiltration...

25. [Agent Skills: Explore security threats and controls - Red Hat Developer](https://developers.redhat.com/articles/2026/03/10/agent-skills-explore-security-threats-and-controls) -
    Learn how to manage the security threats and access controls associated with
    adopting the new Agent ...

26. [Agent Skills - Claude API Docs](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) -
    Key security considerations: Audit thoroughly: Review all files bundled in
    the Skill: SKILL.md, scri...

AgentSkills.io sharpens and operationalizes the SKILL.md pattern with very
concrete guidance on how to create, evolve, and keep skills reliable over time.
Its specification and creation docs effectively turn “skills as docs” into
“skills as rigorously engineered, versioned components” with measurable routing
behavior and lifecycle rules.
[agentskills](https://agentskills.io/specification)

Below is an extension of the earlier research, focused specifically on what
AgentSkills.io adds around creation and maintenance.

---

## What AgentSkills.io adds to the spec

AgentSkills.io serves as the canonical specification site for the Agent Skills
open standard originally developed by Anthropic, and the GitHub spec now simply
points to it as the source of truth. It defines a minimal, but explicit, on‑disk
structure:
[github](https://github.com/anthropics/skills/blob/main/spec/agent-skills-spec.md)

```text
skill-name/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
├── assets/           # Optional: templates, resources
└── ...               # Any additional files or directories
```

The SKILL.md file must contain YAML frontmatter followed by markdown
instructions; frontmatter and body are allowed to be arbitrarily rich, but the
spec standardizes key fields like `name` and `description` and places concrete
bounds on some of them (for example, description length). In the broader
ecosystem, this aligns with previously described patterns (progressive
disclosure, optional scripts and references), but AgentSkills.io codifies them
into a formal spec implementors can test against.
[inference](https://inference.sh/blog/skills/agent-skills-overview)

---

## Creation: opinionated guidance beyond “write a doc”

### Directory and SKILL.md structure

The spec explicitly states that a “skill is a directory containing, at minimum,
a SKILL.md file,” with optional `scripts/`, `references/`, and `assets/`
subdirectories for code, docs, and templates. This reinforces the pattern of
skills as operational bundles, not just text instructions, and matches the
architecture used by major clients (Claude, VS Code Agent Skills, Copilot,
Cursor, etc.).
[platform.claude](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

The SKILL.md structure is:

- YAML frontmatter with required fields.
- Markdown body containing instructions with no format restrictions.
  [agentskills](https://agentskills.io/specification)

The “no format restrictions” clause in the body is important: the spec
intentionally stays permissive so different organizations can embed structured
sections, checklists, or internal conventions without breaking interoperability,
while tools still depend on frontmatter fields for routing, display, and
validation. [inference](https://inference.sh/blog/skills/agent-skills-overview)

### Frontmatter fields with operational semantics

The `description` field gets unusually detailed treatment:

- Must be 1–1024 characters.
- Should describe both what the skill does and when to use it.
- Should include specific keywords that help the model recognize relevant
  prompts. [agentskills](https://agentskills.io/specification)

Later creation docs expand this into an explicit “routing design” problem: the
description is framed not as a marketing tagline, but as a decision rule the
agent uses to decide whether to load the skill. This tight coupling between
description and routing is consistent with broader practice but made explicit
and testable here.
[agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)

AgentSkills.io’s quickstart then anchors creation in a concrete, minimal
example: a dice‑rolling skill that gives an agent an RNG‑backed “roll dice”
capability, walking through writing SKILL.md and arranging files in the standard
directory layout. This matches the earlier observation that skills should encode
concrete workflows rather than abstract knowledge, but now with an official,
tutorialized entry point.
[agentskills](https://agentskills.io/skill-creation/quickstart)

---

## Creation as an iterative, evaluated process

The “Optimizing skill descriptions” guide is where AgentSkills.io goes beyond
most existing docs: it treats description authoring as a measurable optimization
problem with an explicit eval loop.
[agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)

Key aspects:

- **Imperative phrasing:** “Use this skill when…” rather than “This skill
  does…”, because the agent is choosing actions, not reading marketing copy.
  [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
- **Intent‑focused:** Describe user intent, not implementation details (CSV
  analysis vs “uses pandas and matplotlib”), since routing is driven by how
  users phrase requests.
  [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
- **Aggressive scope coverage:** Encourage listing contexts where the skill
  should apply “even if they don’t explicitly mention ‘CSV’ or ‘analysis’,”
  trading a bit of recall vs precision that can later be tuned via evals.
  [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
- **Concise but complete:** Enough detail to capture scope while not bloating
  context across many skills.
  [agentskills](https://agentskills.io/specification)

Then, it prescribes an eval methodology that is unusually concrete for
“documentation”:

1. Build ~20 labeled prompts (“eval queries”), half that should trigger and half
   that should not.
   [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
2. Vary phrasing, explicitness, detail, and complexity to cover real‑world
   variation and near‑misses.
   [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
3. Run each query multiple times (recommended 3) and measure **trigger
   rate**—fraction of runs where the skill was invoked.
   [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
4. Define pass conditions: should‑trigger queries need a trigger rate above a
   threshold (default 0.5), should‑not‑trigger queries need a rate below that
   threshold.
   [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
5. Split into train (~60%) and validation (~40%) sets, and optimize the
   description against train failures while monitoring validation to avoid
   overfitting (e.g., not just copying rare keywords from failing prompts).
   [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
6. Iterate, then select the best description by validation pass rate, not
   necessarily the last revision.
   [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)

This effectively imports machine‑learning style train/validation methodology
into skill authoring, something the broader literature had only alluded to in
general terms around “iterative testing and refinement.” It operationalizes a
core research theme: routing quality is critical, and can be engineered and
measured at the skill level rather than treated as a black box.
[newsletter.victordibia](https://newsletter.victordibia.com/p/implementing-claude-code-skills-from)

---

## Maintenance: explicit lifecycle hooks and quality control

While the specification itself is largely static, the ecosystem guidance and
creation docs imply a lifecycle model consistent with “skills as code.”
[agentskills](https://agentskills.io/skill-creation/quickstart)

### Description optimization and regression control

By recommending a train/validation split and multiple iterations, AgentSkills.io
effectively treats each description change as a candidate “release” that must
beat or match prior versions on a fixed eval set before being adopted. Combined
with external work on registries and versioning (e.g., immutable versions and
history in open registries and proposed package managers like Skilldex), this
supports a workflow where:
[agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)

- SKILL.md changes are versioned in Git.
- Each change to the description (or broader instructions) is evaluated via the
  described triggering tests.
- Only versions that improve or preserve validation performance are promoted.
  [arxiv](https://arxiv.org/html/2604.16911v1)

This dovetails with the earlier research theme that skills should be treated
like code with CI/eval pipelines, not static docs.
[fortegrp](https://www.fortegrp.com/insights/skills-vs-documents-your-agent-is-only-as-good-as-its-last-skill-update)

### Preventing drift and maintaining routing fidelity

The description optimization guide also provides a practical strategy for
handling drift as the environment, model, or surrounding skills change:

- Use near‑miss negatives to ensure the description defines boundaries between
  adjacent skills or capabilities, reducing cross‑skill confusion as new skills
  are added.
  [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
- When train set failures occur, adjust scope (narrow or broaden) at the
  conceptual level instead of keyword‑stuffing, to maintain robustness across
  phrasing variants and new prompt styles.
  [agentskills](https://agentskills.io/skill-creation/optimizing-descriptions)
- Periodically add fresh eval queries not used during optimization to detect
  overfitting and drift, particularly after major changes in dependent systems
  (APIs, tools) or model upgrades.
  [fortegrp](https://www.fortegrp.com/insights/skills-vs-documents-your-agent-is-only-as-good-as-its-last-skill-update)

This aligns closely with external advice on preventing skills from drifting out
of sync with underlying tools and processes, but adds concrete techniques to
maintain routing behavior under change.
[mondoo](https://mondoo.com/blog/agent-skills-real-power-real-risk)

### Maintenance across clients

The docs note that how a skill is discovered and registered depends on the
client (skills directory, config file, CLI flag, etc.), and recommend using
client‑side observability (logs, tool call histories) to see when a skill was
loaded. That has direct implications for maintenance:
[agentskills](https://agentskills.io/clients)

- You can track whether a skill that “should be important” is actually being
  invoked in production, and adjust descriptions or references accordingly.
- You can detect **dead skills**—ones that never trigger in real workloads—and
  either deprecate or redesign them.
- You can spot skills that trigger too often or inappropriately and refine their
  scope using the same eval tooling.
  [mondoo](https://mondoo.com/blog/agent-skills-real-power-real-risk)

In the broader research context, this connects to calls for runtime
observability and registry governance: AgentSkills.io gives the spec layer;
registries and platform tooling provide discovery, versioning, and audit trails.
[agenticskills](https://agenticskills.io)

---

## How AgentSkills.io shapes the research landscape on creation & maintenance

Putting this in context of the earlier literature:

- It **codifies** the SKILL.md pattern that prior work described more
  informally: the directory structure, SKILL.md frontmatter, and body semantics
  are now precise enough that tools like Skilldex and ecosystem registries can
  validate conformance against a spec instead of reverse‑engineering platform
  behavior.
  [github](https://github.com/anthropics/skills/blob/main/spec/agent-skills-spec.md)
- It **elevates creation** from “write instructions” to a repeatable, evaluated
  process, with a focus on description quality as measurable routing behavior,
  which makes it a natural target for further research (e.g., automated
  description synthesis, optimal thresholds, multi‑skill routing strategies).
  [arxiv](https://arxiv.org/html/2602.12430v3)
- It **bridges into maintenance** by embedding eval‑loop thinking and client
  observability into the docs, aligning with external calls to treat skills as
  versioned, testable software assets and providing concrete techniques to
  manage drift and avoid brittle routing.
  [youtube](https://www.youtube.com/watch?v=XUzUf_HCgvk)

For your purposes, if you are designing or researching SKILL.md‑style agents,
AgentSkills.io gives you:

- A specification you can formally validate against when generating or linting
  SKILL.md files programmatically.
  [github](https://github.com/anthropics/skills/blob/main/spec/agent-skills-spec.md)
- A ready‑made methodology for measuring and improving skill triggering, which
  can be extended into more general eval pipelines (e.g., combining routing
  evals with task‑completion metrics).
  [arxiv](https://arxiv.org/html/2602.12430v3)
- A conceptual anchor for maintenance practices that tie together spec
  conformance, version control, evals, and runtime observability.
  [arxiv](https://arxiv.org/html/2604.16911v1)

Would it be most useful if the next step focused on (a) turning these
creation/maintenance practices into a concrete checklist you can apply to your
own skills, or (b) outlining research questions and experiments you could run on
top of the AgentSkills.io spec (e.g., automated skill generation, routing
algorithms, or drift detection)?

MCP defines _how_ agents talk to tools and data; Agent Skills define _how_
agents should behave when using them. Skills sit above MCP in the stack as
portable workflow instructions that organize and interpret the structured
capabilities MCP exposes.
[modelcontextprotocol](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)

Below is how they fit together in the broader tooling and context‑management
ecosystem, grounded in the 2025‑11‑25 MCP spec.

---

## MCP’s role: tools, resources, and prompts

The Model Context Protocol 2025‑11‑25 spec standardizes a JSON‑RPC–based way for
LLM applications to connect to external tools and data sources. MCP defines:
[modelcontextprotocol](https://modelcontextprotocol.info/specification/)

- **Servers** that expose capabilities as:
    - **Tools**: callable operations with structured JSON inputs/outputs (e.g.,
      `deployApp`, `getIssues`).
      [modelcontextprotocol](https://modelcontextprotocol.io/specification/2025-06-18)
    - **Resources**: readable data (files, documents, tables) discoverable via
      `resources/list` and fetched with `resources/read`.
      [modelcontextprotocol](https://modelcontextprotocol.io/specification/2025-06-18)
    - **Prompts**: parameterized prompt templates the client can list and
      invoke.
      [modelcontextprotocol](https://modelcontextprotocol.io/specification/2025-06-18)
- **Clients** (IDEs, agent frameworks, apps) that:
    - Discover available tools/resources/prompts.
    - Append their descriptions and schemas into model context.
    - Orchestrate tool calls and manage auth, scopes, and transport.
      [anthropic](https://www.anthropic.com/news/model-context-protocol)

The 2025‑11‑25 version adds richer auth and interaction primitives (OpenID
Connect Discovery, incremental scope consent, sampling tool‑calling,
experimental tasks for durable work), but its core purpose remains: a standard,
secure way to expose external capabilities and data to agents.
[modelcontextprotocol](https://modelcontextprotocol.io/specification/2025-11-25/changelog)

**Important:** MCP itself does _not_ say _what_ workflows to follow with those
tools; it just publishes the menu and the calling contract.
[anthropic](https://www.anthropic.com/news/model-context-protocol)

---

## Agent Skills: workflow & behavior layer on top of MCP

Agent Skills are defined as lightweight, reusable instruction bundles
(directories with SKILL.md and optional scripts/resources) that teach agents how
to carry out specific tasks. In the MCP docs, they are explicitly framed as a
way to guide AI coding assistants through MCP server design and usage:
[agentskills](https://agentskills.io/home)

> “For MCP development, [Agent Skills] encode the design decisions (deployment
> model, tool patterns, auth) so your agent can interrogate your use case and
> scaffold a server that fits.”
> [modelcontextprotocol](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)

More generally, Anthropic’s engineering write‑up describes skills as
complementing MCP: MCP connects to tools and data; skills encode complex
workflows that _use_ those tools safely and effectively. Blog and vendor content
distill this into a division of responsibilities:
[anthropic](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

- **MCP:** Standard interface to external systems and data.
  [modelcontextprotocol](https://modelcontextprotocol.info/specification/)
- **Skills:** Structured instructions and examples that tell the model how to
  orchestrate tools, interpret outputs, and comply with domain‑specific best
  practices.
  [developers.redhat](https://developers.redhat.com/articles/2026/05/25/mcp-servers-vs-skills-choosing-right-context-your-ai)

A typical stack looks like:

| Layer          | What it defines                                        | Example question it answers                                                                                                                                              |
| -------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MCP server     | Tools/resources/prompts and auth for a system          | “What can I call, with which JSON schema?” [modelcontextprotocol](https://modelcontextprotocol.io/specification/2025-06-18)                                              |
| Agent Skill    | Workflows, patterns, and guardrails over those tools   | “How should I _use_ these tools for X?” [modelcontextprotocol](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)                                     |
| Agent / client | When to load skills, route tasks, and call MCP servers | “Given this user request, what should I do?” [developers.redhat](https://developers.redhat.com/articles/2026/05/25/mcp-servers-vs-skills-choosing-right-context-your-ai) |

---

## How Skills and MCP interact in practice

### 1. Skills describing MCP server design and usage

The MCP docs have a dedicated “Build with Agent Skills” guide that shows skills
acting as _design blueprints_ for MCP servers.
[modelcontextprotocol](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)

- The skill encodes decisions like deployment model, authentication strategy,
  tool patterns, and typical workflows for a given use case (e.g.,
  “customer‑support knowledge base MCP server”).
  [modelcontextprotocol](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)
- The agent, guided by that skill, can ask structured questions about the user’s
  requirements and then scaffold an MCP server that conforms to both the MCP
  spec and the organization’s conventions.
  [modelcontextprotocol](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)

In this mode, Agent Skills are _meta‑tools_ that help you build the MCP layer
itself, effectively turning SKILL.md into a reusable design pattern for MCP
server creation and maintenance.

### 2. Skills orchestrating calls to existing MCP servers

Once MCP servers exist, skills can orchestrate them:

- MCP exposes tools like `listKubernetesResources`, `getDeployment`,
  `scaleDeployment`, and resources such as cluster configs.
  [developers.redhat](https://developers.redhat.com/articles/2026/05/25/mcp-servers-vs-skills-choosing-right-context-your-ai)
- A deployment or SRE skill can define a safe rollout workflow: check health,
  apply changes, monitor metrics, and roll back on failure, using those MCP
  tools in a specific order with guardrails.
  [anthropic](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- The client loads this skill only when a user request matches its description
  (“deploy a new version of service X to staging”), keeping context lean while
  still having rich, tested procedures available.
  [inference](https://inference.sh/blog/skills/agent-skills-overview)

Red Hat’s guidance captures this distinction: MCP “standardizes how your AI
agent talks to external data sources,” whereas skills “are reusable, structured
instructions that teach your LLM how to do something,” often involving those
MCP‑exposed tools.
[developers.redhat](https://developers.redhat.com/articles/2026/05/25/mcp-servers-vs-skills-choosing-right-context-your-ai)

### 3. Hybrid context: MCP resources vs skill context

Community discussions note that MCP’s resources feature can itself act as a kind
of “context injection” mechanism—serving documents, schemas, or config that the
model reads before responding. Skills provide a complementary, higher‑level
mechanism:
[reddit](https://www.reddit.com/r/mcp/comments/1r0yn2b/mcp_or_skills_for_delivering_extra_context_to_ai/)

- **MCP resources**: Arbitrary data blobs (docs, files) the agent can fetch on
  demand.
- **Skills**: Curated, structured instruction sets (plus optional local
  resources/scripts) that are designed around specific workflows and include
  activation metadata. [agentskills](https://agentskills.io/specification)

A common pattern in practice is:

1. Skill tells the agent _which_ MCP resources to fetch and _how_ to use them
   (e.g., “always load `schema.yaml` and `policy.md` before modifying customer
   records”).
2. MCP ensures those resources and tools are exposed in a consistent, secure way
   across environments.
   [anthropic](https://www.anthropic.com/news/model-context-protocol)

---

## Where Skills sit in the broader ecosystem

Several ecosystem pieces make the relationship clearer:

- Anthropic explicitly positions skills as an open standard that complements
  MCP, not as an alternative: MCP for connectivity, skills for domain‑ and
  workflow‑specific behavior.
  [anthropic](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- Third‑party analyses describe skills as “inert knowledge” that depends on the
  agent having capabilities (MCP tools or other mechanisms) to actually do work,
  reinforcing that skills themselves do not execute actions.
  [ravichaganti](https://ravichaganti.com/blog/agent-skills-vs-model-context-protocol-how-do-you-choose/)
- Hybrid recommendations (“MCP + Skills works best”) emphasize that skills are
  lightweight, low‑token ways to shape behavior across many contexts, while MCP
  gives robust, audited integration to external systems.
  [reddit](https://www.reddit.com/r/mcp/comments/1r0yn2b/mcp_or_skills_for_delivering_extra_context_to_ai/)

Putting it into a conceptual stack:

1. **Model**: General reasoning and language capability.
2. **Agent runtime / client**: Conversation management, routing, tool‑calling
   orchestration.
3. **Context integration standards**:
    - MCP: Tools/resources/prompts from external systems.
      [github](https://github.com/modelcontextprotocol/modelcontextprotocol)
    - Other APIs: non‑MCP integrations, local files, etc.
4. **Knowledge/workflow packaging**:
    - Agent Skills (SKILL.md): workflows, patterns, guardrails, and activation
      metadata that tell the model how to apply those integrations.
      [agentskills](https://agentskills.io/home)
5. **Ecosystem services**:
    - Registries, evaluators, security scanners, and governance around both MCP
      servers and skills. [arxiv](https://arxiv.org/html/2604.16911v1)

In short: MCP is about _plumbing_ and _contracts_; Agent Skills are about
_procedure_ and _practice_.

---

## Implications for design, maintenance, and research

Given this separation, some useful design and research implications emerge:

- **Design:** Use MCP to expose tools and data in a uniform, secure way; use
  skills to encode organization‑specific workflows, policies, and best practices
  for using those tools. This keeps MCP servers generic and skills tailored.
  [anthropic](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- **Maintenance:** Changes in MCP servers (new tools, auth changes, schema
  updates) should trigger updates and re‑evals of any skills that depend on
  them, reinforcing the “skills as code” lifecycle you are already tracking.
  [mondoo](https://mondoo.com/blog/agent-skills-real-power-real-risk)
- **Security:** MCP handles auth, scopes, and transport security, but skills add
  a prompt‑injection and workflow‑integrity surface that needs its own
  governance (reviews, evals, signing, registry policies), especially when
  skills call high‑privilege MCP tools.
  [snyk](https://snyk.io/blog/skill-scanner-false-security/)
- **Research:** There is a natural space for work on:
    - Joint design of skills and MCP tool schemas for robust orchestration.
    - Automatic synthesis of skills from MCP server descriptions (and vice
      versa, scaffolding servers from skills, as in the MCP docs).
      [arxiv](https://arxiv.org/html/2602.12430v3)
    - Evaluation frameworks that measure end‑to‑end reliability across the
      skill + MCP boundary, not just one layer in isolation.
      [youtube](https://www.youtube.com/watch?v=XUzUf_HCgvk)

If you’re building out your own stack, the key decision is where to draw the
line between “generic MCP server capabilities” and “skill‑level workflows and
policies.” Would it be helpful if the next step focused on a concrete
architecture sketch that shows how to layer your SKILL.md libraries over
specific MCP servers you care about (e.g., internal APIs, Git, Kubernetes, CRM)?
