---
type: service
id: claude-service
title: Claude Service
description: "How this skrpt uses Anthropic Claude for feature analysis, decomposition, and specification writing"
tags: [Production, Tested]
connections: []
metadata:
  provider: "anthropic"
  model: "claude-sonnet"
  estimated_duration: "N/A"
---

## Claude Service — Feature Spec Pipeline

This skrpt uses Anthropic Claude as its primary AI service for all analytical and generative tasks within the feature specification pipeline.

### Usage Pattern

Claude is invoked at each stage of the pipeline:

1. **Feature Brief Generation** — Claude analyses the rough feature idea, applies the feature-decomposition skill, and produces a structured brief. This requires strong analytical reasoning to identify implicit requirements and decompose abstract concepts into concrete components.

2. **User Story Writing** — Claude converts decomposed components into properly formatted user stories. This requires understanding of user-centric thinking and the ability to articulate benefits rather than implementations.

3. **Acceptance Criteria Generation** — Claude produces Given/When/Then criteria from user stories. This requires precision and the ability to identify measurable outcomes from qualitative descriptions.

4. **Edge Case Analysis** — Claude systematically works through six analysis dimensions to identify scenarios that are not covered by the happy path. This requires adversarial thinking and broad knowledge of common failure modes.

5. **Specification Assembly** — Claude compiles all outputs into a cohesive document, resolving inconsistencies and adding structural elements like dependency maps and implementation recommendations.

### Configuration

- **Temperature:** 0.3 for analytical tasks (decomposition, acceptance criteria, edge cases), 0.5 for generative tasks (brief generation, story writing, assembly)
- **Max tokens:** 4000 per invocation, 8000 for the final assembly step
- **Context window:** The full pipeline accumulates context. Each stage receives the outputs of all previous stages as input.

### Requirements

- An active Anthropic API key or Claude CLI access
- Sufficient token quota for the full pipeline (approximately 15,000 tokens per feature specification)
- No external network access required beyond the Anthropic API endpoint
