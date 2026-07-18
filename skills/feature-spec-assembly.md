---
type: skill
id: feature-spec-assembly
title: Feature Spec Assembler
description: "Compiling the feature brief, user stories, acceptance criteria, edge cases, and risk assessment into a single, cohesive feature specification document"
tags: [Production, Planning, Strategy]
connections:
  - target: llm-service
    type: runs_on
  - target: feature-spec-template
    type: references
metadata:
  estimated_duration: "4 minutes"
  avg_tokens: 4000
  trigger: manual
---

## Feature Spec Assembler

This skill assembles the outputs of every upstream stage into the workflow's real deliverable: a single, implementation-ready feature specification document that engineering, design, and leadership can all use.

### Core Capability

Given the feature brief, the user stories, the acceptance criteria, the edge-case analysis, and the risk assessment as its evidence base, this skill compiles them into one coherent specification following the feature-spec-template — with an executive summary, a stories section organised by component and MoSCoW priority, criteria grouped by story, an edge-case and risk register ordered by severity, a dependency map, and an implementation-priority recommendation.

### Method

1. **Consolidation:** Pull each section from its upstream artifact rather than regenerating it, preserving the analysis already produced.
2. **Cross-checks:** Verify every story has at least one acceptance criterion, every brief component appears in the stories, and no sections contradict one another.
3. **Prioritisation:** Derive a suggested build order and flag critical-path components from the dependency map.

### Output Structure

A single markdown specification document with consistent heading levels and tables where they aid readability — the finished feature spec, ready for engineering handoff and for the final language-polish pass.
