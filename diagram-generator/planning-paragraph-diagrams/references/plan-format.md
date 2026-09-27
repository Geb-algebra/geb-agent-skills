# Paragraph Diagram Plan Format

## Required structure

Produce Markdown with this structure. Headings may be localized, but the fields and their meanings are fixed.

````markdown
# Diagram plan

Source: `<path-to-source-markdown>`
Mode: intuitive | detailed

## Applied contexts

- `$context-skill-name`

## Diagrams

### Paragraph 1

Topic sentence: ...

ASCII composition:

```text
┌...┐
│...│
└...┘
```

Blindly inferred topic: ...

Comparison: ...

Verdict: Pass
````

Use the source-order index among prose paragraphs for `Paragraph N`; do not count headings, lists, tables, code blocks, or image-only blocks. Include entries only for selected paragraphs. Do not copy either the complete source document or complete paragraph into the plan. The topic sentence is the only source sentence required in an entry.

`Mode` is required and applies to the whole plan. Record exactly `intuitive` or `detailed`. Follow an explicit user selection. Otherwise infer it from intended use: presentation or spoken-explanation support selects `intuitive`, while a handout, reference, or other document read without a presenter selects `detailed`. Use `intuitive` when intended use is unknown.

The field name `Blindly inferred topic` is retained in both modes for format compatibility. In `intuitive` mode it contains the evaluator's single inferred topic; in `detailed` mode it contains the evaluator's complete inferred reconstruction.

`Applied contexts` contains the names of all Context Skills actually read while making the plan, including visual styles. Use their discoverable Skill names, such as `$diagram-design-principles`, without paths or snapshots. Do not list Process Skills. Write `- None` when no Context Skill was read.

The base format has no concept list. A concept list or any other section is added only when an applied Context or the intended downstream implementation requires it. Extensions must not replace or weaken the required fields.

Do not include image filenames, image directories, link destinations, or other implementation-selected output locations.

Plan every composition within the capabilities and constraints of the intended implementation method. Apply requirements supplied by that implementation method when planning, and do not plan visual detail or effects that the method cannot reproduce—for example, do not require numerous rich illustrations from an implementation limited to ordinary presentation shapes.

The ASCII composition is a structural contract for elements, topology, containment, semantic ordering, directed source-to-target connections, and coarse relative placement. Downstream implementations preserve recognizable left/right and above/below relations, the primary layout direction, and rough element order; they do not reverse those relations or change a horizontal arrangement into a vertical one. It is not a rendering specification for exact coordinates, distances, alignment, proportions, size, shape, color, typography, or style. Implementations optimize those details and the visual treatment for their medium rather than mechanically tracing the ASCII grid. The composition's outer border is a canvas boundary, not a visible container, unless the plan explicitly gives it semantic meaning.

## Blind evaluation

For every diagram:

1. Fix the exact ASCII composition that will appear in the plan.
2. The planning agent itself reads the source Markdown and extracts the complete content before the target paragraph starts as preceding content. Do not include any part of the target paragraph or anything after it. For the first target paragraph, preceding content may be empty.
3. Start a fresh subagent without conversation history or applied Skills. Use the evaluator model requested by the user when one is specified. Otherwise use the lowest-capability model tier available from the current provider: Luna in Codex, Haiku in Claude Code, and the equivalent lowest-level model in other providers' model families. Do not silently substitute a higher-level model when the required low-level model is available.
4. Construct the evaluator's prompt by embedding the exact ASCII composition and the literal extracted preceding content directly in the prompt. When preceding content is empty, embed only the composition. In `intuitive` mode, ask for the single topic the composition communicates in that context. In `detailed` mode, ask for a detailed reconstruction of all meaning the composition communicates in that context, including propositions, qualifications, causes, evidence, and contrasts.
5. Never give the evaluator the source file, its path, an attachment, a file or resource reference, or an instruction such as “read this file through line N.” Do not let it retrieve the source through filesystem, workspace, search, or document tools. The evaluator works only from the text embedded directly in its prompt and does not read any other document. In this blind stage, also do not give it the target paragraph, topic sentence, later source content, expected interpretation, applied Contexts, concept list, or explanatory material written by the planner.
6. After its answer is fixed, give the same subagent the comparison source selected by the plan mode. Ask it to compare that source only with its already-fixed `Blindly inferred topic`. The fixed inference is the evidence being evaluated: do not reinterpret the ASCII composition, produce a new inference, repair or supplement the fixed inference, or credit the composition for meaning absent from that inference. Preceding content may resolve context but cannot supply new meaning introduced by the target paragraph. Fail even if a post-reveal reading of the composition could recover meaning absent from the fixed inference.
   - `intuitive`: Give only the topic sentence. Pass only when the fixed inference preserves that sentence's new central meaning. Differences in details not required by the topic sentence are outside the comparison.
   - `detailed`: Give the complete target paragraph. Pass only when the fixed inference preserves every distinct proposition, qualification, cause, item of evidence, example, and contrast contributed by the paragraph without omission, reversal, or serious misunderstanding. Treat a detail as required whenever removing it would reduce or change the information expressed by the paragraph.
7. Record the subagent's initial answer verbatim as `Blindly inferred topic`, including the complete reconstruction produced in `detailed` mode. Record its comparison verbatim as `Comparison` and its final `Pass` or `Fail` as `Verdict`.
8. A failure requires revising the composition and repeating the evaluation with a new subagent.

The ASCII composition in the evaluation and the plan must be identical, including whitespace, annotations, and symbols. Any later change invalidates the evaluation and requires the complete procedure to be repeated with a new fresh subagent that has none of the previous evaluation content.
