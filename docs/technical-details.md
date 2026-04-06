---
layout: default
title: Technical details
---

# Technical details

Sharp Shader keeps shader authoring inside ordinary C# and generates HLSL inside the Unity workflow.

Use this page as the single technical guide for:
- the current authoring surface;
- how generation runs;
- where generated outputs appear;
- which current building blocks are part of the supported package contract.

Specialized references stay separate:
- [C# to HLSL types](./type-mapping.html)
- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Resources](./resources.html)

## Authoring surface

The current public markers are:
- `ShaderFunction` for translated shader logic;
- `ShaderStruct` for user-defined shader-visible structs;
- `ShaderGraphFunction` for functions that should also emit Shader Graph-facing artifacts;
- `ShaderBind` for external binding scenarios, but not as a promoted public beta workflow.

The current supported style is centered on:
- explicit translated methods;
- explicit translated structs;
- explicit diagnostics for unsupported forms.

In practice, the package contract prefers:
- clear shader-owned code;
- clear function signatures;
- deterministic generation behavior;
- narrow, explicit feature boundaries.

## Core authoring forms

### Conditionals

Author ternary logic as ordinary C# conditional expressions:

```csharp
return condition ? whenTrue : whenFalse;
```

This is the intended way to express shader-style conditional selection in the supported C# subset.

If you need masked selection with a vector or matrix boolean condition, use `ShaderMathCompat.mask(...)` instead of ordinary C# ternary.

### Arrays

The current surface supports one-dimensional fixed-size arrays.

Supported usage is centered on:
- local declarations;
- parameters;
- struct fields where the current surface allows them.

Do not assume full C# array behavior or implicit dynamic sizing in shader-facing code.

### User structs

Use `ShaderStruct` for user-defined shader-visible structs.

The intended model is:
- explicit field layout in source;
- explicit use in translated shader methods;
- deterministic generation rather than broad C# object-model emulation.

Current struct authoring is centered on:
- field-based structs;
- supported constructor forms;
- clear diagnostics when a form falls outside the current supported surface.

### Vectors and matrices

Vector and matrix families follow the `Unity.Mathematics` style.

Use the dedicated type mapping page for the detailed reference:
- [C# to HLSL types](./type-mapping.html)

### Constructors

Author constructors in ordinary C# / `Unity.Mathematics` style:

```csharp
new float3(1f, 2f, 3f)
math.float3(1f, 2f, 3f)
```

Sharp Shader normalizes supported constructor-style forms to canonical HLSL constructor emit.

### Casts

Author explicit casts in normal C# form:

```csharp
(float3)x
```

When needed, compatibility conversions can also be expressed through `ShaderMathCompat.to_*`.

### Constants

Ordinary compile-time constants can participate in generation when translated shader code references them.

Current intended behavior:
- referenced compile-time constants can be emitted into generated HLSL;
- non-local referenced constants are hoisted to stable generated global names.

## Generation workflow

The current Unity entry points are:
- `Tools/SharpShader/Generate`
- `Tools/SharpShader/Auto Generate On Script Compile`

At a high level, generation:
1. reads generator data from loaded assemblies;
2. validates and compiles the intermediate shader representation;
3. emits per-file generated HLSL into the Unity project;
4. regenerates Shader Graph artifacts where the current supported path allows it.

Generated outputs live in:
- `Assets/ShaderGen`

The main generated artifacts are:
- `<SourceFile>.generated.hlsl`
- `Generated.CompileAll.hlsl`
- `SubGraphs/` when `ShaderGraphFunction` authoring is present

`Generated.CompileAll.hlsl` is a technical compile harness, not a normal user-authored shader asset.

Generation is expected to behave reproducibly:
- supported authoring should generate and compile cleanly;
- unsupported authoring should fail clearly with actionable diagnostics;
- generated outputs should stay explicit and inspectable inside the Unity project.

Detailed validation and release-prep gates exist, but they are supporting infrastructure rather than primary package features.

## Current technical building blocks

The current package includes:
- generated HLSL emit from supported C# authoring;
- referenced constant closure for compile-time values;
- the current Shader Graph bridge for explicitly marked functions;
- texture, sampler, and resource stubs for authoring and validation;
- CPU-side behavior stubs and emulation helpers for selected shader-facing types;
- `Unity.Mathematics` as the CPU-side backing for shader-oriented numeric code and stubs;
- asmdef-aware generator placement and scoped generator behavior in multi-assembly Unity projects.

## Shader Graph behavior

Shader Graph-facing outputs are generated only for explicitly marked functions and only where the current Shader Graph path supports the involved types.

When Shader Graph generation is intentionally skipped:
- the main translation pipeline is still expected to succeed;
- the skipped state is represented explicitly rather than silently ignored.

## Unsupported forms

The current supported surface is intentionally incomplete.

When authoring falls outside the supported surface, the expected behavior is:
- fail clearly;
- provide actionable diagnostics;
- avoid misleading partial success.

## See also

- [Quick start](./quick-start.html)
- [C# to HLSL types](./type-mapping.html)
- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Resources](./resources.html)
