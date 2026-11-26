# Where this skill comes from

`pack/` holds three skills from awesome-gamedev-agent-skills by Abhishek Barali and the awesome-gamedev-agent-skills contributors,
copied unchanged from its own repository so it ships in raea's plugin and installer beside the raea skill.

- Source: https://github.com/gamedev-skills/awesome-gamedev-agent-skills
- Commit: `c6ca6c41c839b68319ffc08430b99ab768debc32` (12 November 2026)
- Licence: Apache-2.0 (`LICENSE` here, with the repository's `NOTICE`)
- Copied: `skills/web-engines/threejs-scene-setup`, `threejs-materials-lighting` and `threejs-gltf-loading`.
- Left out: the other 74 skills (other engines, genres, workflows), its router, evals and tests.
- Added here: `SKILL.md` (a router over `pack/`, written for this repository) and this file. Nothing in `pack/` is
  changed. Links inside `pack/` that point outside the copied skills (to the source repository's docs) don't resolve
  here; read them in the source repository.

## What it runs

Nothing. The skills are guidance and JavaScript examples.

## Updating it

Copy the source repository's skills at a newer commit over `pack/` (the same folders), update the commit above, and
read the diff before committing it.
