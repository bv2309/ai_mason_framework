# AI Mason V1

![AI Mason V1](ai_mason/bv2309.png)

AI Mason is a context-building framework for AI-assisted software delivery.
It defines a repeatable way to turn scattered requirements into a structured blueprint that tools like OpenAI Codex can execute against.

## What AI Mason Is

AI Mason organizes project intent in three layers:

1. `bricks`: atomic instruction units (what to build/change, acceptance criteria, constraints).
2. `walls`: scoped bundles of bricks for a specific deliverable.
3. `blueprint`: a normalized software planning model (product, architecture, data, quality, security, operations, etc.).

The `openai_mason.json` file acts like a compiler profile. Its `build_wall` instruction describes how to:

1. Load the selected wall and all referenced bricks.
2. Sort and map that context into blueprint categories/subcategories.
3. Fill blueprint fields with implementation-ready guidance.
4. Validate completeness and ask for feedback when context is insufficient.

## Intended Purpose

AI Mason is intended to:

1. Reduce ambiguous prompting by forcing structured inputs.
2. Prevent important engineering domains from being missed.
3. Make AI-generated output auditable through explicit acceptance criteria and constraints.
4. Support iterative refinement (update bricks/walls, then rebuild blueprint context).

In short: it is a planning and instruction scaffold for producing production-grade software context before or during code generation.

## Folder Model

```text
ai_mason/
  openai_mason.json                  # compiler profile + build behavior
  blueprint/                         # target context model (all fields start null)
  bricks/brick_template.json         # template for atomic instruction units
  walls/wall_template.json           # template for grouped execution scope
```

## How It Should Be Used

1. Create one or more brick files from `bricks/brick_template.json`.
2. Fill each brick with clear intent, instruction(s), acceptance criteria, and constraints.
3. Create a wall from `walls/wall_template.json` and list relevant brick paths in `brick_sources`.
4. Run the `build_wall` process (using your AI runtime/Codex workflow) so wall + bricks are mapped into blueprint files.
5. Review blueprint completeness across all domains and resolve open questions.
6. Iterate: update bricks/wall based on feedback, then rebuild.
7. Use the completed blueprint as the authoritative context for implementation, testing, docs, and operations.

## Practical Guidance

1. Keep bricks small and testable. One concern per brick is better than broad mixed intent.
2. Write acceptance criteria as observable outcomes, not vague goals.
3. Use constraints aggressively to prevent undesired architectural drift.
4. Do not mix unrelated walls; each wall should represent one coherent delivery objective.
5. Treat blueprint files as the single source of truth for execution context.

## Current State

This repository currently provides schema/templates and a compiler instruction contract.
It does not include an execution CLI; the framework is designed to be consumed by an AI agent workflow that reads these JSON artifacts and materializes blueprint content.
