---
layout: default
title: Quick Start
---

# Quick Start

Fastest path to the first generated HLSL output.

## 1. Install into a Unity project

Install Sharp Shader from the [Unity Asset Store](https://assetstore.unity.com/packages/slug/368862).

## 2. Write a shader function in C#

Use the public Sharp Shader attributes:
- `[ShaderFunction]`
- `[ShaderStruct]`

Example:

```csharp
using SharpShader;
using SharpShader.Hlsl;
using Unity.Mathematics;

public static class MyShaderLib
{
    [ShaderFunction]
    public static float3 Tint(float3 color, float3 tint)
    {
        return color * tint;
    }
}
```

## 3. Run generation in Unity

Run:
- `Tools/SharpShader/Generate`

If you want generation to run automatically after script recompilation, enable:
- `Tools/SharpShader/Auto Generate On Script Compile`

## 4. Use the generated HLSL

The generated project outputs include:
- `Assets/ShaderGen/<SourceFile>.generated.hlsl`
- `Assets/ShaderGen/SubGraphs/` when `[ShaderGraphFunction]` attribute is present

The generated HLSL can then be referenced from Unity shader-side workflows.

## 5. Validate the result

If everything is working:
- Unity Console has no Sharp Shader errors;
- Unity Console shows generation result info and timings;
- generated files appear under `Assets/ShaderGen`.

If something is unsupported or broken, Sharp Shader reports diagnostics instead of failing silently.

## More Info

- [Technical details](./technical-details.html)
- [Troubleshooting](./troubleshooting.html)
- [Docs index](./docs-index.html)
