---
name: write-pad
description: Write your Pad (a markdown file named `pad.md` in this repository). Use when the user instructs you to write a pad.md.
---

# Write Pad

Write your Pad (a markdown file named `pad.md` in this repository that has instructions for you) following the "Execution" section below.

You can write only the Pad throughout this session. DO NOT implement anything and DO NOT change any other docs.

## Execution

1. **Handle user input**:
   - **If the user provided inline instructions** (e.g., `/write-pad {instructions}`):
     - Create `pad.md` at the project root with title `# [Change Name]` and `## Instruction` section
     - Write the user's inline instructions into the `## Instruction` section with NO MODIFICATIONS (except formatting as markdown if needed)
     - Proceed to step 2
   - **If no inline instructions were provided**:
     - Find the Pad by searching for `pad.md` in this repo
     - If you can't find it or find multiple, ask the user for its path and stop your work
     - **If pad.md is empty or only contains user instructions without any sections:**
       - Create the initial structure with a title `# [Change Name]` and `## Instruction` section
       - Move any existing content from pad.md into the `## Instruction` section
       - Proceed to step 2
     - **If pad.md already has sections:**
       - Check if "Instruction" section has at least a brief description of the change. If not, ask the user to fill the section and stop your work.
2. Check the language used in the "Instruction" section and use the same language for your work.
3. Check which sections (`## Current` and `## New`) exist and are already filled in.
4. Read all completed sections, and if they include file names and line numbers for related code, read those as well.
5. Determine which sections need to be written:
   - Identify all empty or missing sections among `## Current` and `## New`
   - If all sections are complete, ask the user what to do next
6. **Default behavior**: Write all remaining sections sequentially, following the "Self-Review Loop" below for each section.
   - **Exception**: If the user explicitly requests section-by-section review (e.g., "review each section", "one section at a time", "confirm before proceeding"), write only one section, ask for user review, and **STOP WORKING** until the user provides feedback or approval.
7. **Self-Review Loop** (for each section):
   - Write the section following "Section Guidelines" below
   - Review what you wrote against "Principles" and "Section Guidelines"
   - If any violation is found, revise the section
   - Repeat review and revision until no violations remain
   - Only after confirming no violations, proceed to the next section
8. When all sections are complete, inform the user that the Pad is ready for review.

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

### NO ambiguities but DO NOT guess

DO NOT use any vague terms (e.g., "or", "probably", "seems to be"). Keep investigating until ambiguity is gone; if you still can't find the info, DO NOT guess, instead mark it as [**NEEDS INFORMATION**: {describe what you need}].

## Section Guidelines

### Instruction Section

Describe the changes. This section should already be written by the user before you start working.

Expected contents:

- What changes will be made
- Which files will be modified (with file paths)
- Which existing implementations in which files are relevant
- Libraries to be used
- Edge cases to consider

### Common Subsection Guidelines

Both "Current" and "New" sections have three subsections: **Behavior**, **Key Entities**, and **Implementation/Implementation Plan**. Follow these guidelines for all subsections:

#### Behavior Subsection Guidelines

Describe the **outermost interface** behavior only.

**Interface Boundary Rules**:

- **Functions/classes**: Public API only. NO internal sub-functions, helper methods, or implementation details.
- **APIs**: Endpoint interface (request/response) only. NO internal services, database operations, or internal objects.
- **App features**: UI behavior only. NO APIs, services, or functions called internally.

**Requirements**:

- Black-box description from user's/caller's perspective
- Comprehensive test coverage: ALL scenarios (normal paths, edge cases, error cases, input combinations)
- Non-technical language suitable for non-technical reviewers

#### Key Entities Subsection Guidelines

Describe the **conceptual model**, NOT implementation.

**Focus on**:

- What concepts/objects exist in the domain
- What they represent in business/domain terms
- How they relate conceptually
- Key attributes (what data, not how implemented)

**DO NOT mention**:

