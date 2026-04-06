# AI-Native Engineering Pack

## Purpose

This document curates the current set of notes into a coherent pack on how software engineering is changing in the age of AI, how teams should adapt, how to decide which agentic workflows to use across the software development lifecycle, and how to roll these practices out inside a real engineering organization.

The documents now use publication-style filenames so the pack is easier to share and reference internally.

Throughout the pack, `Claude Code` and `OpenAI Codex` are used as recurring reference examples. They are included not as the only relevant tools, but as representative examples of two important patterns in the current landscape: guided, workflow-oriented support for bounded engineering tasks, and broader, tool-connected support across multiple phases of the SDLC.

The pack is intended to be read as a progression:

1. understand why the role of software engineering is changing,
2. ask how AI should improve governance, consistency, traceability, and accountability across the lifecycle,
3. understand how Scrum team roles, responsibilities, and deliverables change in an AI-supported environment,
4. understand how the SDLC should be supported by agents, skills, and plugins,
5. compare `Claude Code` and `OpenAI Codex` by lifecycle phase,
6. use a practical decision matrix to choose the right workflow for a given situation,
7. and turn the ideas into an adoption roadmap for a real team or organization.

## Included Documents

### `software-engineering-in-the-age-of-ai.md`

**Focus:** Why software engineering is changing in the age of AI

This document synthesizes the first two articles in `hybrid-teams.md` and explains:

- how software development is shifting from manual code production toward verification, governance, and systems thinking,
- how the role of the software engineer is changing,
- and why teams need to redesign their ways of working when AI is involved throughout the lifecycle.

Read this first if the goal is to understand the broader change in engineering work.

### `governing-ai-supported-engineering.md`

**Focus:** Why AI should first be framed as a governance and operating-model question

This document bridges the conceptual gap between the first document and the tooling discussion by explaining:

- why governance should be considered across the full lifecycle,
- why teams need consistent ways of working in an AI-enabled environment,
- why reproducibility, traceability, and auditability matter more as generation gets faster,
- and why these concerns should shape the choice of tooling rather than follow it.

Read this second if the goal is to move from the broad shift in engineering to the operating principles that should guide AI adoption.

### `ai-team-role-changes.md`

**Focus:** How Scrum team roles change in an AI-supported engineering environment

This document bridges governance principles and workflow design by explaining:

- how key Scrum team roles evolve when AI is part of delivery,
- how responsibilities and expected deliverables shift,
- where AI assists each role most effectively,
- and what remains strongly human-owned.

Read this third if the goal is to understand how governance and AI support translate into concrete changes in team roles and day-to-day work.

### `supporting-the-sdlc-with-agents-skills-and-plugins.md`

**Focus:** How the SDLC should be supported by agents, skills, and plugins

This document builds on the first two documents and explains:

- how agents can support each phase of the SDLC,
- how skills and plugins can encode repeatable engineering practices,
- how governance and quality controls should be preserved,
- and what organizational guardrails are needed so teams benefit from AI without degrading code quality or consistency.

Read this fourth if the goal is to move from role and governance principles to concrete SDLC support mechanisms.

### `claude-code-vs-openai-codex-by-sdlc-phase.md`

**Focus:** Comparison of `Claude Code` vs `OpenAI Codex` by SDLC phase

This document provides:

- a phase-by-phase comparison table,
- a summary of where each tool appears stronger,
- common strengths and risks,
- and a concise recommendation section.

Read this fifth if the goal is to compare the two tool families in a structured way.

### `ai-workflow-decision-matrix.md`

**Focus:** How to choose which workflow to use in practice

This document provides:

- a decision matrix for different engineering situations,
- quick heuristics,
- a simple decision tree,
- recommended organizational use cases,
- and minimum guardrails that should apply regardless of the tool choice.

Read this sixth if the goal is practical decision-making.

### `ai-supported-engineering-adoption-roadmap.md`

**Focus:** How to introduce AI-supported engineering practices in a real organization

This document provides:

- adoption principles,
- rollout phases from preparation to scaling,
- role-specific guidance,
- recommended guardrails,
- suggested metrics,
- common failure modes,
- and a sample 90-day rollout sequence.

Read this seventh if the goal is organizational execution rather than analysis alone.

## Suggested Reading Paths

### For leadership or strategy readers

Read:

1. `software-engineering-in-the-age-of-ai.md`
2. `governing-ai-supported-engineering.md`
3. `ai-team-role-changes.md`
4. `supporting-the-sdlc-with-agents-skills-and-plugins.md`

Then skim:

5. `claude-code-vs-openai-codex-by-sdlc-phase.md`
6. `ai-workflow-decision-matrix.md`
7. `ai-supported-engineering-adoption-roadmap.md`

This path is best for readers who want the big picture first and practical selection guidance second.

### For engineering managers or tech leads

Read:

1. `software-engineering-in-the-age-of-ai.md`
2. `governing-ai-supported-engineering.md`
3. `ai-team-role-changes.md`
4. `supporting-the-sdlc-with-agents-skills-and-plugins.md`
5. `ai-workflow-decision-matrix.md`
6. `ai-supported-engineering-adoption-roadmap.md`

Then use:

7. `claude-code-vs-openai-codex-by-sdlc-phase.md`

This path is best for readers who need to design team practices and choose working methods.

### For hands-on engineers

Read:

1. `ai-workflow-decision-matrix.md`
2. `claude-code-vs-openai-codex-by-sdlc-phase.md`

Then go deeper with:

3. `governing-ai-supported-engineering.md`
4. `ai-team-role-changes.md`
5. `supporting-the-sdlc-with-agents-skills-and-plugins.md`
6. `software-engineering-in-the-age-of-ai.md`
7. `ai-supported-engineering-adoption-roadmap.md`

This path is best for readers who first want to know what to do in concrete day-to-day situations.

## Core Through-Line Across the Pack

All seven documents are built around the same core idea:

- AI is making code generation easier,
- which increases the importance of judgment, verification, and governance,
- which means teams need better workflows rather than just faster tools,
- and which makes structured agent usage, reusable skills, clear repository instructions, and explicit human checkpoints more important than ever.

The pack therefore does not argue for blind automation. It argues for a disciplined AI-supported engineering model in which:

- agents do the repetitive first pass,
- workflows encode good engineering behavior,
- teams share consistent ways of working,
- and humans remain accountable for architecture, review, release, and production integrity.

## What The Pack Now Covers

Taken together, the pack now covers seven distinct questions:

1. Why is software engineering changing?
2. How should AI improve governance, consistency, reproducibility, traceability, and auditability across engineering work?
3. How do Scrum team roles, responsibilities, and deliverables change in an AI-supported environment?
4. How should the SDLC be supported by agents, skills, and plugins?
5. How do `Claude Code` and `OpenAI Codex` compare by phase?
6. How should a team choose the right workflow in practice?
7. How should an organization adopt these practices safely and effectively?

That makes the set usable both as a thinking tool and as a starting point for internal adoption work.
