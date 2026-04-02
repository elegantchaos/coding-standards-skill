# Implementation Guidance

Use this file when deciding how broad a change should be and how code should be structured.

## Precedence

- Follow repository-local `AGENTS.md` first.
- Then follow any local guidance explicitly referenced by that `AGENTS.md`.
- Use relevant skills.
- Use `~/.local/share/agents/COMMON.md` only to fill gaps or resolve ambiguity.
- Never let shared fallback guidance override explicit local repository rules.

## Change Strategy

- Apply focused changes to perform the requested actions.
- Fix root problems, don't layer workarounds.
- You are allowed to adopt a new architecture, but ask first. Explain what problem it solves and why it is necessary.
- You are allowed to modernize code aggressively.
- You are allowed to add complexity to the design, but ask first. Explain what problem it solves and why it is necessary.

## Refactoring

- Refactor aggressively to avoid code duplication.
- Prefer a series of small refactorings to one large one.
- If you introduce a new architecture or idiom, refactor the existing codebase to stay consistent.

## Backwards Compatibility

- Assume that backwards compatibility is not required, unless explicitly requested.
- Assume that you can break existing API contracts, unless explicitly prohibited.
- Do not add shims, wrappers, adapters, aliases, or backward-compatibility layers, unless explicitly requested.
- Treat a refactored API, tool, script, or interface as the new source of truth.
- Update known call sites, tests, and documentation as part of the same change.
- If compatibility support is requested, make it explicit and keep its scope tight.

## Interfaces And Dependencies

- Keep interfaces explicit, intentionally small, and unsurprising.
- Avoid hidden coupling and surprising side effects.
- Do not add dependencies without clear justification.
- Keep secrets and credentials out of source control and out of committed configuration.

## Formatting

- Prefer formatters and linters over manual stylistic rewriting.
- Use project configuration or language-specific guidance to determine format/lint tooling.

## Documentation

- Update when workflows, commands, designs, architecture or implementation changes.
- Avoid referring to the past - document the current state.
- Remove stale or contradictory docs rather than layering new text on top.
- Keep factual, concise, and aligned with current behavior.
- If specifically instructed to produce a migration guide, you can provide historical context, otherwise avoid it.

## Comments

- Update whenever code is touched.
- Do not use to restate symbol names or obvious control flow.
- Remove stale or contradictory comments rather than layering new text on top.
- Avoid referring to previous behaviour, migrations, legacy in comments.
- State what the code does now, not what it used to do.

### Inline Comments

- Keep inline comments sparse
- Reserve them for subtle logic that a future maintainer could misread.
- Focus on intent, invariants, side effects, and non-obvious constraints.

### Documentation Comments

- Add to all types and members, including private members
- For the benefit of someone browsing the code.
- To allow IDEs to surface documentation in their UIs.
- They should be compact but informative.
- They do not need to slavishly repeat every parameter or return type.
- Add a larger comment before each type definition giving its purpose and design.

## Path Portability

- Do not embed machine-specific absolute paths in committed code, documentation, or configuration.
- Prefer repository-relative paths for resources that live in the current repository.
