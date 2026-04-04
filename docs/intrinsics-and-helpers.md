# Intrinsics and Helpers

This page explains where shader-style math and helper operations should come from in C# authoring.

It is a practical beta guide, not a full overload catalog.

## Default rule: use `Unity.Mathematics`

For most scalar and vector math, prefer `Unity.Mathematics.math`.

Typical examples:
- `math.abs`
- `math.min`
- `math.max`
- `math.clamp`
- `math.saturate`
- `math.dot`
- `math.length`
- `math.normalize`
- `math.lerp`
- `math.smoothstep`
- `math.floor`
- `math.ceil`
- `math.frac`
- `math.sin`
- `math.cos`
- `math.pow`

Typical authoring setup:

```csharp
using Unity.Mathematics;
```

The intended model is:
- write shader math in C# with `Unity.Mathematics`;
- let `SharpShader` normalize it to canonical HLSL emit where needed.

If plain `Unity.Mathematics` is not enough, there are two additional helper surfaces:
- `ShaderMathMatrixCompat` for matrix-oriented helpers;
- `ShaderMathCompat` for a narrower compatibility layer.

## If `Unity.Mathematics` is not enough: `ShaderMathMatrixCompat`

`Unity.Mathematics.math` is not the whole story for matrix authoring.

For matrix-specific convenience operations, use `ShaderMathMatrixCompat`.

Common cases:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `ShaderMathMatrixCompat.GetRow(m, i)` | `m[i]` |
| `ShaderMathMatrixCompat.GetColumn(m, i)` | direct column vector access / construction |
| `ShaderMathMatrixCompat.SetRow(m, i, v)` | `m[i] = v` |
| `ShaderMathMatrixCompat.SetColumn(m, i, v)` | direct per-component column write |
| `ShaderMathMatrixCompat.saturate(m)` | matrix-wide `saturate` intent |
| `ShaderMathMatrixCompat.lerp(a, b, t)` | matrix-wide `lerp` intent |
| `ShaderMathMatrixCompat.sin(m)` | matrix-wide `sin` intent |

These are authoring helpers. Generated HLSL is normalized to direct matrix/vector operations rather than preserving helper calls verbatim.

## If you still need the compat layer: `ShaderMathCompat`

Use `ShaderMathCompat` when plain `math.*` does not express the intended shader authoring form cleanly.

Current practical uses:
- `mask(...)` conditional selection helpers;
- constructor-style helper forms when needed.
- a few narrow compatibility helpers such as `abs` for `half`.

Examples:

```csharp
ShaderMathCompat.float3(x, y, z)
ShaderMathCompat.mask(condition, b, a)
```

Common cases:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `ShaderMathCompat.float3(x, y, z)` | `float3(x, y, z)` |
| `ShaderMathCompat.float4x4(c0, c1, c2, c3)` | `float4x4(c0, c1, c2, c3)` |
| `ShaderMathCompat.mask(condition, b, a)` | `condition ? b : a` |
| `ShaderMathCompat.abs(x)` for `half` | `abs(x)` |

### `mask(...)`

`ShaderMathCompat.mask(...)` is the helper for explicit masked selection across vector and matrix families.

Use it when you want to choose between `whenFalse` and `whenTrue` based on a vector or matrix boolean condition.

Typical form:

```csharp
ShaderMathCompat.mask(condition, whenTrue, whenFalse)
```

Vector example:

| C# authoring | Generated HLSL intent |
| --- | --- |
| `ShaderMathCompat.mask(mask3, b, a)` | `mask3 ? b : a` |

Matrix example (`float2x2`):

| C# authoring | Generated HLSL intent |
| --- | --- |
| `ShaderMathCompat.mask(maskM, m1, m0)` | `maskM ? m1 : m0` |

Current implementation note:
- in translated shader code, `mask(...)` is currently lowered to a conditional expression;
- the docs describe the generated shader result shown in the examples above, not a promise about the exact intermediate rewrite steps.

Why not ordinary C# ternary:
- ordinary `condition ? whenTrue : whenFalse` in C# expects a scalar `bool` condition;
- `mask(...)` works with `bool2`, `bool3`, `bool4`, and boolean matrix families;
- use `mask(...)` when you need vector/matrix boolean conditions rather than a scalar `bool`.

If ordinary C# ternary already expresses the intent clearly, prefer the ternary.

For casts and reinterpret helpers such as `to_*`, `asint`, `asuint`, and `asfloat`, see:
- [C# to HLSL types](./type-mapping.md)

## What not to assume

Do not treat this beta as:
- a full replacement for every HLSL intrinsic;
- a promise that every `Unity.Mathematics` overload is part of the supported public beta surface;
- a promise that every helper in runtime is equally promoted in public docs.

If a function family is not documented in the public beta docs, do not assume it is part of the stable public contract yet.

## See also

- [C# to HLSL types](./type-mapping.md)
- [Authoring model](./authoring-model.md)
- [Resources](./resources.md)
- [Beta scope](./beta-scope.md)
