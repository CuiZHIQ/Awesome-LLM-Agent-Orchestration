# Awesome LLM Agent Orchestration

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Last Updated](https://img.shields.io/badge/Last%20Updated-2026--09--04-blue)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-green)

> A curated research map for **LLM agent scheduling, orchestration, routing, tool dispatch, multi-agent coordination, and workflow optimization**.
>
> Recent papers, benchmarks, and open-source systems for agent routers, orchestration policies, workflow graphs, MCP/tool environments, and routing evaluation.

---

## News

- `2026-09-04`: Added 2026 accepted papers and pruned the list around orchestration, routing, workflow graphs, tool dispatch, and runtime scheduling.
- `2026-07-02`: Refocused the list toward recent orchestra/router work, added 2026 agent-routing and multi-agent-orchestration papers, and switched the public repository to MIT licensing.
- `2026-07-01`: Initial version. Built a taxonomy-first paper list for LLM agent orchestration.

---

## Table of Contents

- [Introduction](#introduction)
- [DeepResearch Taxonomy](#deepresearch-taxonomy)
- [Reading Roadmap](#reading-roadmap)
- [2026 Accepted Papers](#2026-accepted-papers)
- [Fresh 2026 Watchlist](#fresh-2026-watchlist)
- [Papers](#papers)
  - [Surveys, Taxonomies, and Position Papers](#surveys-taxonomies-and-position-papers)
  - [Planning, Control Loops, and Search](#planning-control-loops-and-search)
  - [Tool, API, and Function-Calling Orchestration](#tool-api-and-function-calling-orchestration)
  - [Multi-Agent Collaboration and Team Orchestration](#multi-agent-collaboration-and-team-orchestration)
  - [Model Routing, Agent Routing, Cascades, and MoE Routers](#model-routing-agent-routing-cascades-and-moe-routers)
  - [Workflow Graphs, Runtime Scheduling, Memory, and Optimization](#workflow-graphs-runtime-scheduling-memory-and-optimization)
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

This list stays close to runtime decisions: planning, routing, scheduling, workflow graphs, memory, tool dispatch, and evaluation. General agent papers are left out unless they change one of those decision layers.

## DeepResearch Taxonomy

| Research line | Core scheduling question | Typical mechanisms | Representative papers |
| --- | --- | --- | --- |
| Planning and control loops | How should a goal be decomposed into executable steps and revised from observations? | ReAct loop, plan-and-execute, MCTS, symbolic planners, value-guided search | ReAct, RAP, LLM+P, LATS |
| Tool/API orchestration | When should each tool be called, and how should multi-tool results be composed? | API retrieval, function planner, tool compiler, async/parallel execution | Toolformer, ToolLLM, HuggingGPT, LLMCompiler, AnyTool |
| Model routing | Should a request go to a cheaper model, a stronger model, a specialist model, or a model ensemble? | Cascades, preference routers, uncertainty routers, bandit routers, bi-level routers | RouteLLM, R2-Router, ACE-Router, EvoRoute, VDAR-Router |
| Agent routing and team formation | Which agent should handle each subtask, how should work be divided, and how should agents communicate? | Role assignment, dynamic team selection, debate, committee, graph topology | Conductor, MAS-Orchestra, GraphPlanner, ProgRouter, AgentRouter |
| Workflow graph optimization | How can agent workflow graphs be generated, tuned, reused, and evolved automatically? | Agentic computation graphs, edge optimization, workflow memory, latency-cost-reliability tradeoff | GPTSwarm, Graph-of-Agents, BudgetMem, Gated-Memory Routing, AggAgent |
| Runtime scheduling | How should calls across tools, agents, and models be parallelized, retried, and budgeted? | DAG scheduler, parallel function calls, async function calls, early stop, budget-aware routing | LLMCompiler, AsyncLM, ProgRouter, Budget-Aware Tool Use, INFRAMIND |
| Memory and workflow reuse | How can successful trajectories be stored, retrieved, and turned into better routing decisions? | Episodic memory, workflow induction, procedural memory, gated retrieval | Agent Workflow Memory, BudgetMem, Gated-Memory Routing, LEGOMem |
| Evaluation | How should long-horizon task completion, routing quality, cost, and latency be measured? | Interactive tool environments, execution-based grading, user simulators, router benchmarks | ComplexMCP, MCP-Bench, SwarmBench, LLMRouterBench |

---

## Reading Roadmap

If you only read twelve papers first:

1. **[Learning to Orchestrate Agents in Natural Language with the Conductor](https://arxiv.org/abs/2512.04388)** — ICLR 2026. RL-trained natural-language conductor for topology and prompt orchestration.
2. **[MAS-Orchestra](https://arxiv.org/abs/2601.14652)** — ICML 2026. Holistic multi-agent orchestration as function-calling RL.
3. **[ProgRouter](https://arxiv.org/abs/2608.25992)** — Findings of EMNLP 2026. Online progress-guided agent routing under quality-cost trade-offs.
4. **[GraphPlanner](https://arxiv.org/abs/2604.23626)** — ICLR 2026. Query-specific workflow routing from graph memory.
5. **[Graph-of-Agents](https://arxiv.org/abs/2604.17148)** — ICLR 2026. Graph-based multi-agent communication and aggregation.
6. **[R2-Router](https://arxiv.org/abs/2602.02823)** — ICML 2026. Routing as reasoning over model choice and output-length budget.
7. **[ACE-Router](https://aclanthology.org/2026.acl-long.281/)** — ACL 2026. History-aware routing from MCP tools to the open Agent Web.
8. **[EvoRoute](https://aclanthology.org/2026.acl-long.1771/)** — ACL 2026. Experience-driven self-routing for cost-latency-quality trade-offs.
9. **[Learning What to Retain](https://arxiv.org/abs/2609.00237)** — EMNLP 2026. Gated-memory routing for efficient multi-agent collaboration.
10. **[Budget-Aware Tool Use Enables Effective Agent Scaling](https://arxiv.org/abs/2511.17006)** — COLM 2026. Budget-aware planning and verification for tool-augmented agents.
11. **[MCP-Bench](https://proceedings.iclr.cc/paper_files/paper/2026/hash/9e4b14eb6f16fe7b5818a8d633a0606a-Abstract-Conference.html)** — ICLR 2026. MCP-server benchmark for tool-using agents.
12. **[SwarmBench](https://arxiv.org/abs/2608.30661)** — Findings of EMNLP 2026. Evaluation suite for dynamically orchestrated agent swarms.

---

## 2026 Accepted Papers

| Paper | Venue | Orchestration angle |
| --- | --- | --- |
| **[Learning to Orchestrate Agents in Natural Language with the Conductor](https://arxiv.org/abs/2512.04388)** | ICLR 2026 | Learns a natural-language controller for worker prompts and communication topology. |
| **[DiSRouter: Distributed Self-Routing for LLM Selections](https://arxiv.org/abs/2510.19208)** | ICLR 2026 | Lets LLMs self-route instead of relying on one centralized selector. |
| **[Graph-of-Agents: A Graph-based Framework for Multi-Agent LLM Collaboration](https://arxiv.org/abs/2604.17148)** | ICLR 2026 | Treats collaboration as agent selection, message edges, and pooled responses. |
| **[GraphPlanner: Graph Memory-Augmented Agentic Routing for Multi-Agent LLMs](https://arxiv.org/abs/2604.23626)** | ICLR 2026 | Retrieves graph memory to build query-specific routing workflows. |
| **[TRINITY: An Evolved LLM Coordinator](https://arxiv.org/abs/2512.04695)** | ICLR 2026 | Evolves a compact coordinator for Thinker, Worker, and Verifier teams. |
| **[SLM-MUX: Orchestrating Small Language Models for Reasoning](https://openreview.net/forum?id=317bcKF4zv)** | ICLR 2026 | Picks among small language models with a training-free confidence signal. |
| **[MCP-Bench](https://proceedings.iclr.cc/paper_files/paper/2026/hash/9e4b14eb6f16fe7b5818a8d633a0606a-Abstract-Conference.html)** | ICLR 2026 | Tests tool agents through MCP servers rather than toy API calls. |
| **[MAS-Orchestra](https://arxiv.org/abs/2601.14652)** | ICML 2026 | Generates a full multi-agent system in one function-calling RL step. |
| **[R2-Router](https://arxiv.org/abs/2602.02823)** | ICML 2026 | Routes both model choice and output-length budget. |
| **[BudgetMem](https://arxiv.org/abs/2602.06025)** | ICML 2026 | Routes agent memory across budget tiers at runtime. |
| **[ComplexMCP](https://arxiv.org/abs/2605.10787)** | ICML 2026 | Provides stateful, interdependent MCP tool environments for agent evaluation. |
| **[When LLMs Develop Languages](https://openreview.net/forum?id=ovpL0ujD6j)** | ICML 2026 | Lets a router choose compact symbolic protocols for agent communication. |
| **[AgentRouter](https://aclanthology.org/2026.acl-long.33/)** | ACL 2026 | Routes collaborative QA through a knowledge graph of agent capabilities. |
| **[ACE-Router](https://aclanthology.org/2026.acl-long.281/)** | ACL 2026 | Scales history-aware routing across MCP tools and Agent-Web candidates. |
| **[EvoRoute](https://aclanthology.org/2026.acl-long.1771/)** | ACL 2026 | Reuses experience to choose Pareto-efficient LLM backbones at each step. |
| **[MTRouter](https://aclanthology.org/2026.acl-long.2045/)** | ACL 2026 | Handles model choice in multi-turn trajectories under a cost budget. |
| **[InferenceDynamics](https://aclanthology.org/2026.acl-long.383/)** | ACL 2026 | Profiles model skills so specialized LLM pools can be routed more carefully. |
| **[TRouter](https://aclanthology.org/2026.acl-long.1007/)** | ACL 2026 | Synthesizes task-profile data for cold-start routing. |
| **[LatentGate](https://aclanthology.org/2026.acl-industry.153/)** | ACL 2026 Industry | Adds a low-latency semantic gate for many specialized agents. |
| **[LLMRouterBench](https://aclanthology.org/2026.findings-acl.1881/)** | Findings of ACL 2026 | Gives routing work a large, latency-aware benchmark. |
| **[BiCSRouter](https://aclanthology.org/2026.findings-acl.947/)** | Findings of ACL 2026 | Switches between single-agent and multi-agent execution. |
| **[RouterHGC](https://aclanthology.org/2026.findings-acl.1589/)** | Findings of ACL 2026 | Models MAS routing as a heterogeneous graph problem. |
| **[How Robust Are Router-LLMs?](https://aclanthology.org/2026.eacl-long.351/)** | EACL 2026 | Stress-tests routers under task, privacy, and safety shifts. |
| **[GMTRouter](https://arxiv.org/abs/2511.08590)** | Findings of EMNLP 2026 | Personalizes routing from multi-turn interaction graphs. |
| **[Learning What to Retain: Gated-Memory Routing for Efficient Collaboration in Multi-Agent LLM Systems](https://arxiv.org/abs/2609.00237)** | EMNLP 2026 | Uses gated execution memory for role, backbone, and halting decisions. |
| **[ProgRouter](https://arxiv.org/abs/2608.25992)** | Findings of EMNLP 2026 | Routes online from progress, remaining difficulty, time, and cost. |
| **[SwarmBench](https://arxiv.org/abs/2608.30661)** | Findings of EMNLP 2026 | Evaluates LLMs as orchestrators of dynamic agent swarms. |
| **[VDAR-Router](https://arxiv.org/abs/2607.18098)** | Findings of EMNLP 2026 | Retrieves difficulty profiles for training-free model routing. |
| **[Calibration is the Bottleneck](https://arxiv.org/abs/2609.00949)** | Findings of EMNLP 2026 | Separates action-choice calibration from execution failure in multi-turn tool calls. |
| **[FlexRouter](https://research.adobe.com/publication/flexrouter-learning-complementary-model-sets-for-flexible-llm-routing/)** | COLM 2026 | Routes to complementary model sets instead of one best model. |
| **[Routesplain](https://arxiv.org/abs/2511.09373)** | COLM 2026 | Makes software-task routing explainable and editable. |
| **[Agentic Aggregation for Parallel Scaling of Long-Horizon Agentic Tasks](https://arxiv.org/abs/2604.11753)** | COLM 2026 | Aggregates parallel long-horizon agent rollouts with an inspection agent. |
| **[Budget-Aware Tool Use Enables Effective Agent Scaling](https://arxiv.org/abs/2511.17006)** | COLM 2026 | Gives tool agents a live budget signal and changes behavior under constraints. |
| **[StateBridge](https://arxiv.org/abs/2608.13317)** | COLM 2026 | Passes aligned hidden states between agents as a latent communication channel. |
| **[Meta-Harness](https://arxiv.org/abs/2603.28052)** | COLM 2026 | Searches over the harness code that stores, retrieves, and presents context. |
| **[OFA-MAS](https://dl.acm.org/doi/10.1145/3774904.3792537)** | WWW 2026 | Generates adaptive multi-agent collaboration graphs. |
| **[Assemble Your Crew](https://github.com/Shiy-Li/ARG-Designer)** | AAAI 2026 Oral | Designs communication topology through autoregressive graph generation. |

---

## Fresh 2026 Watchlist

| Paper | Status | Why track it |
| --- | --- | --- |
| **[Codebook Agent: Amortized Topology Design for LLM Multi-Agent Systems](https://arxiv.org/abs/2609.02264)** | arXiv 2026 | Compresses successful MAS topologies into a small codebook and routes queries to decoded communication graphs. |
| **[The Differential Reasoning Router](https://arxiv.org/abs/2608.30224)** | arXiv 2026 | Jointly routes between direct reasoning, expensive reasoning, and human escalation in production-style annotation. |
| **[Uno-Orchestra: Parsimonious Agent Routing via Selective Delegation](https://arxiv.org/abs/2605.05007)** | arXiv 2026 | Studies when not to delegate, a practical counterweight to always-on multi-agent orchestration. |
| **[Agent-as-a-Router: Agentic Model Routing for Coding Tasks](https://arxiv.org/abs/2606.22902)** | arXiv 2026 | Uses an agent as the router for coding-task model selection. |
| **[INFRAMIND: Infrastructure-Aware Multi-Agent Orchestration](https://arxiv.org/abs/2606.11440)** | arXiv 2026 | Couples planner/router/scheduler decisions to real-time infrastructure state. |
| **[LEMON](https://arxiv.org/abs/2605.14483)** | arXiv 2026 | Learns executable orchestration specs through counterfactual reinforcement learning. |
| **[Scaling Enterprise Agent Routing](https://arxiv.org/abs/2606.17519)** | arXiv 2026 | Studies routing degradation, diagnosis, and recovery in a large production-style agent/tool catalog. |
| **[The Workload-Router-Pool Architecture](https://arxiv.org/abs/2603.21354)** | arXiv 2026 | Frames LLM serving as workload-aware routing across model pools. |
| **[Accuracy Is Speed](https://arxiv.org/abs/2604.15732)** | arXiv 2026 | Shows why long-context serving routers should treat accuracy as part of latency. |

---

## Papers

### Surveys, Taxonomies, and Position Papers

1. **[A Survey of Task Planning with Large Language Models](https://spj.science.org/doi/10.34133/icomputing.0124)** — iComputing 2025. `survey` `planning`
   - Useful for separating natural-language planning, symbolic planning, and LLM-modulo planning.

2. **[The Orchestration of Multi-Agent Systems: Architectures, Protocols, and Communication](https://arxiv.org/abs/2601.13671)** — arXiv 2026. `survey` `multi-agent-orchestration`
   - Covers orchestration layers, communication protocols, and coordination architectures.

3. **[LLM-Based Multi-Agent Orchestration: A Survey of Frameworks, Patterns, and Challenges](https://www.mdpi.com/1999-5903/18/6/326)** — Future Internet 2026. `survey` `frameworks`
   - Surveys multi-agent orchestration patterns, production concerns, and evaluation methods.

4. **[From Static Templates to Dynamic Runtime Graphs: A Survey of Workflow Optimization for LLM Agents](https://arxiv.org/abs/2603.22386)** — arXiv 2026. `survey` `workflow-optimization`
   - Treats agent workflows as computation graphs and groups the main optimization methods.

---

### Planning, Control Loops, and Search

1. **[ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629)** — ICLR 2023. `plan-act-observe`
   - The canonical loop for interleaving reasoning, environment action, and observation.

2. **[Reasoning with Language Model is Planning with World Model](https://aclanthology.org/2023.emnlp-main.507/)** — EMNLP 2023. `RAP` `world-model` `MCTS`
   - Uses an LLM as both world model and reasoning agent, with MCTS-style planning.

3. **[LLM+P: Empowering Large Language Models with Optimal Planning Proficiency](https://arxiv.org/abs/2304.11477)** — arXiv 2023. `symbolic-planner` `PDDL`
    - Routes natural-language planning problems through classical planners.

4. **[Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models](https://proceedings.mlr.press/v235/zhou24r.html)** — ICML 2024. `LATS` `agent-search`
    - Integrates reasoning, acting, planning, value estimation, and reflection.

5. **[Planning with Language Models Through the Lens of Efficiency](https://proceedings.neurips.cc/paper_files/paper/2024/hash/fa080fe0f218871faec1d8ba20e491d5-Abstract-Conference.html)** — NeurIPS 2024. `planning` `efficiency`
    - Analyzes when planning with LMs is computationally efficient.

6. **[Position: LLMs Can't Plan, But Can Help Planning in LLM-Modulo Frameworks](https://arxiv.org/abs/2402.01817)** — ICML 2024. `position` `LLM-modulo`
    - Argues for routing LLMs into planner/verifier/tool modules rather than relying on pure generation.

---

### Tool, API, and Function-Calling Orchestration

1. **[Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761)** — NeurIPS 2023. `tool-use`
   - Learns when to call tools, what arguments to pass, and how to consume results.

2. **[ART: Automatic Multi-Step Reasoning and Tool-Use for Large Language Models](https://arxiv.org/abs/2303.09014)** — arXiv 2023. `tool-chain`
   - Builds multi-step tool-use trajectories from task demonstrations.

3. **[HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face](https://arxiv.org/abs/2303.17580)** — NeurIPS 2023. `model-dispatch` `controller`
   - LLM controller plans subtasks, selects Hugging Face models, executes, and summarizes.

4. **[Chameleon: Plug-and-Play Compositional Reasoning with Large Language Models](https://arxiv.org/abs/2304.09842)** — NeurIPS 2023. `tool-selection` `compositional`
   - Selects and composes tools/modules for multimodal reasoning.

5. **[RESTGPT: Connecting Large Language Models with Real-World RESTful APIs](https://arxiv.org/abs/2306.06624)** — arXiv 2023. `REST` `api-agent`
    - Plans and executes REST API calls from OpenAPI-style documentation.

6. **[ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs](https://arxiv.org/abs/2307.16789)** — ICLR 2024. `ToolBench` `API-routing`
    - Large-scale API dataset, retriever, tool-use model, and evaluation pipeline.

7. **[AnyTool: Self-Reflective, Hierarchical Agents for Large-Scale API Calls](https://proceedings.mlr.press/v235/du24h.html)** — ICML 2024. `hierarchical-router` `API`
    - Hierarchical API retrieval plus self-reflection for large API spaces.

8. **[An LLM Compiler for Parallel Function Calling](https://proceedings.mlr.press/v235/kim24y.html)** — ICML 2024. `parallel-function-calling` `DAG`
    - Builds a function-call plan, fetches ready tasks, and executes independent calls in parallel.

9. **[An LLM-Tool Compiler for Fused Parallel Function Calling](https://arxiv.org/abs/2405.17438)** — arXiv 2024. `tool-compiler`
    - Extends compiler-style function orchestration with fused parallel calls.

10. **[Asynchronous LLM Function Calling](https://arxiv.org/abs/2412.07017)** — arXiv 2024. `async` `runtime`
    - Enables LLMs to generate and execute function calls concurrently.

11. **[Budget-Aware Tool Use Enables Effective Agent Scaling](https://arxiv.org/abs/2511.17006)** — COLM 2026. `budget-aware` `tool-use`
    - Gives tool-augmented agents continuous budget awareness and adapts planning and verification under tool-call constraints.

---

### Multi-Agent Collaboration and Team Orchestration

**Recent accepted work**

| Paper | Venue | Focus |
| --- | --- | --- |
| **[Learning to Orchestrate Agents in Natural Language with the Conductor](https://arxiv.org/abs/2512.04388)** | ICLR 2026 | RL-trained natural-language conductor that writes worker prompts and communication topology. |
| **[MAS-Orchestra](https://arxiv.org/abs/2601.14652)** | ICML 2026 | Holistic function-calling RL for generating complete multi-agent systems. |
| **[ProgRouter](https://arxiv.org/abs/2608.25992)** | Findings of EMNLP 2026 | Online progress-aware routing across multi-agent workflow steps. |
| **[Learning What to Retain](https://arxiv.org/abs/2609.00237)** | EMNLP 2026 | Gated memory routing for role, backbone, and halting decisions during collaboration. |
| **[Graph-of-Agents](https://arxiv.org/abs/2604.17148)** | ICLR 2026 | Graph-based agent selection, edge construction, message passing, and response pooling. |
| **[GraphPlanner](https://arxiv.org/abs/2604.23626)** | ICLR 2026 | Graph-memory-augmented routing workflow generation for multi-agent LLMs. |
| **[OFA-MAS](https://dl.acm.org/doi/10.1145/3774904.3792537)** | WWW 2026 | One-for-all adaptive topology generation for cross-domain MAS tasks. |
| **[Assemble Your Crew](https://github.com/Shiy-Li/ARG-Designer)** | AAAI 2026 Oral | Autoregressive graph generation for automatic communication-topology design. |
| **[TRINITY](https://arxiv.org/abs/2512.04695)** | ICLR 2026 | Evolved coordinator for Thinker, Worker, and Verifier collaboration. |
| **[Agentic Aggregation for Parallel Scaling of Long-Horizon Agentic Tasks](https://arxiv.org/abs/2604.11753)** | COLM 2026 | Aggregation agent for parallel long-horizon rollouts in search and deep research. |
| **[StateBridge](https://arxiv.org/abs/2608.13317)** | COLM 2026 | Training-free latent communication channel between LLM agents. |

**Earlier related work**

1. **[AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation](https://arxiv.org/abs/2308.08155)** — arXiv 2023. `framework` `conversation-programming`
   - General framework for composing conversable agents, tools, code, and humans.

2. **[AgentVerse: Facilitating Multi-Agent Collaboration and Exploring Emergent Behaviors](https://arxiv.org/abs/2308.10848)** — ICLR 2024. `team-recruitment` `collaboration`
   - Expert recruitment, collaborative decision-making, action execution, and evaluation.

3. **[MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework](https://arxiv.org/abs/2308.00352)** — ICLR 2024 Oral. `SOP` `software-team`
   - Encodes standard operating procedures into role-based agent workflows.

4. **[ChatDev: Communicative Agents for Software Development](https://aclanthology.org/2024.acl-long.810/)** — ACL 2024. `software-dev` `chat-chain`
   - Uses specialized agents and chat chains for design, coding, testing, and documentation.

5. **[Dynamic LLM-Agent Network: An LLM-agent Collaboration Framework with Agent Team Optimization](https://arxiv.org/abs/2310.02170)** — arXiv 2023 / OpenReview. `dynamic-team` `agent-selection`
   - Selects useful agents and dynamically adjusts communication structure.

6. **[GPTSwarm: Language Agents as Optimizable Graphs](https://proceedings.mlr.press/v235/zhuge24a.html)** — ICML 2024 Oral. `agent-graph` `edge-optimization`
   - Represents agents and societies as graphs and optimizes node prompts and edges.

7. **[Mixture-of-Agents Enhances Large Language Model Capabilities](https://arxiv.org/abs/2406.04692)** — ICLR 2025. `agent-ensemble` `layered-collaboration`
    - Uses layered agents where later agents synthesize previous agents' outputs.

8. **[Magentic-One: A Generalist Multi-Agent System for Solving Complex Tasks](https://arxiv.org/abs/2411.04468)** — arXiv 2024. `generalist-agent` `manager-worker`
    - Manager coordinates specialized agents for browsing, coding, file operations, and terminal work.

9. **[AgentOrchestra: A Hierarchical Multi-Agent Framework for General-Purpose Task Solving](https://arxiv.org/abs/2506.12508)** — arXiv 2025. `hierarchical` `orchestration`
    - High-level planner coordinates modular specialist agents.

10. **[Multi-Agent Collaboration via Evolving Orchestration](https://arxiv.org/abs/2505.19591)** — arXiv 2025. `evolutionary-orchestration`
    - Studies automatic evolution of multi-agent collaboration patterns.

11. **[Difficulty-Aware Agentic Orchestration for Query-Specific Multi-Agent Workflows](https://arxiv.org/abs/2509.11079)** — arXiv 2025. `difficulty-aware` `query-routing`
    - Adapts the agent workflow to query difficulty.

12. **[Learning Latency-Aware Orchestration for Parallel Multi-Agent Systems](https://arxiv.org/abs/2601.10560)** — arXiv 2026. `latency-aware` `parallel-agents`
    - Optimizes orchestration under latency constraints.

13. **[Multi-Agent Coordination Adaptation via Structure-Guided Orchestration](https://arxiv.org/abs/2605.25746)** — arXiv 2026. `structure-guided` `coordination`
    - Adapts coordination structure instead of using fixed communication graphs.

14. **[Reward Modeling for Multi-Agent Orchestration](https://arxiv.org/abs/2606.13598)** — arXiv 2026. `reward-model` `orchestration`
    - Uses reward modeling to guide multi-agent orchestration decisions.

15. **[PerspectiveGap: A Benchmark for Multi-Agent Orchestration Prompting](https://arxiv.org/abs/2606.08878)** — arXiv 2026. `benchmark` `prompting`
    - Tests prompt-level orchestration of agents with different perspectives.

16. **[LEMON: Learning Executable Multi-Agent Orchestration via Counterfactual Reinforcement Learning](https://arxiv.org/abs/2605.14483)** — arXiv 2026. `counterfactual-RL` `orchestration-policy`
    - Learns role design, capacity assignment, and dependency structure as a single executable orchestration specification.

17. **[INFRAMIND: Infrastructure-Aware Multi-Agent Orchestration](https://arxiv.org/abs/2606.11440)** — arXiv 2026. `infra-aware` `planner-router-scheduler`
    - Conditions topology, role selection, model calls, and queue scheduling on real-time infrastructure state.

---

### Model Routing, Agent Routing, Cascades, and MoE Routers

**Recent accepted work**

| Paper | Venue | Focus |
| --- | --- | --- |
| **[R2-Router](https://arxiv.org/abs/2602.02823)** | ICML 2026 | Jointly routes over model choice and output-length budget. |
| **[ACE-Router](https://aclanthology.org/2026.acl-long.281/)** | ACL 2026 | History-aware routing from MCP tools to open Agent-Web ecosystems. |
| **[EvoRoute](https://aclanthology.org/2026.acl-long.1771/)** | ACL 2026 | Experience-driven model routing at each agent step. |
| **[AgentRouter](https://aclanthology.org/2026.acl-long.33/)** | ACL 2026 | Knowledge-graph-guided routing for collaborative multi-agent QA. |
| **[MTRouter](https://aclanthology.org/2026.acl-long.2045/)** | ACL 2026 | Cost-aware multi-turn routing with history-model embeddings. |
| **[InferenceDynamics](https://aclanthology.org/2026.acl-long.383/)** | ACL 2026 | Capability and knowledge profiling for specialized model pools. |
| **[TRouter](https://aclanthology.org/2026.acl-long.1007/)** | ACL 2026 | Task-profile-guided data synthesis for cold-start routing. |
| **[BiCSRouter](https://aclanthology.org/2026.findings-acl.947/)** | Findings of ACL 2026 | Bi-level routing across single-agent and multi-agent regimes. |
| **[RouterHGC](https://aclanthology.org/2026.findings-acl.1589/)** | Findings of ACL 2026 | Heterogeneous graph contrastive learning for MAS routing. |
| **[LatentGate](https://aclanthology.org/2026.acl-industry.153/)** | ACL 2026 Industry | Low-latency semantic routing for hundreds of specialized agents. |
| **[LLMRouterBench](https://aclanthology.org/2026.findings-acl.1881/)** | Findings of ACL 2026 | Unified 400K-instance benchmark for LLM routing. |
| **[GMTRouter](https://arxiv.org/abs/2511.08590)** | Findings of EMNLP 2026 | Personalized routing over multi-turn user interactions. |
| **[ProgRouter](https://arxiv.org/abs/2608.25992)** | Findings of EMNLP 2026 | Online progress-guided routing across multi-agent workflow steps. |
| **[Learning What to Retain](https://arxiv.org/abs/2609.00237)** | EMNLP 2026 | Gated memory routing for role and backbone selection under execution-history overload. |
| **[VDAR-Router](https://arxiv.org/abs/2607.18098)** | Findings of EMNLP 2026 | Difficulty-aware retrieval-based routing with explicit query analysis. |
| **[FlexRouter](https://research.adobe.com/publication/flexrouter-learning-complementary-model-sets-for-flexible-llm-routing/)** | COLM 2026 | Routes to complementary model sets rather than a single model. |
| **[Routesplain](https://arxiv.org/abs/2511.09373)** | COLM 2026 | Faithful, intervenable routing for software-related tasks. |
| **[DiSRouter](https://arxiv.org/abs/2510.19208)** | ICLR 2026 | Distributed self-routing with self-aware LLM agents. |
| **[GraphPlanner](https://arxiv.org/abs/2604.23626)** | ICLR 2026 | Graph-memory-augmented agentic routing workflow generation. |
| **[SLM-MUX](https://openreview.net/forum?id=317bcKF4zv)** | ICLR 2026 | Training-free routing among small language models. |
| **[How Robust Are Router-LLMs?](https://aclanthology.org/2026.eacl-long.351/)** | EACL 2026 | Robustness benchmark for preference-data and commercial routers. |

**Earlier related work**

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

8. **[LLMRouterBench: A Massive Benchmark and Unified Framework for LLM Routing](https://aclanthology.org/2026.findings-acl.1881/)** — Findings of ACL 2026. `routing-benchmark`
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

**Recent accepted work**

| Paper | Venue | Focus |
| --- | --- | --- |
| **[GraphPlanner](https://arxiv.org/abs/2604.23626)** | ICLR 2026 | Generates multi-agent routing workflows from graph memory. |
| **[Graph-of-Agents](https://arxiv.org/abs/2604.17148)** | ICLR 2026 | Uses graph structure for selective activation, message passing, and pooling. |
| **[ProgRouter](https://arxiv.org/abs/2608.25992)** | Findings of EMNLP 2026 | Online, state-dependent routing for long-horizon multi-agent workflows. |
| **[Learning What to Retain](https://arxiv.org/abs/2609.00237)** | EMNLP 2026 | Learned write/retrieval gates and adaptive halting for compact workflow state. |
| **[OFA-MAS](https://dl.acm.org/doi/10.1145/3774904.3792537)** | WWW 2026 | Learns adaptive MAS topology design with MoE graph generative models. |
| **[Assemble Your Crew](https://github.com/Shiy-Li/ARG-Designer)** | AAAI 2026 Oral | Automatically generates multi-agent communication graphs. |
| **[Learning to Orchestrate Agents in Natural Language with the Conductor](https://arxiv.org/abs/2512.04388)** | ICLR 2026 | Learns natural-language workflow construction over arbitrary worker pools. |
| **[BudgetMem](https://arxiv.org/abs/2602.06025)** | ICML 2026 | Query-aware budget-tier routing for runtime agent memory. |
| **[When LLMs Develop Languages](https://openreview.net/forum?id=ovpL0ujD6j)** | ICML 2026 | Router-selected symbolic protocols for efficient multi-agent communication. |
| **[Agentic Aggregation for Parallel Scaling of Long-Horizon Agentic Tasks](https://arxiv.org/abs/2604.11753)** | COLM 2026 | Interactive aggregation over multiple parallel long-horizon trajectories. |
| **[Budget-Aware Tool Use Enables Effective Agent Scaling](https://arxiv.org/abs/2511.17006)** | COLM 2026 | Runtime budget tracker and adaptive test-time scaling for tool-augmented agents. |
| **[StateBridge](https://arxiv.org/abs/2608.13317)** | COLM 2026 | Hidden-state alignment for training-free latent agent communication. |
| **[Meta-Harness](https://arxiv.org/abs/2603.28052)** | COLM 2026 | Outer-loop optimization over context, retrieval, and harness code for agent systems. |

**Earlier related work**

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

---

### Benchmarks and Evaluation

**Recent accepted work**

| Paper | Venue | Focus |
| --- | --- | --- |
| **[ComplexMCP](https://arxiv.org/abs/2605.10787)** | ICML 2026 | Dynamic, interdependent, large-scale MCP tool sandbox for agents. |
| **[MCP-Bench](https://proceedings.iclr.cc/paper_files/paper/2026/hash/9e4b14eb6f16fe7b5818a8d633a0606a-Abstract-Conference.html)** | ICLR 2026 | Complex real-world MCP-server tasks for tool-using LLM agents. |
| **[LLMRouterBench](https://aclanthology.org/2026.findings-acl.1881/)** | Findings of ACL 2026 | Unified benchmark for performance, cost, and latency-aware LLM routing. |
| **[SwarmBench](https://arxiv.org/abs/2608.30661)** | Findings of EMNLP 2026 | Evaluates accuracy, efficiency, cost, and process quality for agent-swarm orchestration. |
| **[Calibration is the Bottleneck](https://arxiv.org/abs/2609.00949)** | Findings of EMNLP 2026 | Action-class diagnostic for multi-turn tool-calling and agent calibration failures. |
| **[How Robust Are Router-LLMs?](https://aclanthology.org/2026.eacl-long.351/)** | EACL 2026 | Tests routing fragility across task categories and safety-sensitive settings. |

**Earlier related work**

1. **[AppWorld: A Controllable World of Apps and People for Benchmarking Interactive Coding Agents](https://aclanthology.org/2024.acl-long.850/)** — ACL 2024. `API-apps` `interactive-coding`
   - Simulated app ecosystem with APIs, users, state-based tests, and collateral-damage checks.

2. **[RouterBench: A Benchmark for Multi-LLM Routing System](https://arxiv.org/abs/2403.12031)** — arXiv 2024. `router-eval`
    - Dedicated benchmark for model-routing systems.

3. **[tau-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains](https://arxiv.org/abs/2406.12045)** — arXiv 2024. `user-simulation` `tool-agent`
    - Tests tool agents in multi-turn interactions with simulated users and policies.

4. **[ToolLLM / ToolBench](https://arxiv.org/abs/2307.16789)** — ICLR 2024. `tool-benchmark`
    - Tool-use dataset and evaluator for large API spaces.

5. **[API-Bank](https://arxiv.org/abs/2304.08244)** — EMNLP 2023. `api-benchmark`
    - Benchmark for API-augmented agents, including tool selection and error recovery.

6. **[AgentBoard: An Analytical Evaluation Board of Multi-turn LLM Agents](https://github.com/hkust-nlp/AgentBoard)** — NeurIPS 2024. `agent-eval`
    - Evaluation board for multi-turn agent tasks and failure analysis.

7. **[LLMRouterBench: A Massive Benchmark and Unified Framework for LLM Routing](https://aclanthology.org/2026.findings-acl.1881/)** — Findings of ACL 2026. `router-benchmark`
    - Large routing benchmark for model-selection research.

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
10. **[RouteLLM](https://github.com/lm-sys/RouteLLM)** — Open-source framework for LLM routing.
11. **[RouterBench](https://github.com/withmartian/routerbench)** — Data and code for LLM routing benchmarks.
12. **[ACE-Router](https://github.com/euyis1019/ACE-Router)** — History-aware routing for MCP tools and Agent-Web-style ecosystems.
13. **[Graph-of-Agents](https://github.com/UNITES-Lab/GoA)** — Graph-based multi-agent communication and aggregation.
14. **[GraphPlanner](https://github.com/ulab-uiuc/GraphPlanner)** — Graph-memory-augmented agentic routing for multi-agent LLMs.
15. **[BudgetMem](https://github.com/ViktorAxelsen/BudgetMem)** — Budget-tier routing for runtime agent memory.
16. **[SLM-MUX](https://github.com/slm-mux/SLM-MUX)** — Training-free routing across small language models.
17. **[GMTRouter](https://github.com/ulab-uiuc/GMTRouter)** — Personalized LLM routing over multi-turn user interactions.
18. **[Gated-Memory Routing](https://github.com/rajibrhasan/gated-memory-routing)** — Memory-gated routing for efficient multi-agent collaboration.
19. **[Budget-Aware Agent](https://github.com/google-research/budget-aware-agent)** — Budget tracker and budget-aware test-time scaling for tool-use agents.
20. **[Tool-Calling Calibration](https://github.com/fbj2333/tool-calling-calibration)** — Multi-turn tool-calling action-class diagnostic.
21. **[MCP-Bench](https://github.com/Accenture/mcp-bench)** — MCP-server benchmark for complex tool-using agents.
22. **[ComplexMCP](https://github.com/ATH-MaaS/complex-mcp)** — Dynamic, interdependent, large-scale MCP tool sandbox.
23. **[ToolBench](https://github.com/OpenBMB/ToolBench)** — Tool-use instruction data and evaluation.

### Suggested Paper Entry Template

```markdown
1. **[Paper Title](paper-url)** — Venue Year. `tag-1` `tag-2`
   - Orchestration relevance: one sentence explaining which part of the planner/router/scheduler/executor/memory/evaluation stack it addresses.
```

---

## Contributing

Contributions are welcome. Please include:

- Paper title and link, preferably official proceedings or arXiv `/abs/` link.
- Venue/year in the same style as existing entries.
- One or two tags, such as `model-router`, `tool-use`, `multi-agent`, `workflow-memory`, `benchmark`.
- A short note explaining the orchestration/scheduling relevance.

---

## License

This project is licensed under the [MIT License](LICENSE).
