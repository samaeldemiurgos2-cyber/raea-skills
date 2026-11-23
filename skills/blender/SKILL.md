---
name: blender
description: "Blender 5.2+ work driven by an agent, in Python (bpy) over the Blender MCP or headless: modeling, sculpting, retopology and UVs, PBR materials and texture baking, character rigging and skinning, facial shape keys, clothing and hair, animation, lighting and look-dev, rendering, geometry nodes, simulation, game export, and a QA gate for every asset. Use when the work happens inside Blender. A raea scene that loads a .blend or runs a saved Blender script goes through the raea skill first. From EL4CTEO's blender-skills (MIT)."
metadata:
  raea-tested-against: 0.1.0-rc1
---

# Blender

These are EL4CTEO's Blender agent skills, copied unchanged into `pack/` (UPSTREAM.md says from where). They are
written and verified for Blender 5.3 and need 5.2 LTS or later. Each skill's `scripts/` run inside Blender: over the
Blender MCP's `execute_blender_code`, or headless with `blender -b -P script.py -- ARGS`. Each returns JSON.

Start with [pack/blender-core/SKILL.md](pack/blender-core/SKILL.md): how code runs, the 5.x API changes and how to
verify a result. Then open the skill for the task. [pack/blender-workflow-recipes/SKILL.md](pack/blender-workflow-recipes/SKILL.md)
chains them end to end (a game prop, a rigged and animated character). Any mesh you make or edit goes through
[pack/blender-asset-qa/SKILL.md](pack/blender-asset-qa/SKILL.md) before it leaves Blender.

raea opens .blend files and runs saved Blender scripts itself (`raea blender`; see `raea/3d/blender.md` and
`raea/3d/blend-files.md`). Use those for a raea project's assets, and this skill for the Blender work behind them.

## Known traps (found rigging and exporting a character on Blender 5.2.1, 23 November 2026)

- **`turntable.py`'s studio rig overexposes by about two stops under AgX** (the key scales with distance squared).
  Lower `view_settings.exposure` (about -2) or the lights' power, and check the 18% grey backdrop reads grey. It also
  resets the scene's frame range to 1-120.
- **A web GLB with meshopt doesn't load in Bevy** (Blender writes `EXT_meshopt_compression` into
  `extensionsRequired`). Export with `--set export_meshopt_compression_enable=false` for anything but three.js.
- **Clips start one frame late** unless exported with `export_anim_slide_to_zero=true`; a loop then holds its first
  pose for a frame at every seam.
- **A loop needs cyclic handles.** Add a `CYCLES` F-curve modifier before baking so auto-clamped handles don't flatten
  at the ends (what `loop_check` reports as a dip); `bake_action` and the glTF exporter read the evaluated curve.
- **Looking at frames headless:** the skills' `look(mode="frames")` is the Blender MCP's. Headless, call
  `review_shots.run()` once per frame.
- `bake_action` names clips `RIG|Clip`; rename the action before export if code finds clips by name.

