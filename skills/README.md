# raea for Claude

raea is the Render Anything Engine. You write a video, a motion graphic, a game or a 3D scene as React and TypeScript,
and raea renders it on your computer's GPU with an engine built on Bevy. The same file renders to video, plays live as
a game, or renders single frames to check. This plugin teaches Claude to use raea well and connects Claude Code to it.

## What's in it

- **The raea skill** (`raea/`). It covers how to install raea, write a composition, render and check it, and what each
  kind of work needs: footage cut by its words, motion graphics and type, sound and music, 3D scenes (Bevy materials,
  lights, physics, Gaussian splats), games, app interfaces, generated media, and delivery. Its `reference/` files are
  generated from raea's code, so they list the real verbs, flags and SDK imports.
- **The video-decompiler skill** (`video-decompiler/`), by James Dimachkie, MIT. It makes a short product film (a
  launch film, a demo, a brand film) as raea code: take a good film of its kind apart, write yours on one page, build
  picture and sound on one clock, have it read blind, then show a person. Its tools are Python, in an environment of
  their own; `video-decompiler/UPSTREAM.md` says where it comes from, what it runs and how it's updated.
- **Three skills by others for the engines underneath**, each copied unchanged at a pinned commit with its licence;
  each folder's `UPSTREAM.md` says where it comes from and what it runs:
  - **bevy** (`bevy/`): Chris Gliddon's bevy-skills, MIT. 31 skills for Bevy 0.20, the engine raea is built on: ECS,
    rendering, PBR materials and WESL shaders, cameras, particles, animation, UI, physics, profiling, and moving code up
    from Bevy 0.17-0.19.
  - **blender** (`blender/`): EL4CTEO's Blender Agent Skills, MIT. 28 skills for Blender 5.2 and later, from modeling,
    rigging and look-dev to baking and game export, with Python scripts that run inside Blender.
  - **threejs** (`threejs/`): three skills from gamedev-skills' awesome-gamedev-agent-skills, Apache-2.0. three.js r187
    scene setup, glTF loading, and materials and lighting, each with a symptom-to-fix list.
- **Two hooks** (`hooks/`), for Claude Code and Cowork. Before Claude runs a shell command, a command that opens a
  still, a video or a sound in the Mac's viewer is stopped once and Claude is told to use `raea show`, which puts it in
  the raea app where you can answer it; the same command again goes through. This happens only while the raea app is
  installed. After Claude saves a composition (a `.tsx` file that calls `registerRoot`), `raea check --quick` runs on
  it and Claude gets what it finds.

## Install the plugin

Install it from this repository in Claude Code (2.1.275 or later):

```
/plugin install raea --marketplace shinyobjectz/raea-skills
```

Claude's plugin directory carries an edition of this plugin without the hooks and the skill's TypeScript kits
(`directory/` in the repository), since it takes neither from an organization Anthropic hasn't verified. Once it's
listed, you can add that edition from **Customize > Plugins** on claude.ai, or with `/plugin directory` in Claude Code.

## Install raea

The plugin uses the `raea` command, which you install yourself:

- macOS (Apple Silicon) or Linux (x86_64): `curl -fsSL https://raea.io/install | sh`
- Windows 10 or 11, in PowerShell: `irm https://raea.io/install.ps1 | iex`

Until `raea` is on your PATH the hooks do nothing, and the skill tells Claude how to install it when you ask for
something that needs it. raea's installer also copies the skill into `~/.claude/skills`; with the plugin you can set
`RAEA_NO_SKILLS=1` when you install raea to skip that copy.

If you already ran `raea skills install --agent claude`, the same two hooks are in `~/.claude/settings.json`, and the
plugin's hook script steps aside so they never run twice.

## Where it works

| | Skill | Hooks |
|---|---|---|
| Claude Code | yes | yes |
| Cowork | yes | yes, when raea is installed where the session runs |
| Chat on claude.ai | yes | no (chat doesn't run hooks) |

Rendering needs raea on a computer, so in chat the skill can explain and write compositions but can't render them.

## What it runs and sends

The plugin itself sends nothing anywhere and stores nothing. Its hook script (`hooks/raea-hook.sh`) runs
`raea hook claude` on your computer, which reads the tool call Claude Code hands it, may run raea's quick check on the
saved file, and keeps a small marker under `~/.raea/hooks` so a command it stopped goes through when tried again. It
reads `~/.claude/settings.json` only to see whether raea's hooks are already there.

The video-decompiler skill's tools run on your computer too (Python, `ffmpeg`, `ffprobe` and `raea`) and reach no
network; they write under `~/.vd` and in the film's folder (`video-decompiler/UPSTREAM.md`).

The blender skill's scripts run inside Blender on your computer and reach no network; the bevy skill's few helpers read
the files you give them (`blender/UPSTREAM.md`, `bevy/UPSTREAM.md`). The threejs skill runs nothing.

The raea skill tells Claude to run the `raea` command, which works on your computer. A few of raea's verbs reach the
network when you ask for them: the installer downloads raea from raea.io, `raea gen` calls the generation providers you
set up with your own keys (and spends your money there, so the skill has Claude quote the cost first), and a review
link made in the raea app uploads the cut you choose to share. raea's privacy policy is at https://raea.io/privacy/.

## Source and license

This folder is the `skills/` folder of
[shinyobjectz/raea-skills](https://github.com/shinyobjectz/raea-skills), where the skill is written and checked.
Apache-2.0; the copied guides keep their notices (`raea/3d/NOTICE`, `raea/craft/NOTICE`). `video-decompiler/` is MIT,
copied from [JimGHTB12/video-decompiler](https://github.com/JimGHTB12/video-decompiler) with its `LICENSE` and
`NOTICE`; the fonts, pictures and sounds in its `library/` keep their own licences, listed there. `bevy/` is MIT, copied
from [chrisgliddon/bevy-skills](https://github.com/chrisgliddon/bevy-skills); `blender/` is MIT, copied from
[EL4CTEO/blender-skills](https://github.com/EL4CTEO/blender-skills); `threejs/` is Apache-2.0, copied from
[gamedev-skills/awesome-gamedev-agent-skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills) with its
`NOTICE`. Each keeps its `LICENSE`. Questions and bugs:
[issues](https://github.com/shinyobjectz/raea-skills/issues).
