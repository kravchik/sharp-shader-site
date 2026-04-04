---
layout: default
title: C# to HLSL Types
---

# C# to HLSL Types

This page shows the current beta authoring model for numeric types, swizzles, constructors, and casts in `SharpShader`.

It is a practical mapping guide, not a full overload reference.

## Scalar types

Common scalar authoring types map directly to the same HLSL scalar families:

| C# authoring type | Generated HLSL family |
| --- | --- |
| `bool` | `bool` |
| `int` | `int` |
| `uint` | `uint` |
| `float` | `float` |
| `double` | `double` |
| `half` | `half` |

## Vector types

`SharpShader` follows the `Unity.Mathematics` vector families.

| C# authoring type | Generated HLSL family |
| --- | --- |
| `bool2`, `bool3`, `bool4` | `bool2`, `bool3`, `bool4` |
| `int2`, `int3`, `int4` | `int2`, `int3`, `int4` |
| `uint2`, `uint3`, `uint4` | `uint2`, `uint3`, `uint4` |
| `float2`, `float3`, `float4` | `float2`, `float3`, `float4` |
| `double2`, `double3`, `double4` | `double2`, `double3`, `double4` |
| `half2`, `half3`, `half4` | `half2`, `half3`, `half4` |

Typical component and swizzle access keeps the same intent:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `v.x`, `v.y`, `v.z`, `v.w` | `v.x`, `v.y`, `v.z`, `v.w` |
| `v.xy`, `v.xyz`, `v.wzyx` | the same swizzle in HLSL |

## Matrix types

The beta surface currently follows the same `Unity.Mathematics` matrix naming families.

| C# authoring type family | Generated HLSL family |
| --- | --- |
| `boolNxM` | `boolNxM` |
| `intNxM` | `intNxM` |
| `uintNxM` | `uintNxM` |
| `floatNxM` | `floatNxM` |
| `doubleNxM` | `doubleNxM` |

Examples:

| C# authoring type | Generated HLSL family |
| --- | --- |
| `float3x3` | `float3x3` |
| `float4x4` | `float4x4` |
| `int3x4` | `int3x4` |
| `uint2x2` | `uint2x2` |
| `double4x4` | `double4x4` |
| `bool3x3` | `bool3x3` |

Matrix authoring uses the `Unity.Mathematics` column fields:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `m.c0`, `m.c1`, ... | `m.c0`, `m.c1`, ... |
| `m[i]` | `m[i]` |

## Constructors

The supported authoring surface intentionally accepts several constructor-style forms and normalizes them to canonical HLSL constructors.

Typical setup:

```csharp
using Unity.Mathematics;
using static Unity.Mathematics.math;
```

Common cases:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `new float3(1f, 2f, 3f)` | `float3(1.0, 2.0, 3.0)` |
| `using static Unity.Mathematics.math;`<br>`float3(1f, 2f, 3f)` | `float3(1.0, 2.0, 3.0)` |
| `ShaderMathCompat.float3(1f, 2f, 3f)` | `float3(1.0, 2.0, 3.0)` |
| `using static Unity.Mathematics.math;`<br>`float4(x)` | `float4(x, x, x, x)` |
| `using static Unity.Mathematics.math;`<br>`float2(v)` | `float2(v.xy)` |
| `using static Unity.Mathematics.math;`<br>`float3x3(c0, c1, c2)` | `float3x3(c0, c1, c2)` |

What to keep in mind:
- `using static Unity.Mathematics.math` makes `float2/float3/float4/...` and `floatNxM(...)` authoring forms available directly;
- `new floatN(...)`, `floatN(...)`, and `ShaderMathCompat.floatN(...)` converge to the same constructor intent when the form is supported;
- some accepted C# constructor forms are lowered to a more explicit HLSL shape for backend portability.

## Casts and conversion helpers

Common cases:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `(float3)x` | `((float3)x)` |
| `ShaderMathCompat.to_float3(x)` | `((float3)x)` |
| `ShaderMathCompat.asint(x)` | `asint(x)` |
| `ShaderMathCompat.asfloat(x)` | `asfloat(x)` |

Preferred rule:
- use ordinary C# casts first;
- use `ShaderMathCompat.to_*` or `as*` helpers when that expresses the shader intent more clearly or matches the available beta surface better.

## What this page is not

This page does not claim:
- every overload for every numeric family;
- full resource type coverage;
- broad backend guarantees beyond the current beta environment.

For the current public beta contract, also see:
- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Authoring model](./authoring-model.html)
- [Resources](./resources.html)
- [Beta scope](./beta-scope.html)
- [Generation workflow](./generation-workflow.html)
