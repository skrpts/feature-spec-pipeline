---
type: workflow
id: feature-spec-pipeline
title: Feature Spec Pipeline
description: "End-to-end workflow for generating detailed feature specifications from rough ideas through user stories, acceptance criteria, and edge case analysis"
tags: [Production, Tested]
connections:
  - target: feature-decomposition
    type: uses
  - target: acceptance-criteria-writing
    type: uses
  - target: edge-case-analysis
    type: uses
  - target: feature-brief-generator
    type: uses
  - target: user-story-writer
    type: uses
  - target: acceptance-criteria-prompt
    type: uses
  - target: edge-case-finder
    type: uses
  - target: stakeholder-analysis
    type: uses
  - target: risk-assessment
    type: uses
  - target: feature-spec-assembler
    type: uses
  - target: risk-assessment-prompt
    type: uses
  - target: llm-service
    type: runs_on
  - target: feature-spec-standards
    type: references
  - target: product-strategy-guide
    type: references
  - target: feature-spec-guide
    type: references
  - target: feature-spec-template
    type: references
metadata:
  estimated_duration: "20 minutes"
  avg_tokens: 15000
  trigger: manual
---

## Feature Spec Pipeline

This workflow transforms a rough feature idea into a complete, implementation-ready feature specification. It follows a structured five-stage pipeline, with each stage building upon the outputs of the previous one.

### Stage 1: Feature Brief Generation

**Input:** A rough feature idea — anything from a single sentence to a paragraph of notes.

1. Invoke the **feature-brief-generator** prompt using the **feature-decomposition** skill.
2. The prompt takes the raw idea and produces a structured feature brief containing:
   - A clear problem statement
   - Target users and their context
   - High-level scope boundaries (what is in scope, what is explicitly out)
   - A list of decomposed feature components
3. **Validation gate:** The brief must contain at least 3 decomposed components. If fewer are identified, re-run with additional context or ask the user for clarification.

### Stage 2: User Story Writing

**Input:** The structured feature brief from Stage 1.

1. Invoke the **user-story-writer** prompt for each decomposed component.
2. Each component produces one or more user stories in standard format (As a... I want... So that...).
3. Stories are grouped by component and prioritised using MoSCoW labels.
4. **Validation gate:** Each component must produce at least one user story. Stories without a clear "So that..." clause are flagged for revision.

### Stage 3: Acceptance Criteria

**Input:** The complete set of user stories from Stage 2.

1. Invoke the **acceptance-criteria-prompt** using the **acceptance-criteria-writing** skill.
2. For each user story, generate 3-7 acceptance criteria in Given/When/Then format.
3. Criteria must be testable — no subjective language ("should look good", "must be fast").
4. **Validation gate:** Any criterion containing subjective terms is automatically rewritten with measurable thresholds.

### Stage 4: Edge Case Analysis

**Input:** User stories and acceptance criteria from Stages 2-3.

1. Invoke the **edge-case-finder** prompt using the **edge-case-analysis** skill.
2. Systematically identify edge cases across six dimensions:
   - Input boundaries (empty, maximum, malformed)
   - Concurrency and timing
   - Permission and access control
   - Data integrity and state transitions
   - Integration failure modes
   - Performance under load
3. Each edge case is categorised by severity (Critical, High, Medium, Low).
4. **Validation gate:** At least 5 edge cases must be identified. Fewer suggests insufficient analysis depth.

### Stage 5: Specification Assembly

**Input:** All outputs from Stages 1-4.

1. Invoke the **feature-spec-assembler** prompt.
2. Compile the feature brief, user stories, acceptance criteria, and edge cases into a single specification document following the **feature-spec-template**.
3. Add a dependency map showing relationships between components.
4. Include an implementation priority recommendation.
5. **Output:** A complete feature specification document ready for engineering handoff.

### Error Handling

- **Insufficient input:** If the initial idea is too vague (fewer than 10 words), prompt the user for additional context before proceeding.
- **Component explosion:** If decomposition yields more than 12 components, suggest splitting into multiple feature specs.
- **Circular dependencies:** If the dependency map reveals circular references between components, flag them for architectural review.
- **Missing context:** If any stage cannot produce meaningful output due to missing domain knowledge, pause and request clarification rather than generating speculative content.

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.feature_idea}}` | Yes | The rough feature idea or feature request you want to turn into a specification | `Offline mode for field users who lose connectivity in warehouses` |
| `{{input.business_context}}` | No | Any business, customer, or platform context that should shape the specification | `Enterprise prospects cite offline support as a deal-breaker` |
| `{{input.constraints}}` | No | Known technical or policy constraints | `Must work with the existing sync architecture` |

## Outputs

| Name | Description |
|------|-------------|
| A complete feature specification document ready for engineering handoff | A complete feature specification document ready for engineering handoff |

## Setup

Before running this workflow:

1. No external services required — paste your content directly and provide any supporting context as inputs or source nodes.
2. Review the included documents, assets, or source nodes and customise them to match your team, brand, or domain conventions where needed.
3. No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- The longer synthesis stages benefit from a model with strong reasoning and a generous context window.
- Extraction, classification, and formatting steps generally run well on smaller or faster models.
- Because there are no vendor-specific integrations here, provider choice is mostly a trade-off between speed, quality, and cost.

## Example Input

To test this workflow immediately after import:

```
Feature Idea: "Offline mode for field users who lose connectivity in warehouses"
Business Context: "Enterprise prospects cite offline support as a deal-breaker"
Constraints: "Must work with the existing sync architecture"
```

