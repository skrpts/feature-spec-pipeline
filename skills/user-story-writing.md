---
type: skill
id: user-story-writing
title: User Story Writer
description: "Converting decomposed feature components into well-structured, independently deliverable user stories with MoSCoW prioritisation"
tags: [Production, Planning, Strategy]
connections:
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "3 minutes"
  avg_tokens: 2500
  trigger: manual
---

## User Story Writer

This skill converts the components identified in the feature brief into a precise, actionable set of user stories that an engineering team can pick up and deliver independently.

### Core Capability

Given the decomposed feature brief as its evidence base, this skill writes user stories in the standard "As a... I want... So that..." form for each component, assigns a MoSCoW priority and a size estimate to every story, and keeps each story independently deliverable so no story depends on another being completed first.

### Method

1. **Role grounding:** Anchor every "As a..." clause in a specific user segment named in the feature brief, never a generic "user".
2. **Single-action framing:** Keep each "I want..." clause to one specific action; split any story whose action clause needs an "and".
3. **Benefit test:** Ensure every "So that..." clause states a genuine user or business benefit, not a restatement of the feature.
4. **Prioritisation:** Apply MoSCoW (Must / Should / Could / Won't-this-iteration) so deferral decisions are visible and scope creep stays in check.

### Output Structure

Stories grouped by priority, each with a story ID, the standard-format story, a MoSCoW label, a size estimate, and implementation notes. The story set feeds the acceptance-criteria, edge-case, and specification-assembly stages downstream.
