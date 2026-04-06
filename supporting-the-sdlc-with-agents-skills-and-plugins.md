# Supporting the SDLC with Agents, Skills, and Plugins

## Overview

This document assumes the reader has already read `software-engineering-in-the-age-of-ai.md` and `governing-ai-supported-engineering.md` and accepts the central premise: software engineering is changing, teams need to adapt, and human accountability remains essential even as AI takes on more of the mechanical work.

The question now is more practical: how should the software development lifecycle be supported by agents, skills, and plugins so that a team can improve speed without losing governance, consistency, code quality, or architectural integrity?

This document focuses on that question. It follows the governance framing introduced in `governing-ai-supported-engineering.md` and uses the earlier `OpenAI` article on AI-native engineering teams and the additional point 3 links in `hybrid-teams.md`, especially the `Claude Code` `/feature-dev` workflow, to outline how tools such as `Claude Code` and `OpenAI Codex` can support the SDLC in concrete ways.

It also adds analysis of where these tools are genuinely useful, where they are risky, and what operating guardrails are needed so that junior and senior engineers alike work in a consistent, reviewable, and trustworthy way.

## Short Recap from `software-engineering-in-the-age-of-ai.md`

The first document argued that:

- code generation is becoming cheaper and faster,
- verification, judgment, and system stewardship are becoming more valuable,
- engineering teams need to adapt how they work rather than simply adding AI to existing habits,
- and the role of the engineer is shifting from syntax producer toward systems governor, reviewer, and accountable owner.

This document takes the next step. If those ideas are true, and if the governance concerns in `governing-ai-supported-engineering.md` are taken seriously, then the SDLC should be redesigned so that:

- agents assist in each phase where structured support is useful,
- skills and plugins encode repeatable team practices,
- repositories expose the right context, constraints, and tools,
- and governance remains visible and enforceable throughout delivery.

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

## 4. Concrete Differences Between Claude Code and OpenAI Codex

The two tool families overlap a great deal, but they are not identical in emphasis.

### 4.1 Where Claude Code Stands Out

Based on the `/feature-dev` materials, `Claude Code` is especially strong when the team wants to package a development methodology into a clear guided workflow.

Its strengths include:

- explicit multi-phase feature development,
- specialized agents with distinct roles,
- structured pauses for human approval,
- and a strong fit for medium-complexity, bounded feature work.

This makes it particularly attractive for organizations that want to teach and enforce a disciplined engineering flow rather than rely on free-form prompting.

### 4.2 Where OpenAI Codex Stands Out

Based on the `OpenAI` guide, `Codex` is especially strong as a more general AI-native engineering collaborator across the full SDLC, especially where the agent can interact with real tools, instructions, tests, review workflows, and operational systems.

Its strengths include:

- end-to-end SDLC support rather than only implementation,
- integration with real tool execution,
- the ability to operate inside broader organizational workflows,
- and support for repository-level instructions such as `AGENTS.md` to create repeatable behavior.

This makes it well suited to organizations that want agents embedded not just in coding, but in planning, testing, reviewing, documenting, and operations.

### 4.3 The More Important Point

In practice, the most important distinction may not be `Claude Code` versus `OpenAI Codex`.

The more important distinction is:

- unstructured prompting versus structured workflow,
- isolated generation versus tool-backed validation,
- and individual usage habits versus team-level operating standards.

An organization that gets those things right will probably do well with either family of tools. An organization that gets them wrong will produce inconsistent outcomes with both.

## 5. Organizational Implications

If a team wants agents, skills, and plugins to genuinely improve the SDLC, then several organizational changes are required.

### 5.1 Standardize How AI Is Used

Teams should not leave agent usage entirely to personal style. Some flexibility is fine, but core workflows should be standardized.

Examples:

- a default feature workflow,
- a default review workflow,
- a default testing workflow,
- a default doc-update workflow,
- and a default incident-triage workflow.

This prevents the situation where one engineer uses the tools carefully while another uses them casually and produces lower-integrity output.

### 5.2 Teach Junior and Senior Engineers Differently

Junior engineers need structured workflows that teach them how to explore, clarify, design, test, and review. Senior engineers need workflows that amplify judgment rather than replacing it.

This means AI enablement should not just be tool training. It should also be engineering-method training.

