# Testing

These are general rules for how to go about testing.
Platform-specific rules are allowed to take precedence.

## Non-UI Code

- Use red/green TDD. Add the tests first.
- Ensure that new code has high test coverage.
- Consider adding unit tests for older code to improve coverage.
- Tests should be deterministic.
- Unit tests should not require network access.
- Full end-to-end integration tests can require network access if it is essential.
- Focus testing on changed behavior, important failure paths, and regression risk rather than chasing raw coverage numbers.
- Prefer tests through stable interfaces, and avoid excessive mocking when cheap real collaborators are available.
- If relevant tests cannot be run, report the exact gap and the likely risk.

## UI Code

User Interface code may be hard to unit test.

If the platform has a live preview feature (for example, #Preview for SwiftUI), create previews.

If the platform has a UI-testing framework (for example, XCTest UI testing for Swift), use it.
Create UI tests that target important behaviours, state changes, and key navigation.
UI tests can be fragile - avoid creating tests that are sensitive to stylistic or layout changes.

Use previews to support fast iteration, but do not treat them as a full replacement for other relevant UI or integration validation.
