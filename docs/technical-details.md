# Technical details

Key features in the current beta package:
- author shader logic in a supported C# subset and generate HLSL in Unity;
- use explicit authoring markers such as `ShaderFunction`, `ShaderStruct`, and `ShaderGraphFunction`;
- generate per-file HLSL outputs into the Unity project workflow;
- emit compile-time ordinary constants by reference closure;
- surface actionable diagnostics for unsupported authoring forms;
- support iterative shader development inside the Unity authoring workflow.
