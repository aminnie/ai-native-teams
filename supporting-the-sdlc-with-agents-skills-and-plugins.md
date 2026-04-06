# Supporting the SDLC with Agents, Skills, and Plugins

## Overview

This document assumes the reader has already read `software-engineering-in-the-age-of-ai.md`, `governing-ai-supported-engineering.md`, and `ai-team-role-changes.md` and accepts the central premise: software engineering is changing, teams need to adapt, and human accountability remains essential even as AI takes on more of the mechanical work.

The question now is more practical: how should the software development lifecycle be supported by agents, skills, and plugins so that a team can improve speed without losing governance, consistency, code quality, or architectural integrity?

This document focuses on that question. It follows the governance framing introduced in `governing-ai-supported-engineering.md`, builds on the role implications outlined in `ai-team-role-changes.md`, and uses the earlier `OpenAI` article on AI-native engineering teams and the additional point 3 links in `source-notes.md`, especially the `Claude Code` `/feature-dev` workflow, to outline how tools such as `Claude Code` and `OpenAI Codex` can support the SDLC in concrete ways.

It also adds analysis of where these tools are genuinely useful, where they are risky, and what operating guardrails are needed so that junior and senior engineers alike work in a consistent, reviewable, and trustworthy way.

## Position in the Series

The earlier documents establish three ideas that this document takes as given:

- software engineering is shifting from manual code production toward verification, governance, and stewardship,
- AI should be introduced as part of a governed operating model rather than as ad hoc tooling,
- and Scrum team roles change meaningfully once AI becomes part of delivery.

This document builds on those ideas by looking at the SDLC itself and asking how agents, skills, plugins, and repository guidance can support each phase in concrete ways.

## 1. Why Structured Agent Support Matters

The most important lesson from both the `OpenAI` and `Claude Code /feature-dev` materials is that the value does not come from "letting the model code." It comes from structuring the work.

The `Claude Code` `/feature-dev` plugin is useful here because it makes the workflow explicit. Rather than jumping directly from request to implementation, it moves through seven phases:

1. discovery,
2. codebase exploration,
3. clarifying questions,
4. architecture design,
5. implementation,
6. quality review,
7. summary.

That structure is important because it encodes good engineering behavior. It forces exploration before coding, clarification before design, design before implementation, and review before completion.

The `OpenAI` article makes a similar point at the organizational level. It shows that agents can contribute to planning, design, build, test, review, documentation, and operations, but only if the team deliberately defines what is delegated, what is reviewed, and what remains human-owned.

This is the real inflection point. The future is unlikely to be "one super-agent that does everything." It is more likely to be a combination of:

- workflow-level agents for bounded tasks,
- reusable skills and plugins that encode team practices,
- repository-level instructions and conventions,
- and human checkpoints at the points where ambiguity, risk, or trade-offs matter most.

In other words, the most useful AI support is not just smarter generation. It is better engineering process encoded into the toolchain.

## 2. A Practical Model: What Each Tool Type Does

Before looking phase by phase, it helps to distinguish three categories of support.

### 2.1 Agents

Agents are the active workers. They explore, propose, implement, test, review, and summarize.

Examples:

- `Claude Code` using `/feature-dev` or specialized agents such as code-explorer, code-architect, and code-reviewer.
- `OpenAI Codex`-style agents working across a repository with access to tests, linters, planning instructions, and operational tools.

Agents are strongest when the task has:

- a defined scope,
- visible constraints,
- accessible repository context,
- and a verifiable end condition.

### 2.2 Skills and Plugins

Skills and plugins are the process layer. They package good engineering habits into a reusable form.

Examples:

- a `Claude Code` plugin such as `/feature-dev`,
- repo-specific skills for code review, testing, migrations, or incident triage,
- standard agent workflows for feature delivery, bug fixing, or dependency upgrades.

These are important because they reduce variation in how people use AI. Without them, every engineer invents their own prompting style and quality bar. With them, the team gets a more repeatable way of working.

### 2.3 Repository Context and Guardrail Files

These are the durable instructions that shape agent behavior inside a codebase.

Examples:

- `CLAUDE.md`,
- `AGENTS.md`,
- architecture notes,
- contribution standards,
- testing instructions,
- service ownership maps,
- and release or incident runbooks.

These artifacts help ensure that the model sees not only the code, but also the operating expectations around the code.

This matters because a powerful agent without local context tends to produce generic output. A somewhat less powerful agent with good local guidance often produces more useful and more compliant work.

## 3. Supporting the SDLC Phase by Phase

