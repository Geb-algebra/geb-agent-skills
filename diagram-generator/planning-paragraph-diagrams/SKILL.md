---
name: planning-paragraph-diagrams
description: Use when paragraph-written Markdown needs a reusable diagram plan before implementation, including when a diagram request is handled in Plan Mode and the plan must be created in that session.
---

# Planning Paragraph Diagrams

## Purpose

Create an implementation-independent Markdown plan in which every selected prose paragraph has exactly one explanatory diagram.

## Mode

Choose one mode for the whole plan and record it in the plan. An explicit user choice overrides every inference.

- Use `intuitive` for presentation slides, spoken explanations, and other material where a presenter or surrounding delivery supplements the diagram. If neither the user nor the intended use indicates a mode, use `intuitive` for backward compatibility.
- Use `detailed` for handouts, reference material, and other documents intended to be understood without a presenter.

In `intuitive` mode, prioritize intuitive understanding over precision and completeness without changing the topic. The composition communicates the topic sentence's new central meaning, uses later sentences only when they help explain that meaning, and keeps text to short labels and the minimum necessary explanation.

In `detailed` mode, the composition makes the complete paragraph semantically recoverable. It preserves every distinct proposition contributed by the topic and supporting sentences, including qualifications, causes, evidence, examples, and contrasts, without omission, reversal, or distortion; a detail is required whenever removing it would reduce or change the information expressed by the paragraph. Continue to express meaning through shapes, placement, connections, containment, and other diagrammatic relationships wherever possible. Use explanatory prose attached to the relevant element or relationship only for meaning that visual structure cannot preserve accurately. Do not substitute transcription for diagrammable meaning by copying, paraphrasing, or distributing the paragraph's sentences, clauses, or equivalent restatements across one or more text containers.

## Outcome

The outcome is Markdown content conforming to [the plan format](references/plan-format.md) and [the ASCII composition rules](references/ascii-compositions.md). Read both references before producing or revising a plan.

The completed plan has these observable properties in every mode:

- It identifies the source Markdown by path without copying its full text.
- It records exactly one mode, `intuitive` or `detailed`, for the whole plan.
- Every selected prose paragraph has one plan entry, and every plan entry belongs to one selected prose paragraph.
- No diagram combines paragraphs, and no paragraph has multiple diagrams.
- Each entry identifies its paragraph by prose-paragraph number and uses that paragraph's first sentence as its topic sentence.
- It records, by Skill name, every Context Skill actually read while planning.
- Each entry contains one exact ASCII composition and a passing mode-appropriate blind evaluation of the meaning inferred from that composition.
- Each composition is realizable within the capabilities and constraints of its intended implementation method and does not depend on visual richness that method cannot reproduce.
- It contains no image output path or filename.
- Context- or implementation-specific additions are present only when the applicable Context or intended implementation requires them.

### Intuitive

In `intuitive` mode, the completed plan also has these observable properties:

- Later sentences supply supporting detail only when it helps explain the topic sentence without changing the diagram's topic.
- Each composition itself communicates the topic sentence's new central meaning. Preceding source content may provide context but does not carry that new meaning in place of the composition.

### Detailed

In `detailed` mode, the completed plan also has these observable properties:

- Every distinct meaning contributed by the complete paragraph is represented while the topic sentence remains the paragraph identifier.
- Each composition itself communicates every distinct meaning newly contributed by the complete paragraph. Preceding source content may provide context but does not carry the target paragraph's new meaning in place of the composition.

Only prose paragraphs are eligible by default. Headings, lists, tables, code blocks, and existing images are not prose paragraphs. The user may select or exclude prose paragraphs, but selection does not relax one paragraph–one diagram.

## Plan Mode

When a diagram request is handled in Plan Mode, use this Skill during that Plan Mode session and produce the actual diagram-plan Markdown defined above. Complete the Context loading, ASCII compositions, and blind evaluations in the current session.

Do not return a meta-plan that says the diagram plan, ASCII compositions, or evaluations will be created later. The Plan Mode outcome is the completed diagram plan itself, not a plan for making that plan. Defer only implementation work such as generating final images, editing the source Markdown, or producing another output format.
