---
name: spec-as-source-development
description: >-
  Keep human intent authoritative in a living README and linked requirements,
  derive subordinate technical design, and implement and verify software against
  those sources. Use when the user requests Spec-as-Source Development (SASD),
  or a project explicitly adopts this workflow.
---

# Spec-as-Source Development

**A lightweight SDD framework for keeping human intent authoritative while making implementation regenerable.**

Deliberate human decisions define what the software should do. The README and linked requirements preserve that intent; the agent derives technical sub-specifications, implementation, and verification from it. Discoveries feed back into explicit human decisions and revisions. Keep the specification concise, current, and sufficient to rebuild the required behavior without reverse-engineering the old implementation.

## Establish the sources

Read the relevant requirements, technical design, and working instructions before changing behavior. Inspect the affected implementation to understand the work, without treating its current behavior as proof of what is wanted.

Use these document roles, respecting equivalent locations already designated by the project:

| Source | Authority |
| --- | --- |
| `README.md` and explicitly linked requirements | Product purpose, observable behavior, desired qualities, and constraints. Human intent governs what is wanted. |
| `ARCHITECTURE.md` | Consequential technical choices, interfaces, data models, implementation sub-specifications, and useful rationale. Design governs how requirements are realized and remains subordinate to them. |
| `AGENTS.md` | How to work in the project: this convention, document locations, engineering practices, and development/check commands. |

Prefer an existing `DESIGN.md` over creating a competing architecture document. Extract requirements into a linked `REQUIREMENTS.md` or focused documents only when useful. Give each decision one authoritative home; link instead of duplicating it. Document roles matter more than filenames. Do not create empty documents to satisfy a template.

## Capture decisions and expose gaps

The human authors and deliberately revises the requirements. The agent may help explore possible edits or draft wording, but agent-written requirements remain proposals until the human has carefully reviewed them and accepted them as expressing conscious, intentional decisions.

Before implementing a new or changed expectation, ensure its authoritative source records that human decision. Preserve the human's meaning and wording. Apply exact human-authored or already accepted edits directly; do not require repeated approval.

Capture qualities and constraints as well as features. “Make it pretty” establishes a visual expectation; it does not authorize an invented design system or arbitrary metric. Use examples or a focused question when the distinction affects the result.

Actively expose consequential omissions, ambiguities, contradictions, and conflicts between sources and implementation. Explain their effect, propose useful options, and obtain human judgment where needed. Keep proposals and unresolved questions visibly separate from accepted requirements. Continue independent work while a consequential decision is unresolved.

Use engineering judgment for routine implementation details within accepted requirements. Necessary engineering work can follow from requirements without becoming additional product scope.

If existing requirements already state or clearly imply the correct behavior, fix the defect and add appropriate regression coverage without inventing a new requirement. If a defect reveals a missing expectation, resolve and capture it. Apply the same distinction to technical commitments in the design.

Keep durable expectations and consequential technical decisions out of chat-only history, temporary plans, and test-only assertions.

## Derive the necessary design

Develop technical sub-specifications only to the depth needed for the selected work. Record consequential boundaries, interfaces, dependencies, algorithms, and rationale when they will guide implementation or future changes. Connect them to the requirements they serve. Leave incidental details to the code.

Make routine technical choices autonomously. Seek a human decision when a choice would change product intent or introduce a consequential product tradeoff not already decided. Once a design decision is documented, follow it or deliberately revise it before implementing a conflicting approach.

Avoid restating requirements, narrating the codebase, or preserving task breakdowns as permanent specification. Generated design must not silently add product expectations.

## Implement the README

Make the implementation match the README and linked requirements. Implement all described behavior unless it is qualified as planned. Consider planned behavior in the design without implementing it.

For revisions, the human edits requirements on a clean working copy. Propagate the diff into design, implementation, and tests, and verify against the updated requirements. Commit the related changes together after review.

### Marking planned behavior

For example:

- A `Planned features` section for deferred features.
- A `[Planned]` prefix on a feature bullet.
- An inline note such as `[Planned: allow filtering to unfinished tasks]`, scoped to the enclosed detail.

## Verify against intent

Derive expected outcomes from the requirements, independently of the implementation's answers. For each affected behavior, identify what would demonstrate conformance. Use meaningful tests, inspection, or direct evaluation appropriate to the requirement, and check applicable architectural constraints too.

Code can inform test mechanics, coverage, and internal correctness checks. It cannot establish intended product behavior. Do not bless observed outputs as expected results without grounding them in the specification. Tests can cover implied cases and internal invariants without turning every assertion into another requirement.

For a covered defect, demonstrate the failure and correction where practical. For a subjective quality, use direct evaluation or agreed examples rather than pretending a passing unit test proves satisfaction. State what was checked, what passed, and what remains uncertain. Passing tests alone does not establish that the specification is complete.

## Revise freely and leave durable context

When the human changes a decision, revise its source in place and reconcile affected design, implementation, and tests. Remove obsolete statements; use version control for history. Earlier approval, generated plans, and existing tests do not overrule an explicit revision.

Distinguish withdrawal of a feature from removal of redundant wording; clarify consequential ambiguity rather than guessing. Do not rewrite requirements to excuse accidental implementation drift.

Preserve enough intent and consequential design to recreate required behavior. Any outcome that must survive regeneration belongs in those sources. Code and tests may be revised or regenerated as useful; this does not require wholesale rewrites or promise identical code. Verify each resulting implementation against the retained intent.

Finish with a concise account of the intent changed, the result, verification, and unresolved decisions or incomplete work. Leave current documents sufficient for the next session to continue without relying on this chat. Keep documentation and verification proportional to the change.
