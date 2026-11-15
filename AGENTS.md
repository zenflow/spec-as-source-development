# Agent instructions

## Development workflow

Read and follow [Spec-as-Source Development](skills/spec-as-source-development/SKILL.md) when maintaining this repository.

SKILL.md defines the methodology. Read [README.md](README.md) for its purpose and adoption experience, and [ARCHITECTURE.md](ARCHITECTURE.md) for package decisions.

## Working in this repository

- Keep changes focused on the requested outcome and preserve unrelated work.
- Keep the canonical methodology in `skills/spec-as-source-development/SKILL.md`.
- Keep the skill self-contained and its description specific about when it applies.
- Update README guidance and examples when a change affects them; link to rules rather than copying them.
- Keep `LICENSE` and `skills/spec-as-source-development/LICENSE.txt` identical.
- Add supporting files only when they solve a concrete need.
- Report what changed, what was verified, and anything incomplete or unverified.

## Checks

There is no build step or application test suite.

For each change:

- Check edited Markdown for broken local links and section anchors, and review its rendered structure.
- Verify that the skill name matches its directory and its YAML description is present.
- Check that native and standalone adoption instructions agree with `examples/AGENTS.md`.
- Walk through the README bootstrap example, including the transition between milestones.
- Compare the license notices.

When the Agent Skills reference validator is available:

```sh
skills-ref validate skills/spec-as-source-development
```

For meaningful workflow changes, exercise the affected cases in a disposable project:

| Case | What to inspect |
| --- | --- |
| New or revised expectation | Intent is captured faithfully and reflected in design, implementation, and verification. |
| Reversed decision | Obsolete requirements, design decisions, code, and tests are reconciled. |
| Planned stage | Scope stays within the selected stage and delivery status stays truthful. |
| Defect covered by existing requirements | The fix and regression coverage do not create a redundant requirement. |
| Consequential gap | The agent exposes the unresolved question without silently deciding product scope. |
| Verification | Expected outcomes come from requirements rather than copied implementation behavior. |

Use fresh-context agents for behavioral evaluation when available. Give them the skill and realistic task inputs without the expected answer; inspect their actual changes and check results. Do not claim a behavioral check passed unless it was exercised.
