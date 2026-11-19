---
name: spec-as-source-development
description: >-
  Keep human intent authoritative in a living README and linked requirements,
  maintain revisable technical design, and implement and verify software against
  those sources. Use when the user requests Spec-as-Source Development (SASD),
  or a project explicitly adopts this workflow.
---

# Spec-as-Source Development

**A lightweight spec-driven development framework for keeping human intent authoritative while making implementation regenerable.**

Deliberate human decisions define what the software should do. The README and linked requirements preserve that intent; technical design records how to realize it, including implementation choices supplied by the human. The agent develops the design, implementation, and verification within those requirements. Discoveries feed back into decisions and revisions at the appropriate source. Keep the specification concise, current, and sufficient to rebuild the required behavior without reverse-engineering the old implementation.

This skill governs the authority and evolution of requirements and their relationship to design, implementation, and verification. Specific engineering practices, such as test-driven development or isolated test development, are left to project instructions and optional companion skills.

## Establish the sources

Read the relevant requirements, technical design, and working instructions before making changes. Inspect the affected implementation to understand the work, without treating its current behavior as proof of what is wanted.

Use these document roles, respecting equivalent locations already designated by the project:

| Source | Authority |
| --- | --- |
| `README.md` and explicitly linked requirements | Product purpose, observable behavior, desired qualities, and constraints. Human intent governs what is wanted. |
| `ARCHITECTURE.md` | Current technical choices and preferences from the human or agent, interfaces, data models, implementation sub-specifications, and useful rationale. Design governs how requirements are realized, remains subordinate to them, and can be revised within them. |
| `AGENTS.md` | How to work in the project: this workflow, document locations, engineering practices, and development/check commands. |

Prefer an existing `DESIGN.md` over creating a competing architecture document. Extract requirements into a linked `REQUIREMENTS.md` or focused documents only when useful. Give each decision one authoritative home; link instead of duplicating it. Document roles matter more than filenames. Do not create empty documents to satisfy a template.

Classify a decision by what it governs, regardless of who supplied it. Put required outcomes in requirements and implementation choices in design. Split mixed statements: “use vanilla JavaScript and `localStorage` so tasks persist between visits” supplies both technical direction and a persistence requirement.

Requirements can include constraints that are not visible to end users. If the human explicitly makes an implementation choice binding across implementations, record that constraint in the README or linked requirements and reference it from the design. Otherwise, treat human implementation choices as revisable design. Clarify consequential ambiguity about whether a choice is binding.

## Capture decisions and expose gaps

The human authors and deliberately revises the requirements. The agent may help explore possible edits or draft wording, but agent-written requirements remain proposals until the human has carefully reviewed them and accepted them as expressing conscious, intentional decisions.

Before implementing a new or changed requirement, ensure its authoritative source records that human decision. Preserve the human's meaning and wording. Apply exact human-authored or already accepted edits directly; do not require repeated approval.

When the human states a decision in conversation, the decision is accepted; record it faithfully in the appropriate source and implement it. Capture product intent in requirements and implementation direction in design before building. For requirements, only the wording you drafted remains a proposal: report it so the human can review it when accepting the work. Product expectations the agent identifies still require a human decision before implementation.

Usage instructions in the README, such as installation, commands, and configuration, describe observable behavior and are requirements. When implementation introduces usage the requirements do not specify, decide it as routine engineering unless it is consequential, document it in the README, and report the wording as drafted.

Capture qualities and constraints as well as features. “Make it pretty” establishes a visual expectation; it does not authorize an invented design system or arbitrary metric. Use examples or a focused question when the distinction affects the result.

Actively expose consequential omissions, ambiguities, contradictions, and conflicts between sources and implementation. Explain their effect, propose useful options, and obtain human judgment where needed. Keep proposals and unresolved questions visibly separate from accepted requirements. Continue independent work while a consequential decision is unresolved.

Use engineering judgment for routine implementation details within accepted requirements. Necessary engineering work can follow from requirements without becoming additional product scope.

