# Contributor Guidelines
This project defines an interoperable model for annotating sport video for coaching purposes.

Contributions are welcome, but the long-term goal is stability and interoperability, not feature completeness. These guidelines exist to ensure that extensions remain coherent, implementable, and aligned with the project’s design principles.

## 1. Core principles
All contributions must respect the following principles:

### 1.1 Backward compatibility
* Valid v0 annotations must remain valid in all future versions.
* Breaking changes require a major version and strong justification.
* New fields must be optional by default.

### 1.2 Minimalism first
* Do not add fields unless there is a clear, demonstrated coaching use case.
* Prefer composition over expansion (add a new object rather than extending many existing ones).
* If a feature can be implemented at the application level, it probably does not belong in the core model.

### 1.3 Separation of concerns
Contributions must respect the conceptual boundaries of the model:

| Concern               | Belongs where       |
| --------------------- | ------------------- |
| What happened         | `body`, `aspect`    |
| Why it was annotated  | `role`              |
| Where/when it applies | `target`            |

Avoid mixing concerns in a single field.

### 1.4 Standards alignment
* Reuse existing standards whenever possible.
* Do not redefine mechanisms that already exist in:
  * W3C Web Annotation
  * Media Fragments
  * SVG

## 2. Scope discipline
### 2.1 In scope
* Semantic extensions related to coaching interpretation
* Additional annotation roles
* Aspect refinements
* Relationships between annotations
* Optional evaluation layers

### 2.2 Out of scope
* UI or rendering requirements
* Coaching methodology or pedagogy
* User accounts, permissions, or workflows
* Transport protocols or real-time systems

Proposals that blur these boundaries are likely to be rejected.

## 3. Proposing changes
All non-trivial contributions must include:

1. **Problem statement**
   * What real coaching problem does this solve?
   * Why is v0 insufficient?

2. **Minimal proposal**
   * What is the smallest change that addresses the problem?
   * What is explicitly *not* included?

3. **Compatibility analysis**
   * Does this break existing annotations?
   * How should v0 consumers handle this change?

4. **Mapping to standards**
   * How does this relate to W3C Web Annotation concepts?
   * Is an existing mechanism being reused or extended?

5. **Examples**
   * At least one concrete JSON example
   * Preferably one cross-sport example

## 4. Vocabulary and semantics
### 4.1 Controlled vocabularies
* New controlled vocabularies must be:
  * Clearly scoped
  * Justified by multiple sports
  * Extensible
* Avoid sport-specific terms at the top level.

### 4.2 Naming conventions
* Use lowercase snake_case or lowercase words for values.
* Avoid overloaded terms.
* Prefer coach-facing language over academic jargon.

## 5. JSON Schema contributions
When modifying or adding schemas:

* Keep schemas readable by humans
* Avoid deep nesting unless necessary
* Use `additionalProperties: false` intentionally
* Provide migration notes when extending schemas

All schema changes must be accompanied by:

* Validation examples
* At least one negative example (what should fail)

## 6. Extension strategy
Extensions should be:

* Additive
* Optional
* Independently usable

Avoid designs where:

* One extension implicitly requires another
* Consumers must implement multiple features to support one use case


## 7. Documentation expectations
Every contribution must update or include:

* Rationale explaining *why* the change exists
* Examples showing *how* it is used
* Clear statements of non-goals

If the contribution introduces a new concept, it must be explained in plain language.

## 8. Decision-making and review
* Preference is given to proposals that:

  * Reduce ambiguity
  * Improve interoperability
  * Align with existing standards
* Simpler solutions are favored over expressive ones.
* Disagreement should be resolved by reference to:

  * Coaching practice
  * Interoperability impact
  * Long-term maintenance cost

## 9. What makes a good contribution
A strong contribution typically:

* Solves a real coaching problem
* Adds one concept, not many
* Includes clear examples
* Leaves room for future evolution
* Respects the spirit of v0

## 10. Final note to contributors
This project values restraint as much as innovation.

The most valuable contributions are often those that:
* Say “not yet”
* Clarify boundaries
* Make the model easier to understand and implement

If in doubt, propose less — it can always be extended later.
