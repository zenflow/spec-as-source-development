# Spec-as-Source Development

**A lightweight SDD framework for keeping human intent authoritative while making implementation regenerable.**

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

You [author the requirements](skills/spec-as-source-development/SKILL.md#capture-decisions-and-expose-gaps) and revise them deliberately. The agent can help explore possible edits; carefully review any wording it drafts before accepting it as your intent. Routine engineering remains autonomous. Consequential product choices come back to you. The resulting repository carries enough intent and design for another session to continue, revise, or rebuild the required behavior.

## Bootstrap a project

- Install from your application project with the [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md): `npx skills add zenflow/spec-as-source-development --skill spec-as-source-development`.
- Add to `AGENTS.md` ([starter](examples/AGENTS.md)): `For development work in this project, read and follow the installed spec-as-source-development skill.`
- Optional: [install Ponytail](https://github.com/DietrichGebert/ponytail/blob/main/INSTALL.md) to favor smaller implementations.

Write a small target README organized around the product. Tag the features you want to build first **[In progress]** and accepted future features **[Planned]**. Completed features stay in place and lose their tags:

```markdown
# Pocket Tasks

A local command-line task list for one person.

Tasks are saved on your machine and persist between runs. No account or network is needed, and output is kept concise and readable in a terminal.

## Features

Features marked **[In progress]** are under development and may be incomplete. Features marked **[Planned]** are not available yet. Unmarked features are available now.

### Capturing tasks

- **[In progress]** Add a task with a non-empty title.
- **[In progress]** List saved tasks in creation order, showing each task's ID and title.
- **[In progress]** An empty list says there are no tasks.

### Finishing tasks

- **[Planned]** Mark a task complete by ID.
- **[Planned]** Show completion status in the task list.
- **[Planned]** Filter the task list to unfinished tasks.

### Exporting

- **[Planned]** Export all tasks to JSON, including IDs, titles, and completion status.
```

Then iterate:

1. **Generate:** “Implement the features tagged [In progress] in the README.” The agent records the needed design, builds it, and verifies the behavior.
2. **Refine:** Try it. Edit the README with the details you want changed. Let the agent reconcile the implementation and checks.
3. **Accept and commit:** Review the result and verification, remove the [In progress] tags from completed features, and commit the requirements, design, code, and tests together.
4. **Continue in a fresh chat:** Choose the next features to build, change their [Planned] tags to [In progress], open a fresh chat, and return to step 1.

Tags select the work; verification establishes availability. See [stage semantics](skills/spec-as-source-development/SKILL.md#implement-the-selected-stage). Add usage instructions and project commands as they become real.

### As you iterate

A new feature, a changed preference, or a reversed decision follows the same loop. A defect already covered by the requirements needs a fix and appropriate regression coverage; it does not need another specification. If you discover an expectation that was never recorded, capture it.

The skill guides agent behavior; review and verification establish whether it followed through. Regenerable means the intended behavior and consequential design survive replacement of the implementation, not that every change requires starting over.

## Lineage and maintenance

The name draws on Birgitta Böckeler's distinction between [spec-first, spec-anchored, and spec-as-source development](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html). The workflow grew from [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html), its former name here.

For changes to this skill, keep the workflow in SKILL.md and the onboarding here. Package decisions are in [ARCHITECTURE.md](ARCHITECTURE.md); repository working instructions are in [AGENTS.md](AGENTS.md).

[MIT license](LICENSE).