The `OpenAI` article already outlines seven SDLC phases. This document keeps those, but expands them into eight practical phases by splitting production delivery from ongoing maintenance. That produces a more operationally useful model:

1. Discover and scope
2. Plan
3. Design
4. Build
5. Test and verify
6. Review and approve
7. Document and prepare release
8. Deploy, operate, and learn

For each phase below, the analysis covers:

- what agents can contribute,
- where `Claude Code` and `OpenAI Codex` are likely to help,
- and what must remain under human control.

### 3.1 Discover and Scope

This phase happens before implementation. It includes problem framing, interpreting requests, identifying existing patterns, and determining what is actually in scope.

#### How agents help

Agents can:

- read issue descriptions and specifications,
- search the codebase for similar features or prior implementations,
- identify likely dependency areas,
- trace execution paths,
- surface ambiguities and missing assumptions,
- and summarize the likely blast radius of a change.

This is where the `Claude Code` `/feature-dev` discovery and codebase exploration phases are particularly strong. Its parallel code-explorer pattern is a good example of how AI can reduce early ambiguity by exploring relevant parts of the repository before implementation starts.

`OpenAI Codex`-style support fits well here too, especially where the agent can read both the specification and the codebase, then map feature requests to concrete services, modules, or flows.

#### What skills and plugins add

Skills and plugins can standardize this phase by requiring the agent to always answer the same questions:

- What problem are we solving?
- Which systems are affected?
- What constraints already exist?
- What is out of scope?
- What assumptions still need human confirmation?

This kind of standardization is especially valuable for junior engineers, because it teaches a repeatable way to frame work rather than rewarding vague prompting.

#### Human ownership

Humans must still decide:

- whether the problem is worth solving,
- whether the discovered scope is acceptable,
- whether adjacent systems should be included or deferred,
- and whether the framing matches business intent.

If teams allow agents to shape scope without review, they risk subtle expansion, under-scoping, or missing organizational constraints that are not visible in the repository.

### 3.2 Plan

Planning turns a scoped problem into a practical delivery approach.

#### How agents help

Agents can:

- break a feature into sub-tasks,
- identify dependencies and sequencing,
- draft acceptance criteria,
- propose milestone plans,
- estimate likely implementation difficulty,
- and produce draft implementation notes or plans.

The `OpenAI` article explicitly highlights this as one of the early high-value uses of coding agents. In many teams, planning is slowed by the need to manually gather codebase context. Agents can shorten that loop by making the first pass.

In `OpenAI Codex`-style workflows, this is especially useful when tied to planning artifacts such as `PLAN.md`, issue trackers, or repository instructions. In `Claude Code`, this can be achieved via a structured plugin flow or a skill that requires design and planning before edits.

#### What skills and plugins add

A good planning skill or plugin should force consistency in:

- task decomposition,
- risk identification,
- assumptions,
- dependencies,
- test implications,
- and rollback thinking.

This helps move the team away from "start coding and discover later" and toward "surface uncertainty before implementation."

#### Human ownership

Humans still own:

- prioritization,
- trade-offs between speed and quality,
- sequencing across teams,
- capacity decisions,
- and non-technical risks.

An agent can draft a plan, but it cannot fully understand roadmap pressure, stakeholder politics, or broader organizational timing.

### 3.3 Design

Design includes architecture, interface choices, system boundaries, user flow implications, and the overall implementation shape.

#### How agents help

Agents can:

- propose multiple design options,
- compare minimal-change versus cleaner-architecture approaches,
- reuse existing patterns from the codebase,
- generate component or service stubs,
- translate UI concepts into implementation outlines,
- and call out integration risks early.

This is the clearest point of overlap between the `Claude Code` `/feature-dev` architecture phase and the `OpenAI` design guidance. Both point toward the same model: the agent should propose, compare, and explain options, not silently choose and move on.

#### Claude Code strengths

`Claude Code` is especially strong here when used through `/feature-dev`, because the workflow explicitly generates multiple architectural approaches and pauses for a human choice. That pause is important. It makes the design step explicit rather than accidental.

#### Codex strengths

`OpenAI Codex`-style agents may be especially useful when design needs to incorporate broader tool access, such as test tools, design references, repo-specific instructions, or other engineering systems. They can help carry design intent through into implementation and validation, not just produce a design sketch.

#### Human ownership

Humans must still own:

- cross-system architectural choices,
- long-term maintainability trade-offs,
- performance and security posture,
- and consistency with the broader platform direction.

This is one of the most dangerous places to over-delegate. Agents can propose sensible local solutions that are still wrong for the system as a whole.

### 3.4 Build

