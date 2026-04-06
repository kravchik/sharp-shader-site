---
layout: default
title: Troubleshooting
---

# Troubleshooting

## `Generate` does not produce expected outputs

Check:
- that your shader-authoring code compiles as normal C# first;
- that the package is installed and visible to Unity;
- that you are using supported authoring markers such as `ShaderFunction`, `ShaderStruct`, and explicit `ShaderGraphFunction`.

Then run:
- `Tools/SharpShader/Generate`

Expected outputs live in:
- `Assets/ShaderGen/*.generated.hlsl`
- `Assets/ShaderGen/SubGraphs/` when `ShaderGraphFunction` authoring is present

## Shader Graph output is missing or skipped

This usually means one of two things:
- the function was not explicitly marked as `ShaderGraphFunction`;
- the current Shader Graph bridge does not support one of the involved types.

Shader Graph support is explicit and narrower than the normal HLSL generation path.
A successful HLSL generate does not imply that every function can also become a SubGraph.

## Diagnostics appear for unsupported authoring

This is expected when code falls outside the supported surface.
The intended behavior is:
- supported authoring generates cleanly;
- unsupported authoring fails with explicit diagnostics instead of partial or misleading output.

Use these docs as the contract boundary:
- [Technical details](./technical-details.html)
- [Resources](./resources.html)
- [Docs index](./index.html)

## Visual example assets are not in the package

This is intentional.
The shipped package contains code-first examples and demo tests.
Visual demo shaders and materials currently live in `usecase1` rather than in the package itself.

## Unity recompiles broadly after generator-related changes

This is a known limitation of the current generator delivery model.
It does not mean generation is broken, but it can make iteration noisier than the final desired workflow.

## Projects with custom `.asmdef` scopes only generate partially

By default, Sharp Shader does not require any manual generator DLL placement.

If your project introduces custom Unity assemblies with `.asmdef`,
Sharp Shader coverage follows those Unity assembly boundaries.

In that case:
- copy `SharpShader.Generator.dll` into the custom assembly scope that contains
  Sharp Shader authoring code;
- if several custom assembly scopes contain Sharp Shader authoring code, copy
  the DLL into each of them;
- generated outputs still appear in the shared project output folder:
  - `Assets/ShaderGen/`

If code in one custom assembly generates correctly but code in another does not,
the most likely cause is that the second assembly scope does not currently see
the Sharp Shader generator DLL.

## `Generated.IR.json` is not present

This is expected in the normal user-facing generate path.
`Generated.IR.json` is now treated as an internal optional pipeline artifact rather than a default public output.

## Something works in generated HLSL but not in Shader Graph

Treat the HLSL path and the Shader Graph path as related but not identical surfaces.
The current package supports a narrower Shader Graph bridge than the core HLSL generation path.
If a function depends on unsupported Shader Graph resource or type forms, SubGraph generation may be skipped even when HLSL generation succeeds.
