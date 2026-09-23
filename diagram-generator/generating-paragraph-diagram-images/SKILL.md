---
name: generating-paragraph-diagram-images
description: Use when a paragraph diagram plan must be implemented as raster images and inserted into its referenced Markdown source.
---

# Generating Paragraph Diagram Images

## Purpose

Implement an existing paragraph diagram plan as raster images linked from the source Markdown, without planning or redesigning the diagrams.

## Input

The input is Markdown produced by `planning-paragraph-diagrams`. Accept it only when it contains the source path, `Applied contexts`, and for every diagram a prose-paragraph number, topic sentence, exact ASCII composition, blind evaluation, and passing verdict. Legacy `illustrating-paragraphs` plans are not accepted.

Resolve and read every Context Skill named in `Applied contexts` before implementation. Stop and report the unresolved name if any Context cannot be loaded; do not substitute general conventions. Validate every Context-required plan extension, such as the common concept list required by `$diagram-design-principles`.

Read the source Markdown from the recorded path. Count prose paragraphs by the planning format's rules and require the recorded paragraph number to have the recorded topic sentence. Stop on a missing file, mismatch, failed verdict, missing semantic field, or Context inconsistency. Mechanical omissions in output filenames, directories, relative links, and link syntax are implementation decisions, not plan errors.

## Outcome

The completed implementation has these observable properties:

- Each plan entry has exactly one corresponding raster image, with no omissions or duplicates.
- Each image implements the entry's exact topic, ASCII composition, applied Contexts, and Context-specific definitions without replanning them.
- Every image has an exact 16:9 aspect ratio and uses the frame to its outer edge with zero exterior whitespace, margin, or padding.
- The implementation chooses collision-free image locations and filenames suited to the source document and repository; the plan is not modified to add them.
- One valid relative image link is immediately after each target paragraph and points to its corresponding existing image.
- The source prose and its order are unchanged, and no unrelated source content is changed.

Choose alt text from the planned topic sentence. Before completion, inspect the saved files and edited Markdown to verify image dimensions, one-to-one correspondence, insertion positions, relative link resolution, and preservation of source content.

