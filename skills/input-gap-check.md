---
type: skill
id: input-gap-check
title: Input Gap Check
description: "Checks whether enough material exists to run the workflow, flags missing inputs and weak assumptions"
tags: [Production, Quality]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Evaluates the inputs provided to a workflow and determines whether they are sufficient to produce a quality output. Identifies missing information, thin evidence, unstated assumptions, and areas where the input is too vague to act on.

Run this before committing to a full pipeline execution — it's cheaper to discover gaps early than to produce a flawed output and revise.

## When to Use

- At the start of any workflow that depends on user-provided input
- Before a research or analysis pipeline processes incomplete source material
- When planning content, features, or campaigns and the brief may be underspecified
- After collecting data to check whether the dataset is sufficient for the intended analysis

## What It Checks

1. **Missing inputs** — required fields or materials that haven't been provided
2. **Thin inputs** — material that exists but is too brief or vague to support the workflow's stages
3. **Unstated assumptions** — things the workflow will assume if not explicitly addressed
4. **Scope mismatches** — inputs that don't match the workflow's expected format or scope
5. **Dependency gaps** — downstream stages that need output from upstream stages that may not produce enough

## What It Does NOT Do

- Judge the quality of the content itself (use `evidence-claim-check` or `consistency-check`)
- Fill in the gaps (it reports them; the user provides the missing material)
- Run the workflow — it's a pre-flight check

## Inputs

The workflow's expected inputs (from the brief or manifest) and the actual inputs provided.

## Outputs

A gap report listing: inputs present, inputs missing, inputs that are thin or ambiguous, and recommendations for what to provide before proceeding.
