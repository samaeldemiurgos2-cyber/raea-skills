---
name: bevy
description: "Bevy 0.20 engine work in Rust: the app and ECS, rendering and PBR materials, WESL shaders, cameras and tonemapping, particles, animation, assets, UI, physics, profiling, and moving code up from Bevy 0.17-0.19. Use when writing or fixing Rust that uses Bevy (raea's engine and its Bevy SDK, a Bevy game or tool), or when a Bevy API recalled from memory doesn't compile. A raea composition in TypeScript goes through the raea skill. From Chris Gliddon's bevy-skills (MIT)."
metadata:
  raea-tested-against: 0.1.0-rc1
---

# Bevy 0.20

raea's engine is Bevy 0.20, the version every skill here is written for. These are Chris Gliddon's bevy-skills, copied
unchanged into `pack/` (UPSTREAM.md says from where). Open the one the task needs; each says which sibling covers the rest.

Start with [pack/bevy/SKILL.md](pack/bevy/SKILL.md) when the task spans several areas. When code written from memory
fails to compile, the migration skills list what changed in each release: renamed types, moved modules, and behaviour
that changed silently (`Tonemapping::None` became a raw passthrough in 0.20; bloom luma became linear in 0.19).

This skill is for Rust. Scenes, films and games made with raea in TypeScript go through the raea skill
(`raea/3d.md`), which maps raea's components onto Bevy's.

