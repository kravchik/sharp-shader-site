---
layout: default
title: Resources
---

# Resources

Sharp Shader exposes shader-facing resource types as explicit C# runtime types. Use them in translated method signatures and resource access code, then let generation lower them to the matching HLSL resource forms.

## Resource families

Texture, sampler, and buffer/resource families include:
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

These are explicit shader-facing types. They are not intended to model arbitrary general-purpose C# resource objects.

## Typical usage

The common authoring pattern is to place resources directly in translated function signatures:

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

## Supported placement

Resource types are primarily intended for:
- function parameters;
- local aliases of supported resource parameters.

Do not assume arbitrary resource placement across the full C# type system.

## Texture value families

Not every resource/value combination is valid.

One practical example:
- `Texture2D<T>` supports translation for scalar and vector families built around:
  - `float`
  - `half`
  - `int`
  - `uint`
  - `bool`
  - narrower `double` support

Treat documented resource families as the contract. Do not assume every generic type argument is valid just because the generic C# form exists.

## Samplers

Sampler authoring uses the explicit runtime types:
- `SamplerState`
- `SamplerComparisonState`

Use them as explicit parameters in translated functions.

## Buffers and read/write resources

The runtime surface also includes read-only and read-write buffer/resource families.

If your workflow depends heavily on buffer or RW resource forms, use the documented guides and current validated examples as the source of truth rather than assuming broad parity with every HLSL form.

## See also

- [C# to HLSL types](./type-mapping.html)
- [Technical details](./technical-details.html)
- [Docs index](./docs-index.html)
