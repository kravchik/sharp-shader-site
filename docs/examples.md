---
layout: default
title: Examples
---

# Examples

The shipped beta examples are intentionally small.
They are meant to show two things clearly:
- the supported authoring shape for small shader functions;
- that the same logic stays ordinary C# code and can be tested with standard Unity Test Framework / NUnit tests.

## Package examples

The package currently ships three code-first examples in:
- `Packages/com.kravchik.cs2hlsl/Examples/Functions/`

Current examples:
- `SampleGrayscaleTintLibExample`
- `HeightFogLibExample`
- `ToonShadingLibExample`

Matching demo tests live in:
- `Packages/com.kravchik.cs2hlsl/Examples/Tests/`

Current demo tests:
- `SampleGrayscaleTintTestExample`
- `HeightFogTestExample`
- `ToonShadingTestExample`

## What these examples are for

Use them to learn the current beta authoring model:
- plain `ShaderFunction` authoring;
- compact `Unity.Mathematics`-based logic;
- explicit `ShaderGraphFunction` entrypoints where Shader Graph-facing emit is intended;
- ordinary C# testability for the same logic.

These examples are intentionally narrow. They are not meant to imply broad shader-library coverage.

## Visual examples

The package examples are currently code-first.
The visual demo shaders and materials live in `usecase1`, not in the shipped package.
This is intentional for the current beta because package-shipped active visual shader assets would otherwise create avoidable first-import friction.

## Recommended way to read them

A practical order is:
1. start with `SampleGrayscaleTintLibExample`;
2. look at its matching `SampleGrayscaleTintTestExample`;
3. then move to `HeightFogLibExample` and `ToonShadingLibExample`.

See also:
- [Quick start](./quick-start.html)
- [Generation workflow](./generation-workflow.html)
- [Troubleshooting](./troubleshooting.html)
