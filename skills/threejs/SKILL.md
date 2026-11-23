---
name: threejs
description: "Plain three.js r187 scenes: setup (import maps, renderer, camera, animation loop, resize, controls, WebGPU renderer), glTF and GLB loading with Draco, Meshopt and KTX2 and animation playback, and materials, lights, shadows, environment lighting and tone mapping, each with a symptom-to-fix list (a black mesh, washed-out colour, missing or blocky shadows). Use when writing or debugging a three.js page or scene outside raea. three.js inside a raea composition goes through the raea skill. From gamedev-skills' awesome-gamedev-agent-skills (Apache-2.0)."
metadata:
  raea-tested-against: 0.1.0-rc1
---

# three.js

Three skills from gamedev-skills' awesome-gamedev-agent-skills, copied unchanged into `pack/` (UPSTREAM.md says from
where). They target three.js r187 and record the release they were last checked against. Each has a Verify section and
a Gotchas list written as symptom → cause → fix: start there when something renders wrong.

three.js inside a raea composition (`<R3F>`, `<Three program>`, TSL node materials) goes through the raea skill
(`raea/3d/r3f.md`), which says what raea draws and what it doesn't yet.

| Skill | Use when |
|---|---|
| [threejs-gltf-loading](pack/threejs-gltf-loading/SKILL.md) | Loads glTF/GLB models into three.js r187 and plays their animations: GLTFLoader, DRACO, Meshopt and KTX2 decoders, AnimationMixer cross-fades and SkeletonUtils clones. … |
| [threejs-materials-lighting](pack/threejs-materials-lighting/SKILL.md) | Lights and shades three.js r187 scenes: standard, physical and unlit materials, lights, shadows, HDR environment lighting and tone mapping. Use when a mesh renders black … |
| [threejs-scene-setup](pack/threejs-scene-setup/SKILL.md) | Sets up and debugs a plain three.js r187 game or 3D scene: import maps, Scene, PerspectiveCamera and WebGLRenderer, setAnimationLoop with Timer, resize, OrbitControls … |
