# SharpShader

`SharpShader` is a Unity-oriented beta toolchain for authoring shader logic in C# and generating HLSL from it.

It is built for technical users who want shader authoring to behave more like normal engineering work:
- shader logic lives in ordinary C# functions and structs;
- generation and compile steps are explicit and repeatable;
- unsupported forms fail with diagnostics instead of looking half-supported;
- example code stays testable with standard Unity Test Framework / NUnit tests.

This beta is intentionally narrow.
It does not claim full HLSL coverage or broad production-ready workflow coverage yet.

## What You Get In The Current Beta

- C# authoring through `ShaderFunction`, `ShaderStruct`, and explicit `ShaderGraphFunction`
- per-file generated HLSL in the Unity workflow
- explicit Shader Graph-facing generation where the current bridge supports it
- compile-time ordinary constants emitted by reference closure
- actionable diagnostics for the main unsupported forms
- shipped code-first examples and demo tests in the package

## Why Use It

`SharpShader` is useful when you want to:
- keep shader logic in a structured, refactorable C# codebase;
- iterate through generate -> compile instead of editing raw HLSL first;
- validate behavior with repeatable checks and narrow diagnostics;
- make shader logic easier to review, test, and change incrementally.

## Start Here

- [Quick start](./docs/quick-start.md)
- [Examples](./docs/examples.md)
- [Generation workflow](./docs/generation-workflow.md)
- [Beta scope](./docs/beta-scope.md)
- [Supported environment matrix](./docs/environment-matrix.md)
- [Troubleshooting](./docs/troubleshooting.md)
- [Full docs index](./docs/index.md)

## Who It Is For

- graphics programmers
- shader/tooling engineers
- technical users who are comfortable with preview constraints

If you need broad production claims across many Unity versions, platforms, or shader workflows, this beta is not there yet.

## Current Limits

Current known limits include:
- the validated environment is intentionally narrow;
- the Shader Graph bridge is narrower than the core HLSL generation path;
- analyzer delivery still causes broad Unity compile fan-out after generator changes;
- visual demo shaders and materials currently live in `usecase1`, while the package ships code-first examples and demo tests.

## Beta Contract

The supported public surface is intentionally explicit.
If a workflow or feature is not described in the public docs, do not treat it as part of the current beta contract.

Read these before treating a workflow as supported:
- [Beta scope](./docs/beta-scope.md)
- [Supported environment matrix](./docs/environment-matrix.md)
- [Docs index](./docs/index.md)
