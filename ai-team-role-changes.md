# AI Team Role Changes in a Scrum Team

## Overview

This document sits between `governing-ai-supported-engineering.md` and `supporting-the-sdlc-with-agents-skills-and-plugins.md`.

It addresses a practical organizational question that naturally follows the governance discussion:

If a team continues to work as a Scrum Team, how do role expectations change when AI becomes part of planning, design, implementation, testing, review, release, and operations?

The central argument is that Scrum does not disappear. The need for shared accountability, cross-functional collaboration, clear increments, and regular inspection and adaptation remains. What changes is the nature of the work performed inside each role.

The governance properties discussed in the previous document now become concrete at the team level. Consistency, reproducibility, traceability, auditability, and clear human accountability show up not only in process design, but also in who owns which decisions, who reviews which artifacts, and what each role is expected to produce.

In that context, several broad shifts become visible:

- more work shifts from first-pass production to oversight and refinement,
- more effort moves toward judgment, orchestration, and quality control,
- and more deliverables become structured artifacts that help humans and AI work together consistently.

This document focuses on six roles:

1. Product Owner or Product Manager
2. Software Engineer
3. Quality Engineer, Automation
4. Quality Engineer, Manual
5. DevSecOps
6. Engineering Manager

For each role, it outlines:

- how responsibilities change,
- which activities remain primarily human-owned,
- where AI can assist most effectively,
- and what deliverables become more important in an AI-supported Scrum environment.

## 1. The Scrum Context Should Remain Intact

If the team continues to work as a Scrum Team, the goal should not be to replace Scrum ceremonies with automation. The goal should be to make Scrum artifacts, events, and responsibilities more effective.

In practice, that means:

- backlog refinement becomes more evidence-rich,
- sprint planning becomes more code-aware and risk-aware,
- daily coordination becomes more focused on exceptions and decisions,
- sprint reviews can be supported by better summaries and traceability,
- and retrospectives can examine both human and AI-supported workflow performance.

AI can reduce manual effort inside these activities, but it should not remove the need for team alignment, shared understanding, or explicit accountability.

## 2. Cross-Cutting Role Changes

Before looking role by role, several changes apply across the whole Scrum Team.

### 2.1 More orchestration, less first-pass production

Many roles will spend less time creating the first draft of an artifact from scratch and more time:

- specifying intent,
- reviewing AI-generated output,
- validating quality,
- resolving ambiguity,
- and deciding whether the output should be accepted, refined, or rejected.

### 2.2 Better artifacts become more important

As AI becomes part of the workflow, the quality of team artifacts matters more. Weak stories, vague acceptance criteria, undocumented constraints, and unclear standards create poor AI output and inconsistent team behavior.

### 2.3 Deliverables become more explicit

A strong AI-supported Scrum Team relies more heavily on explicit deliverables such as:

- clear backlog items,
- acceptance criteria,
- design notes,
- risk and test expectations,
- review evidence,
- release summaries,
- and traceable links from intent to implementation.

### 2.4 Shared accountability remains critical

AI can assist specialized roles, but it does not remove collective ownership of the sprint goal, product quality, or release readiness.

## 3. Role-by-Role Changes

### 3.1 Product Owner or Product Manager

### Primary shift

The Product Owner or Product Manager shifts from being mainly a translator of business intent into requirements toward being a sharper definer of intent, constraints, and success conditions.

As AI reduces the cost of prototyping, specification drafting, and even implementation scaffolding, the bottleneck moves toward:

- prioritization,
- clarity of problem framing,
- quality of acceptance criteria,
- and the ability to distinguish between a plausible demo and a production-ready outcome.

### Responsibilities that increase

- writing clearer problem statements and outcome-oriented stories,
- defining stronger acceptance criteria and non-functional expectations,
- identifying constraints, dependencies, and out-of-scope boundaries early,
- validating whether AI-assisted prototypes reflect true product intent,
- and maintaining traceability between user need, requirement, implementation, and release.

