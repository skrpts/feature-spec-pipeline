---
type: skill
id: feature-decomposition
title: Feature Decomposition
description: "Breaking down high-level features into implementable components with clear boundaries and dependencies"
tags: [Production, Tested]
connections:
  - target: llm-service
    type: runs_on
  - target: feature-spec-standards
    type: references
metadata:
  estimated_duration: "3 minutes"
  avg_tokens: 3000
  trigger: manual
---

## Feature Decomposition

This skill enables the systematic breakdown of high-level, often ambiguous feature descriptions into discrete, implementable components. It is the foundational analytical capability that drives the entire feature specification pipeline.

### Core Capability

Given a rough feature idea — which may range from a single sentence to several paragraphs of unstructured notes — this skill produces a structured decomposition that identifies every meaningful component required to deliver the feature.

### Decomposition Method

The decomposition follows a layered approach:

1. **Functional layer:** Identify the distinct user-facing behaviours the feature must support. Each behaviour that could be independently tested or released is a separate component. Ask: "Could a user notice if this specific part were missing?"

2. **Data layer:** Identify the data entities, relationships, and transformations the feature requires. New data models, schema changes, and migration needs are surfaced here. Ask: "What data must exist, change, or be created for this to work?"

3. **Integration layer:** Identify external systems, APIs, or internal services the feature must interact with. Each integration point is a component. Ask: "What does this feature need to talk to?"

4. **Infrastructure layer:** Identify any infrastructure changes — new endpoints, queue configurations, caching requirements, permission models. Ask: "What must be true about the environment for this to run?"

### Output Structure

Each decomposed component includes:

- **Component name:** A clear, concise label (e.g., "Comment threading", "Email notification dispatch")
- **Description:** 2-3 sentences explaining what this component does
- **Layer:** Which decomposition layer it belongs to (Functional, Data, Integration, Infrastructure)
- **Dependencies:** Which other components this one depends on
- **Complexity estimate:** Relative sizing (Small, Medium, Large) based on the number of unknowns and integration points
- **Risk factors:** Known uncertainties or areas requiring further investigation

### Constraints

- Components must be granular enough to be estimable (no component should take more than 2 sprints to implement) but not so fine-grained that they create excessive overhead.
- Every component must have a clear owner — if it is unclear which team would implement a component, that signals an architectural boundary that needs explicit resolution.
- Dependencies between components must be acyclic. Circular dependencies indicate a design problem that should be surfaced, not hidden.
- The decomposition must be exhaustive within the stated scope. Intentionally excluded items belong in an "Out of Scope" section, not silently omitted.

### Quality Indicators

A good decomposition exhibits:
- **Cohesion:** Each component does one thing well
- **Loose coupling:** Components interact through well-defined interfaces
- **Testability:** Each component can be verified independently
- **Estimability:** Teams can provide effort estimates for each component without extensive further analysis
