# 01 — Code quality and Clean Code

**Week 1 theme:** Build software that is maintainable before trying to scale it. Haseeb listed Clean Code, readability, maintainability, and technical debt as the week's learning topics.

## Readability and naming

Code is read more often than it is written. Choose names that communicate role and intent (`pendingSubmission` conveys more than `data`). Use domain words consistently. Avoid abbreviations that force readers to reconstruct meaning, but don't encode details already clear from the surrounding type or module. Comments should explain why a non-obvious decision exists, not repeat what the next line says.

## Small functions and single responsibility

Break complex work at meaningful boundaries: validate input, apply a rule, persist state, publish a result. A focused function is easier to test and reason about when it has one clear job and limited side effects. Tiny functions are not a goal by themselves; excessive indirection can make flow harder to follow. Group code around behavior and concepts rather than arbitrary line length.

## Abstraction and duplication

An abstraction should hide a real implementation choice or name a meaningful concept. It should reduce the amount a caller must know without introducing more complexity than it removes. Similar-looking code is not always the same rule; abstract when the behavior has a common reason to change. If duplication represents one shared invariant, leaving copies risks divergence.

## Errors and failure paths

Make failure explicit. Validate at boundaries, return/raise errors with enough context for the caller to act, preserve causes for diagnosis, and avoid swallowing exceptions. Separate expected business outcomes (e.g., stale revision) from unexpected faults (e.g., DB unavailable). Do not expose secrets, stack traces, or sensitive data in user-visible errors.

## Review questions

- Can a new teammate explain what this module does from its name and public interface?
- Are side effects and failure modes visible?
- Does an abstraction simplify callers, or only move code elsewhere?
- Is repeated logic the same policy or merely similar syntax?

## Sources

- [Robert C. Martin, Clean Code overview](https://www.oreilly.com/library/view/clean-code-a/9780136083238/)
- Hammad shared a Clean Code reading in Slack during Week 1; see the [program timeline](../00-program-guide.md) and [reported study log](07-research-log.md).
