# Where this skill comes from

`pack/` holds bevy-skills by Chris Gliddon,
copied unchanged from its own repository so it ships in raea's plugin and installer beside the raea skill.

- Source: https://github.com/chrisgliddon/bevy-skills
- Commit: `475ed421de043b0a8c1d248243f1e937962dfd02` (3 November 2026)
- Licence: MIT (`LICENSE` here)
- Copied: every `skills/bevy*` folder (31 skills).
- Left out: `skills/similarity-rs` (a code-similarity tool, not Bevy), and the repository's agent files and scripts.
- Added here: `SKILL.md` (a router over `pack/`, written for this repository) and this file. Nothing in `pack/` is
  changed. Links inside `pack/` that point outside the copied skills (to the source repository's docs) don't resolve
  here; read them in the source repository.

## What it runs

Nothing by itself. The skills are guidance and Rust examples. A few carry Python helpers that read the files you give
them and print a report: `bevy-rendering/scripts/audit_renderer_features.py` (a `Cargo.toml`), the `bevy-a11y`
checkers (an input map, contrast, captions) and `bevy-porting/scripts/` (a Unity, Unreal, Godot, GameMaker, Roblox or
Flash project to port). The Flash one runs JPEXS `ffdec`, which you install, to unpack a `.swf`. None of them reaches
the network.

## Updating it

Copy the source repository's skills at a newer commit over `pack/` (the same folders), update the commit above, and
read the diff before committing it.
