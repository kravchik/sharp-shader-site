---
layout: default
title: Sharp Shader
---

# Sharp Shader

`Sharp Shader` lets you develop shader logic in C# and use it as HLSL.

## About

`Sharp Shader` lets you write shaders in C#. With natural IDE support, additional checks, and API guardrails, it greatly simplifies writing, testing, debugging, maintaining, and evolving shaders.
It is also AI-development-friendly because shader logic stays in ordinary C# code that can participate in normal .NET tooling, testing, execution, and static analysis.

## Features

- IDE editing support for shader authoring code: autocomplete, hover, and error highlighting
- debugging and inspection through CPU-simulated counterparts
- testing support through standard Unity Test Framework / NUnit workflows
- AI-development-friendly workflow through testable C# units and ordinary project tooling
- code reusability across ordinary C# logic and shader-facing authoring code
- Shader Graph node generation for explicitly marked functions
- CPU-side math and behavior stubs for shader-oriented authoring workflows

## Spec

- shader logic authored through ordinary C# functions, structs, and `Sharp Shader` attributes;
- automatic or explicit generation and compile workflow inside Unity;
- generated HLSL outputs written under `Assets/ShaderGen`;
- constant propagation and reference-closure emission for ordinary compile-time constants;
- Shader Graph bridge for generated functions;
- texture, sampler, and resource stubs for authoring and validation;
- CPU-side behavior stubs and emulation helpers for selected shader-facing types;
- `Unity.Mathematics` used as the CPU-side backing for shader-oriented numeric code and stubs;
- asmdef-aware generator placement and scoped analyzer/generator behavior in multi-assembly Unity projects;

## Plans

Current work is focused on:
- widening validated authoring and generation coverage;
- adding more shader-specific errors and warnings;
- stronger IDE integration and editor-side tooling;
- better linting and static-analysis workflows for engineering-heavy and agent-driven setups;
- extending support across more shader target types and pipelines;
- compute shader support;
- broader CPU emulation coverage for shader-facing behavior;
- extending the Shader Graph bridge;

## Links

- [Unity Asset Store](https://assetstore.unity.com/packages/slug/368862)
- [Official Site](http://sharpshader.com)
- [Quick start](./docs/quick-start.html)
- [Changelog](./docs/changelog.html)
- [Docs](./docs/docs-index.html)
