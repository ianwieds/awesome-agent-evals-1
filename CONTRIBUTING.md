# Contributing

Thanks for adding to this list. A few rules to keep quality high.

## What belongs here

- **Agent evaluation.** Tools, libraries, benchmarks, or methodology specifically for evaluating AI agents (multi-turn, tool-using, environment-acting).
- **Pure LLM benchmarks** belong here only if they are widely used as part of agent evaluation (e.g., HumanEval as a coding-agent baseline).
- **Methodology resources** (articles, papers) belong in *Reading & Methodology* if they offer durable, non-obvious insight — not vendor blog announcements.

## What does not belong

- Generic LLM benchmarks with no agent angle.
- Agent *frameworks* (LangGraph, AutoGen, CrewAI). Those have their own lists.
- Closed/private tools that you can't actually use.
- Preprints with no code or reproducible artifact.
- Marketing pages without substance.

## Entry format

```
- [Name](link) — One-line description. No marketing copy.
```

- **Link first**, name as the link text.
- **One line**, ideally under 120 chars.
- Say what makes it distinct, not what it markets itself as.
- For benchmarks: name the domain, task type, and what makes it hard.
- For platforms: name the actual primary use case (tracing? eval? red-teaming?).
- For libraries: language/runtime and integration story (CI? notebook? pytest?).

## Ordering

- Within a section, group by importance/adoption, not strict alphabetical.
- If unsure, alphabetical is fine.

## Duplicates and overlap

If a tool overlaps heavily with an existing entry, your PR should explain *the difference* in the entry text — not just add another bullet.

## Removing entries

PRs to remove abandoned or misleading entries are welcome. Note last-commit date or specific signal in the PR description.

## Style

- US English in descriptions.
- Don't capitalize "agent" / "evaluation" / "benchmark" mid-sentence.
- Backtick `code identifiers` (metric names, command names).
- Avoid superlatives ("best", "most powerful"). Pick a concrete distinguishing trait instead.
