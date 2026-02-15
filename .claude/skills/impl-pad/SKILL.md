---
name: impl-pad
description: Implement following your Pad (a markdown file named `pad.md`). Use When the user instructs you to implement something, specifying pad.md.
---

# Implement Pad

Implement following your Pad (a markdown file named `pad.md` in this repository that has instructions for you) following the "Execution" section below.

## Execution

1. Find the Pad by searching the name `pad.md` in this repo. if you can't find or find multiple, ask the user its path and stop your work.
2. Read the "Instruction" in the Pad and understand user's instruction.
3. Check the language used in the "Instruction" section and use the same language for your work.
4. Read the "Current" section and the source code referred in the section to understand current implementation.
5. Read the "New" section, especially the "Step-by-step Implementation" in the "Implementation Plan" subsection, to understand how you should implement.
6. Follow the step-by-step implementation plan to complete the implementation.
7. **Verify all behaviors in the Pad are satisfied**:
   - Read the `## New` section's `### Behavior` subsection in the Pad
   - This section contains test cases that must ALL be satisfied
   - **Prioritize automated testing**:
   - **Only use manual testing when**:
     - No testing framework is available, OR
     - Automated tests fail due to complexity or environmental issues (e.g., UI tests with element finding issues, async timing problems)
   - For each behavior listed in the format "**Given** [initial state], **When** [action], **Then** [expected outcome]":
     - Verify using automated tests (preferred) or manual testing (fallback)
   - If any behavior is NOT satisfied, fix the implementation and verify again
   - Repeat this verification loop until ALL behaviors are confirmed to work correctly
8. When all behaviors are verified, inform the user that implementation is complete and all behaviors have been confirmed.

## Principles

### Do not rely on descriptions of the implementation

Docs may lie; implementations do not.

When working, you may use **only the following four types of information** as authoritative:

- The implemented source code
- Coding conventions or guidelines that *do not* describe the implementation
- Any content in the Pad *outside* the `### Current` section
- Your prior knowledge and information outside this repository (e.g., public documentation)

Documents that *describe the implementation*—including specifications, design docs, and the contents of the Pad’s `## Current` section—may be used **only as guidance** to help you understand the implementation, guidelines, or instructions.
They must **never** be treated as authoritative.

After reading any implementation description, you must verify that the actual implementation matches the description.
If it does not, treat the description as false and ignore it.

### Don’t be afraid of rework

Always watch closely to ensure the Pad entries are correct and sufficient to fulfill the instructions. If you notice any issues, stop immediately and inform the user of what needs to be corrected.
