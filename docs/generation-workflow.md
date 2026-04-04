---
layout: default
title: Generation Workflow
section: docs
nav_order: 40
nav_title: Generation Workflow
---

# Generation Workflow

## Entry point

The current Unity entry point is:
- `Tools/SharpShader/Generate`

## What generation does

At a high level, generation:
1. reads generator data from loaded assemblies;
2. validates and compiles the intermediate shader representation;
3. emits per-file generated HLSL into the Unity project;
4. regenerates Shader Graph artifacts where the current supported path allows it.

## Generated files

Generated outputs live in:
- `Assets/ShaderGen`

The main generated artifacts are:
- `<SourceFile>.generated.hlsl`
- `Generated.CompileAll.hlsl`
- `SubGraphs/` when `ShaderGraphFunction` authoring is present

`Generated.CompileAll.hlsl` is a technical compile harness, not a normal user-authored shader asset.

## Shader Graph behavior

Shader Graph-facing outputs are generated only for explicitly marked functions and only where the current Shader Graph path supports the involved types.

When Shader Graph generation is intentionally skipped:
- the main translation pipeline is still expected to succeed;
- the skipped state is represented explicitly rather than silently ignored.

## Validation

The current beta contract expects generation to behave in a reproducible way:
- supported authoring should generate and compile cleanly;
- unsupported authoring should fail clearly with actionable diagnostics;
- generated outputs should stay explicit and inspectable inside the Unity project.

Detailed validation and release-prep gates exist, but they are supporting infrastructure rather than primary user-facing package features.
