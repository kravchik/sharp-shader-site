---
layout: default
title: Authoring Model
section: docs
nav_order: 50
nav_title: Authoring Model
---

# Authoring Model

`SharpShader` lets you author shader logic in a supported C# subset and generate HLSL from it inside the Unity workflow.

Use this page as the broad guide for:
- how shader-facing code is structured;
- which common forms are part of the intended authoring model;
- how to express basic control and data-shaping patterns.

Specialized topics stay in separate pages:
- [C# to HLSL types](./type-mapping.html)
- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Resources](./resources.html)

## Current public authoring markers

- `ShaderFunction`
  - marks a method as shader-translated logic
- `ShaderStruct`
  - marks a struct as a shader-visible user type
- `ShaderGraphFunction`
  - explicitly marks a translated function as Shader Graph-facing
- `ShaderBind`
  - exists for external binding, but is not part of the promoted public beta surface

## Current authoring style

The supported beta model is centered on:
- explicit translated methods;
- explicit translated structs;
- explicit generated output in Unity;
- explicit diagnostics for unsupported forms.

The public beta contract prefers:
- clear shader-owned code;
- clear function signatures;
- deterministic generation behavior;
- narrow, explicit feature boundaries.

## Ternary expressions

Author ternary logic as ordinary C# conditional expressions:

```csharp
return condition ? whenTrue : whenFalse;
```

This is the expected way to express shader-style conditional selection in the supported C# subset.

If you need masked selection with a vector or matrix boolean condition, use `ShaderMathCompat.mask(...)` instead of ordinary C# ternary.

## Arrays

The current beta surface supports one-dimensional fixed-size arrays.

Use explicit fixed lengths where the current contract requires them.

Supported usage is centered on:
- local declarations;
- parameters;
- struct fields where the current surface allows them.

Do not assume full C# array behavior or implicit dynamic sizing in shader-facing code.

## User structs

Use `ShaderStruct` for user-defined shader-visible structs.

The intended model is:
- explicit field layout in source;
- explicit use in translated shader methods;
- deterministic generation, rather than broad C# object-model emulation.

Current user-struct authoring is centered on:
- field-based structs;
- supported constructor forms;
- clear diagnostics when a form falls outside the beta surface.

## Vectors and matrices

Vector and matrix families follow the `Unity.Mathematics` style.

Use the dedicated type mapping page for the detailed reference:
- [C# to HLSL types](./type-mapping.html)

## Constructors

Author constructors in ordinary C# / `Unity.Mathematics` style:

```csharp
new float3(1f, 2f, 3f)
math.float3(1f, 2f, 3f)
```

`SharpShader` normalizes supported constructor-style forms to canonical HLSL constructor emit.

## Casts

Author explicit casts in normal C# form:

```csharp
(float3)x
```

When needed, compatibility conversions can also be expressed through `ShaderMathCompat.to_*`.

## Constants

Ordinary compile-time constants can participate in generation when translated shader code references them.

Current intended behavior:
- referenced compile-time constants can be emitted into generated HLSL;
- non-local referenced constants are hoisted to stable generated global names.

## Shader Graph-facing functions

Shader Graph-facing emit is explicit.

That means:
- translated functions are not automatically treated as Shader Graph-facing;
- `ShaderGraphFunction` marks the functions that are intended for that surface.

## Unsupported forms

The beta model is intentionally incomplete.

When authoring falls outside the supported surface, the expected behavior is:
- fail clearly;
- provide actionable diagnostics;
- avoid misleading partial success.

## See also

- [C# to HLSL types](./type-mapping.html)
- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Resources](./resources.html)
- [Generation workflow](./generation-workflow.html)
- [Beta scope](./beta-scope.html)