| Skill | What it covers |
|---|---|
| [blender-addon-development](pack/blender-addon-development/SKILL.md) | Write Blender 5.3 add-ons as extensions - blender_manifest.toml, operators/panels/menus/property groups/preferences, bpy.props rules after 5.0, undo/redo, modal and … |
| [blender-animation](pack/blender-animation/SKILL.md) | Animation in Blender 5.3 - slotted/layered actions and the channelbag API, Python keyframing, F-curves, game loops with pop/hitch checks, NLA clips, pose library … |
| [blender-asset-qa](pack/blender-asset-qa/SKILL.md) | Mandatory review gate for any mesh or asset created or edited in Blender. Detects z-fighting, floating/detached parts, inverted or inconsistent normals … |
| [blender-character-rigging](pack/blender-character-rigging/SKILL.md) | Character rigging in Blender 5.3 - Rigify metarig fit/generate, bone naming/roll/collections, DEF/MCH/control layers, IK/FK, robust skinning (heat + proxy fallback) … |
| [blender-clothing](pack/blender-clothing/SKILL.md) | Game clothing in Blender 5.3 - garments from body regions (ease offset, thickness), skin-weight transfer, hiding covered body faces, cloth-sim draping for folds … |
| [blender-core](pack/blender-core/SKILL.md) | Foundation for any Blender 5.2+ task an agent drives - running bpy via MCP (live) or headless CLI, context overrides, locale-safe node lookup, enum discovery, 5.x API … |
| [blender-environment-kits](pack/blender-environment-kits/SKILL.md) | Game environments in Blender 5.3 - terrain from noise or heightmaps (erosion, terraces, play areas, slope/height materials, 16-bit heightmaps + splat maps for UE/Unity) … |
| [blender-export-pipelines](pack/blender-export-pipelines/SKILL.md) | Export from Blender 5.3 with verified presets - Roblox (FBX/glTF, cages, R15, SurfaceAppearance), Unity (FBX, Humanoid), Unreal (FBX skeletal, Nanite, UCX), Godot/web … |
| [blender-facial-shapekeys](pack/blender-facial-shapekeys/SKILL.md) | Facial rigs and shape keys in Blender 5.3 - ARKit 52 blendshapes, visemes for lip-sync, sculpting expressions, splitting symmetric shapes into Left/Right, mirroring … |
| [blender-game-optimization](pack/blender-game-optimization/SKILL.md) | Optimize Blender assets for real-time engines - triangle/material/texture/bone budgets per platform (mobile, Roblox, web, VR, console, PC), LOD chains, decimation modes … |
| [blender-geometry-nodes](pack/blender-geometry-nodes/SKILL.md) | Geometry Nodes in Blender 5.3 - fields, domains, attributes, instancing, zones (simulation/repeat/for-each), closures/bundles, lists, SDF grids, node tools, baking, plus … |
| [blender-hair-grooming](pack/blender-hair-grooming/SKILL.md) | Hair and fur in Blender 5.3 - hair curves on a surface, guides + interpolated children with the bundled hair node assets (clump, curl, noise, droop), density masks … |
| [blender-hardsurface-modeling](pack/blender-hardsurface-modeling/SKILL.md) | Hard-surface and prop modeling in Blender 5.3 - blockout-to-detail flow, non-destructive modifier stacks (Mirror, Boolean Exact/Manifold, Bevel, Weighted Normal, Smooth … |
| [blender-lighting-lookdev](pack/blender-lighting-lookdev/SKILL.md) | Lighting, cameras and look-dev in Blender 5.3 - studio 3-point and product lighting, HDRI environments, sun/sky exteriors, interiors, light linking, physically based … |
| [blender-pbr-materials](pack/blender-pbr-materials/SKILL.md) | Physically based materials in Blender 5.3 - metal/roughness rules, Principled BSDF inputs, color spaces (sRGB vs Non-Color), measured albedo/F0 values, texture-set … |
| [blender-pipeline-automation](pack/blender-pipeline-automation/SKILL.md) | Automate Blender 5.3 at scale - headless CLI flags, batch convert/inventory/run-any-skill-script over folders of .blend/.fbx/.glb/.obj/.usd, sharding, bpy pip module … |
| [blender-rendering](pack/blender-rendering/SKILL.md) | Render with Blender 5.3 Cycles/EEVEE/Workbench - quality presets, GPU setup, adaptive sampling, denoising, light paths, color management (AgX, Khronos PBR Neutral … |
| [blender-retopology-uv](pack/blender-retopology-uv/SKILL.md) | Retopology and UVs in Blender 5.3 - auto retopo (Quadriflow, Decimate, planar), deformation edge flow, seams, unwrap (Angle Based, Minimum Stretch, Smart), pixel-margin … |
| [blender-scene-setup](pack/blender-scene-setup/SKILL.md) | Set up and audit Blender scenes the way studios do - units and real-world scale, collection layout, naming conventions (SM_/SK_/T_/M_), origins, linking vs appending … |
| [blender-sculpting](pack/blender-sculpting/SKILL.md) | Sculpting in Blender 5.3 - base-to-detail workflow, voxel remesh, dyntopo, multires, 5.x brush types, masks/face sets, symmetry, plus headless-safe procedural ops for … |
| [blender-simulation](pack/blender-simulation/SKILL.md) | Physics in Blender 5.3 - rigid bodies (density mass, shapes, bake to keys), classic cloth presets and pinning, new node-based Cloth/Hair Dynamics (XPBD, Collider … |
| [blender-stylized-npr](pack/blender-stylized-npr/SKILL.md) | Stylized / NPR looks in Blender 5.3 - toon and cel shading (bands, shadow tint, rim, hard specular), anime faces with custom normals, inverted-hull outlines with … |
| [blender-texture-baking](pack/blender-texture-baking/SKILL.md) | Bake texture maps in Blender 5.3 Cycles - high-to-low normal maps with cage/extrusion, AO, curvature, ID, thickness, base color/roughness/metallic from procedurals, ORM … |
| [blender-texturing](pack/blender-texturing/SKILL.md) | Texture authoring in Blender 5.3 - smart-material layers (edge wear, cavity grime, dust, rust, roughness breakup) from curvature/AO masks, z-fight-safe decal and sticker … |
| [blender-time-of-day](pack/blender-time-of-day/SKILL.md) | Time of day and atmosphere in Blender 5.3 - measured sky + sun for dawn, morning, noon, golden hour, sunset, blue hour, overcast, night/moonlight with stars and city … |
| [blender-video-editing](pack/blender-video-editing/SKILL.md) | Video in Blender 5.3 - Video Sequencer edits from Python (clips, image sequences, crossfades, titles, music fades, proxies, color management, H.264/AAC output) and … |
| [blender-weather-fx](pack/blender-weather-fx/SKILL.md) | Weather effects in Blender 5.3 - looping Geometry Nodes rain, snow, dust, ash and embers with ground hits and splashes, wet surfaces, puddles with animated ripples, wall … |
| [blender-workflow-recipes](pack/blender-workflow-recipes/SKILL.md) | End-to-end Blender 5.3 playbooks chaining the blender-* skills with QA gates - game props (mid-poly, high-to-low), game characters (sculpt/AI mesh to rigged, animated … |