Build is where most people first think of AI coding support, but in mature workflows it is just one phase among several.

#### How agents help

Agents can:

- generate multi-file implementations,
- scaffold data models, APIs, and UI components,
- wire features into existing services,
- perform bounded refactors,
- update tests alongside code,
- fix obvious build or type errors,
- and produce reviewable diffs.

The `OpenAI` article is strongest here in practical terms. It describes agents as first-pass implementers for well-specified work. That is a useful mental model. The engineer no longer needs to personally draft every line of boilerplate, but must still shape, inspect, and refine the outcome.

`Claude Code` helps here when its implementation is preceded by discovery, clarification, and architecture approval. `OpenAI Codex` helps here when it can execute a full loop that includes repo exploration, coding, testing, and iteration.

#### What skills and plugins add

This is where skills and plugins can do the most to protect consistency. A good build skill can require the agent to:

- follow existing patterns before inventing new ones,
- avoid unnecessary file churn,
- keep changes within agreed scope,
- include tests when appropriate,
- and document assumptions made during implementation.

This can reduce the most common failure mode of agentic coding: local cleverness that leaves behind inconsistent patterns or hidden maintenance costs.

#### Human ownership

Humans still own:

- whether the implementation actually matches intent,
- whether abstractions are justified,
- whether complexity has crept in,
- and whether the resulting code should become part of the long-term codebase.

This is where the earlier warning about "liability amplification" becomes practical. Generated code is not yet an asset just because it compiles.

### 3.5 Test and Verify

As code generation becomes cheaper, this phase becomes more important, not less.

#### How agents help

Agents can:

- suggest test cases from requirements and code,
- generate unit or integration tests,
- identify untested branches or edge cases,
- run tests and iterate on failures,
- compare expected and actual behavior,
- and surface likely regression risks.

The `OpenAI` article rightly treats testing as foundational in an AI-native workflow. If agents are producing more code, the team must also improve its ability to validate more code.

#### Claude Code and Codex patterns

Both `Claude Code` and `OpenAI Codex` can help here, but the useful distinction is not the model. It is the workflow.

The best pattern is usually:

- generate or refine tests in a separate reviewable step,
- ensure the tests fail for the right reasons before the feature is considered complete,
- then let the agent iterate against the real test output.

This reduces the risk of shallow "tests that merely agree with the generated code."

#### What skills and plugins add

A testing skill can enforce:

- required test types by component,
- naming and structure conventions,
- expectations for failure-first validation,
- and commands the agent should run before claiming completion.

This is especially valuable for consistency across senior and junior engineers. It turns testing from a matter of individual discipline into a team default.

#### Human ownership

Humans must still own:

- whether the tests actually express intended behavior,
- whether important edge cases are missing,
- whether performance or security risks are sufficiently validated,
- and whether the test suite is providing real signal rather than just coverage numbers.

Good teams will increasingly treat high-quality tests as the contract that allows more agent autonomy.

### 3.6 Review and Approve

Review is where generated output is turned into organizationally acceptable output.

#### How agents help

Agents can:

- review code for bugs, convention drift, or maintainability concerns,
- identify obvious anti-patterns,
- check for repeated logic or weak abstractions,
- compare changes against repository guidance,
- and summarize likely risks for human reviewers.

The `Claude Code` `/feature-dev` quality review phase is a good example of a structured review pattern. The use of specialized reviewers with distinct focuses is especially useful. It mirrors how strong human reviewers think: correctness, elegance, and convention compliance are not the same thing.

The `OpenAI` article similarly argues that AI review can increase baseline review coverage, especially by catching issues before another engineer spends time on the pull request.

#### What skills and plugins add

A review skill can define:

- what counts as a blocking issue,
- what should be treated as a recommendation,
- what reviewers should always inspect,
- and how the agent should present findings concisely.

This matters because one of the biggest failure modes of AI review is noise. If the review process becomes verbose and low signal, people will ignore it.

#### Human ownership

Humans still own:

- final approval,
- accountability for merge readiness,
- the architectural and product implications of the change,
- and the decision that the code is fit for production.

A strong operating model treats AI review as mandatory first-pass review, not as a substitute for human code review on non-trivial changes.

### 3.7 Document and Prepare Release

Documentation should be treated as part of delivery, not leftover admin.

#### How agents help

Agents can:

- summarize what changed,
- draft module or service documentation,
- update architecture notes,
- generate release summaries,
- list impacted systems and configurations,
- and propose rollout or support notes.

The `OpenAI` article is strong on this point: documentation becomes much easier to keep current when agents are asked to produce it as part of the delivery loop rather than after the fact.

