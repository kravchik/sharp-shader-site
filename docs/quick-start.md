---
layout: default
title: Quick Start
section: docs
nav_order: 20
nav_title: Quick Start
---

# Quick Start

This quick start covers the current supported beta path.

## 1. Install into a Unity project

The current beta assumes a Unity project that can install the package and already has `com.unity.mathematics` available.

For the current public path, ensure:
- the package is visible to Unity;
- `com.unity.mathematics` is present;
- the project opens and compiles scripts normally.

The validated beta environment is documented separately in:
- [Supported environment matrix](./environment-matrix.html)

## 2. Author a shader function in C#

Use the current public authoring markers:
- `ShaderFunction`
- `ShaderStruct`

Example:

```csharp
using Cs2Hlsl;
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

Use the Unity integration flow:
- `Tools/SharpShader/Generate`

Generation writes outputs into:
- `Assets/ShaderGen`

## 4. Use the generated HLSL

The generated project outputs include:
- `<SourceFile>.generated.hlsl`
- `SubGraphs/` when `ShaderGraphFunction` authoring is present

The generated HLSL can then be referenced from Unity shader-side workflows.

## 5. Validate the result

For the supported beta workflow, validate that:
- generation succeeds;
- Unity compile validation succeeds;
- unsupported forms produce actionable diagnostics instead of partial output.

See:
- [Generation workflow](./generation-workflow.html)
- [Examples](./examples.html)
- [Troubleshooting](./troubleshooting.html)
- [Authoring model](./authoring-model.html)
- [Beta scope](./beta-scope.html)
