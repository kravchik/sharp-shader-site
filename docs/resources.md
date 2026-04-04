---
layout: default
title: Resources
section: docs
nav_order: 80
nav_title: Resources
---

# Resources

This page gives a short public overview of the current resource authoring surface.

It is a beta summary, not a full resource API reference.

## Current model

Resource authoring uses explicit shader-facing resource types from the runtime surface.

Typical families include:
- `Texture1D<T>`
- `Texture2D<T>`
- `Texture2DArray<T>`
- `Texture3D<T>`
- `TextureCube<T>`
- `TextureCubeArray<T>`
- `Texture2DMS<T>`
- `Texture2DMSArray<T>`
- `SamplerState`
- `SamplerComparisonState`
- read-only / read-write buffer families

## Where resources are supported

In the current public beta contract, resource types are primarily intended for:
- function parameters;
- local aliases of supported resource parameters.

Do not assume arbitrary resource placement across the full C# type system.

## Typical resource authoring

Typical usage keeps the authoring shape close to shader code:

```csharp
[ShaderFunction]
public static float4 SampleColor(Texture2D<float4> texture, SamplerState sampler, float2 uv)
{
    return texture.Sample(sampler, uv);
}
```

The intended model is:
- write resource access in explicit shader-facing method signatures;
- use resource methods in familiar shader-style forms;
- let generation normalize them to canonical HLSL object-method calls.

## Texture value families

The current beta surface does not claim every possible resource/value combination.

One practical example from the current MVP surface:
- `Texture2D<T>` supports current MVP translation for scalar and vector families built around:
  - `float`
  - `half`
  - `int`
  - `uint`
  - `bool`
  - narrower `double` support

Treat documented resource families as the public contract. Do not assume every generic type argument is valid just because the C# generic form exists.

## Samplers

Sampler authoring uses explicit runtime types:
- `SamplerState`
- `SamplerComparisonState`

Use them as explicit parameters in translated functions.

## Buffers and read/write resources

The runtime surface also includes read-only and read-write buffer/resource families.

That surface exists, but the current public beta docs keep the contract summary intentionally short.

If your workflow depends heavily on buffer or RW resource forms, treat the documented beta pages and current validated examples as the source of truth rather than assuming broad parity with all HLSL forms.

## See also

- [Authoring model](./authoring-model.html)
- [C# to HLSL types](./type-mapping.html)
- [Generation workflow](./generation-workflow.html)
- [Beta scope](./beta-scope.html)
