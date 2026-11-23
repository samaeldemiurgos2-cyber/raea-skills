# Where this skill comes from

`pack/` holds Blender Agent Skills by EL4CTEO,
copied unchanged from its own repository so it ships in raea's plugin and installer beside the raea skill.

- Source: https://github.com/EL4CTEO/blender-skills
- Commit: `1a1cc6c49312f9f370aae86f52b7b907f29c94f6` (21 November 2026, release 1.3.3)
- Licence: MIT (`LICENSE` here)
- Copied: every `skills/blender-*` folder (28 skills).
- Left out: the repository's installer, tests, tools, docs, assets and its own plugin manifests (this repository's `skills/.claude-plugin/plugin.json` lists the skill).
- Added here: `SKILL.md` (a router over `pack/`, written for this repository) and this file. Nothing in `pack/` is
  changed. Links inside `pack/` that point outside the copied skills (to the source repository's docs) don't resolve
  here; read them in the source repository.

## What it runs

Each skill's `scripts/` are Python for Blender 5.2 or later. They run inside Blender, over the Blender MCP or
`blender -b -P`, change the open scene or the files you name, and print JSON. None of them reaches the network. (Some skills
suggest assets from libraries such as Poly Haven, fetched through the Blender MCP, not by these scripts.)

## Updating it

Copy the source repository's skills at a newer commit over `pack/` (the same folders), update the commit above, and
read the diff before committing it.
