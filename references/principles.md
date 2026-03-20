# Engineering Principles

Use this file for cross-language design and implementation decisions.

## How To Apply These Principles

- Treat principles as heuristics, not rigid laws.
- If principles conflict, prioritize correctness and safety first, then maintainability, then simplicity and clarity, then performance work, then flexibility for hypothetical future needs.
- If a change increases complexity, state why that complexity is necessary now.
- Prefer local, focused changes over broad refactors unless architecture changes are required.
- Keep public surface area intentionally small.
- Align with established project patterns unless there is a clear, documented reason to diverge.

## Required Principles

### DRY

Intent: Reduce duplication that increases defects and maintenance cost.

Do:
- deduplicate business rules before presentation details
- keep one authoritative source for mutable facts

Don't:
- repeat the same rule in multiple modules
- force abstractions across unrelated contexts

Tradeoff: Over-deduplication can hide intent; keep duplication when it preserves clarity and boundaries.

### Single Source Of Truth

Intent: Keep each important fact, rule, or configuration owned in one clear place.

Do:
- define canonical ownership for configuration, data transformations, and business rules
- derive secondary views from the authoritative source instead of copying values around

Don't:
- let multiple modules drift into owning the same decision
- patch inconsistencies by synchronizing duplicated state manually

Tradeoff: Centralizing ownership can require more deliberate boundaries, but it reduces drift and contradiction.

## Preferred Principles

### KISS

Intent: Prefer the simplest implementation that meets current requirements.

Do:
- choose direct solutions with minimal moving parts
- remove unnecessary abstraction layers

Don't:
- introduce generic frameworks for one-off behavior
- add configurability without concrete need

Tradeoff: Simple local code can duplicate some structure; combine with DRY when duplication becomes costly.

### YAGNI

Intent: Avoid speculative flexibility.

Do:
- implement only validated current requirements
- delay abstraction until concrete reuse appears

Don't:
- design extension points for imagined scenarios
- expose broad APIs just in case

Tradeoff: Deferring generalization can require later refactors; this is preferred to upfront over-engineering.

### Make Illegal States Unrepresentable

Intent: Prevent invalid states through types and constrained interfaces.

Do:
- model domains with enums, value objects, and refined types
- encode invariants at construction boundaries

Don't:
- rely only on late runtime checks for core invariants
- represent constrained states as unconstrained primitives

Tradeoff: Richer types increase model complexity but reduce runtime error paths.

### Dependency Injection

Intent: Make dependencies explicit and replaceable.

Do:
- inject collaborators through constructors or parameters
- keep side-effecting resources behind explicit interfaces

Don't:
- hide dependencies in globals or singletons
- bind logic directly to concrete infrastructure where avoidable

Tradeoff: Extra wiring overhead buys testability and composability.

### Composition Over Inheritance

Intent: Build behavior from small composable units rather than deep hierarchies.

Do:
- compose capabilities with focused types and interfaces
- prefer delegation over inheritance trees

Don't:
- use inheritance for code reuse when behavior is not truly subtype-compatible
- create deep inheritance stacks with implicit coupling

Tradeoff: Composition can introduce more objects but improves change isolation.

### Command-Query Separation

Intent: Keep mutation and information retrieval separate.

Do:
- make commands mutate state without returning derived query data
- make queries return data without side effects

Don't:
- mix mutation and complex reads in one operation
- hide writes inside query-like APIs

Tradeoff: A more explicit API shape can mean extra calls but lowers surprise and coupling.

### Law Of Demeter

Intent: Minimize coupling across module boundaries.

Do:
- keep interactions with direct collaborators
- expose focused interfaces at boundaries

Don't:
- chain through internal object graphs
- depend on transitive implementation details

Tradeoff: Wrapping dependencies can add adapter code but improves modularity.

### Structured Concurrency

Intent: Make concurrency lifetimes and ownership explicit.

Do:
- scope async work to clear task, actor, or thread boundaries
- define ownership for shared mutable state

Don't:
- spawn unscoped background work without lifecycle management
- share mutable state across concurrency domains without protection

Tradeoff: Structured orchestration can add ceremony but improves correctness and cancellation behavior.

### Design By Contract

Intent: Define and enforce preconditions, postconditions, and invariants at boundaries.

Do:
- validate assumptions at module and API boundaries
- fail early with clear diagnostics when contracts are violated

Don't:
- allow silent contract violations to propagate
- rely on callers inferring hidden preconditions

Tradeoff: Runtime checks have small overhead but reduce ambiguity and debugging cost.

### Idempotency

Intent: Make repeated execution of the same side-effecting request safe where appropriate.

Do:
- use idempotency keys or equivalent guards for retried create and update operations
- ensure retries converge to one externally visible result

Don't:
- make retries produce duplicate side effects
- couple retry behavior to unstable timing assumptions

Tradeoff: Idempotency requires state tracking but is critical for resilient workflows.
