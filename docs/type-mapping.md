---
layout: default
title: C# to HLSL Types
---

# C# to HLSL Types

## Scalar types

Common C# scalar types map directly to the same HLSL scalar families:

| C# type  | HLSL     |
|----------|----------|
| `bool`   | `bool`   |
| `int`    | `int`    |
| `uint`   | `uint`   |
| `float`  | `float`  |
| `double` | `double` |
| `half`   | `half`   |

## Vector types

Sharp Shader follows the `Unity.Mathematics` vector families.

| C# type                         | HLSL                            |
|---------------------------------|---------------------------------|
| `bool2`, `bool3`, `bool4`       | `bool2`, `bool3`, `bool4`       |
| `int2`, `int3`, `int4`          | `int2`, `int3`, `int4`          |
| `uint2`, `uint3`, `uint4`       | `uint2`, `uint3`, `uint4`       |
| `float2`, `float3`, `float4`    | `float2`, `float3`, `float4`    |
| `double2`, `double3`, `double4` | `double2`, `double3`, `double4` |
| `half2`, `half3`, `half4`       | `half2`, `half3`, `half4`       |

Typical component and swizzle access keeps the same intent:

| C#                         | HLSL                       |
|----------------------------|----------------------------|
| `v.x`, `v.y`, `v.z`, `v.w` | `v.x`, `v.y`, `v.z`, `v.w` |
| `v.xy`, `v.xyz`, `v.wzyx`  | the same swizzle in HLSL   |

## Matrix types

Sharp Shader follows the same `Unity.Mathematics` matrix naming families.

| C# type family | HLSL        |
|----------------|-------------|
| `boolNxM`      | `boolNxM`   |
| `intNxM`       | `intNxM`    |
| `uintNxM`      | `uintNxM`   |
| `floatNxM`     | `floatNxM`  |
| `doubleNxM`    | `doubleNxM` |

Examples:

| C# type     | HLSL        |
|-------------|-------------|
| `float3x3`  | `float3x3`  |
| `float4x4`  | `float4x4`  |
| `int3x4`    | `int3x4`    |
| `uint2x2`   | `uint2x2`   |
| `double4x4` | `double4x4` |
| `bool3x3`   | `bool3x3`   |

Matrix access uses the `Unity.Mathematics` column fields:

| C#                  | HLSL                |
|---------------------|---------------------|
| `m.c0`, `m.c1`, ... | `m.c0`, `m.c1`, ... |
| `m[i]`              | `m[i]`              |

## Constructors

Several constructor-style forms map to canonical HLSL constructors.

Typical setup:

```csharp
using SharpShader.Hlsl;
using Unity.Mathematics;
using static Unity.Mathematics.math;
```

Common cases:

| C#                                                               | HLSL                    |
|------------------------------------------------------------------|-------------------------|
| `new float3(1f, 2f, 3f)`                                         | `float3(1.0, 2.0, 3.0)` |
| `using static Unity.Mathematics.math;`<br>`float3(1f, 2f, 3f)`   | `float3(1.0, 2.0, 3.0)` |
| `Builtins.float3(1f, 2f, 3f)`                                    | `float3(1.0, 2.0, 3.0)` |
| `using static Unity.Mathematics.math;`<br>`float4(x)`            | `float4(x, x, x, x)`    |
| `using static Unity.Mathematics.math;`<br>`float2(v)`            | `float2(v.xy)`          |
| `using static Unity.Mathematics.math;`<br>`float3x3(c0, c1, c2)` | `float3x3(c0, c1, c2)`  |

Notes:

- `using static Unity.Mathematics.math` makes `float2/float3/float4/...` and `floatNxM(...)` forms available directly;
- `new floatN(...)`, `floatN(...)`, and `Builtins.floatN(...)` converge to the same constructor intent when the form is
  supported;
- some accepted C# constructor forms are lowered to a more explicit HLSL shape for backend portability.

## Casts and conversion helpers

`Builtins` conversion and reinterpret helpers live in `SharpShader.Hlsl`.

Common cases:

| C#                      | HLSL          |
|-------------------------|---------------|
| `(float3)x`             | `((float3)x)` |
| `Builtins.to_float3(x)` | `((float3)x)` |
| `Builtins.asint(x)`     | `asint(x)`    |
| `Builtins.asfloat(x)`   | `asfloat(x)`  |

Preferred rule:

- use ordinary C# casts first;
- use `Builtins.to_*` or `as*` helpers when that expresses the shader intent more clearly or matches the available
  surface better.

See also:

- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Technical details](./technical-details.html)
- [Resources](./resources.html)
- [Docs index](./docs-index.html)
