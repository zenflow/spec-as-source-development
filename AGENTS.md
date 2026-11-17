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

## Releasing

- Versions are Git tags (X.Y.Z) with a GitHub release of the same tag; no version file exists.
- Check gh release view <previous tag> and mirror its structure: title `Spec-as-Source Development vX.Y.Z`, summary, install command pinned with `@vX.Y.Z`, README link at the tag, MIT line.
- Summarize changes since the last tag (`git log <tag>..HEAD`) in the notes; commit docs first, then tag the pushed `main` commit.