### Responsibilities that remain strongly human

- prioritization decisions,
- value trade-offs,
- stakeholder alignment,
- interpretation of ambiguous customer needs,
- and final acceptance that functionality meets the intended business outcome.

### Where AI assists best

AI can help product roles by:

- summarizing customer or issue data,
- drafting first-pass stories and acceptance criteria,
- identifying likely codebase dependencies or impacted systems,
- generating prototype flows,
- surfacing ambiguities before sprint planning,
- and preparing release notes or change summaries tied back to the original request.

### Expected deliverables in an AI-supported Scrum Team

- more precise backlog items,
- better-defined acceptance criteria,
- explicit assumptions and constraints,
- links between stories and affected systems,
- and reviewable prototype or workflow drafts where useful.

### Practical implication

The role becomes less about producing more tickets and more about producing clearer, more decision-ready work for the team and for the AI-supported workflow.

### 3.2 Software Engineer

### Primary shift

The Software Engineer shifts from being primarily the author of implementation detail toward being the designer, reviewer, and accountable owner of AI-assisted implementation.

The engineer still builds software, but the highest-value work increasingly lies in:

- architecture,
- decomposition,
- verification,
- code review,
- and management of complexity and risk.

### Responsibilities that increase

- decomposing work into bounded tasks suitable for AI assistance,
- selecting appropriate patterns and guardrails,
- reviewing AI-generated code critically,
- checking for architectural consistency and long-term maintainability,
- strengthening tests and validation logic,
- and preventing low-value generated complexity from entering the codebase.

### Responsibilities that remain strongly human

- final ownership of implementation decisions,
- architectural judgment,
- risk acceptance for technical trade-offs,
- handling novel or ambiguous problems,
- and merge readiness on meaningful changes.

### Where AI assists best

AI can help software engineers by:

- exploring the codebase,
- drafting implementations,
- proposing design alternatives,
- generating tests,
- fixing mechanical build or type issues,
- assisting with refactors,
- and producing initial review summaries.

### Expected deliverables in an AI-supported Scrum Team

- cleaner design notes,
- bounded implementation plans,
- reviewable diffs,
- stronger test updates,
- explicit rationale for important trade-offs,
- and better-documented impact summaries.

### Practical implication

The engineer becomes less of a syntax producer and more of a system steward, implementation reviewer, and workflow orchestrator.

### 3.3 Quality Engineer, Automation

### Primary shift

The Quality Engineer focused on automation shifts from manually authoring large quantities of test code toward being a designer of test strategy, automation patterns, and verification quality.

As AI makes it easier to generate test scripts, the value of the role moves toward deciding:

- what should be tested,
- what kinds of automation are reliable,
- what coverage actually matters,
- and whether generated tests provide signal or only volume.

### Responsibilities that increase

- defining automation strategy by layer,
- designing reusable test patterns and frameworks,
- validating AI-generated tests,
- identifying missing edge cases and failure modes,
- strengthening CI validation loops,
- and monitoring test reliability and false confidence.

### Responsibilities that remain strongly human

- deciding test architecture,
- determining meaningful coverage,
- identifying high-risk behaviors,
- challenging weak or superficial tests,
- and deciding whether the test suite is giving trustworthy evidence.

### Where AI assists best

AI can help automation engineers by:

- generating first-pass tests,
- proposing edge cases,
- updating tests after implementation changes,
- identifying stale or duplicated tests,
- explaining failing test behavior,
- and helping maintain automation assets.

### Expected deliverables in an AI-supported Scrum Team

- explicit test strategy by story or feature,
- validated test suites rather than only generated tests,
- stronger coverage around business-critical and risk-critical paths,
- and better reporting on what test evidence actually demonstrates.

### Practical implication

The role becomes more strategic and architectural. The automation engineer increasingly acts as a test systems designer and evidence quality owner.

### 3.4 Quality Engineer, Manual

### Primary shift

