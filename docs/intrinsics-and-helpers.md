---
layout: default
title: Intrinsics and Helpers
---

# Intrinsics and Helpers

Most intrinsics come from `Unity.Mathematics.math`.

Helper types such as `Builtins` and `MatrixBuiltins` live in `SharpShader.Hlsl`.

HLSL translation supports only calls of function annotated with `[ShaderFunction]` and of functions defined in `Unity.Mathematics.math`, `SharpShader.Hlsl.Builtins`, and `SharpShader.Hlsl.MatrixBuiltins`.

## `Unity.Mathematics`

For most scalar and vector math, prefer `Unity.Mathematics.math`.

Typical examples:

```csharp
using static Unity.Mathematics.math;

float3 n = normalize(normal);
float ndotl = saturate(dot(n, lightDir));
float3 color = lerp(albedo * 0.2f, albedo, ndotl);
```

## `MatrixBuiltins`

`MatrixBuiltins` contains helper functions for matrices.

Common cases:

| C#                                  | Generated HLSL                             |
|-------------------------------------|--------------------------------------------|
| `MatrixBuiltins.GetRow(m, i)`       | `m[i]`                                     |
| `MatrixBuiltins.GetColumn(m, i)`    | direct column vector access / construction |
| `MatrixBuiltins.SetRow(m, i, v)`    | `m[i] = v`                                 |
| `MatrixBuiltins.SetColumn(m, i, v)` | direct per-component column write          |
| `MatrixBuiltins.saturate(m)`        | matrix-wide `saturate` intent              |
| `MatrixBuiltins.lerp(a, b, t)`      | matrix-wide `lerp` intent                  |
| `MatrixBuiltins.sin(m)`             | matrix-wide `sin` intent                   |

## `Builtins`

`Builtins` contains shader-oriented helper forms that do not fit cleanly into plain `math.*`.

It contains:
- constructor-style helper forms such as `float3(...)` and `float4x4(...)`;
- `mask(...)` for vector and matrix boolean selection;
- a small number of helper forms such as `abs` for `half`;
- explicit conversion and reinterpret helpers such as `to_*`, `asint`, `asuint`, and `asfloat`.

Typical uses:
- `mask(...)` conditional selection helpers;
- constructor-style helper forms when needed;
- explicit conversion or reinterpret helpers when ordinary C# syntax is not the clearest fit.

Examples:

```csharp
Builtins.float3(x, y, z)
Builtins.mask(condition, b, a)
```

Common cases:

| C#                         | Generated HLSL intent      |
|----------------------------|----------------------------|
| `float3(x, y, z)`          | `float3(x, y, z)`          |
| `float4x4(c0, c1, c2, c3)` | `float4x4(c0, c1, c2, c3)` |
| `mask(condition, b, a)`    | `condition ? b : a`        |
| `abs(x)`                   | `abs(x)`                   |

### `mask(...)`

`Builtins.mask(...)` is the helper for explicit masked selection across vector and matrix families.

Use it when you want explicit conditional selection driven by a vector or matrix boolean condition.

Typical form:

```csharp
Builtins.mask(condition, whenTrue, whenFalse)
```

Vector/Matrix example:

| C#                  | Generated HLSL intent |
|---------------------|-----------------------|
| `mask(mask3, b, a)` | `mask3 ? b : a`       |
| `cond ? b : a`      | `cond ? b : a`        |

When to use `mask` instead of an ordinary C# ternary:
- ordinary `condition ? whenTrue : whenFalse` in C# expects a scalar `bool` condition;
- HLSL ternary also works with `bool2`, `bool3`, `bool4`, and boolean matrix families;
- `mask(...)` mirrors that HLSL behavior.

For conversion and reinterpret helpers such as `to_*`, `asint`, `asuint`, and `asfloat`, see:
- [C# to HLSL types](./type-mapping.html)

## See also

- [C# to HLSL types](./type-mapping.html)
- [Technical details](./technical-details.html)
- [Resources](./resources.html)
- [Docs index](./docs-index.html)
