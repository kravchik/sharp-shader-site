---
layout: default
title: Supported Environment Matrix
section: docs
nav_order: 100
nav_title: Supported Environment Matrix
---

# Supported Environment Matrix

This matrix describes the environment that is currently validated for the beta contract.

It is intentionally narrow.
If an environment is not listed here, it should not be treated as part of the validated beta surface yet.

## Current Validated Matrix

| Area | Status | Notes |
| --- | --- | --- |
| Unity Editor | Validated | `6000.3.6f1` |
| Host OS | Validated | macOS |
| Main Unity batch workflow | Validated | generate, compile validation, expected-fail validation |
| Clean-install smoke | Validated | dev-local disposable smoke via `file:` package install |
| Pre-release validation sweep | Validated | one-command local gate |
| Build target used in validation | Validated | `StandaloneOSX` |
| Backend compile path used in validation | Validated | current Unity/Metal path |

## Not Yet Part of the Validated Beta Matrix

The following are not yet part of the validated beta contract:
- Windows as a full beta validation path;
- release-like install smoke from a staged or published package source;
- UAS install validation;
- broad cross-platform backend validation;
- broad public-example validation across multiple environments.

## Expected Limits and Caveats

Current expected caveats include:
- analyzer delivery still has a broad Unity compile-fan-out cost after generator updates;
- clean-install smoke is currently narrower than the final desired install matrix;
- Shader Graph emit is explicit-marker-based and does not imply full Shader Graph feature coverage;
- unsupported forms are expected to fail clearly rather than compile partially.

## Interpretation Rule

For beta:
- treat the matrix above as the validated environment;
- treat anything outside it as unvalidated, even if some internal experiments or partial probes exist.