### 5.3 Shift Metrics Away from Raw Output

If teams start measuring success mainly by how much code was generated or how quickly tickets moved, they will create the wrong incentives.

Better measures include:

- cycle time to validated change,
- defect escape rate,
- rollback rate,
- architectural consistency,
- review quality,
- and documentation freshness.

### 5.4 Invest in Repository Hygiene

Agents perform much better when the repository is understandable.

That means:

- keeping architectural notes current,
- documenting conventions,
- exposing test commands clearly,
- maintaining service ownership information,
- and preserving useful examples of good implementations.

This is not optional overhead. It is part of making the team genuinely AI-native.

## 6. Recommended Guardrails

If the aim is governance, consistency, and codebase integrity, then the following guardrails should be explicit.

### 6.1 Require Human Approval at Key Checkpoints

At minimum, humans should explicitly approve:

- final scope,
- major design choice,
- production-risking implementation changes,
- and merge or release readiness.

### 6.2 Use Skills and Plugins to Encode Team Practice

Do not rely only on memory or informal norms. Encode expectations into:

- `AGENTS.md`,
- `CLAUDE.md`,
- plugins,
- reusable skills,
- and review checklists.

### 6.3 Separate Generation from Validation

The same agent session can support both, but the team should conceptually separate:

- drafting,
- testing,
- review,
- and final approval.

This reduces self-confirming loops where the generator also implicitly declares itself correct.

### 6.4 Keep Tasks Bounded

The `Claude Code` `/feature-dev` guidance is right to stress medium-complexity, bounded tasks.

Teams should avoid giving agents:

- very vague objectives,
- whole-system refactors in one pass,
- hidden organizational assumptions,
- or authority to make irreversible production decisions.

### 6.5 Make Quality Gates Runnable

If agents are going to help deliver software, then tests, linters, review checks, and release validations must be runnable and understandable.

Quality gates should be:

- automated where possible,
- easy to invoke,
- visible in repo instructions,
- and meaningful enough to block low-quality output.

### 6.6 Preserve Auditability

Teams should be able to see:

- what the agent was asked to do,
- what decisions it proposed,
- what changed,
- what tests ran,
- and who approved the result.

This is especially important in regulated, safety-sensitive, or business-critical environments.

### 6.7 Treat AI Review as Mandatory but Not Sufficient

For non-trivial changes, AI review should be a standard first pass. But it should not replace human review where the consequences of error are meaningful.

### 6.8 Prefer Subtraction Over Generated Sprawl

Agents make it easy to add code. Teams must become more disciplined about deleting unnecessary code, rejecting gratuitous abstractions, and protecting the long-term readability of the repository.

## 7. A Practical Target Operating Model

Putting all of this together, a realistic target model for an engineering team might look like this:

- Every meaningful feature starts with a structured discovery and planning flow.
- Agents explore the codebase and surface ambiguities before implementation begins.
- Skills and plugins encode the team's standard workflow for feature work, testing, review, and documentation.
- The repository includes durable guidance files that define conventions, commands, patterns, and guardrails.
- Agents implement bounded changes and run validation loops.
- AI review happens before human review.
- Human engineers remain accountable for design choice, merge approval, release approval, and production operation.
- Post-release learning is documented and fed back into skills, instructions, and workflow improvements.

This is the difference between "developers occasionally using AI" and an actual AI-supported SDLC.

## 8. Conclusion

The most promising future is not one in which `Claude Code`, `OpenAI Codex`, or any other tool simply replaces engineers at each stage of the lifecycle.

It is one in which the SDLC itself is redesigned so that:

- agents do the repetitive first pass,
- skills and plugins encode disciplined ways of working,
- repository guidance makes local conventions visible,
- and humans retain ownership of judgment, governance, and integrity.

The practical implication is clear: if engineering teams want to benefit from AI without degrading their codebase, they need to invest not only in models, but in workflows.

That means building a delivery system where exploration, clarification, design, implementation, testing, review, documentation, and operations are all supported by agents in deliberate ways, with human checkpoints and visible quality gates throughout.

The organizations that do this well will probably not be the ones with the most autonomous agents. They will be the ones with the clearest workflows, the best encoded practices, and the strongest discipline around what remains unmistakably human.
