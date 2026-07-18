---
type: workflow
id: feature-spec-pipeline
title: Feature Spec Pipeline
description: "End-to-end workflow for generating detailed feature specifications from rough ideas through user stories, acceptance criteria, and edge case analysis"
tags: [Production, Tested, Planning, Quality]
connections:
  - target: feature-decomposition
    type: uses
  - target: user-story-writing
    type: uses
  - target: acceptance-criteria-writing
    type: uses
  - target: edge-case-analysis
    type: uses
  - target: stakeholder-analysis
    type: uses
  - target: risk-assessment
    type: uses
  - target: feature-spec-assembly
    type: uses
  - target: language-polish
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
  - target: brief-compliance-check
    type: uses
  - target: consistency-check
    type: uses
  - target: input-gap-check
    type: uses
metadata:
  estimated_duration: "20 minutes"
  avg_tokens: 15000
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "feature-decomposition"
  - "user-story-writing"
  - "acceptance-criteria-writing"
  - "edge-case-analysis"
  - "stakeholder-analysis"
  - "risk-assessment"
  - "feature-spec-assembly"
  - "brief-compliance-check"
  - "consistency-check"
  - "input-gap-check"
execution:
  - skill: "feature-decomposition"
    step_type: "generation"
    prompt: "feature-brief-generator"
    output: { name: "feature_brief", type: "text" }
  - skill: "user-story-writing"
    prompt: "user-story-writer"
    step_type: "generation"
    output: { name: "user_stories", type: "list" }
    bindings:
      feature_brief:
        from_step: "Feature Decomposition"
        field: output
  - skill: "acceptance-criteria-writing"
    prompt: "acceptance-criteria-prompt"
    step_type: "generation"
    output: { name: "acceptance_criteria", type: "list" }
    bindings:
      feature_brief:
        from_step: "Feature Decomposition"
        field: output
      user_stories:
        from_step: "User Story Writer"
        field: output
  - skill: "edge-case-analysis"
    prompt: "edge-case-finder"
    step_type: "synthesis"
    output: { name: "edge_cases", type: "list" }
    bindings:
      feature_brief:
        from_step: "Feature Decomposition"
        field: output
      user_stories:
        from_step: "User Story Writer"
        field: output
      acceptance_criteria:
        from_step: "Acceptance Criteria Writing"
        field: output
  - skill: "stakeholder-analysis"
    prompt: "analyse-stakeholders"
    step_type: "synthesis"
    output: { name: "stakeholder_analysis", type: "text" }
    context:
      org_context: "No additional organisational context"
  - skill: "risk-assessment"
    prompt: "risk-assessment-prompt"
    step_type: "synthesis"
    output: { name: "risk_assessment", type: "text" }
    context:
      initiative_context: "No additional initiative context"
  - skill: "feature-spec-assembly"
    prompt: "feature-spec-assembler"
    step_type: "synthesis"
    output: { name: "feature_spec", type: "text" }
    bindings:
      feature_brief:
        from_step: "Feature Decomposition"
        field: output
      user_stories:
        from_step: "User Story Writer"
        field: output
      acceptance_criteria:
        from_step: "Acceptance Criteria Writing"
        field: output
      edge_cases:
        from_step: "Edge Case Analysis"
        field: output
      risk_assessment:
        from_step: "Risk Assessment"
        field: output
  - skill: "language-polish"
    prompt: "polish-language"
    step_type: "content"
    output: { name: "polished_spec", type: "text" }
    context:
      voice_profile: "Neutral professional tone"
      grammar_strictness: "Professional"
    bindings:
      source:
        from_step: "Feature Spec Assembler"
        field: output
  - parallel:
    - skill: "brief-compliance-check"
      prompt: "check-brief-compliance"
      step_type: "review"
      output: { name: "compliance_verdict", type: "decision" }
      context:
        audience_profile: "General professional audience"
        compliance_brief: "No specific compliance requirements"
        compliance_depth: "Standard"
    - skill: "consistency-check"
      prompt: "check-consistency"
      step_type: "review"
      output: { name: "consistency_verdict", type: "decision" }
      context:
        voice_profile: "Neutral professional tone"
        consistency_strictness: "Standard"
    - skill: "input-gap-check"
      prompt: "check-input-gaps"
      step_type: "validation"
      output: { name: "input_gaps", type: "decision" }
---

## Feature Spec Pipeline

This workflow transforms a rough feature idea into a complete, implementation-ready feature specification. It follows a structured multi-stage pipeline, with each stage building upon the outputs of the previous one.

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
3. Stories are grouped by component and prioritized using MoSCoW labels.
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
3. Each edge case is categorized by severity (Critical, High, Medium, Low).
4. **Validation gate:** At least 5 edge cases must be identified. Fewer suggests insufficient analysis depth.

### Stage 5: Stakeholder Analysis

**Input:** The feature brief from Stage 1.

1. Invoke the **analyse-stakeholders** prompt using the **stakeholder-analysis** skill.
2. Identify the stakeholders affected by the feature, their interests, and their influence.
3. Surface any stakeholder concerns that should shape the specification or its rollout.

### Stage 6: Risk Assessment

**Input:** The feature brief and the analysis from the preceding stages.

1. Invoke the **risk-assessment-prompt** using the **risk-assessment** skill.
2. Enumerate the delivery and product risks for the initiative, each with a likelihood, an impact, and a mitigation.
3. This assessment is folded into the risk register of the assembled specification.

### Stage 7: Specification Assembly

**Input:** All outputs from Stages 1-6 (feature brief, user stories, acceptance criteria, edge cases, and risk assessment).

1. Invoke the **feature-spec-assembler** prompt using the **feature-spec-assembly** skill.
2. Compile the feature brief, user stories, acceptance criteria, edge cases, and risk assessment into a single specification document following the **feature-spec-template**.
3. Add a dependency map showing relationships between components.
4. Include an implementation priority recommendation.
5. **Output:** A complete feature specification document ready for engineering handoff.

### Stage 8: Polish & Quality Review

**Input:** The assembled specification from Stage 7.

1. Run the **language-polish** step over the assembled specification to produce the final, consistently-voiced document.
2. In parallel, run the quality gates: **brief-compliance-check**, **consistency-check**, and **input-gap-check**.
3. Each gate returns a verdict; unresolved gaps or inconsistencies are flagged for revision before handoff.

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
2. Review the included documents, assets, or source nodes and customize them to match your team, brand, or domain conventions where needed.
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

