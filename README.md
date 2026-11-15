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

You define the desired behavior and qualities in the README or linked requirements. The agent exposes consequential gaps, derives the necessary technical sub-specifications in `ARCHITECTURE.md`, and implements everything not qualified as planned. Expected test outcomes come from requirements; design and code supply the mechanics. Discoveries become explicit decisions, then updates to the affected documents, code, and tests.

You [author the requirements](skills/spec-as-source-development/SKILL.md#capture-decisions-and-expose-gaps) and revise them deliberately. The agent can help explore possible edits; carefully review any wording it drafts before accepting it as your intent. Routine engineering remains autonomous. Consequential product choices come back to you. The resulting repository carries enough intent and design for another session to continue, revise, or rebuild the required behavior.

## Bootstrap a project

- Install this skill from your application project with the [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md): `npx skills add zenflow/spec-as-source-development --skill spec-as-source-development`.
- Add to `AGENTS.md`: `For development work in this project, read and follow the installed spec-as-source-development skill.` Or copy the [starter](examples/AGENTS.md).
- Optionally install companion skills, such as [Ponytail](https://github.com/DietrichGebert/ponytail/blob/main/INSTALL.md) for smaller implementations: `npx skills add DietrichGebert/ponytail --skill ponytail`.
- Start from a clean working copy and write the README for the product you want. If it's too much to build well in one pass, mark the deferred parts as planned. This keeps the full vision visible while you implement and refine it in stages.

For example:

```markdown
# Pocket Tasks

A small web app for keeping track of everyday tasks.

Built with vanilla JavaScript and browser `localStorage`, so your list is saved between visits in the same browser. No account or backend required.

## Features

- Add tasks and check them off as you go.
- Edit or delete tasks when plans change.
- Switch between all tasks and those still to do.

## Planned features

- Organize tasks with tags.
- Export your list as a JSON backup.
```

Then iterate:

1. **Generate:** “Implement the README.” The agent records the needed design, builds it, and verifies the behavior.
2. **Refine:** Try it. Edit the README to clarify or change what you want, then ask the agent to update the implementation. Repeat until satisfied.
3. **Accept and commit:** Review the result and verification, then commit the requirements, design, code, and tests together.
4. **Continue in a fresh chat:** Start from a clean working copy and edit the README for the next iteration. Remove planned qualifications for features you want to implement, then repeat.

See the [implementation rule and ways to mark planned behavior](skills/spec-as-source-development/SKILL.md#implement-the-readme). Add usage instructions and project commands as they become real.

### As you iterate

A new feature, a changed preference, or a reversed decision follows the same loop. A defect already covered by the requirements needs a fix and appropriate regression coverage; it does not need another specification. If you discover an expectation that was never recorded, capture it.

The skill guides agent behavior; review and verification establish whether it followed through. Regenerable means the intended behavior and consequential design survive replacement of the implementation, not that every change requires starting over.

## Planned features

These additions to the methodology are planned and not yet available:

- Instructions and features for integrating the workflow into existing (brownfield) projects.

## Lineage and maintenance

The name draws on Birgitta Böckeler's distinction between [spec-first, spec-anchored, and spec-as-source development](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html). The workflow grew from [README-driven development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html), its former name here.

For changes to this skill, keep the workflow in SKILL.md and the onboarding here. Package decisions are in [ARCHITECTURE.md](ARCHITECTURE.md); repository working instructions are in [AGENTS.md](AGENTS.md).

[MIT license](LICENSE).
