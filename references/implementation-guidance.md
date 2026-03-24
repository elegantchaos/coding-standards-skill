# Implementation Guidance

Use this file when deciding how broad a change should be and how code should be structured.

## Change Strategy

- Prefer minimal, focused changes that solve the requested problem.
- Prefer fixing root causes over layered workarounds.
- Modernize or adopt a new architecture only when it is warranted by the problem.
- Avoid leaving a code path half-migrated into mixed styles without a clear reason.
- Keep diffs focused and easy to review.
- If a structural change adds complexity, explain what concrete duplication, failure mode, or maintenance risk it resolves.

## Compatibility And Refactoring

- Do not add shims, wrappers, adapters, aliases, or backward-compatibility layers unless compatibility support is explicitly required.
- When refactoring an API, tool, script, or interface, treat the refactored version as the new source of truth.
- Update known call sites, tests, and documentation as part of the same change rather than preserving old entry points by default.
- If compatibility support is genuinely needed, make it explicit and keep its scope tight.

## Interfaces And Dependencies

- Keep interfaces explicit, intentionally small, and unsurprising.
- Avoid hidden coupling and surprising side effects.
- Do not add dependencies without clear justification.
- Keep secrets and credentials out of source control and out of committed configuration.

## Documentation And Comments

- Keep documentation factual and aligned with current behavior.
- Update documentation and comments when workflows, commands, or architecture change.
- Do not use comments to restate symbol names or obvious control flow.
- Keep inline comments sparse and reserve them for subtle logic that a future maintainer could misread.
- Add documentation comments to all types and members, including private members:
  - For the benefit of someone browsing the code.
  - To allow IDEs to surface documentation in their UIs.
  - They should be compact but informative.
  - They do not need to slavishly repeat every parameter or return type.
  - Add a larger comment before each type definition giving its purpose and design.
