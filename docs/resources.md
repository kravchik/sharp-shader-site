---
layout: default
title: Resources
---

# Resources

Sharp Shader exposes shader-facing resource types as explicit C# types. They provide both shader API and basic CPU simulation for testing and debugging.

These types live in `SharpShader.Hlsl`.

You use them as a parameter to a function. In C# unit tests you can also create them.

## Resource families

Sampled texture families:
- `Texture1D<T>`
- `Texture1DArray<T>`
- `Texture2D<T>`
- `Texture2DArray<T>`
- `Texture3D<T>`
- `TextureCube<T>`
- `TextureCubeArray<T>`
- `Texture2DMS<T>`
- `Texture2DMSArray<T>`

Read-only buffer families:
- `Buffer<T>`
- `StructuredBuffer<T>`
- `ByteAddressBuffer`

Read-write texture and buffer families:
- `RWBuffer<T>`
- `RWTexture1D<T>`
- `RWTexture1DArray<T>`
- `RWTexture2D<T>`
- `RWTexture2DArray<T>`
- `RWTexture3D<T>`
- `RWStructuredBuffer<T>`
- `RWByteAddressBuffer`
- `AppendStructuredBuffer<T>`
- `ConsumeStructuredBuffer<T>`

Sampler families:
- `SamplerState`
- `SamplerComparisonState`

Helper view types such as `mips`/`sample` slices are also part of the public surface for the relevant texture families.

## Typical usage

The common pattern is to use resources as parameters in translated functions:

```csharp
[ShaderFunction]
public static float4 SampleColor(Texture2D<float4> texture, SamplerState sampler, float2 uv)
{
    return texture.Sample(sampler, uv);
}
```

The same types can also be created in C# tests for CPU-side validation:

```csharp
var texture = new Texture2D<float4>(2, 2, new[]
{
    new float4(1, 0, 0, 1),
    new float4(0, 1, 0, 1),
    new float4(0, 0, 1, 1),
    new float4(1, 1, 1, 1),
});

var sampler = SamplerState.PointClamp;
float4 color = texture.Sample(sampler, new float2(0.25f, 0.25f));
```

## See also

- [C# to HLSL types](./type-mapping.html)
- [Technical details](./technical-details.html)
- [Docs index](./docs-index.html)