| Skill | Use when |
|---|---|
| [bevy-a11y](pack/bevy-a11y/SKILL.md) | designing or auditing high-standard video-game accessibility in Bevy 0.20, integrating screen readers and focus navigation, supporting adaptive controllers and complete … |
| [bevy-animation](pack/bevy-animation/SKILL.md) | wiring AnimationPlayer + AnimationGraphHandle, building an AnimationGraph from glTF clips, blending state-driven animations with AnimationTransitions::play, isolating … |
| [bevy-assets](pack/bevy-assets/SKILL.md) | loading with AssetServer::load or AssetServer::load_builder().with_settings(..), holding a Handle<T>, spawning a glTF scene with WorldAssetRoot (Handle<WorldAsset>) … |
| [bevy-audio](pack/bevy-audio/SKILL.md) | implementing audio in Bevy 0.20 with AudioPlayer, PlaybackSettings, AudioSink or SpatialAudioSink, spatial listeners, application mix groups, ambience/music transitions … |
| [bevy-cameras](pack/bevy-cameras/SKILL.md) | spawning Camera3d or Camera2d, choosing a Projection, rendering to an image with the RenderTarget component, adding Hdr / Tonemapping::Linear / ScreenSpaceTransmission … |
| [bevy-capture](pack/bevy-capture/SKILL.md) | adding CapturePlugin to record a Camera3d or Camera2d to video, spawning CaptureBundle with RenderTarget::target_headless, calling Capture::start with … |
| [bevy-cargo-features](pack/bevy-cargo-features/SKILL.md) | picking Bevy 0.20 Cargo features — top-level 2d/3d/ui/audio, mid-level 3d_api/3d_bevy_render/ui_api/common_api, headless default_app, input opt-ins … |
| [bevy-core-concepts](pack/bevy-core-concepts/SKILL.md) | wiring up an App, writing a Plugin, choosing between Update and FixedUpdate, ordering Startup/PreUpdate/PostUpdate, writing an exclusive system that takes &mut World as … |
| [bevy-custom-assets](pack/bevy-custom-assets/SKILL.md) | implementing AssetLoader for a custom format, deriving TypePath on the loader, loading dependencies through LoadContext::load or … |
| [bevy-diagnostics-profiling](pack/bevy-diagnostics-profiling/SKILL.md) | profiling Bevy 0.20 with DiagnosticPath, DiagnosticsStore, info_span!, RenderDiagnosticsPlugin, or the RenderDebugOverlay: custom metrics, CPU/GPU pass timings … |
| [bevy-ecs-components](pack/bevy-ecs-components/SKILL.md) | defining #[derive(Component)], declaring required components with #[require(...)], writing observers with On<E> or lifecycle observers with On<Add<T>> (NOT On<Add, T>) … |
| [bevy-ecs-queries](pack/bevy-ecs-queries/SKILL.md) | writing Query<D, F> with With/Without/Or, detecting changes with Changed<T>/Added<T>, parallelising with par_iter_mut, looking up entity lists with … |
| [bevy-ecs-systems](pack/bevy-ecs-systems/SKILL.md) | deriving SystemParam, grouping with SystemSet, gating execution with .run_if(on_message::<M>) / in_state(...) / resource_exists::<R>, combining conditions with … |
| [bevy-fluent](pack/bevy-fluent/SKILL.md) | adding localization to a Bevy 0.20 app with es-fluent-manager-bevy 0.21, defining typed messages with #[derive(EsFluent)], wrapping UI text in FluentText<T> … |
| [bevy-input-actions](pack/bevy-input-actions/SKILL.md) | building Bevy 0.20 input with InputSystems, entity-based Gamepad/GamepadSettings, AccumulatedMouseMotion, or CursorOptions: rebindable actions, hot-plugging, deadzones … |
| [bevy-migration-0-17-to-0-18](pack/bevy-migration-0-17-to-0-18/SKILL.md) | upgrading from Bevy 0.17 to Bevy 0.18, when an LLM writes EventReader/EventWriter/Trigger<E> instead of MessageReader/MessageWriter/On<E>, when mesh.insert_attribute … |
| [bevy-migration-0-18-to-0-19](pack/bevy-migration-0-18-to-0-19/SKILL.md) | upgrading from Bevy 0.18 to Bevy 0.19, when TextLayout::new_with_justify or TextFont { font_size: 24.0, font: handle } stops compiling (now TextLayout::justify … |
| [bevy-migration-0-19-to-0-20](pack/bevy-migration-0-19-to-0-20/SKILL.md) | upgrading from Bevy 0.19 to Bevy 0.20, when On<Add, T> or On<Pointer<Click>> stops compiling (now On<Add<T>> and On<PointerClick>), when … |
| [bevy-pbr-materials](pack/bevy-pbr-materials/SKILL.md) | spawning Mesh3d with StandardMaterial, writing a custom Material with AsBindGroup and a .wesl shader, enabling shadow_maps_enabled / contact_shadows_enabled on lights … |
| [bevy-physics](pack/bevy-physics/SKILL.md) | adding RapierPhysicsPlugin, spawning RigidBody/Collider, reading CollisionEvent or PhysicsQuarantineEvent, querying with ReadRapierContext, configuring … |
| [bevy-porting](pack/bevy-porting/SKILL.md) | porting a game project to Bevy 0.20 from another engine — Unity (Prefab, MonoBehaviour, Animator, UGUI), Unreal, Godot, Cocos, vanilla JavaScript / Phaser, Flash/SWF … |
| [bevy-rendering](pack/bevy-rendering/SKILL.md) | choosing Bevy 0.20's built-in renderer versus an API-only, headless, or external renderer; selecting forward or deferred PBR; writing render systems in … |
| [bevy-save-load](pack/bevy-save-load/SKILL.md) | designing Bevy 0.20 persistence with DynamicWorldBuilder, DynamicWorld::serialize, WorldAssetRoot, IoTaskPool, or SettingsPlugin: stable IDs, versioned save … |
| [bevy-testing](pack/bevy-testing/SKILL.md) | testing Bevy 0.20 with App::update, TimeUpdateStrategy, FixedUpdate, MessageCursor, or On<E> observers: deterministic stepping, async-task draining with poll_once and no … |
| [bevy-ui](pack/bevy-ui/SKILL.md) | building Bevy 0.20 UI with Node, ui_widgets::Button, Hovered / Pressed / Activate, children![], TextFont with FontSource and FontSize, BorderRadius / CornerRadius … |
| [bevy-vfx](pack/bevy-vfx/SKILL.md) | adding GPU particles via bevy_hanabi 0.20.0 (HanabiPlugin, EffectAsset, ParticleEffect, ExprWriter, SpawnerSettings, modifiers like SetPositionSphereModifier / … |
| [bevy-voxel-data](pack/bevy-voxel-data/SKILL.md) | defining voxel blocks in RON (name, textures, flags), building a runtime palette mapping BlockId -> BlockDef, baking per-block textures into a KTX2 atlas (ktx2 + … |
| [bevy-voxel-pipeline](pack/bevy-voxel-pipeline/SKILL.md) | meshing voxel chunks with block-mesh-rs (greedy_quads / visible_block_faces), translating a GreedyQuadsBuffer into a Bevy 0.20 Mesh via try_insert_attribute, choosing … |
| [bevy-voxel-runtime](pack/bevy-voxel-runtime/SKILL.md) | turning voxel edits into production Bevy 0.20 remesh work with AsyncComputeTaskPool, poll_once, Mesh3d, and Rapier Collider: dirty/halo fan-out, revision tokens … |
| [bevy-wasm-webgpu](pack/bevy-wasm-webgpu/SKILL.md) | targeting Bevy 0.20 at wasm32-unknown-unknown, choosing the webgl2 or webgpu feature, setting WgpuSettings { backends, priority: WgpuSettingsPriority::WebGPU } … |
| [bevy](pack/bevy/SKILL.md) | starting any Bevy task, choosing between Update and FixedUpdate, picking Cargo feature flags, or recalling which sibling skill covers ECS, assets, rendering, UI, or … |
