---
name: feature-sliced-design
description: Guidance for designing, auditing, and migrating frontend codebases to Feature-Sliced Design (FSD), including layers/slices/segments, public API rules, import constraints, and tooling (Steiger/ESLint/CLI). Use when asked to propose FSD folder structures, evaluate whether FSD fits a project, plan incremental migration, or enforce FSD boundaries.
---

# Feature-Sliced Design

## Overview
Apply FSD consistently by turning requirements into layers, slices, and segments, then enforcing boundaries with public API rules and tooling.

## Workflow Decision Tree
1. **User asks “Should we adopt FSD?”**
   - Assess whether current architecture is causing real friction (feature delivery, onboarding, refactoring). If not, recommend staying put.
2. **User asks for structure or migration**
   - Proceed with the core workflow and provide a concrete folder tree + rules.

## Core Workflow
1. **Establish scope**: Confirm it is an application (not a library) and identify the pain points to solve.
2. **Choose minimal layers**: Start with `app`, `pages`, `shared`; add `entities` and `features` only when there is true reuse.
3. **Define slices by domain**: Use business terms; avoid creating too many features.
4. **Define segments by purpose**: Prefer `ui`, `api`, `model`, `lib`, `config`.
5. **Set public API policy**: Enforce index-based public APIs and prohibit deep imports across slices.
6. **Enforce import rules**: Same-layer slice imports are prohibited; only import from lower layers.
7. **Tooling**: Add Steiger and/or ESLint rules; optionally use CLI generators.
8. **Migration**: Reshape `app/shared` first, then `pages/widgets`, then extract `entities/features` and resolve violations.

## Output Expectations
- Provide an explicit folder tree example.
- State the import rules and public API policy clearly.
- Offer a staged migration plan and verification steps.

## References
- Load `references/fsd_core.md` for detailed rules, pitfalls, and tool commands.