- File names, class names, function names
- Implementation details (storage, processing)
- Technical implementation choices

#### Implementation Subsection Guidelines

Map conceptual model to actual code.

**Requirements**:

- Every detail must include file paths and line numbers
- Document which files/classes/modules implement each entity
- Where entity data is stored/managed
- Which functions/methods handle operations
- Reusable implementations and reference patterns

### Current Section

Investigate current implementation and its gap from "Instruction" section requirements.

Attach file paths and line numbers for *every* item. NO vague terms ("or", "probably", "seems to be"). If unclear, mark [**NEEDS INFORMATION**: {describe what you need}].

This section has four subsections:

#### Behavior

See "Behavior Subsection Guidelines" above for detailed requirements.

Format:

```markdown
### Behavior

1. **Given** [initial state], **When** [action], **Then** [current outcome]
2. **Given** [initial state], **When** [action], **Then** [current outcome]
[... continue for ALL scenarios including edge cases and errors]
```

Example for a function:

```markdown
### Behavior

1. **Given** a valid email address, **When** validateEmail() is called, **Then** returns true
2. **Given** an email without @ symbol, **When** validateEmail() is called, **Then** returns false
3. **Given** null, **When** validateEmail() is called, **Then** throws TypeError
```

Example for an API:

```markdown
### Behavior

1. **Given** valid credentials in request body, **When** POST /api/login, **Then** returns 200 with JWT token
2. **Given** incorrect password, **When** POST /api/login, **Then** returns 401 with error message
```

#### Key Entities

See "Key Entities Subsection Guidelines" above for detailed requirements.

Trace entity relations and extract all related entities without omission.

Format:

```markdown
### Key Entities

- **[Entity Name]**: [What it represents in domain terms, key attributes, relationships to other entities]
- **[Entity Name]**: [What it represents in domain terms, key attributes, relationships to other entities]
```

Example:

```markdown
### Key Entities

- **User**: Represents a person using the system. Has name and email. Can create multiple Projects.
- **Project**: Represents a work item that Users can collaborate on. Has a title and description. Belongs to one owner User.
```

#### Implementation

See "Implementation Subsection Guidelines" above for detailed requirements.

Map each entity from "Key Entities" to actual code implementation.

Format:

```markdown
### Implementation

**[Entity Name from Key Entities]**:
- Implemented in [file path:line number]
- Data structure defined at [file path:line number]
- Key operations: [operation name] at [file path:line number]

**Reusable implementations**:
- [Shared utility/component] at [file path:line number]
- [Similar implementation reference] at [file path:line number]
```

Example:

```markdown
### Implementation

**User**:
- Implemented as `User` class in src/models/user.ts:15-45
- Database schema defined in src/db/schema.ts:30-40
- User creation handled by `createUser()` in src/services/userService.ts:100-120

**Project**:
- Implemented as `Project` interface in src/types/project.ts:10-25
- Stored in PostgreSQL, schema at src/db/migrations/003_create_projects.sql:1-20
- CRUD operations in src/services/projectService.ts:30-150

**Reusable implementations**:
- Validation utility functions in src/utils/validation.ts:20-50 can be reused for input validation
- Error handling pattern from src/services/userService.ts:200-210 should be followed
```

#### Gap from Requirements

Summarize what is missing or different from the Instruction section requirements across all aspects (behavior, entities, implementation).

Format:

```markdown
### Gap from Requirements

- [What behavior is missing or different]
- [What entities or attributes are missing]
- [What implementation is missing or needs modification]
```

Example:

```markdown
### Gap from Requirements

- validateEmail() does not validate emails with multiple @ symbols (should return false)
- validateEmail() does not handle empty string input (should return false)
- validateEmail() does not check for domain name validity
- User entity is missing authentication credentials (password hash, authentication tokens)
- Project entity is missing status and creation date attributes
- Missing "ProjectMember" entity for collaboration feature
- No authentication logic implemented (src/auth/authenticate.ts does not exist)
- Missing API endpoints for user registration and login
```

