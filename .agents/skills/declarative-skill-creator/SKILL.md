---
name: declarative-skill-creator
description: Create, revise, or review declarative activity-defining Agent Skills that govern how a specific task, such as reviewing or implementing, is performed. Distinguish them from information-providing Skills such as tool guidance, domain knowledge, organizational review criteria, or information-governance rules; apply this Skill only to activity-defining content. Define purpose, observable outcomes, task-specific premises, and prohibited boundaries while removing unnecessary How, and automatically extract reusable premises or constraints into separate information-providing Skills. Use when asked to create or edit an activity Skill or SKILL.md, simplify an over-prescriptive workflow, translate a procedure into outcome conditions, or judge whether instructions about how to work are justified.
---

# Declarative Skill Creator

Create concise, durable Skills that let agents choose the best way to achieve the purpose for the current situation and available capabilities.

Treat the following as the design contract for the Skill being created. Choose how to satisfy the contract according to the request, target environment, and available capabilities.

## Applicability

Classify the proposed Skill by the kind of value it contributes before applying the rest of this design contract.

- **Information-providing Skill**: Supply facts, rules, criteria, or reference knowledge that an agent can use while performing one or more activities. Examples include tool usage, domain knowledge, organizational review criteria, and information-governance rules.
- **Activity-defining Skill**: Govern the performance of a particular task. Examples include how to conduct a review or how to implement a change.

Apply this design contract only to activity-defining content. Do not reshape a purely information-providing Skill around this Skill's purpose, outcomes, premises, constraints, or How criteria.

Treat mixed content according to the role of each part. Keep the activity definition within the activity-defining Skill and move independently useful information to an information-providing Skill.

## Skill Content

The skill should include the following four sections:

* Purpose
* Outcomes
* Premises
* Constraints

Purpose and Outcomes are required. Premises and Constraints should be included only when necessary.

### Purpose

State why the Skill exists and how using it should improve the user's situation or the target system.

Express the purpose as the value to achieve beyond merely producing an artifact or performing an operation. Use the purpose to prevent shortcuts that satisfy the output format while defeating the underlying intent.

### Outcomes

State the observable completion conditions that demonstrate achievement of the purpose.

Ensure the resulting Skill satisfies all of the following:

- Make the required artifacts, target end state, quality conditions, and verifiable acceptance criteria clear.
- Cover enough of the purpose that the agent cannot reasonably stop with a materially incomplete result.
- Prevent proxy outcomes from being satisfied at the expense of the actual purpose.
- Conform to the target platform, user instructions, and repository requirements.
- Make what the Skill does and which requests should trigger it clear from its description.

### Premises

State which information the agent may rely on when deciding how to achieve the purpose and outcomes, including the scope within which that information is valid.

Include only facts needed to choose an effective approach, such as the target codebase, request, expected behavior, and available environment. Receive information that varies by execution as input instead of fixing it in the Skill.

Do not make guesses, unverified descriptions, or rapidly changing information permanent premises.

### Constraints

State the boundaries the agent must not cross while achieving the purpose.

Describe prohibited actions, unacceptable states, and invariants that must remain true while leaving every other option available. Do not disguise a command that forces one route as a constraint.

Prohibit the resulting Skill from doing any of the following:

- Omitting either the purpose or the outcomes.
- Exhaustively restating knowledge a capable agent already possesses.
- Turning preferences, conventions, or past implementations into mandatory procedures or tools without a genuine requirement.
- Embedding execution-specific premises or constraints as permanent rules.
- Keeping reusable premises or constraints inside an activity-defining Skill.
- Duplicating the same information in the Skill body and supporting resources.
- Treating compliance with a fixed procedure as a substitute for achieving the purpose or outcomes.

## Separate Reusable Premises and Constraints

Determine the scope of every premise and constraint included with an activity definition.

- Treat it as **activity-specific** when its validity depends on this activity's purpose, outcomes, or execution context and it would not independently guide another Skill.
- Treat it as **reusable information** when it can guide another activity or Skill independently. This includes tool knowledge, domain knowledge, organizational criteria, system-wide principles, and information-governance rules, even when they are especially relevant to the current activity.

Keep activity-specific premises and constraints in the activity-defining Skill. Automatically create a separate information-providing Skill for reusable information, make that Skill the single source of truth, and remove the duplicated content from the activity-defining Skill. Make both Skills independently discoverable and make their relationship clear enough that they can be applied together when needed.

Do not turn execution-specific input into a separate Skill merely to remove it from the activity definition.

## When to Include How

Omit instructions about procedures, sequence, tools, implementation methods, or mandatory activities by default.

Include such instructions only to the extent that at least one of the following is true:

- Performing the specified action or method is itself part of the required result because of a law, audit rule, contract, scientific reproducibility requirement, or equivalent obligation.
- Concrete examples show that the current agent repeatedly makes the same mistake even when the purpose, outcomes, premises, and constraints are complete.

First determine whether a route requirement can be expressed as a precondition, postcondition, invariant, ordering constraint, or observable evidence. Retain only the portion for which the specific method itself is a requirement.

Limit instructions that compensate for current capability gaps to the smallest local gotcha, recommended activity, or fallback that prevents the demonstrated failure. Keep them distinguishable from permanent purpose, outcomes, premises, and constraints. Give each one a reason, scope, and condition under which it can be removed.

When only fixed operations without situational judgment remain, determine whether a script, workflow engine, CI/CD system, permission control, or other deterministic mechanism is a more appropriate boundary than an AI Skill.

## Artifact Information Design

Keep only declarations needed on every use in the Skill body. Move detailed domain knowledge, conditional information, and temporary scaffolding into supporting resources that can be loaded only when needed. Bundle scripts only when deterministic automation is itself needed for the outcome. Do not create explanatory files that do not directly support the result.

Read [Declarative Transformation Patterns](references/declarative-patterns.md) only when concrete transformation or completed Skill examples would help.