If existing requirements already state or clearly imply the correct behavior, fix the defect and add appropriate regression coverage without inventing a new requirement. If a defect reveals a missing product expectation, resolve and capture it. Handle technical gaps under the design rules below.

Keep durable expectations and consequential technical decisions out of chat-only history, temporary plans, and test-only assertions.

## Derive the necessary design

Develop technical sub-specifications from requirements, existing design, and human implementation direction, only to the depth needed for the selected work. Record consequential boundaries, interfaces, dependencies, algorithms, and rationale when they will guide implementation or future changes. Connect them to the requirements they serve. Leave incidental details to the code.

Choose and revise technical design autonomously within accepted requirements. Human implementation direction establishes the starting design; design remains revisable regardless of who proposed or reviewed it. Follow documented choices or deliberately revise them, recording the reason before implementing a conflicting approach. Report consequential revisions. Seek a human decision when a choice would change a requirement or introduce a consequential product tradeoff not already decided.

Avoid restating requirements, narrating the codebase, or preserving task breakdowns as permanent specification. Generated design must not silently add product expectations.

## Implement the README

Make the implementation match the README and linked requirements. Implement all described behavior unless it is qualified as planned. Consider planned behavior in the design without implementing it.

Treat the last commit as the reconciled baseline: committed requirements, design, implementation, and tests are expected to agree. At the start of an iteration, identify the requested change from the human's instructions and uncommitted edits to requirements or design, including new linked files. An iteration may change only the design while preserving requirements. During refinement, identify further changes from the sources previously read and the human's feedback; when the earlier wording is unavailable, compare against the baseline. If the requested change is unclear, such as when source edits were committed separately or unrelated changes are present, ask a focused question rather than guessing. Never discard changes you did not make.

Reconcile the affected documents, implementation, and tests with accepted requirements and current design, and verify the result. Do not commit until the human accepts it; then commit the requirements, design, code, and tests together, restoring a reconciled baseline.

### Marking planned behavior

Any clear marker works, for example:

- A `Planned features` section for deferred features.
- A `[Planned]` prefix on a feature bullet.
- An inline note such as `[Planned: allow filtering to unfinished tasks]`, scoped to the enclosed detail.

## Verify against intent

Derive expected outcomes from the requirements, independently of the implementation's answers. For each affected behavior, identify what would demonstrate conformance. Use meaningful tests, inspection, or direct evaluation appropriate to the requirement, and check conformance to the current design too.

Code can inform test mechanics, coverage, and internal correctness checks. It cannot establish intended product behavior. Do not bless observed outputs as expected results without grounding them in the specification. Tests can cover implied cases and internal invariants without turning every assertion into another requirement.

For a covered defect, demonstrate the failure and correction where practical. For a subjective quality, use direct evaluation or agreed examples rather than pretending a passing unit test proves satisfaction. State what was checked, what passed, and what remains uncertain. Passing tests alone does not establish that the specification is complete.

## Revise freely and leave durable context

When the human revises a requirement or either party revises the design within those requirements, update its source in place and reconcile affected documents, implementation, and tests. Remove obsolete statements; use version control for history. Earlier approval, generated plans, and existing tests do not overrule a deliberate revision.

Distinguish withdrawal of a feature from removal of redundant wording; clarify consequential ambiguity rather than guessing. Do not rewrite requirements to excuse accidental implementation drift.

Preserve enough intent and consequential design to recreate required behavior. Regeneration preserves requirements and uses the current design, which can evolve under the same revision rules. Code and tests may be revised or regenerated as useful; this does not require wholesale rewrites or promise identical code. Verify each resulting implementation against the retained intent.

Finish with a concise account of the intent changed, including requirement wording you drafted, consequential design revisions and their reasons, the result, verification, and unresolved decisions or incomplete work. Leave current documents sufficient for the next session to continue without relying on this chat. Keep documentation and verification proportional to the change.