#### What skills and plugins add

Documentation skills can encode:

- what kinds of changes require docs updates,
- where docs should live,
- expected templates,
- what "why" information must be included,
- and what customer-facing or support-facing release notes should contain.

Without this, AI tends to generate plausible but shallow summaries.

#### Human ownership

Humans still own:

- whether the documentation explains the real rationale,
- whether operational and support implications are accurate,
- and whether external communication is safe and appropriate.

For internal docs, agents can do a large fraction of the drafting work. For external docs, human review should remain strict.

### 3.8 Deploy, Operate, and Learn

This phase covers release execution, incident response, production diagnostics, maintenance, and learning from what happened.

#### How agents help

Agents can:

- inspect logs and telemetry,
- correlate incidents with recent changes,
- trace likely root causes through the codebase,
- summarize suspicious deploy diffs,
- propose diagnostics or candidate fixes,
- and support post-incident writeups.

The `OpenAI` article explicitly highlights this phase as an area where coding agents become more useful when they can access operational data as well as the codebase.

This is one of the clearest examples of why tools and integrations matter. A coding agent without telemetry, logs, deploy history, and repo access cannot help much during operations. A coding agent with those inputs can become a strong triage assistant.

#### What skills and plugins add

Operational skills can encode:

- incident triage steps,
- log and metric lookup patterns,
- escalation rules,
- rollback criteria,
- and post-incident documentation expectations.

These are valuable because incidents are exactly when teams regress to inconsistent behavior under pressure.

#### Human ownership

Humans must still own:

- production change approval,
- incident command,
- risk acceptance,
- and final remediation decisions.

No matter how capable the agent becomes, production accountability should remain unmistakably human.

## 4. Tool Comparison in Context

The detailed comparison between `Claude Code` and `OpenAI Codex` is intentionally separated into `ai-tools-by-sdlc-phase.md`, and the situation-based selection guidance sits in `ai-workflow-decision-matrix.md`.

Within the argument of this document, the main point is narrower. The important distinction is less about product branding and more about workflow shape:

- guided, workflow-oriented support for bounded tasks,
- broader, tool-connected support across multiple SDLC phases,
- and the quality of the guardrails that govern how either approach is used.

Organizations that get those workflow choices right can benefit from multiple tool families. Organizations that get them wrong will struggle even with capable tools.

## 5. Organizational Implications

If a team wants agents, skills, and plugins to genuinely improve the SDLC, several organizational changes follow directly from the phase-by-phase analysis above:

- standardize a small number of default workflows rather than leaving AI usage entirely to personal style,
- teach junior and senior engineers differently, with more emphasis on judgment, review, and governed execution,
- shift metrics away from raw output and toward validated outcomes,
- and invest in repository hygiene so agents can work against clear conventions, commands, and ownership boundaries.

These implications are expanded further in `ai-supported-engineering-adoption-roadmap.md`, which turns them into rollout guidance.

## 6. Core Guardrails

This document uses the SDLC lens to show where AI can help. The corresponding constraint is that AI support should operate within a small number of explicit guardrails:

- key scope, design, merge, and release decisions remain human-approved,
- generation and validation should be treated as distinct activities,
- tasks should stay bounded enough to be reviewable,
- quality gates should be runnable and meaningful,
- and the workflow should preserve auditability of what was proposed, changed, tested, and approved.

The detailed governance rationale for these controls is developed in `governing-ai-supported-engineering.md`, and the more operational rollout version appears in `ai-supported-engineering-adoption-roadmap.md`.

## 7. A Practical Target Operating Model

Taken together, the sections above point to a practical operating model:

- every meaningful feature starts with structured discovery, planning, and design,
- agents explore, draft, and validate within defined boundaries,
- skills and plugins encode repeatable team practice,
- repository guidance makes conventions and commands explicit,
- AI review happens before human review where appropriate,
- and humans remain accountable for judgment, acceptance, release, and production integrity.

This is the difference between occasional AI use and a genuinely AI-supported SDLC.

## 8. Conclusion

The most promising future is not one in which `Claude Code`, `OpenAI Codex`, or any other tool simply replaces engineers at each stage of the lifecycle.

It is one in which the SDLC is redesigned so that:

- agents handle the repetitive first pass,
- skills and plugins encode disciplined ways of working,
- repository guidance makes local conventions visible,
- and humans retain ownership of judgment, governance, and integrity.

The comparison, decision, and adoption documents that follow build on this foundation by showing how different tool patterns fit the lifecycle, how teams can choose among them, and how an organization can adopt them safely.
