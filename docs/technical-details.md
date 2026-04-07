---
layout: default
title: Technical details
---

# Technical details

Sharp Shader keeps shader logic in ordinary C# and generates HLSL inside the Unity workflow.

Key features:
- shader logic written in C# and converted into HLSL;
- generated per-file HLSL outputs inside `Assets/ShaderGen`;
- function, struct, and constant generation;
- Shader Graph nodes generated for explicitly marked functions;
- IDE-friendly workflow with normal autocomplete, hover, navigation, and compiler feedback;
- testable and debuggable shader logic through ordinary Unity and .NET tooling;
- AI-development-friendly workflow because shader logic stays in normal C# units and can participate in project tooling and static analysis;
- explicit diagnostics for unsupported source forms;
- built-in helper surface for constructor-style forms, explicit helper conversions, reinterpret helpers, and masked selection;
- texture, sampler, and resource surface in `SharpShader.Hlsl`;
- CPU-side runtime stubs and emulation helpers in `SharpShader.Runtime` for selected shader-facing behavior;
- `Unity.Mathematics` as the CPU-side backing for shader-oriented numeric code and stubs;
- asmdef-aware generator placement for multi-assembly Unity projects;

See also:
- [Quick start](./quick-start.html)
- [C# to HLSL types](./type-mapping.html)
- [Intrinsics and helpers](./intrinsics-and-helpers.html)
- [Resources](./resources.html)
- [Troubleshooting](./troubleshooting.html)