The Quality Engineer focused on manual testing shifts away from repetitive scripted regression execution and toward exploratory testing, experience validation, ambiguity detection, and risk-based assessment.

As AI and automation take more of the routine execution workload, the distinct value of manual quality work becomes more visible in areas where human judgment still matters most.

### Responsibilities that increase

- exploratory testing,
- validation of user journeys and edge cases,
- detection of workflow ambiguity,
- assessment of usability and experiential quality,
- interpretation of inconsistent or suspicious test results,
- and helping the team understand where automation is insufficient.

### Responsibilities that remain strongly human

- judging whether the product behavior feels coherent and trustworthy,
- spotting gaps between stated requirements and actual user experience,
- identifying nuanced failure patterns,
- and deciding where additional human investigation is needed.

### Where AI assists best

AI can help manual quality engineers by:

- generating test ideas and exploratory charters,
- documenting exploratory sessions,
- converting observations into structured defects or follow-up tests,
- summarizing recurring defect patterns,
- and proposing risk areas based on story scope and prior defects.

### Expected deliverables in an AI-supported Scrum Team

- clearer exploratory testing plans,
- better defect descriptions linked to stories and risks,
- richer user-experience observations,
- and sharper recommendations on where automation, manual testing, or additional review is needed.

### Practical implication

The manual quality role becomes less execution-heavy and more insight-heavy. It is increasingly centered on judgment, customer experience, and risk interpretation.

### 3.5 DevSecOps

### Primary shift

The DevSecOps role shifts from being primarily a pipeline maintainer and late-stage control point toward being an enabler of secure, observable, policy-driven delivery in a much faster AI-supported workflow.

As AI-assisted development increases the speed and volume of change, DevSecOps becomes more responsible for ensuring that the delivery system itself can safely absorb that speed.

### Responsibilities that increase

- embedding security, compliance, and operational guardrails into the workflow,
- strengthening policy-as-code and quality gates,
- making telemetry, logs, and operational evidence available for AI-assisted analysis,
- integrating security and deployment feedback directly into developer workflows,
- and managing AI-related risks such as over-permissioned agents, secret exposure, weak audit trails, or unsafe automation.

### Responsibilities that remain strongly human

- approval of sensitive production changes,
- definition of security policy and exception handling,
- interpretation of high-risk findings,
- incident command for serious events,
- and final accountability for operational and security posture.

### Where AI assists best

AI can help DevSecOps roles by:

- summarizing pipeline failures,
- triaging alerts,
- correlating incidents with recent changes,
- suggesting likely root causes,
- identifying missing controls,
- assisting with policy checks,
- and generating first-pass remediation or rollback guidance.

### Expected deliverables in an AI-supported Scrum Team

- stronger pipeline guardrails,
- clearer deployment and rollback criteria,
- better security and operational evidence,
- documented exception paths,
- and improved release-readiness summaries.

### Practical implication

DevSecOps becomes more central, not less. The role increasingly governs the trustworthiness of the delivery system that both humans and AI rely on.

### 3.6 Engineering Manager

### Primary shift

The Engineering Manager shifts from managing mainly people and delivery throughput toward managing a socio-technical system made up of people, workflows, tools, guardrails, and increasingly capable AI support.

In an AI-supported Scrum Team, the manager becomes more responsible for whether the overall system of work is coherent, sustainable, and appropriately governed.

### Responsibilities that increase

- defining and reinforcing standard ways of working,
- deciding where AI should and should not be used,
- monitoring whether quality, learning, and accountability are improving,
- coaching different roles on how their work is changing,
- ensuring that role boundaries do not become fuzzy in unsafe ways,
- and managing the balance between speed and stewardship.

### Responsibilities that remain strongly human

- team design,
- performance and growth conversations,
- conflict resolution,
- prioritization of improvement work,
- risk escalation,
- and judgment about whether the team is operating safely and effectively.

### Where AI assists best

AI can help engineering managers by:

