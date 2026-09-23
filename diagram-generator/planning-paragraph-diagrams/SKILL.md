---
name: planning-paragraph-diagrams
description: Use when paragraph-written Markdown needs a reusable diagram plan before implementation, including when a diagram request is handled in Plan Mode and the plan must be created in that session.
---

# Planning Paragraph Diagrams

## Purpose

Create an implementation-independent Markdown plan in which every selected prose paragraph has exactly one explanatory diagram.

## Outcome

The outcome is Markdown content conforming to [the plan format](references/plan-format.md) and [the ASCII composition rules](references/ascii-compositions.md). Read both references before producing or revising a plan.

The completed plan has these observable properties:

- It identifies the source Markdown by path without copying its full text.
- Every selected prose paragraph has one plan entry, and every plan entry belongs to one selected prose paragraph.
- No diagram combines paragraphs, and no paragraph has multiple diagrams.
- Each entry identifies its paragraph by prose-paragraph number and uses that paragraph's first sentence as its topic sentence.
- Later sentences may supply supporting detail only when it helps explain that topic sentence without changing the diagram's topic.
- It records, by Skill name, every Context Skill actually read while planning.
- Each entry contains one exact ASCII composition and a passing blind evaluation of the topic inferred from that composition.
- Each composition is realizable within the capabilities and constraints of its intended implementation method and does not depend on visual richness that method cannot reproduce.
- Each composition itself communicates the topic sentence's new central meaning; preceding source content may provide context but does not carry that new meaning in place of the composition.
- It contains no image output path or filename.
- Context- or implementation-specific additions are present only when the applicable Context or intended implementation requires them.

Only prose paragraphs are eligible by default. Headings, lists, tables, code blocks, and existing images are not prose paragraphs. The user may select or exclude prose paragraphs, but selection does not relax one paragraph–one diagram.

## Plan Mode

When a diagram request is handled in Plan Mode, use this Skill during that Plan Mode session and produce the actual diagram-plan Markdown defined above. Complete the Context loading, ASCII compositions, and blind evaluations in the current session.

Do not return a meta-plan that says the diagram plan, ASCII compositions, or evaluations will be created later. The Plan Mode outcome is the completed diagram plan itself, not a plan for making that plan. Defer only implementation work such as generating final images, editing the source Markdown, or producing another output format.
