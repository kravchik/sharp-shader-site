---
layout: default
title: Beta Scope
section: docs
nav_order: 90
nav_title: Beta Scope
---

# Beta Scope

`SharpShader` is a Unity-oriented preview toolchain for authoring shader logic in C# and generating HLSL from it.

This beta is intentionally narrow.
It is meant to provide:
- a usable authoring model;
- a reproducible generate -> compile workflow;
- explicit diagnostics for unsupported forms;
- a small validated surface that can grow later.

It is not a claim of full HLSL coverage or broad production readiness.

## Intended Audience

This beta is primarily for:
- graphics programmers;
- shader/tooling engineers;
- technical users who are comfortable working with preview constraints.

It is not yet positioned as a zero-surprise solution for every Unity project shape or every shader workflow.

## Supported Beta Contract

At a high level, the current beta contract includes:
- C# authoring through `ShaderFunction` and `ShaderStruct`;
- a validated emitted HLSL/lowering contract;
- per-file generation in the current Unity workflow;
- explicit Shader Graph-facing emit through `ShaderGraphFunction`;
- compile-time ordinary constants emitted by reference closure;
- actionable diagnostics for the main unsupported authoring forms;
- a one-command pre-release validation sweep for the currently validated environment.

The exact emitted/lowering and Unity workflow contracts are fixed in internal source-of-truth indexes and are expected to stay explicit rather than accidental.

## Intentionally Out of Scope

This beta does not claim support for:
- full HLSL language coverage;
- complete texture/resource surface completion;
- external constants as part of the public beta contract;
- every late-pass language feature still tracked in MVP progress;
- broad cross-platform validation beyond the currently validated environment.

Unsupported forms should fail clearly rather than appear partially supported.

## Validated Workflow

The current validated workflow is:
1. install the package in Unity;
2. author a supported C# shader file;
3. run generation;
4. compile the generated shader path;
5. use diagnostics when the authoring falls outside the supported contract.

The current beta preparation also includes:
- end-to-end positive validation;
- expected-fail validation;
- clean-install smoke for the current dev-local path;
- one-command pre-release validation.

## Known Limits

Current known limits include:
- analyzer delivery still has a broad Unity compile-fan-out cost;
- validated install smoke is still narrower than the final desired matrix;
- visual demo shaders/materials live in `usecase1`, while the package ships code-first examples and demo tests;
- the beta surface is explicit, but intentionally incomplete.

## Preview Status

This is a beta/preview release.

The goal is to make the supported contract clear and reproducible first, then widen the surface deliberately.
If a workflow is not explicitly supported yet, it should be treated as outside the beta contract.