- summarizing delivery patterns,
- surfacing bottlenecks and workflow drift,
- identifying repeated review or defect themes,
- drafting operating guidelines,
- summarizing incidents and retrospectives,
- and helping connect engineering metrics with observed team behavior.

### Expected deliverables in an AI-supported Scrum Team

- clearer team standards,
- explicit workflow guardrails,
- role guidance for engineers and quality roles,
- better retrospective insights,
- and stronger evidence for process improvement decisions.

### Practical implication

The Engineering Manager becomes less of a throughput tracker and more of a designer and steward of the team’s human-AI operating model.

## 4. Role Comparison at a Glance

Appendix A provides the compact comparison tables for readers who want a side-by-side summary of current expectations, AI-supported future expectations, human-owned decisions, strengthened artifacts, and best-fit AI assistance by role.

## 5. Implications for Scrum Artifacts and Events

If these role changes are taken seriously, the Scrum Team’s artifacts and events also become more explicit.

### Product Backlog and Sprint Backlog

These become more structured and more machine-readable in practice, with greater emphasis on:

- explicit acceptance criteria,
- non-functional expectations,
- dependencies and constraints,
- and links to test and review expectations.

### Sprint Planning

This becomes more evidence-driven, because AI can help surface:

- likely impacted systems,
- similar historical changes,
- possible design options,
- and likely verification needs.

### Daily Scrum

This can become less of a status round and more of a coordination checkpoint focused on:

- unresolved ambiguity,
- blocked reviews,
- validation failures,
- risky assumptions,
- and changes requiring human decisions.

### Sprint Review

This can be supported by stronger summaries, traceability, and evidence showing:

- what changed,
- why it changed,
- what was validated,
- and what risks remain.

### Retrospective

This should now inspect not only team collaboration, but also:

- quality of AI-supported workflows,
- where prompts or tooling created drift,
- where guardrails were weak,
- and which role expectations need to be clarified further.

## 6. Conclusion

If a Scrum Team remains in place, AI does not eliminate roles. It changes the center of gravity of each role.

Across all six roles, the pattern is consistent:

- less value comes from producing first drafts manually,
- more value comes from setting intent, governing quality, reviewing outputs, interpreting risk, and maintaining coherence,
- and the best deliverables become those that make the whole workflow clearer, more reproducible, and more auditable.

This is why role clarity becomes more important, not less, in an AI-supported Scrum Team.

The next document in the series then builds on this conclusion by looking at how agents, skills, and plugins can be used to support the SDLC in concrete ways.

## Appendix A: Role Comparison Tables

The following tables summarize the role shifts in a more compact form.

### A.1 Current Scrum Role Expectations vs AI-Supported Role Expectations


| Role                             | Current Scrum emphasis                                                                    | AI-supported future emphasis                                                                                                                       |
| -------------------------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Product Owner or Product Manager | Backlog ownership, requirement clarification, prioritization, stakeholder communication   | Intent definition, sharper acceptance criteria, earlier constraint setting, traceability, validation of AI-assisted prototypes and outcomes        |
| Software Engineer                | Implementation, design, defect fixing, code review, delivery of working software          | Architecture, task decomposition, AI-assisted implementation oversight, validation, complexity control, technical risk ownership                   |
| Quality Engineer, Automation     | Test automation authoring, framework maintenance, regression support, CI test execution   | Test strategy, validation of AI-generated tests, evidence quality, edge-case design, reliability of automation and feedback loops                  |
| Quality Engineer, Manual         | Manual regression execution, scripted testing, defect reporting, user-flow validation     | Exploratory testing, user-experience validation, ambiguity detection, interpretation of risk, assessment of automation gaps                        |
| DevSecOps                        | Pipeline support, environment management, deployment enablement, security checks          | Policy-driven delivery guardrails, secure AI-enabled pipelines, observability, risk triage, control design, trustworthy release workflows          |
| Engineering Manager              | Team delivery oversight, staffing, coaching, process facilitation, performance management | Human-AI operating-model stewardship, workflow standardization, quality and governance oversight, role clarity, sustainable adoption of AI support |


