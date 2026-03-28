---
name: domain-driven-development
description: Implement the entire application with domain-driven development (DDD) architecture. Use when you design and implement the overall architecture of the application, define domain objects and their relationships, implement business logic in services, and create APIs and UI components for the domain objects and logic.
---

# Domain-Driven Development (DDD) Architecture

## Layers

Our DDD architecture has three layers.

### Domain (`domain/[domain name]/`)

This layer contains all domain-related code, including domain objects, business logic, APIs.

**Interface of this layer must be technology-agnostic** and have no dependencies on any third-party libraries, specific storage or UI technologies.
Internally you can use any third-party libraries, but the interface must be clean and technology-agnostic to ensure that the core domain logic is reusable and testable without any specific technologies.

This layer must not have any dependencies on the other layers.

Read [rules/domain.md](rules/domain.md) for details on Domain Objects, Factories, Repositories, and Services.

### External Services (`external/`)

This layer contains code related to external services, such as LLM backends, databases, queues, etc.
This layer is responsible for connecting our application to external services.

Read [rules/external.md](rules/external.md) for guidelines on external service integration.

### Adapters (`adapter/[domain name]/`)

This layer contains code that connects the core to specific technologies, such as storages (Repository implementation), queues, LLM backends etc., which are set up in the `external/` layer.

This layer just connects core domain objects and logic to specific technologies, so it must be as thin as possible and contain no business logic.

Read [rules/adapters.md](rules/adapters.md) for adapter implementation patterns.

### UI components (`component/`)

This layer contains reusable React UI components that are not specific to any domain, such as buttons, modals, form inputs, etc.
These components should be as dumb as possible, with no business logic or domain-specific knowledge.

Read [rules/components.md](rules/components.md) for component design principles.

### Domain-UI (`domain-ui/[domain name]/`)

This layer contains React components dedicated for representing the domain objects and logic.
These components should focus on representing a single domain object with no reusability across domains.
These components can use domain objects and logic from the core layer, but they must not have their own business logic.

Read [rules/domain-ui.md](rules/domain-ui.md) for domain-specific component patterns.

### Use cases (`usecase/`)

This layer contains functions that implement specific use cases of the application by combining domain objects, services, and APIs.

At the early stage of development, you can implement use cases directly in Route Modules without creating this layer, but as the application grows, you should refactor the code to create this layer and move use case components here to keep Route Modules thin and focused on routing and data loading/mutation.

Read [rules/usecase.md](rules/usecase.md) for use case implementation patterns.

### Application (`app/`)

This layer combines all the above layers to implement the actual application using React Router Framework Mode.
It contains Route Modules, global UI components (e.g., navigation, footer), and any other code related to the overall application structure.

Read [rules/app.md](rules/app.md) for application structure and integration guidelines.

## Directory Structure

```
domain
├── [domain name]
│   ├── models.ts
│   ├── lifecycle.ts
│   └── services.ts
external
├── [service name]
│   └── [filename]
adapters
├── [domain name]
│   └── [adapter name].ts
components
├── [component name].tsx
domain-ui
├── [domain name]
│   └── [component name].ts
usecase
├── [use case name].ts
app
├── [directory structure for React Router Framework Mode]
[other files and directories like tsconfig.json, package.json, etc.]
```

## Principles

### Keep it minimal and simple

The architecture should be as simple as possible while still adhering to DDD principles. Avoid over-engineering such as unnecessary abstractions, DTOs or patterns that do not add clear value to the application.