---
name: domain-driven-development
description: Implement the entire application with domain-driven development (DDD) architecture. Use when you design and implement the overall architecture of the application, define domain objects and their relationships, implement business logic in services, and create APIs and UI components for the domain objects and logic.
---

# Domain-Driven Development (DDD) Architecture

## Layers

Our DDD architecture has three layers.

### External Services (`external/`)

This layer contains code related to external services, such as LLM backends, databases, queues, etc.
This layer is responsible for connecting our application to external services, **but it must be domain-agnostic**.

### UI components (`components/`)

This layer contains reusable React UI components that are not specific to any domain, such as buttons, modals, form inputs, etc.
These components should be as dumb as possible, with no business logic or domain-specific knowledge.

### Domain (`domain/`)

This layer contains all domain-related code, including domain objects, business logic, APIs and **UI components dedicated for representing the domain objects**.

This layer has three sub-layers:

#### Core (`domain/[domain name]/core/`)

This layer contains domain objects (as TypeScript types) and business logic (as pure functions).
**Interface of this layer must be technology-agnostic** and have no dependencies on any third-party libraries, specific storage or UI technologies.
Internally you can use any third-party libraries, but the interface must be clean and technology-agnostic to ensure that the core domain logic is reusable and testable without any specific technologies.



#### Adapters (`domain/[domain name]/adapters/`)

This layer contains code that connects the core to specific technologies, such as storages, queues, LLM backends etc.
This layer just connects core domain objects and logic to specific technologies, so it must be as thin as possible and contain no business logic.

#### UI (`domain/[domain name]/ui/`)

This layer contains React components dedicated for representing the domain objects and logic. 
These components should focus on representing a single domain object with no reusability across domains.
These components can use domain objects and logic from the core layer, but they must not have their own business logic.

### Application (`app/`)

This layer combines all the above layers to implement the actual application using React Router Framework Mode.
It contains Route Modules, global UI components (e.g., navigation, footer), and any other code related to the overall application structure.

## Directory Structure

```
domain
├── [domain name]
│   ├── core
│   │   ├── models.ts
│   │   ├── lifecycle.ts
│   │   ├── services.ts
│   │   └── index.ts
│   ├── adapters
│   │   ├── [adapter name].ts
│   │   └── index.ts
│   └── ui
│       ├── [Component name].tsx
│       └── index.ts
external
components
app
```

## Rules

### Domain Objects

Domain objects must be defined as **TypeScript types branded with `__brand` fields** in `domain/[domain name]/core/models.ts`.
Every Value Object (typically properties of entities) must be branded.
Entities itself should not be branded. Correctness of the entities is guaranteed by the Factory functions.
This ensures that domain objects are not accidentally created or manipulated without using the correct factories and services,

```ts
export type UserId = string & { __brand: "UserId" };
export type UserName = string & { __brand: "UserName" };
export type UserEmail = string & { __brand: "UserEmail" };
export type User = {
  // not branded
  id: UserId;
  name: UserName;
  email: UserEmail;
};
```

### Factories

Each domain object must have a Factory function in `domain/[domain name]/core/lifecycle.ts` that ensures the correctness of the created objects.

Factories may use validation libraries (e.g. Zod) only as an internal implementation detail. Specifically:
- Validation libraries must not appear in factory public interfaces, types, or errors.
- Factory inputs and outputs must consist only of primitives and domain types.
- The choice of validation library must be replaceable without affecting callers.

```ts
export type User = { ... };
// Zod schema is NOT exported
const userNameSchema = z.string().min(1).max(50);

export function validateUserName(value: string): UserName {
  const result = userNameSchema.safeParse(value);

  if (!result.success) {
    // ドメイン語彙で失敗を表現する
    // ZodError をそのまま投げない
    throw new Error("Invalid UserName");
  }

  return result.data as UserName;
}

export function createUser({
  _id?: string,
  _name: string,
  _email: string
}): User {
  const id = _id ? validateId(_id) : crypto.randomUUID() as UserId;
  const name = validateUserName(_name); // string -> UserName
  const email = validateUserEmail(_email); // string -> UserEmail
  return {
    id: id,
    name: name,
    email: email,
  };
}
```

Every instances of domain objects must be created via the Factory functions, and direct object creation is prohibited.

### Repositories

For each domain object, there must be a Repository.

Abstract Repository interfaces must be defined in `domain/[domain name]/core/lifecycle.ts`, and concrete Repository implementations must be defined in `domain/[domain name]/adapters/` that connect the abstract Repository interfaces to specific storage technologies.

```ts
// core/lifecycle.ts
export interface UserRepository {
  getById(id: UserId): Promise<User | null>;
  save(user: User): Promise<void>;
  delete(id: UserId): Promise<void>;
}

// adapters/repository.ts
import { UserRepository } from "../core/lifecycle";
export class UserRepositoryImpl implements UserRepository {
  async getById(id: UserId): Promise<User | null> {
    // connect to specific storage and return User
  }

  async save(user: User): Promise<void> {
    // connect to specific storage and save User
  }

  async delete(id: UserId): Promise<void> {
    // connect to specific storage and delete User
  }
}
```

### Services

Any calculation from or manipulation of domain objects must be implemented as pure functions in `domain/[domain name]/core/services.ts`.
These functions take domain objects as arguments, return updated copies of domain objects, and never mutate their arguments or access any storage.
All business logic must be implemented in these service functions, and they must be thoroughly unit tested.

```ts
export function updateUserEmail(user: User, newEmail: string): User {
  const updatedEmail = validateUserEmail(newEmail); // string -> UserEmail
  return {
    ...user,
    email: updatedEmail,
  };
}
```

Simple CRUD shouldn't be services. They should be acheved just by calling factories (C) and repositories `get` (R), `save` (U) and `delete`(D)

### APIs

Each domain should have a set of APIs (as functions) exposed to applications and other domains in `app/domain/[domain name]/index.ts`. These APIs must cover all use cases of all features but must be as few as possible (no redundancy allowed).

```ts
export async function createUser(name: string, email: string): Promise<User> {
  const user = createUser({ _name: name, _email: email });
  await userRepository.save(user);
  return user;
}
```

### UI components for domain objects