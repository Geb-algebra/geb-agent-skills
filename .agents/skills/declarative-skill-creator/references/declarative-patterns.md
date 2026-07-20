# Declarative Transformation Patterns

## Convert How into declarations

Use these conversions when the specified method is not itself required:

| Procedural statement | Declarative expression |
| --- | --- |
| Always run the test command after making changes | All relevant automated tests pass |
| Read the configuration file first | Treat the configuration file as an authoritative source for configuration and ensure the result is consistent with it |
| Review before deploying to production | Do not change production without a recorded approval, and include the approval history in the result |
| Implement this with API X | If compatibility with API X is required, define that compatibility as an outcome; otherwise, do not prescribe it as a means |
| Inspect every file in order | Identify every target that affects the outcome and ensure all acceptance criteria are satisfied |

## Example: Bug-fixing Skill

### Purpose

Restore the user's ability to use the affected feature correctly.

### Outcomes

- The reported reproduction conditions no longer produce the bug.
- The expected behavior is verifiable.
- All relevant automated tests pass.
- Existing public APIs and unrelated behavior remain intact.

### Premises

- The target codebase, reported behavior, expected behavior, and executable test environment.

### Constraints

- Do not preserve the bug by changing tests away from the expected behavior.
- Do not break existing public APIs.

This definition does not prescribe the investigation order, edited files, tools, or repair method.

Place organization-wide source-authority or production-safety rules in separate information-providing Skills rather than this activity Skill.

## Example: Development-progress visibility Skill

### Purpose

Enable early detection of sprint delays and unaddressed work so that stakeholders can make the necessary decisions.

### Outcomes

- Represent the design, implementation, and test status of every feature in CSV format.
- Make delays, unaddressed work, and unknown ownership identifiable.
- Do not present information absent from the inputs as a verified fact.

### Premises

- The sprint plan, feature list, owners, and current design, implementation, and test status.

### Constraints

- Do not modify the source systems.
- Do not guess unknown values.
- Do not treat implementation status alone as overall progress.

This definition does not prescribe the information-gathering order, aggregation tool, or CSV-generation method.
