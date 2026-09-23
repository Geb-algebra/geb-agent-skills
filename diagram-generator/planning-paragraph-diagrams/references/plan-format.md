# Paragraph Diagram Plan Format

## Required structure

Produce Markdown with this structure. Headings may be localized, but the fields and their meanings are fixed.

````markdown
# Diagram plan

Source: `<path-to-source-markdown>`

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

`Applied contexts` contains the names of all Context Skills actually read while making the plan, including visual styles. Use their discoverable Skill names, such as `$diagram-design-principles`, without paths or snapshots. Do not list Process Skills. Write `- None` when no Context Skill was read.

The base format has no concept list. A concept list or any other section is added only when an applied Context or the intended downstream implementation requires it. Extensions must not replace or weaken the required fields.

Do not include image filenames, image directories, link destinations, or other implementation-selected output locations.

Plan every composition within the capabilities and constraints of the intended implementation method. Apply requirements supplied by that implementation method when planning, and do not plan visual detail or effects that the method cannot reproduce—for example, do not require numerous rich illustrations from an implementation limited to ordinary presentation shapes.

## Blind evaluation

For every diagram:

1. Fix the exact ASCII composition that will appear in the plan.
2. From the source Markdown, take the complete content before the target paragraph starts as preceding content. Do not include any part of the target paragraph or anything after it. For the first target paragraph, preceding content may be empty.
3. Start a fresh subagent without conversation history or applied Skills. Use the evaluator model requested by the user when one is specified. Otherwise use the lowest-capability model tier available from the current provider: Luna in Codex, Haiku in Claude Code, and the equivalent lowest-level model in other providers' model families. Do not silently substitute a higher-level model when the required low-level model is available.
4. Give it the exact ASCII composition together with the preceding content and ask for the single topic the composition communicates in that context. When preceding content is empty, give it only the composition.
5. In this blind stage, do not give it the target paragraph, topic sentence, later source content, expected interpretation, applied Contexts, concept list, or explanatory material written by the planner.
6. After its answer is fixed, give the same subagent the topic sentence and ask it to compare that sentence only with its already-fixed `Blindly inferred topic`. The fixed inference is the evidence being evaluated: do not reinterpret the ASCII composition, produce a new inference, repair or supplement the fixed inference, or credit the composition for meaning absent from that inference. Pass only when the fixed inference itself preserves the topic sentence's new central meaning. If the fixed inference omits, reverses, or seriously misunderstands that meaning, fail even if a post-reveal reading of the composition could recover it. Differences in details not required by the topic sentence are outside the comparison and are not reasons to fail.
7. Record the subagent's initial answer verbatim as `Blindly inferred topic`, its comparison verbatim as `Comparison`, and its final `Pass` or `Fail` as `Verdict`.
8. A failure requires revising the composition and repeating the evaluation with a new subagent.

The ASCII composition in the evaluation and the plan must be identical, including whitespace, annotations, and symbols. Any later change invalidates the evaluation and requires the complete procedure to be repeated with a new fresh subagent that has none of the previous evaluation content.