### New Section

Based on "Instruction" and investigated current implementation, describe **only the changes** from Current section.

**Requirements**:

- **DO NOT repeat information from Current section** - only describe what is new or changed
- Implementation plan must be **specific enough that there's only one way to implement it**
- NO vague terms (e.g., "or", "probably", "might", "could")
- NO ambiguous choices (e.g., "use X or Y", "either A or B")
- If you cannot determine the specific approach, mark it as [**NEEDS INFORMATION**: {describe what you need}]
- Every implementation decision must be concrete and unambiguous

This section has three subsections:

#### Behavior

See "Behavior Subsection Guidelines" above for detailed requirements.

List **only** new behaviors and updated existing behaviors. DO NOT list unchanged behaviors.

Format:

```markdown
### Behavior

1. **Given** [initial state], **When** [action], **Then** [expected outcome]
2. **Given** [initial state], **When** [action], **Then** [expected outcome]
[... continue for ALL new/changed scenarios including edge cases and errors]
```

#### Key Entities

See "Key Entities Subsection Guidelines" above for detailed requirements.

List **only** new entities and updated existing entities. DO NOT list unchanged entities. For updated entities, describe only the changes (e.g., "Add X attribute to Y entity").

Format:

```markdown
### Key Entities

- **[New Entity Name]**: [What it represents in domain terms, key attributes, relationships to other entities]
- **[Existing Entity Name]** (update): [Only the changes - new attributes, new relationships]
```

#### Implementation Plan

See "Implementation Subsection Guidelines" above for detailed requirements.

Structure:

1. **Entity Implementation**: For each new/updated entity, specify files/classes/modules, data structures, and operations (with file paths). DO NOT repeat existing implementation details from Current section.
2. **Step-by-step Implementation**: Ordered list where each step specifies exact files to modify, changes to make, and patterns to follow

After writing, verify plan fulfills all instructions, entity updates, and behaviors.

Format:

```markdown
### Implementation Plan

**Entity Implementation**:

**[New Entity Name]**:
- Will be implemented as [class/interface/type] in [file path]
- Data structure: [description] at [file path]
- Key operations: [list operations with file paths]

**[Existing Entity Name]** (update):
- Add [new field/method] to [file path]
- Modify [existing element] at [file path]

**Step-by-step Implementation**:

1. [Step description]
   - Modify [file path]
   - Add/Update [specific code element]
   - Follow pattern from [reference file path]

2. [Step description]
   - Create [file path]
   - Implement [specific functionality]
   - Use [existing utility/pattern from file path]

[Continue for all steps...]
```

Example:

```markdown
### Implementation Plan

**Entity Implementation**:

**ProjectMember** (new):
- Will be implemented as `ProjectMember` interface in src/types/projectMember.ts (new file)
- Data structure: Add `project_members` table schema in src/db/schema.ts
- Key operations: addMember(), removeMember() in src/services/projectService.ts

**User** (update):
- Add passwordHash, authTokens fields to User class in src/models/user.ts:15-45
- Add authentication methods to src/services/userService.ts

**Project** (update):
- Add status, createdAt fields to Project interface in src/types/project.ts:10-25

**Step-by-step Implementation**:

1. Add authentication fields to User
   - Modify src/models/user.ts
   - Add passwordHash: string and authTokens: string[] properties after line 20
   - Follow the field definition pattern from src/models/user.ts:16-18

2. Create ProjectMember entity
   - Create src/types/projectMember.ts
   - Define ProjectMember interface with userId, projectId, role properties
   - Follow the pattern from src/types/project.ts:10-25

3. Implement authentication service
   - Create src/services/authService.ts
   - Implement login(), register(), validateToken() methods
   - Use bcrypt for password hashing (similar to src/utils/crypto.ts:20-30)
   - Use JWT for tokens (pattern from src/middleware/auth.ts:15-25)

[Continue for all steps...]
```
