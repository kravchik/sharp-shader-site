---
layout: default
title: Changelog
---

# Changelog

## 0.1.0-beta

First public beta / preview scope.

Current highlights:
- C# shader authoring through `ShaderFunction`, `ShaderStruct`, and explicit `ShaderGraphFunction`;
- per-file generated HLSL in the Unity workflow;
- actionable diagnostics for the main unsupported authoring forms;
- compile-time ordinary constants emitted by reference closure;
- validated end-to-end, clean-install, and pre-release validation flows for the current narrow beta environment.

Current intentional limits:
- not full HLSL surface coverage;
- not the full texture/resource completion story;
- not broad cross-platform validation;
- external constants remain outside the public beta contract.
