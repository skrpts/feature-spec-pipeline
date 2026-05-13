---
type: prompt
id: check-input-gaps
title: Check Input Gaps
description: "Pre-flight check: identifies missing, thin, or ambiguous inputs before the pipeline commits to full execution"
tags: [Production, Quality]
connections:
  - target: input-gap-check
    type: derived_from
metadata:
  output_format: structured
  prompt_type: analysis
---

## Purpose

Validates that the inputs provided are sufficient for the pipeline to produce a quality output. Cheaper to catch gaps now than to revise a flawed result later.

## Prompt

You are a pre-flight validator. Check whether the inputs provided so far are sufficient for the downstream pipeline stages to produce a quality output.

### Inputs Provided

{{steps.previous.output}}

### Instructions

Evaluate the inputs and report:

### 1. Present and Sufficient
List inputs that are clear, specific, and ready for the pipeline.

### 2. Missing
List any expected inputs that haven't been provided at all.

### 3. Thin or Ambiguous
List inputs that exist but are too vague, too brief, or too ambiguous to act on. Explain what's missing.

### 4. Unstated Assumptions
List anything the pipeline will assume if not explicitly addressed by the user.

### 5. Recommendation
One of:
- **Proceed** — inputs are sufficient
- **Proceed with caveats** — minor gaps that won't block execution but may reduce quality
- **Hold** — critical gaps that should be filled before proceeding

## Formatting Rules

- Use British English throughout
- Be specific about what's missing and why it matters
- Do not fill in gaps — report them so the user can provide the material