### A.2 Activities Most Changed by AI Support


| Role                             | Activities reduced or reshaped by AI                                                            | Activities increased because of AI                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Product Owner or Product Manager | Manual first-draft story writing, basic prototype preparation, repetitive release note drafting | Requirement sharpening, scope boundary definition, decision quality, acceptance review, ensuring traceability |
| Software Engineer                | Routine scaffolding, boilerplate coding, repetitive refactors, first-pass test writing          | Review of generated code, architecture decisions, verification, guardrail design, maintainability stewardship |
| Quality Engineer, Automation     | Manual bulk test scripting, repetitive test maintenance, routine regression wiring              | Test architecture, validation of generated suites, failure analysis, signal-vs-noise judgment                 |
| Quality Engineer, Manual         | Repetitive scripted execution and low-value regression repetition                               | Exploratory testing, experience-based assessment, nuanced defect analysis, ambiguity surfacing                |
| DevSecOps                        | Manual triage of repetitive alerts, some pipeline diagnostics, repetitive control checking      | Policy definition, exception handling, AI-safe permissions, operational trust and auditability design         |
| Engineering Manager              | Manual aggregation of delivery signals, repetitive reporting, some coordination overhead        | Workflow design, adoption governance, role coaching, balancing speed and quality, measuring real improvement  |


### A.3 Human-Owned Decisions That Should Remain Explicit


| Role                             | Decisions that should remain strongly human-owned                                                         |
| -------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Product Owner or Product Manager | Priority, value trade-offs, stakeholder alignment, acceptance of delivered outcome                        |
| Software Engineer                | Architectural trade-offs, merge readiness, technical risk acceptance, long-term maintainability decisions |
| Quality Engineer, Automation     | Test strategy, sufficiency of coverage, trustworthiness of automation evidence                            |
| Quality Engineer, Manual         | User-experience judgment, exploratory direction, interpretation of subtle defects and behavior gaps       |
| DevSecOps                        | Security exceptions, production approval, incident command, high-risk operational decisions               |
| Engineering Manager              | Team design, role expectations, escalation decisions, accountability and cultural direction               |


### A.4 Likely New or Strengthened Artifacts by Role


| Role                             | Likely new or strengthened artifacts in an AI-supported Scrum Team                                                        |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Product Owner or Product Manager | clearer stories, explicit acceptance criteria, assumptions and constraints, dependency notes, traceable release summaries |
| Software Engineer                | bounded implementation plans, design rationale, review-ready diffs, explicit risk notes, stronger validation evidence     |
| Quality Engineer, Automation     | test strategy notes, coverage rationale, validated generated tests, failure analysis summaries, reliability indicators    |
| Quality Engineer, Manual         | exploratory charters, richer defect narratives, user-journey observations, escalation notes for automation gaps           |
| DevSecOps                        | policy definitions, control evidence, deployment criteria, rollback guidance, security and operational exception logs     |
| Engineering Manager              | workflow standards, role guidance, adoption guardrails, retrospective summaries, improvement metrics and decision logs    |


### A.5 Best AI Assistance by Role


| Role                             | Where AI assists best                                                                                                         |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Product Owner or Product Manager | story drafting, ambiguity surfacing, dependency discovery, prototype support, release summary generation                      |
| Software Engineer                | codebase exploration, implementation drafts, refactor assistance, test generation, first-pass review summaries                |
| Quality Engineer, Automation     | test generation, edge-case suggestion, stale-test detection, failure explanation, automation maintenance support              |
| Quality Engineer, Manual         | exploratory session support, test idea generation, observation structuring, defect summarization, risk pattern surfacing      |
| DevSecOps                        | alert triage, pipeline failure summarization, incident correlation, first-pass remediation suggestions, control gap detection |
| Engineering Manager              | trend summaries, workflow bottleneck analysis, retrospective synthesis, policy drafting, cross-team pattern detection         |
