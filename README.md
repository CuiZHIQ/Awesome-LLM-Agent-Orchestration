# Awesome LLM Agent Orchestration Papers

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Last Updated](https://img.shields.io/badge/Last%20Updated-2026--07--02-blue)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-green)

> A curated research map for **LLM agent scheduling, orchestration, routing, tool dispatch, multi-agent coordination, and workflow optimization**.
>
> A research-oriented taxonomy and paper collection for LLM agent orchestration. Here, "scheduling" includes not only traditional OS-style scheduling, but also task decomposition, tool/model/agent routing, parallel function calling, agent team formation, agent graph/workflow optimization, long-horizon execution, and evaluation.

---

## News

- `2026-07-02`: Refocused the list toward recent orchestra/router work, added 2026 agent-routing and multi-agent-orchestration papers, and switched the public repository to MIT licensing.
- `2026-07-01`: Initial version. Built a taxonomy-first paper list for LLM agent orchestration.

---

## Table of Contents

- [Introduction](#introduction)
- [DeepResearch Taxonomy](#deepresearch-taxonomy)
- [Reading Roadmap](#reading-roadmap)
- [Papers](#papers)
  - [Surveys, Taxonomies, and Position Papers](#surveys-taxonomies-and-position-papers)
  - [Planning, Control Loops, and Search](#planning-control-loops-and-search)
  - [Tool, API, and Function-Calling Orchestration](#tool-api-and-function-calling-orchestration)
  - [Multi-Agent Collaboration and Team Orchestration](#multi-agent-collaboration-and-team-orchestration)
  - [Model Routing, Agent Routing, Cascades, and MoE Routers](#model-routing-agent-routing-cascades-and-moe-routers)
  - [Workflow Graphs, Runtime Scheduling, Memory, and Optimization](#workflow-graphs-runtime-scheduling-memory-and-optimization)
  - [Recent Agentic Applications and Production Orchestration](#recent-agentic-applications-and-production-orchestration)
  - [Benchmarks and Evaluation](#benchmarks-and-evaluation)
- [Resources](#resources)
- [Contributing](#contributing)
- [License](#license)

---

## Introduction

LLM agent orchestration can be understood as how a system decides, for a given goal, **who should act, what should happen first, what can run in parallel, which tool or model to invoke, how to observe feedback, when to stop, and how to reuse prior experience**.

A typical agent orchestration stack contains:

```text
User Goal
  -> Intent / Difficulty Estimator
  -> Planner / Decomposer
  -> Router: model router, tool router, agent router, memory router
  -> Executor Pool: LLMs, tools, APIs, browsers, code runtimes, robots
  -> Scheduler: dependency graph, parallelism, retries, budget, latency
  -> Verifier / Critic / Reward Model
  -> Memory / Workflow Library
  -> Final Synthesizer
```

This list prioritizes work directly related to the stack above. Pure prompt engineering, standard RAG, single-model reasoning, and traditional MoE papers are included only when they provide meaningful insight into routers or schedulers.

## DeepResearch Taxonomy

| Research line | Core scheduling question | Typical mechanisms | Representative papers |
| --- | --- | --- | --- |
| Planning and control loops | How should a goal be decomposed into executable steps and revised from observations? | ReAct loop, plan-and-execute, MCTS, tree/graph search, self-reflection | ReAct, ToT, GoT, RAP, LATS |
| Tool/API orchestration | When should each tool be called, and how should multi-tool results be composed? | API retrieval, function planner, tool compiler, async/parallel execution | Toolformer, ToolLLM, HuggingGPT, LLMCompiler, AnyTool |
| Model routing | Should a request go to a cheaper model, a stronger model, a specialist model, or a model ensemble? | Cascades, preference routers, uncertainty routers, bandit routers | FrugalGPT, RouteLLM, RouterBench, MoA |
| Agent routing and team formation | Which agent should handle each subtask, how should work be divided, and how should agents communicate? | Role assignment, dynamic team selection, debate, committee, graph topology | MetaGPT, AgentVerse, DyLAN, GPTSwarm, AutoGen |
| Workflow graph optimization | How can agent workflow graphs be generated, tuned, reused, and evolved automatically? | Agentic computation graphs, edge optimization, workflow memory, latency-cost-reliability tradeoff | GPTSwarm, Agent Workflow Memory, workflow optimization surveys |
| Runtime scheduling | How should calls across tools, agents, and models be parallelized, retried, and budgeted? | DAG scheduler, parallel function calls, async function calls, early stop, budget-aware routing | LLMCompiler, AsyncLM, latency-aware orchestration |
| Memory and skill reuse | How can successful trajectories be distilled into reusable workflows and skills? | Episodic memory, workflow induction, skill composition, procedural memory | Agent Workflow Memory, LEGOMem, Generative Skill Composition |
| Evaluation | How should long-horizon task completion, routing quality, cost, and safety be measured? | Interactive environments, execution-based grading, user simulators, router benchmarks | AgentBench, WebArena, OSWorld, SWE-bench, GAIA, RouterBench |

---

## Reading Roadmap

If you only read ten papers first:

1. **[Uno-Orchestra](https://arxiv.org/abs/2605.05007)** — arXiv 2026. Selective delegation over decomposition depth, worker choice, and inference budget.
2. **[Agent-as-a-Router](https://arxiv.org/abs/2606.22902)** — arXiv 2026. Treats routing as a context-action-feedback loop with execution-grounded memory.
3. **[INFRAMIND](https://arxiv.org/abs/2606.11440)** — arXiv 2026. Infrastructure-aware planning, per-step routing, and scheduling for multi-agent pipelines.
4. **[Scaling Enterprise Agent Routing](https://arxiv.org/abs/2606.17519)** — arXiv 2026. Studies routing degradation and recovery in a 110-agent, 584-tool production catalog.
5. **[LEMON](https://arxiv.org/abs/2605.14483)** — arXiv 2026. Learns executable multi-agent orchestration specifications with counterfactual RL.
6. **[When Parallelism Pays Off](https://arxiv.org/abs/2606.00953)** — arXiv 2026. Frames multi-agent coding orchestration as cohesion-aware graph partitioning.
7. **[PerspectiveGap](https://arxiv.org/abs/2606.08878)** — arXiv 2026. Benchmark for composing multi-agent orchestration prompts.
8. **[The Workload-Router-Pool Architecture](https://arxiv.org/abs/2603.21354)** — arXiv 2026. Systems view of workload-aware inference routing for agentic workloads.
9. **[LLMCompiler](https://proceedings.mlr.press/v235/kim24y.html)** — ICML 2024. Dependency-aware parallel function calling.
10. **[GPTSwarm](https://proceedings.mlr.press/v235/zhuge24a.html)** — ICML 2024. Language agents represented and optimized as graphs.

---

## Papers

### Surveys, Taxonomies, and Position Papers

1. **[A Survey on Large Language Model based Autonomous Agents](https://arxiv.org/abs/2308.11432)** — arXiv 2023. `survey` `autonomous-agent`
   - Covers agent architecture, memory, planning, tool use, and environments.

2. **[The Rise and Potential of Large Language Model Based Agents: A Survey](https://arxiv.org/abs/2309.07864)** — arXiv 2023. `survey` `agent-architecture`
   - Broad survey of LLM-based agents, agent society, and applications.

3. **[A Survey of Task Planning with Large Language Models](https://spj.science.org/doi/10.34133/icomputing.0124)** — iComputing 2025. `survey` `planning`
   - Useful for separating natural-language planning, symbolic planning, and LLM-modulo planning.

4. **[Advances and Challenges in Foundation Agents](https://arxiv.org/abs/2504.01990)** — arXiv 2025. `survey` `foundation-agent`
   - System-level survey of foundation-model agents, including tool use, memory, evaluation, and deployment.

5. **[The Orchestration of Multi-Agent Systems: Architectures, Protocols, and Communication](https://arxiv.org/abs/2601.13671)** — arXiv 2026. `survey` `multi-agent-orchestration`
   - Directly targets orchestration layers, communication protocols, and coordination architectures.

6. **[LLM-Based Multi-Agent Orchestration: A Survey of Frameworks, Patterns, and Challenges](https://www.mdpi.com/1999-5903/18/6/326)** — Future Internet 2026. `survey` `frameworks`
   - Focuses on multi-agent orchestration patterns, production concerns, and evaluation methodology.

7. **[From Static Templates to Dynamic Runtime Graphs: A Survey of Workflow Optimization for LLM Agents](https://arxiv.org/abs/2603.22386)** — arXiv 2026. `survey` `workflow-optimization`
   - Treats agent workflows as agentic computation graphs and classifies optimization methods.

8. **[Adaptation of Agentic AI: A Survey of Post-Training, Memory, and Skills](https://arxiv.org/abs/2512.16301)** — arXiv 2025. `survey` `memory` `skills`
   - Useful for workflow memory, skill reuse, and post-training adaptation.

---

### Planning, Control Loops, and Search

1. **[ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)** — ICLR 2023. `plan-act-observe`
   - The canonical loop for interleaving reasoning, environment action, and observation.

2. **[Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Models](https://aclanthology.org/2023.acl-long.147/)** — ACL 2023. `planner`
   - Separates plan creation from step execution.

3. **[Reasoning with Language Model is Planning with World Model](https://aclanthology.org/2023.emnlp-main.507/)** — EMNLP 2023. `RAP` `world-model` `MCTS`
   - Uses an LLM as both world model and reasoning agent, with MCTS-style planning.

4. **[Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601)** — NeurIPS 2023. `tree-search`
   - Turns reasoning into tree search with self-evaluation and backtracking.

5. **[Graph of Thoughts: Solving Elaborate Problems with Large Language Models](https://ojs.aaai.org/index.php/AAAI/article/view/29720)** — AAAI 2024. `graph-search`
   - Generalizes thought structures from chains/trees to arbitrary graphs.

6. **[Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366)** — NeurIPS 2023. `reflection` `memory`
   - Adds verbal feedback and episodic memory for trial-to-trial improvement.

7. **[Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651)** — NeurIPS 2023. `self-feedback`
    - Generator, feedback provider, and refiner can be the same LLM.

8. **[LLM+P: Empowering Large Language Models with Optimal Planning Proficiency](https://arxiv.org/abs/2304.11477)** — arXiv 2023. `symbolic-planner` `PDDL`
    - Routes natural-language planning problems through classical planners.

9. **[PromptAgent: Strategic Planning with Language Models Enables Expert-level Prompt Optimization](https://arxiv.org/abs/2310.16427)** — ICLR 2024. `prompt-agent` `MCTS`
    - Treats prompt optimization as search over prompt states and actions.

10. **[Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models](https://proceedings.mlr.press/v235/zhou24r.html)** — ICML 2024. `LATS` `agent-search`
    - Integrates reasoning, acting, planning, value estimation, and reflection.

11. **[Planning with Language Models Through the Lens of Efficiency](https://proceedings.neurips.cc/paper_files/paper/2024/hash/fa080fe0f218871faec1d8ba20e491d5-Abstract-Conference.html)** — NeurIPS 2024. `planning` `efficiency`
    - Analyzes when planning with LMs is computationally efficient.

12. **[Position: LLMs Can't Plan, But Can Help Planning in LLM-Modulo Frameworks](https://arxiv.org/abs/2402.01817)** — ICML 2024. `position` `LLM-modulo`
    - Argues for routing LLMs into planner/verifier/tool modules rather than relying on pure generation.

---

### Tool, API, and Function-Calling Orchestration

1. **[PAL: Program-Aided Language Models](https://arxiv.org/abs/2211.10435)** — ICML 2023. `code-tool` `program-execution`
   - Routes reasoning through generated programs and external interpreters.

2. **[Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761)** — NeurIPS 2023. `tool-use`
   - Learns when to call tools, what arguments to pass, and how to consume results.

3. **[ART: Automatic Multi-Step Reasoning and Tool-Use for Large Language Models](https://arxiv.org/abs/2303.09014)** — arXiv 2023. `tool-chain`
   - Builds multi-step tool-use trajectories from task demonstrations.

4. **[ViperGPT: Visual Inference via Python Execution for Reasoning](https://arxiv.org/abs/2303.08128)** — ICCV 2023. `visual-agent` `python`
   - Uses code as the orchestration interface for visual reasoning.

5. **[Visual Programming: Compositional Visual Reasoning without Training](https://arxiv.org/abs/2211.11559)** — CVPR 2023. `visual-programming`
   - Composes vision modules through generated programs.

6. **[HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face](https://arxiv.org/abs/2303.17580)** — NeurIPS 2023. `model-dispatch` `controller`
   - LLM controller plans subtasks, selects Hugging Face models, executes, and summarizes.

7. **[Chameleon: Plug-and-Play Compositional Reasoning with Large Language Models](https://arxiv.org/abs/2304.09842)** — NeurIPS 2023. `tool-selection` `compositional`
   - Selects and composes tools/modules for multimodal reasoning.

8. **[API-Bank: A Comprehensive Benchmark for Tool-Augmented LLMs](https://arxiv.org/abs/2304.08244)** — EMNLP 2023. `api-benchmark`
   - Evaluates whether LLMs can plan, call, and recover from API interactions.

9. **[CREATOR: Tool Creation for Disentangling Abstract and Concrete Reasoning of Large Language Models](https://arxiv.org/abs/2305.14318)** — EMNLP 2023. `tool-creation`
   - Lets LLMs create tools/functions before solving concrete instances.

10. **[RESTGPT: Connecting Large Language Models with Real-World RESTful APIs](https://arxiv.org/abs/2306.06624)** — arXiv 2023. `REST` `api-agent`
    - Plans and executes REST API calls from OpenAPI-style documentation.

11. **[Gorilla: Large Language Model Connected with Massive APIs](https://arxiv.org/abs/2305.15334)** — NeurIPS 2024. `api-call` `retrieval-aware`
    - Fine-tunes API calling with retrieval-aware training to reduce hallucinated API use.

12. **[ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs](https://arxiv.org/abs/2307.16789)** — ICLR 2024. `ToolBench` `API-routing`
    - Large-scale API dataset, retriever, tool-use model, and evaluation pipeline.

13. **[AnyTool: Self-Reflective, Hierarchical Agents for Large-Scale API Calls](https://proceedings.mlr.press/v235/du24h.html)** — ICML 2024. `hierarchical-router` `API`
    - Hierarchical API retrieval plus self-reflection for large API spaces.

14. **[An LLM Compiler for Parallel Function Calling](https://proceedings.mlr.press/v235/kim24y.html)** — ICML 2024. `parallel-function-calling` `DAG`
    - Builds a function-call plan, fetches ready tasks, and executes independent calls in parallel.

15. **[An LLM-Tool Compiler for Fused Parallel Function Calling](https://arxiv.org/abs/2405.17438)** — arXiv 2024. `tool-compiler`
    - Extends compiler-style function orchestration with fused parallel calls.

16. **[Efficient Tool Use with Chain-of-Abstraction Reasoning](https://aclanthology.org/2025.coling-main.185/)** — COLING 2025. `parallel-tool-use` `abstraction`
    - Decodes abstract reasoning placeholders first, then fills them through tools.

17. **[Asynchronous LLM Function Calling](https://arxiv.org/abs/2412.07017)** — arXiv 2024. `async` `runtime`
    - Enables LLMs to generate and execute function calls concurrently.

---

### Multi-Agent Collaboration and Team Orchestration

1. **[Generative Agents: Interactive Simulacra of Human Behavior](https://dl.acm.org/doi/10.1145/3586183.3606763)** — UIST 2023. `simulation` `memory`
   - Early influential work on agent memory, reflection, and social simulation.

2. **[CAMEL: Communicative Agents for Mind Exploration of Large Language Model Society](https://arxiv.org/abs/2303.17760)** — arXiv 2023. `role-play` `agent-society`
   - Uses role-playing agents and inception prompting for collaborative problem solving.

3. **[AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation](https://arxiv.org/abs/2308.08155)** — arXiv 2023. `framework` `conversation-programming`
   - General framework for composing conversable agents, tools, code, and humans.

4. **[AgentVerse: Facilitating Multi-Agent Collaboration and Exploring Emergent Behaviors](https://arxiv.org/abs/2308.10848)** — ICLR 2024. `team-recruitment` `collaboration`
   - Expert recruitment, collaborative decision-making, action execution, and evaluation.

5. **[MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework](https://arxiv.org/abs/2308.00352)** — ICLR 2024 Oral. `SOP` `software-team`
   - Encodes standard operating procedures into role-based agent workflows.

6. **[ChatDev: Communicative Agents for Software Development](https://aclanthology.org/2024.acl-long.810/)** — ACL 2024. `software-dev` `chat-chain`
   - Uses specialized agents and chat chains for design, coding, testing, and documentation.

7. **[Dynamic LLM-Agent Network: An LLM-agent Collaboration Framework with Agent Team Optimization](https://arxiv.org/abs/2310.02170)** — arXiv 2023 / OpenReview. `dynamic-team` `agent-selection`
   - Selects useful agents and dynamically adjusts communication structure.

8. **[GPTSwarm: Language Agents as Optimizable Graphs](https://proceedings.mlr.press/v235/zhuge24a.html)** — ICML 2024 Oral. `agent-graph` `edge-optimization`
   - Represents agents and societies as graphs and optimizes node prompts and edges.

9. **[AgentScope: A Flexible yet Robust Multi-Agent Platform](https://arxiv.org/abs/2402.14034)** — arXiv 2024. `platform` `multi-agent`
   - Engineering platform for building, observing, and managing multi-agent applications.

10. **[Mixture-of-Agents Enhances Large Language Model Capabilities](https://arxiv.org/abs/2406.04692)** — ICLR 2025. `agent-ensemble` `layered-collaboration`
    - Uses layered agents where later agents synthesize previous agents' outputs.

11. **[Magentic-One: A Generalist Multi-Agent System for Solving Complex Tasks](https://arxiv.org/abs/2411.04468)** — arXiv 2024. `generalist-agent` `manager-worker`
    - Manager coordinates specialized agents for browsing, coding, file operations, and terminal work.

12. **[AgentOrchestra: A Hierarchical Multi-Agent Framework for General-Purpose Task Solving](https://arxiv.org/abs/2506.12508)** — arXiv 2025. `hierarchical` `orchestration`
    - High-level planner coordinates modular specialist agents.

13. **[Multi-Agent Collaboration via Evolving Orchestration](https://arxiv.org/abs/2505.19591)** — arXiv 2025. `evolutionary-orchestration`
    - Studies automatic evolution of multi-agent collaboration patterns.

14. **[Difficulty-Aware Agentic Orchestration for Query-Specific Multi-Agent Workflows](https://arxiv.org/abs/2509.11079)** — arXiv 2025. `difficulty-aware` `query-routing`
    - Adapts the agent workflow to query difficulty.

15. **[Learning Latency-Aware Orchestration for Parallel Multi-Agent Systems](https://arxiv.org/abs/2601.10560)** — arXiv 2026. `latency-aware` `parallel-agents`
    - Optimizes orchestration under latency constraints.

16. **[Multi-Agent Coordination Adaptation via Structure-Guided Orchestration](https://arxiv.org/abs/2605.25746)** — arXiv 2026. `structure-guided` `coordination`
    - Adapts coordination structure instead of using fixed communication graphs.

17. **[Reward Modeling for Multi-Agent Orchestration](https://arxiv.org/abs/2606.13598)** — arXiv 2026. `reward-model` `orchestration`
    - Uses reward modeling to guide multi-agent orchestration decisions.

18. **[PerspectiveGap: A Benchmark for Multi-Agent Orchestration Prompting](https://arxiv.org/abs/2606.08878)** — arXiv 2026. `benchmark` `prompting`
    - Tests prompt-level orchestration of agents with different perspectives.

19. **[LEMON: Learning Executable Multi-Agent Orchestration via Counterfactual Reinforcement Learning](https://arxiv.org/abs/2605.14483)** — arXiv 2026. `counterfactual-RL` `orchestration-policy`
    - Learns role design, capacity assignment, and dependency structure as a single executable orchestration specification.

20. **[INFRAMIND: Infrastructure-Aware Multi-Agent Orchestration](https://arxiv.org/abs/2606.11440)** — arXiv 2026. `infra-aware` `planner-router-scheduler`
    - Conditions topology, role selection, model calls, and queue scheduling on real-time infrastructure state.

21. **[COHORT: Collaborative Orchestration for Hardening via Offensive Replay on Emulated Topologies](https://arxiv.org/abs/2606.30479)** — arXiv 2026. `security` `role-decomposed-workflow`
    - Uses a role-decomposed multi-agent workflow to propose, implement, critique, and replay-test network mitigations.

---

### Model Routing, Agent Routing, Cascades, and MoE Routers

1. **[RouterBench: A Benchmark for Multi-LLM Routing System](https://arxiv.org/abs/2403.12031)** — arXiv 2024. `routing-benchmark`
   - Standardizes LLM router evaluation with many model-response outcomes.

2. **[RouteLLM: Learning to Route LLMs with Preference Data](https://arxiv.org/abs/2406.18665)** — ICLR 2025 / OpenReview. `preference-router`
   - Trains routers that choose between strong and weak models under cost-quality budgets.

3. **[Mixture-of-Agents Enhances Large Language Model Capabilities](https://arxiv.org/abs/2406.04692)** — ICLR 2025. `agent-routing` `ensemble`
   - Also relevant as a model/agent composition router.

4. **[Leveraging Uncertainty Estimation for Efficient LLM Routing](https://arxiv.org/abs/2502.11021)** — arXiv 2025. `uncertainty-router`
   - Routes based on confidence/uncertainty rather than only static task type.

5. **[Arch-Router: Aligning LLM Routing with Human Preferences](https://arxiv.org/abs/2506.16655)** — arXiv 2025. `human-preference` `router`
   - Aligns routing behavior with preference signals.

6. **[Adaptive LLM Routing under Budget Constraints](https://arxiv.org/abs/2508.21141)** — arXiv 2025. `budget-aware`
   - Formulates routing under explicit budget constraints.

7. **[LLM Routing with Dueling Feedback](https://arxiv.org/abs/2510.00841)** — arXiv 2025. `dueling-feedback`
   - Uses pairwise feedback to improve router decisions.

8. **[LLMRouterBench: A Massive Benchmark and Unified Framework for LLM Routing](https://arxiv.org/abs/2601.07206)** — arXiv 2026. `routing-benchmark`
    - Expands benchmark coverage for routing across models and tasks.

9. **[Signal Driven Decision Routing for Mixture-of-Modality Models](https://arxiv.org/abs/2603.04444)** — arXiv 2026. `semantic-router` `multimodal-routing`
   - Introduces vLLM Semantic Router for signal-driven request routing across modality-specialized models.

10. **[LLM Routing as Reasoning: A MaxSAT View](https://arxiv.org/abs/2603.13612)** — arXiv 2026. `reasoning-router` `MaxSAT`
    - Frames routing as a constrained reasoning problem rather than a static classifier.

11. **[Reward-Based Online LLM Routing via NeuralUCB](https://arxiv.org/abs/2603.30035)** — arXiv 2026. `online-routing` `bandit`
    - Online router using bandit-style uncertainty exploration.

12. **[Explainable Model Routing for Agentic Workflows](https://arxiv.org/abs/2604.03527)** — arXiv 2026. `agentic-workflow` `explainable-router`
    - Focuses on routing decisions inside multi-stage agent workflows.

13. **[The Workload-Router-Pool Architecture for LLM Inference Optimization: A Vision Paper from the vLLM Semantic Router Project](https://arxiv.org/abs/2603.21354)** — arXiv 2026. `semantic-router` `serving-architecture`
    - Distills workload-aware inference optimization into workload, router, and pool layers for agentic and multimodal workloads.

14. **[Accuracy Is Speed: Towards Long-Context-Aware Routing for Distributed LLM Serving](https://arxiv.org/abs/2604.15732)** — arXiv 2026. `long-context-routing` `serving`
    - Routes long-context requests by capability because retries make answer accuracy part of end-to-end latency.

15. **[Learning Agent Routing From Early Experience](https://arxiv.org/abs/2605.07180)** — arXiv 2026. `agent-router`
    - Learns which agent should handle a task from early trajectory signals.

16. **[Uno-Orchestra: Parsimonious Agent Routing via Selective Delegation](https://arxiv.org/abs/2605.05007)** — arXiv 2026. `selective-delegation`
    - Routes only when delegation is useful, reducing unnecessary multi-agent overhead.

17. **[Scaling Enterprise Agent Routing: Degradation, Diagnosis, and Recovery](https://arxiv.org/abs/2606.17519)** — arXiv 2026. `enterprise-routing` `tool-catalog`
    - Studies routing degradation in a 110-agent, 584-tool production catalog and shows recovery through embedding-based shortlisting.

18. **[Agent-as-a-Router: Agentic Model Routing for Coding Tasks](https://arxiv.org/abs/2606.22902)** — arXiv 2026. `coding-router`
    - Uses an agent itself as the router for coding-task model selection.

---

### Workflow Graphs, Runtime Scheduling, Memory, and Optimization

1. **[GPTSwarm: Language Agents as Optimizable Graphs](https://proceedings.mlr.press/v235/zhuge24a.html)** — ICML 2024. `workflow-graph`
   - Core paper for treating agent systems as optimizable computation graphs.

2. **[An LLM Compiler for Parallel Function Calling](https://proceedings.mlr.press/v235/kim24y.html)** — ICML 2024. `DAG-scheduler`
   - Concrete runtime scheduling mechanism for dependency-aware function calls.

3. **[Input Conditioned Graph Generation for Language Agents](https://arxiv.org/abs/2406.11555)** — arXiv 2024. `graph-generation`
   - Generates agent graph structures conditioned on the input task.

4. **[Agent Workflow Memory](https://proceedings.mlr.press/v267/wang25bx.html)** — ICML 2025. `workflow-memory`
   - Induces reusable workflows from successful trajectories and retrieves them for new tasks.

5. **[Unifying Language Agent Algorithms with Graph-based Orchestration Engine for Reproducible Agent Research](https://arxiv.org/abs/2505.24354)** — arXiv 2025. `graph-engine` `reproducibility`
   - Aims to standardize agent algorithm expression through graph orchestration.

6. **[LEGOMem: Modular Procedural Memory for Multi-agent LLM Systems for Workflow Automation](https://arxiv.org/abs/2510.04851)** — arXiv 2025. `procedural-memory`
   - Modularizes reusable procedures for multi-agent workflow automation.

7. **[Toward Reliable Design of LLM-Enabled Agentic Workflows: Optimizing Latency-Reliability-Cost Tradeoffs](https://arxiv.org/abs/2605.23929)** — arXiv 2026. `reliability` `cost-latency`
   - Explicitly models agent workflow design as a multi-objective tradeoff.

8. **[FlowSteer: Interactive Agentic Workflow Orchestration via End-to-End User Feedback](https://arxiv.org/abs/2602.01664)** — arXiv 2026. `interactive-orchestration`
   - Uses user feedback to steer workflow construction and revision.

9. **[Governed Memory: A Production Architecture for Multi-Agent Workflows](https://arxiv.org/abs/2603.17787)** — arXiv 2026. `production-memory`
   - Frames memory governance for production multi-agent workflows.

10. **[TRIAGE: Role-Typed Credit Assignment for Agentic Reinforcement Learning](https://arxiv.org/abs/2606.32017)** — arXiv 2026. `credit-assignment` `agentic-RL`
    - Assigns credit by agent role, relevant for learning orchestration policies.

11. **[When Parallelism Pays Off: Cohesion-Aware Task Partitioning for Multi-Agent Coding](https://arxiv.org/abs/2606.00953)** — arXiv 2026. `graph-partitioning` `parallel-coding`
    - Formalizes multi-agent coding orchestration as graph partitioning over communication and computation tradeoffs.

12. **[Characterizing Large Language Model Agentic Workflows: A Study on N8n Ecosystem](https://arxiv.org/abs/2606.29116)** — arXiv 2026. `workflow-mining` `low-code`
    - Analyzes more than 6,000 public n8n workflows to study real-world agentic workflow structures, routing logic, and reliability gaps.

13. **[When LLMs Develop Languages: Symbolic Communication for Efficient Multi-Agent Reasoning](https://arxiv.org/abs/2606.29354)** — ICML 2026. `communication-router` `token-efficiency`
    - Uses a router to select and compose compact symbolic protocols across multiple reasoning agents.

14. **[QVal: Cheaply Evaluating Dense Supervision Signals for Long-Horizon LLM Agents](https://arxiv.org/abs/2606.32034)** — arXiv 2026. `long-horizon` `supervision`
    - Targets cheaper dense supervision for long-horizon agent execution.

15. **[Generative Skill Composition for LLM Agents](https://arxiv.org/abs/2606.32025)** — arXiv 2026. `skill-composition`
    - Composes reusable skills for agents, adjacent to workflow scheduling.

---

### Recent Agentic Applications and Production Orchestration

1. **[COHORT: Collaborative Orchestration for Hardening via Offensive Replay on Emulated Topologies](https://arxiv.org/abs/2606.30479)** — arXiv 2026. `security` `multi-agent-workflow`
   - Role-decomposed agents propose, implement, critique, and replay-test network hardening actions on emulated enterprise topologies.

2. **[Multi-Agent Orchestration for High-Throughput Materials Screening on a Leadership-Class System](https://arxiv.org/abs/2604.07681)** — arXiv 2026. `scientific-workflow` `HPC`
   - Planner-executor agents partition scientific workloads and coordinate parallel execution through MCP and Parsl on supercomputing infrastructure.

3. **[HearthNet: Edge Multi-Agent Orchestration for Smart Homes](https://arxiv.org/abs/2604.09618)** — arXiv 2026. `edge-orchestration` `smart-home`
   - Keeps orchestration, state management, and device control on-premise while using LLM APIs for inference.

4. **[Characterizing Large Language Model Agentic Workflows: A Study on N8n Ecosystem](https://arxiv.org/abs/2606.29116)** — arXiv 2026. `production-workflows` `low-code`
   - Empirically studies real low-code agentic workflows, including routing logic, tool-use structure, autonomy levels, and reliability mechanisms.

5. **[When Parallelism Pays Off: Cohesion-Aware Task Partitioning for Multi-Agent Coding](https://arxiv.org/abs/2606.00953)** — arXiv 2026. `coding-agent` `parallelism`
   - Builds dependency graphs, partitions work, and schedules parallel coding agents when communication overhead is worth it.

6. **[OpenHands: An Open Platform for AI Software Developers as Generalist Agents](https://arxiv.org/abs/2407.16741)** — ICLR 2025. `software-agent-platform`
   - Open platform with code execution, browser use, sandboxing, multi-agent coordination, and benchmark integration.

---

### Benchmarks and Evaluation

1. **[Mind2Web: Towards a Generalist Agent for the Web](https://arxiv.org/abs/2306.06070)** — NeurIPS 2023 Datasets and Benchmarks. `web-agent`
   - Real websites, diverse domains, and instruction-following trajectories.

2. **[AgentBench: Evaluating LLMs as Agents](https://arxiv.org/abs/2308.03688)** — ICLR 2024. `multi-environment`
   - Evaluates LLM agents across operating systems, databases, web, games, and more.

3. **[GAIA: A Benchmark for General AI Assistants](https://proceedings.iclr.cc/paper_files/paper/2024/hash/25ae35b5b1738d80f1f03a8713e405ec-Abstract-Conference.html)** — ICLR 2024. `general-assistant`
   - Real-world questions requiring reasoning, multimodality, browsing, and tool use.

4. **[WebArena: A Realistic Web Environment for Building Autonomous Agents](https://arxiv.org/abs/2307.13854)** — ICLR 2024. `web-environment`
   - Self-hosted realistic websites and execution-based evaluation.

5. **[VisualWebArena: Evaluating Multimodal Agents on Realistic Visual Web Tasks](https://aclanthology.org/2024.acl-long.50/)** — ACL 2024. `multimodal-web`
   - Adds visual grounding requirements to web-agent tasks.

6. **[SWE-bench: Can Language Models Resolve Real-World GitHub Issues?](https://arxiv.org/abs/2310.06770)** — ICLR 2024. `software-engineering`
   - GitHub issue resolution benchmark with real repositories and tests.

7. **[WorkArena: How Capable Are Web Agents at Solving Common Knowledge Work Tasks?](https://arxiv.org/abs/2403.07718)** — ICML 2024. `knowledge-work` `BrowserGym`
   - ServiceNow-based enterprise-work benchmark plus BrowserGym environment.

8. **[AppWorld: A Controllable World of Apps and People for Benchmarking Interactive Coding Agents](https://aclanthology.org/2024.acl-long.850/)** — ACL 2024. `API-apps` `interactive-coding`
   - Simulated app ecosystem with APIs, users, state-based tests, and collateral-damage checks.

9. **[OSWorld: Benchmarking Multimodal Agents for Open-Ended Tasks in Real Computer Environments](https://arxiv.org/abs/2404.07972)** — NeurIPS 2024 Datasets and Benchmarks. `desktop-agent`
   - Real computer environments across OSes with execution-based grading.

10. **[RouterBench: A Benchmark for Multi-LLM Routing System](https://arxiv.org/abs/2403.12031)** — arXiv 2024. `router-eval`
    - Dedicated benchmark for model-routing systems.

11. **[tau-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains](https://arxiv.org/abs/2406.12045)** — arXiv 2024. `user-simulation` `tool-agent`
    - Tests tool agents in multi-turn interactions with simulated users and policies.

12. **[ToolLLM / ToolBench](https://arxiv.org/abs/2307.16789)** — ICLR 2024. `tool-benchmark`
    - Tool-use dataset and evaluator for large API spaces.

13. **[API-Bank](https://arxiv.org/abs/2304.08244)** — EMNLP 2023. `api-benchmark`
    - Benchmark for API-augmented agents, including tool selection and error recovery.

14. **[AgentBoard: An Analytical Evaluation Board of Multi-turn LLM Agents](https://github.com/hkust-nlp/AgentBoard)** — NeurIPS 2024. `agent-eval`
    - Evaluation board for multi-turn agent tasks and failure analysis.

15. **[MLE-bench: Evaluating Machine Learning Agents on Machine Learning Engineering](https://arxiv.org/abs/2410.07095)** — arXiv 2024. `ML-engineering`
    - Kaggle-derived benchmark for ML engineering agents.

16. **[TheAgentCompany: Benchmarking LLM Agents on Consequential Real World Tasks](https://arxiv.org/abs/2412.14161)** — NeurIPS 2025 Datasets and Benchmarks. `digital-worker`
    - Simulated company environment for browsing, coding, running programs, and coworker communication.

17. **[LLMRouterBench: A Massive Benchmark and Unified Framework for LLM Routing](https://arxiv.org/abs/2601.07206)** — arXiv 2026. `router-benchmark`
    - Large routing benchmark for model-selection research.

18. **[ClawBench: Can AI Agents Complete Everyday Online Tasks?](https://arxiv.org/abs/2604.08523)** — arXiv 2026. `web-agent` `agent-eval`
    - Evaluates the end-to-end model-plus-harness stack on 153 everyday tasks across 144 live sites, with isolated execution and five-layer traces.

---

## Resources

### Frameworks and Platforms

1. **[AutoGen](https://github.com/microsoft/autogen)** — Multi-agent conversation framework.
2. **[LangGraph](https://github.com/langchain-ai/langgraph)** — Graph/state-machine style agent workflow framework.
3. **[LangChain Agents](https://github.com/langchain-ai/langchain)** — Tool-using agent abstractions.
4. **[LlamaIndex Agents](https://github.com/run-llama/llama_index)** — Agent and RAG orchestration utilities.
5. **[Semantic Kernel](https://github.com/microsoft/semantic-kernel)** — Planner, skills, and enterprise orchestration toolkit.
6. **[CrewAI](https://github.com/crewAIInc/crewAI)** — Role-based multi-agent workflow framework.
7. **[MetaGPT](https://github.com/FoundationAgents/MetaGPT)** — SOP-driven multi-agent software company.
8. **[ChatDev](https://github.com/OpenBMB/ChatDev)** — Communicative software-development agents.
9. **[AgentScope](https://github.com/modelscope/agentscope)** — Multi-agent platform from ModelScope.
10. **[OpenHands](https://github.com/All-Hands-AI/OpenHands)** — Open-source software-development agent platform.
11. **[SWE-agent](https://github.com/princeton-nlp/SWE-agent)** — Agent-computer interface for software engineering.
12. **[RouteLLM](https://github.com/lm-sys/RouteLLM)** — Open-source framework for LLM routing.
13. **[RouterBench](https://github.com/withmartian/routerbench)** — Data and code for LLM routing benchmarks.
14. **[ToolBench](https://github.com/OpenBMB/ToolBench)** — Tool-use instruction data and evaluation.
15. **[BrowserGym / WorkArena](https://github.com/ServiceNow/WorkArena)** — Browser-agent environment and knowledge-work tasks.
16. **[WebArena](https://github.com/web-arena-x/webarena)** — Self-hosted web-agent benchmark.
17. **[OSWorld](https://github.com/xlang-ai/OSWorld)** — Desktop-agent benchmark environment.
18. **[Open Agent Relay](https://github.com/ShakespeareLabs/open-agent-relay)** — Local-first capability relay that lets remote teammates or agents invoke restricted Claude Code and Codex workflows while prompts, credentials, dependencies, and working directories remain on the operator's machine.

### Suggested Paper Entry Template

```markdown
1. **[Paper Title](paper-url)** — Venue Year. `tag-1` `tag-2`
   - Orchestration relevance: one sentence explaining which part of the planner/router/scheduler/executor/memory/evaluation stack it addresses.
```

---

## Contributing

Contributions are welcome. Please include:

- Paper title and link, preferably official proceedings or arXiv `/abs/` link.
- Venue/year, or mark as `arXiv` if no formal venue is known.
- One or two tags, such as `model-router`, `tool-use`, `multi-agent`, `workflow-memory`, `benchmark`.
- A short note explaining the orchestration/scheduling relevance.

---

## License

This project is licensed under the [MIT License](LICENSE).
