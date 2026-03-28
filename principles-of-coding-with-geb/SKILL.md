---
name: principles-of-coding-with-geb
description: Principles of coding tasks I prefer. Use this skill for EVERY code-related task (e.g., implementation planning, coding, writing documentations).
---

# Principles of Coding

## Do not rely on descriptions of the implementation

Docs may lie; implementations do not.

When working, you may use **only the following four types of information** as authoritative:

- The implemented source code
- Coding conventions or guidelines that *do not* describe the implementation
- Any content outside descriptions of the implementation
- Your prior knowledge and information outside this repository (e.g., public documentation)

Documents that *describe the implementation*—including specifications, design docs, and implementation descriptions—may be used **only as guidance** to help you understand the implementation or guidelines.
They must **never** be treated as authoritative.

After reading any implementation description, you must verify that the actual implementation matches the description.
If it does not, treat the description as false and ignore it.

## NO ambiguities but DO NOT guess

DO NOT use any vague terms (e.g., "or", "probably", "seems to be"). Keep investigating until ambiguity is gone; if you still can't find the info, DO NOT guess, instead mark it as [**NEEDS INFORMATION**: {describe what you need}].
