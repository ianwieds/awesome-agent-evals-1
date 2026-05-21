# Awesome Agent Evals [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of evaluation resources for AI agents — platforms, open-source frameworks, benchmarks, and methodology.

Strong evals are what separate a viral demo from a production agent. The compounding nature of tool calls makes agent evaluation fundamentally harder than single-turn LLM eval, and the ecosystem is fragmenting fast. This list aims to be a *tightly curated* — not exhaustive — entry point.

## Contents

- [Mental Model](#mental-model)
- [Evaluation Platforms](#evaluation-platforms)
- [Open-Source Eval Libraries](#open-source-eval-libraries)
- [Agent Benchmarks](#agent-benchmarks)
  - [Coding Agents](#coding-agents)
  - [Web / Browser Agents](#web--browser-agents)
  - [Computer-Use / OS Agents](#computer-use--os-agents)
  - [Tool-Use & Function-Calling](#tool-use--function-calling)
  - [Conversational / Customer-Service Agents](#conversational--customer-service-agents)
  - [Research / Deep-Research Agents](#research--deep-research-agents)
  - [General / Multi-Domain](#general--multi-domain)
- [Grader Patterns](#grader-patterns)
- [Reading & Methodology](#reading--methodology)
- [Related Lists](#related-lists)
- [Contributing](#contributing)
- [License](#license)

## Mental Model

A scanning lens for the entries below.

**Eval depth**
- *Single-turn* — prompt → response → grade.
- *Multi-turn* — span several turns; state carries across.
- *Agentic* — tool calls compound errors across many turns; small slips become big failures.

**Grader types**
- *Code-based* — fast, deterministic, cheap; brittle to valid variations. (string match, exec tests, state checks)
- *Model-based* (LLM-as-judge) — flexible, scalable; non-deterministic and biased without calibration.
- *Human* — gold standard; slow and expensive. Reserve for calibration sets and final QA.

**Reliability metrics**
- `pass@k` — succeeds at least once in *k* attempts. Useful for capability ceilings.
- `pass^k` — succeeds in *all* *k* attempts. The metric production agents actually need.

## Evaluation Platforms

Hosted/SaaS platforms (some with open-source cores) for tracing, dataset management, and running evals at scale.

- [LangSmith](https://www.langchain.com/langsmith) — Tracing + datasets + LLM-as-judge eval; tight LangChain/LangGraph integration.
- [Langfuse](https://github.com/langfuse/langfuse) — Open-source LLM observability + eval (MIT).
- [Braintrust](https://www.braintrust.dev/) — Eval-first dev loop; strong dataset + experiment UX.
- [Arize Phoenix](https://github.com/Arize-ai/phoenix) — Open-source tracing + evals; OpenTelemetry-native.
- [Patronus AI](https://www.patronus.ai/) — Automated LLM/agent eval + red-teaming.
- [Helicone](https://github.com/Helicone/helicone) — Open-source LLM observability with eval hooks.
- [Agenta](https://github.com/Agenta-AI/agenta) — Open-source LLMOps: prompt mgmt + eval + observability.
- [AgentOps](https://github.com/AgentOps-AI/agentops) — Agent-specific tracing + replay + cost/quality eval.

## Open-Source Eval Libraries

Code-first frameworks you drop into a repo and run in CI.

- [Harbor](https://github.com/harbor-framework/harbor) — Containerized agent-eval framework; runs trials at scale across cloud providers (Daytona, Modal). Hosts the Terminal-Bench 2.0 registry.
- [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) — UK AISI's eval framework; the de-facto choice for frontier-model + agent safety evals.
- [agentevals](https://github.com/langchain-ai/agentevals) — Ready-made trajectory evaluators for agents.
- [Strands Evals](https://github.com/strands-agents/evals) — Multi-agent interaction analysis + automated experiment generation.
- [AWS Agent Evaluation](https://github.com/awslabs/agent-evaluation) — Generative-AI-powered framework for testing virtual agents.
- [DeepEval](https://github.com/confident-ai/deepeval) — Pytest-style; agent-specific metrics (task completion, tool correctness) on top of general LLM metrics.
- [Promptfoo](https://github.com/promptfoo/promptfoo) — CI-friendly prompt/agent evals + red-teaming.
- [OpenAI Evals](https://github.com/openai/evals) — Reference framework + open eval registry; broader than agents but agent-capable.
- [Ragas](https://github.com/explodinggradients/ragas) — RAG metrics; useful when the agent's quality is bottlenecked by retrieval.
- [TruLens](https://github.com/truera/trulens) — Feedback functions over LLM/agent traces.

## Agent Benchmarks

### Coding Agents
- [SWE-bench / SWE-bench Verified](https://www.swebench.com/) — Resolve real GitHub issues end-to-end. The standard.
- [Terminal-Bench](https://www.tbench.ai/) — Agents operating a real shell across multi-step tasks; v2 ships via Harbor.
- [LoCoBench-Agent](https://arxiv.org/abs/2511.13998) — Long-context software engineering in an interactive setting.

### Web / Browser Agents
- [WebArena](https://webarena.dev/) — Realistic self-hosted web environments (e-commerce, GitLab, Reddit clone).
- [VisualWebArena](https://jykoh.com/vwa) — Multimodal extension of WebArena.
- [BrowserGym](https://github.com/ServiceNow/BrowserGym) — Gym-style toolkit for browser agents; common substrate.
- [AgentLab](https://github.com/ServiceNow/AgentLab) — ServiceNow's dev+eval framework atop BrowserGym.
- [Mind2Web](https://github.com/OSU-NLP-Group/Mind2Web) — Generalist web agent benchmark.
- [WebVoyager](https://github.com/MinorJerry/WebVoyager) — Live-website multimodal agent eval.

### Computer-Use / OS Agents
- [OSWorld](https://os-world.github.io/) — Multimodal benchmark for desktop computer-use agents.
- [WindowsAgentArena](https://github.com/microsoft/WindowsAgentArena) — Windows-focused computer-use eval.
- [Android in the Wild (AitW)](https://github.com/google-research/google-research/tree/master/android_in_the_wild) — Mobile UI control.
- [AndroidWorld](https://github.com/google-research/android_world) — Reproducible Android benchmark.

### Tool-Use & Function-Calling
- [Berkeley Function-Calling Leaderboard (BFCL)](https://gorilla.cs.berkeley.edu/leaderboard.html) — The reference tool-use leaderboard.
- [ToolBench](https://github.com/OpenBMB/ToolBench) — 16k+ real-world API tasks.
- [API-Bank](https://github.com/AlibabaResearch/DAMO-ConvAI/tree/main/api-bank) — Tool-augmented LLM eval.
- [MCPEval](https://arxiv.org/abs/2507.12806) — MCP-based automated task generation + deep eval.
- [τ-bench / τ²-bench](https://arxiv.org/abs/2406.12045) — Customer-service-with-tools benchmark; multi-turn, policy-bound.

### Conversational / Customer-Service Agents
- [τ-bench / τ²-bench](https://arxiv.org/abs/2406.12045) — Sierra's go-to benchmark for conversational tool-use agents; policy-bound, dual-control.

### Research / Deep-Research Agents
- [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) — General-assistant benchmark; multi-step research with tools.
- [BrowseComp](https://openai.com/index/browsecomp/) — Hard browsing/research questions for autonomous browsing agents.

### General / Multi-Domain
- [AgentBench](https://github.com/THUDM/AgentBench) — 8 environments covering OS, DB, web, code, games.
- [AgentBoard](https://github.com/hkust-nlp/AgentBoard) — Fine-grained progress-rate metric across domains.
- [AgentQuest](https://arxiv.org/abs/2404.06411) — Modular framework for measuring agent progress.

## Grader Patterns

| Grader | Strengths | Weaknesses | Best For |
|---|---|---|---|
| Code-based | Fast, deterministic, free | Brittle to valid variations | Test execution, structured outputs, state checks |
| Model-based (LLM-as-judge) | Flexible, handles open text | Non-deterministic, biased, costly | Quality, tone, groundedness, rubric scoring |
| Human | Gold-standard | Slow, expensive, doesn't scale | Calibration sets, sensitive domains, final QA |

Production-ready patterns to combine with the above:

- **Trajectory eval** — score the *sequence* of tool calls, not just the final answer. ([agentevals](https://github.com/langchain-ai/agentevals) is a good starting point.)
- **State verification** — after the run, inspect the environment (DB rows, file system, DOM, ticket status) rather than the agent's self-report.
- **Rubric-based LLM judges** — decompose "quality" into specific yes/no assertions; aggregate rather than asking one fuzzy "is this good?" question.
- **Judge calibration** — periodically validate LLM judges against a human-labeled gold set; track drift.
- **`pass^k` consistency** — run the same task *k* times, require all-pass. The metric that actually correlates with shipping.
- **Adversarial / red-team evals** — Patronus, Promptfoo, and Inspect AI all support this.

## Reading & Methodology

- Hamel Husain — [Your AI product needs evals](https://hamel.dev/blog/posts/evals/).
- Eugene Yan — [Evaluating LLM-based judges](https://eugeneyan.com/writing/llm-evaluators/).
- Anthropic — [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents).
- Anthropic — [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents).
- OpenAI — [Practices for governing agentic AI systems](https://openai.com/research/practices-for-governing-agentic-ai-systems).
- Shreya Shankar — [Data flywheels for LLM applications](https://www.sh-reya.com/blog/ai-engineering-flywheel/).
- [VoltAgent/awesome-ai-agent-papers](https://github.com/VoltAgent/awesome-ai-agent-papers) — recent agent papers, including eval-focused work.

## Related Lists

This repo focuses tightly on *agent* evaluation. For broader scope, see:

- [Vvkmnn/awesome-ai-eval](https://github.com/Vvkmnn/awesome-ai-eval) — broader "AI reliability" eval list.
- [onejune2018/Awesome-LLM-Eval](https://github.com/onejune2018/Awesome-LLM-Eval) — LLM eval (EN + 中文), widely referenced.
- [zhangxjohn/LLM-Agent-Benchmark-List](https://github.com/zhangxjohn/LLM-Agent-Benchmark-List) — benchmark-only list.
- [CSHaitao/Awesome-LLMs-as-Judges](https://github.com/CSHaitao/Awesome-LLMs-as-Judges) — LLM-as-judge survey.
- [tjunlp-lab/Awesome-LLMs-Evaluation-Papers](https://github.com/tjunlp-lab/Awesome-LLMs-Evaluation-Papers) — academic survey-driven.
- [BenchGecko/awesome-llm-benchmarks](https://github.com/BenchGecko/awesome-llm-benchmarks) — benchmarks + leaderboards.

## Contributing

PRs welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). Quality bar:

- **Agent-focused.** Pure LLM benchmarks belong elsewhere unless heavily used for agent eval.
- **One line per entry.** Link first, terse description after. No marketing copy.
- **Stable.** Prefer projects with active maintenance and real adoption over preprints with no code.
- **Honest.** If a tool overlaps heavily with another, note the difference rather than duplicating.

## License

[CC0 1.0 Universal](LICENSE) — Public Domain.
