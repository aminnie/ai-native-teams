# Managing an AI-Native SDLC

## Overview

This document assumes the reader has already read `software-engineering-in-the-age-of-ai.md`, `governing-ai-native-engineering.md`, and `ai-team-role-changes.md` and accepts the central premise: software engineering is changing, teams need to adapt, and human accountability remains essential even as AI takes on more of the mechanical work.

### **Deterministic Control Over Non-Deterministic AI**

Traditional software engineering uses deterministic coding techniques that follow strict, predefined rules, producing identical outputs from given inputs. AI coding agents are based on LLMs, are probabilistic and operate on statistical likelihoods, adapting to new data, but producing varied, non-guaranteed outcomes. This distinction between deterministic coding and probabilistic agents represents a fundamental shift from traditional software development to autonomous AI systems.   
  
Conus Greyling ([Kore.ai](http://Kore.ai)):  
  
"AI agents are largely probabilistic...   
They interpret, improvise and sometimes surprise you…  
That is what makes them useful. But It is also what makes them dangerous in production.

> The core tension in agentic AI is this… you want the model to be creative and autonomous, but you also want guarantees."

A more practical question: How should the software development lifecycle be adopted to provide such quarantees and yet continue to remain creative without losing speed, governance, consistency, code quality, or architectural integrity?

This document focuses on that question. It follows the governance framing introduced in `governing-ai-native-engineering.md`, builds on the role implications outlined in `ai-team-role-changes.md`, and uses the earlier `OpenAI` article on AI-native engineering teams and the additional point 3 links in `source-notes.md`, especially the `Claude Code` `/feature-dev` workflow, to outline how tools such as `Claude Code` and `OpenAI Codex` can support the SDLC in concrete ways.

AI coding agents such as Claude Code and Open Codex have introduced a provide a number of mechanisms intented to guide or even control AI agents towards determenistic outputs. These mechanisms were introduced because ad hoc prompting and direct `prompt -> AI -> code` vibe coding workflows do not scale well. At larger scale, those approaches create inconsistency, hidden assumptions, weak traceability, and uneven quality. These issues can often be attributed to the design of AI agent context windows. LLM calls are stateless, and as a result informaton such as the prompt, prompt history, documents referenced, etc passed into every LLM call. When the context starts exceeding design limits, the window is compacted (summarized) leading to what can be interpreted as 'memory loss'. Ad hoc LLM prompt instructions provided earlier such as "create/updete unit tests for every functional change" gets lost, and all of a sudden the test automation stops without the engineer noticing it.

This is where agents, skills, plugins, hooks, and persistent repository guidance help to address this and make AI-assisted work more structured, repeatable, reviewable, and governable and available to not only a single vibe coder and his/her prompts, but all participating team members that is able to collectovely capitalize on artifacts stored in their code repos. Most signficant: Jnior and senior engineers alike now work in a consistent, reviewable, and trustworthy way. 

Before discussing them in detail, it helps to clarify what these mechanisms are:
- AGENTS.md (Static Context/Rules): Is a markdown file in the project root that defines enduring rules for the AI. It is always loaded into the agent's context, providing consistent behavior across tasks.
- Skills (On-demand Behavior): Is a folder containing instructions (and sometimes reference documents and scripts) that the AI loads only when needed. They are used for specific, repeatable tasks like "run test suite" or "create Pull Request".
- Plugins (Packaged Functionality): Is a container that combines multiple skills, system prompts, and configuration settings (like MCP) into a single installable unit. They are designed to package entire workflows and make sharing them
- Hooks (Tool invocation permisioning, logging, auditability): AI agents invoke tools to accomplish work outside the realm of the LLM. For instance, an invoked bash terminal may be requested to delete a subdirectory or edit a .env file. Hooks are shell scripts that execute at fixed lifecycle points, evaluates the tool parameters againts code ruless. A hook may decide that the call is allowed, or block it with a reason. In the latter case, the LLM may re-evaluate its intentions and continue along a different path. "Hooks provide deterministic control wrapped around non-deterministic AI." (Cobus Greyling)

## Position in the Series

The earlier documents establish three ideas that this document takes as given:

- software engineering is shifting from manual code production toward verification, governance, and stewardship,
- AI should be introduced as part of a governed operating model rather than as ad hoc tooling,
- and Scrum team roles change meaningfully once AI becomes part of delivery.

This document builds on those ideas by looking at the SDLC itself and asking how agents, skills, plugins, and repository guidance can support each phase in concrete ways.

## 1. Why Structured Agent Support Matters

The most important lesson from both the `OpenAI` and `Claude Code /feature-dev` materials is that the value does not come from "letting the model code." It comes from structuring the work.

The `Claude Code` `/feature-dev` plugin is useful demonstration of how to makes the entire SDLC workflow explicit. Rather than jumping directly from request to implementation, it moves through seven phases:

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

It should also be noted that agents, skills and plugins are supported by numerous AI enabled IDE and CLI offerings, and that there is a healthy degree of portability between environments. 

## 2. A Practical Model: What Each Tool Type Does

Before looking phase by phase, it helps to distinguish three categories of support. 

### 2.1 AGENTS.md

`AGENTS.md` is an open standard Markdown file placed in the root of a software repository to provide specific, actionable instructions to AI coding agents and assistants. It functions as a kind of README for machines, bridging the gap between general AI knowledge and the specific requirements of a project, such as build commands, coding style, and testing rules.

Purpose and function:

- Centralized instructions: it gives AI agents a single, predictable location for project rules, reducing the need to repeat instructions across prompts.
- Complements `README.md`: while `README.md` is written primarily for humans, `AGENTS.md` focuses on the context AI needs in order to work productively.
- Improved consistency: by defining coding standards, file structures, and dependencies in one place, it helps agents produce more consistent and accurate output.
- Broad adoption: the pattern is supported across a growing set of AI coding tools and environments.

Typical content in an `AGENTS.md` file:

- Project overview: a brief description of the technology stack and purpose.
- Build and test commands: specific commands for installing dependencies, running builds, and executing tests.
- Code style and guidelines: formatting preferences, architectural patterns, and linting rules.
- Dos and don'ts: boundaries on what the agent should not do, such as not using legacy APIs or not modifying particular directories.
- File structure: pointers to key directories and important locations in the repository.

How agents use it:

- Nesting and precedence: in larger repositories, nested `AGENTS.md` files can be used, with the closest one taking precedence for local work.
- Automatic execution support: if test or validation commands are listed, agents can use them as part of their workflow.
- Tool-agnostic guidance: it allows teams to define rules once and apply them across multiple compatible AI tools.

### 2.2 Skills and Plugins

Skills and plugins are part of the process layer. They package good engineering habits into reusable forms, but at different levels of scope.

`skill.md` or `skills.md` is an emerging open-standard Markdown format used to define specific, reusable capabilities for AI agents. A skill acts as modular, on-demand procedural knowledge: instead of asking the agent to infer how to perform a task from a short prompt, the team provides a reusable recipe for doing that task well.

Typical characteristics of skills:

- On-demand behavior: skills are usually loaded only when relevant, which helps avoid prompt bloat and keeps context focused.
- Procedural guidance: they provide step-by-step instructions for repeatable tasks such as analyzing logs, generating API tests, running a security review, or preparing a pull request.
- Portable structure: they are often organized as a directory containing a `skill.md` file plus optional scripts, templates, examples, or supporting resources.
- Reproducibility: they help ensure the same task is performed in a similar way each time, which improves consistency and makes outcomes easier to review.

Typical content in a skill definition:

- Metadata: a clear name and description.
- Instructions: explicit step-by-step guidance for how the task should be performed.
- Optional resources: scripts, examples, or templates that support execution.

Skills are especially useful because they reduce the need for one large, overloaded prompt. Instead of repeatedly restating the same multi-step behavior, the team can encode it once and reuse it across projects and tools.

Plugins operate at a broader level. A plugin can bundle multiple skills, prompts, workflow rules, and sometimes tool integrations into a more complete installable package. If a skill is a reusable recipe for a specific task, a plugin is closer to a packaged workflow system that makes a fuller method easy to install, invoke, and share.

Examples:

- repo-specific skills for code review, testing, migrations, or incident triage,
- a packaged plugin such as `Claude Code` `/feature-dev`,
- and standard agent workflows for feature delivery, bug fixing, or dependency upgrades.

The distinction from `AGENTS.md` is important. `AGENTS.md` provides persistent project-level rules and context. Skills define portable, task-specific actions that can be loaded when needed. Plugins package larger sets of behaviors and workflow support. Together, they reduce variation in how people use AI. Without them, every engineer invents a different prompting style and quality bar. With them, the team gets a more repeatable way of working.

### 2.3 Hooks

Hooks are deterministic commands or scripts that execute at fixed lifecycle points in an AI agent workflow. The key idea is that hooks run outside the model and outside the conversation. They are not advisory prompt text. They are executable controls that fire at predictable moments before or after an agent uses a tool.

This distinction matters because prompt-based safety is probabilistic. A model can usually follow instructions such as "do not edit protected files" or "ask before running risky commands," but that is still not the same as an enforced boundary. Hooks move that control from guidance into execution policy.

In practical terms, hooks act as a permission and control layer around tool use. A hook can:

- inspect a proposed tool call and its arguments,
- allow the action,
- block the action with an explicit reason,
- log the action for audit purposes,
- trigger validation after execution,
- or notify other systems when important events occur.

The most important hook pattern is the pre-execution hook. This runs after the agent has decided which tool to use and with what arguments, but before the tool actually executes. That makes it possible to inspect the real intended action rather than just the model's natural-language explanation of the action.

A pre-execution hook enables several high-value control patterns:
- command protection, such as blocking dangerous shell commands,
- file protection, such as preventing edits to `.env`, key files, CI configuration, or deployment-sensitive assets,
- audit trails, such as logging tool invocations as structured events,
- notifications, such as sending important agent status changes to Slack or another operational channel,
- and size or policy limits, such as rejecting unusually large writes or actions that fall outside allowed boundaries.

The broader relevance to an AI-native SDLC is straightforward. Hooks create deterministic enforcement around non-deterministic reasoning. They let a team preserve agent flexibility while still enforcing hard boundaries for security, compliance, auditability, and operational safety. In other words, they help move AI use from "the model usually follows the rules" to "the workflow enforces the rules."

### 2.4 Repository Context and Guardrail Files

These are the durable instructions that shape agent behavior inside a codebase. Unlike skills, which are usually loaded on demand, repository guidance files provide persistent context that the agent should treat as standing project rules.

Examples:

- `CLAUDE.md`,
- `AGENTS.md`,
- architecture notes,
- contribution standards,
- testing instructions,
- service ownership maps,
- and release or incident runbooks.

### 2.5 Agents

Agents explore, propose, implement, test, review, and summarize. Claude Code and Open Codex may instantiate multiple instances of agents to for instance explore the code base concurrently during a change impact analysis, code reviews, etc.

Examples:

- `Claude Code` using `/feature-dev` or specialized agents such as code-explorer, code-architect, and code-reviewer.
- `OpenAI Codex`-style agents working across a repository with access to tests, linters, planning instructions, and operational tools.

Worker agents are strongest when the task has:

- a defined scope,
- visible constraints,
- accessible repository context,
- and a verifiable end condition.

The artifacts presented above help ensure that the model sees not only the code, but also the operating expectations around the code.

This matters because a powerful agent without local context tends to produce generic output. A somewhat less powerful agent with good local guidance often produces more useful and more compliant work.

## 3. Supporting the SDLC Phase by Phase

This document proposes 7 phases of the SDLC below, and expands them into eight practical phases by splitting production delivery from ongoing maintenance. That produces a more operationally useful model:

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
- Via scripts or MCP integrations directly access e.g. ticketing systems   


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

- break an epic or a feature into user stories and sub-tasks,
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