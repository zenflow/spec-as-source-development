# Architecture

This repository distributes a Markdown workflow. The package has no executable components or build step.

## Package structure

| Path | Responsibility |
| --- | --- |
| `skills/spec-as-source-development/SKILL.md` | Authoritative methodology, agent instructions, and Agent Skills metadata. |
| `skills/spec-as-source-development/LICENSE.txt` | License notice retained when an installer copies only the skill directory. |
| `README.md` | Human-facing essence, motivation, installation, onboarding, and examples. |
| `examples/AGENTS.md` | Starter project instructions that adopt the installed skill. |
| `AGENTS.md` | Instructions and checks for maintaining this repository. |
| `LICENSE` | Repository license. |

The skill uses the [Agent Skills format](https://agentskills.io/specification): a directory named for the skill, containing `SKILL.md` with a YAML name and description.

The skill directory is self-contained. Following its workflow does not require reading this repository's README, examples, or maintainer instructions.

## One maintained definition

Keep the methodology in `SKILL.md`. The README summarizes it and links to the concrete rules, rather than maintaining another rulebook. Reconcile the introduction, adoption guidance, and examples whenever a deliberate methodology change affects them.

The README's [bootstrap instructions](README.md#bootstrap-a-project) use the Skills CLI to install the package and a single `AGENTS.md` instruction to adopt it. Project-specific commands and conventions belong in the adopting project's working instructions.

Both license files contain identical text. The packaged copy preserves the notice in installations that exclude the repository root. Optional companion skills remain external and are not dependencies or bundled instructions.
