# Spec-as-Source Development

**A lightweight SDD framework for keeping human intent authoritative while making implementation regenerable.**

> Preserve human intent as source. Derive implementation and verification independently.

As AI reduces implementation effort, specifying intent and validating results become increasingly important. Spec-driven development gives that work a durable foundation: an explicit description of what the software should do, against which any implementation can be judged.

Spec-as-Source Development is describing and continuously refining software expectations at their source in the README and linked requirements, then letting those decisions propagate into design, implementation, and tests.

[**SKILL.md**](skills/spec-as-source-development/SKILL.md) is the authoritative definition of the methodology and the instructions agents follow. This README explains its purpose and how to use it.

## Why this exists

AI-generated specs can bury your actual requirements under assumptions and unnecessary detail.

This grew out of trying [spec-kit](https://github.com/github/spec-kit), [OpenSpec](https://github.com/Fission-AI/OpenSpec), and spec-kit again. In those attempts, generated quality requirements and implementation details became mixed with deliberate business requirements. Reviewing the expanding documentation took effort, and reversing an approved decision meant reconciling too much generated material.

A simpler habit worked better: carefully edit the README, have an agent implement it, and keep the documents aligned as understanding improves. This skill makes that habit reusable.

The advantage is a specification small enough to understand, authoritative enough to guide work, and easy enough to revise. Human decisions stay distinguishable from agent proposals. Technical detail has its own home. Verification checks intent independently of the implementation's answers. Current documents evolve in place, with history in Git.

## How it works

You define the desired behavior and qualities in the README or linked requirements. The agent exposes consequential gaps, derives the necessary technical sub-specifications in `ARCHITECTURE.md`, and implements the selected scope. Expected test outcomes come from requirements; design and code supply the mechanics. Discoveries become explicit decisions, then updates to the affected documents, code, and tests.

The [source roles](skills/spec-as-source-development/SKILL.md#establish-the-sources), [decision rules](skills/spec-as-source-development/SKILL.md#capture-decisions-and-expose-gaps), and [verification discipline](skills/spec-as-source-development/SKILL.md#verify-against-intent) live in the skill. `AGENTS.md` adopts the workflow and holds project working instructions. Existing document names can stay.

You can edit the requirements yourself or describe a change and let the agent capture it faithfully. Routine engineering remains autonomous. Consequential product choices come back to you. The resulting repository carries enough intent and design for another session to continue, revise, or rebuild the required behavior.

## Install and adopt

This repository contains a self-contained [Agent Skills](https://agentskills.io/specification) package in [`skills/spec-as-source-development/`](skills/spec-as-source-development/).

With this repository checked out locally, run the following from the application project where you want to use it:

```sh
npx skills add /path/to/spec-as-source-development --skill spec-as-source-development
```

Replace the path with your checkout. The [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) supports local sources and agent selection; add `--global` for installation across your projects. Alternatively, copy the complete skill directory into your agent's supported skills location.

Ask your agent to use `spec-as-source-development`. To make it the project default, merge the [starter AGENTS.md](examples/AGENTS.md) into your existing instructions. Its adoption line is:

```markdown
For development work in this project, read and follow the installed
`spec-as-source-development` skill.
```

If your agent has no skill loader, copy `SKILL.md` into the project as `spec-as-source-development.md`, retain its license notice, and replace that line with:

```markdown
For development work in this project, read and follow
[Spec-as-Source Development](spec-as-source-development.md).
```

Use one installation approach per project so there is one copy to update.

### Optional companions

[Ponytail](https://github.com/DietrichGebert/ponytail) is a useful companion for favoring existing code, standard facilities, and smaller implementations. Follow its [installation guide](https://github.com/DietrichGebert/ponytail/blob/main/INSTALL.md) for your agent, and merge any working instructions into your existing `AGENTS.md`.

Add stack-specific testing or browser skills when they help demonstrate the behavior you require. Companion skills support this workflow; their suggestions do not become product requirements automatically.

## Bootstrap a project

Write a small target README. Put the first milestone **In progress** and the rest **Planned**. The status on each heading applies to all its features:

```markdown
# Pocket Tasks

A local command-line task list for one person.

## Expectations

Tasks persist between runs on this machine. No account or network is needed.
Output should be concise and readable in a terminal.

Milestone headings show delivery status. Planned features are not available.

## Milestone 1: Capture tasks [In progress]

- Add a task with a non-empty title.
- List saved tasks in creation order, showing each task's ID and title.
- An empty list says there are no tasks.

## Milestone 2: Finish tasks [Planned]

- Mark a task complete by ID.
- Show completion status in the task list; allow filtering to unfinished tasks.

## Milestone 3: Export [Planned]

- Export all tasks to JSON with their IDs, titles, and completion status.
```

Then iterate:

1. **Generate:** “Use Spec-as-Source Development. Implement milestone 1 from the README.” The agent records the needed design, builds it, and verifies the behavior.
2. **Refine:** Try it. Edit the README or describe the details you want changed. Let the agent reconcile the implementation and checks.
3. **Accept and commit:** Review the result and verification, mark the completed milestone Available, and commit the requirements, design, code, and tests together.
4. **Continue in a fresh chat:** “Move milestone 2 from Planned to In progress and implement it.” Refine, verify, accept, and commit again.

Promotion selects the work; verification establishes availability. See [stage semantics](skills/spec-as-source-development/SKILL.md#implement-the-selected-stage). Add usage instructions and project commands as they become real.

## Work with it day to day

A new feature, a changed preference, or a reversed decision follows the same loop. A defect already covered by the requirements needs a fix and appropriate regression coverage; it does not need another specification. If you discover an expectation that was never recorded, capture it.

For an existing project, start with its current documents and one concrete change. Have the agent identify the relevant gaps without generating a retrospective specification of every line of code.

The skill guides agent behavior; review and verification establish whether it followed through. Regenerable means the intended behavior and consequential design survive replacement of the implementation, not that every change requires starting over.

## Lineage and maintenance

The name draws on Birgitta Böckeler's distinction between [spec-first, spec-anchored, and spec-as-source development](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html). The workflow grew from [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html), its former name here.

For changes to this skill, keep the workflow in SKILL.md and the onboarding here. Package decisions are in [ARCHITECTURE.md](ARCHITECTURE.md); repository working instructions are in [AGENTS.md](AGENTS.md).

[MIT license](LICENSE).
