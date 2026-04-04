# Troubleshooting

This page covers the most common current beta issues and what they mean.

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

In the current beta, Shader Graph support is explicit and intentionally narrower than the normal HLSL generation path.
A successful HLSL generate does not imply that every function can also become a SubGraph.

## Diagnostics appear for unsupported authoring

This is normal when code falls outside the current beta surface.
The intended behavior is:
- supported authoring generates cleanly;
- unsupported authoring fails with explicit diagnostics instead of partial or misleading output.

Use these docs as the contract boundary:
- [Beta scope](./beta-scope.md)
- [Authoring model](./authoring-model.md)
- [Resources](./resources.md)

## Visual example assets are not in the package

This is intentional in the current beta.
The shipped package contains code-first examples and demo tests.
Visual demo shaders and materials currently live in `usecase1` rather than in the package itself.

## Unity recompiles broadly after generator-related changes

This is a known limitation of the current analyzer delivery model.
It does not mean generation is broken, but it can make iteration noisier than the final desired workflow.

## `Generated.IR.json` is not present

This is expected in the normal user-facing generate path.
`Generated.IR.json` is now treated as an internal optional pipeline artifact rather than a default public output.

## Something works in generated HLSL but not in Shader Graph

Treat the HLSL path and the Shader Graph path as related but not identical surfaces.
The current beta supports a narrower Shader Graph bridge than the core HLSL generation path.
If a function depends on unsupported Shader Graph resource or type forms, SubGraph generation may be skipped even when HLSL generation succeeds.
