---
type: asset
id: feature-spec-template
title: Feature Specification Template
description: "Template for the final feature specification document produced by this pipeline"
tags: [Production, Customer-Facing, planning:product, design:product]
connections: []
metadata:
  asset_type: "template"
  format: "markdown"
---

## Feature Specification Template

Use this template structure when assembling the final feature specification document.

---

# Feature Specification: [Feature Name]

| Field | Value |
|-------|-------|
| **Product** | [Product name] |
| **Version** | 1.0 |
| **Author** | [Author name] |
| **Date** | [YYYY-MM-DD] |
| **Status** | Draft / Review / Approved |
| **Reviewers** | [List of reviewers] |

## 1. Executive Summary

[One paragraph, maximum 100 words. A VP should be able to read this and understand what the feature does, why it matters, and what the expected impact is.]

## 2. Problem Statement

[2-3 sentences describing the problem. Focus on user pain, not technical gaps. State who is affected and what the consequence of inaction is.]

## 3. Solution Overview

[3-5 sentences describing the proposed solution. Explain what changes from the user's perspective and what value is delivered.]

## 4. Target Users

| Segment | Description | Frequency of Use | Why It Matters |
|---------|-------------|-------------------|----------------|
| [Primary] | [Description] | [Daily/Weekly/etc.] | [Specific relevance] |
| [Secondary] | [Description] | [Frequency] | [Specific relevance] |

## 5. Scope

### In Scope
- [Capability 1]
- [Capability 2]
- [Continue as needed]

### Out of Scope
- [Excluded item 1 — reason for exclusion]
- [Excluded item 2 — reason for exclusion]

### Future Considerations
- [Potential future extension 1]
- [Potential future extension 2]

## 6. Feature Components

| Component | Layer | Complexity | Dependencies | Risk |
|-----------|-------|------------|--------------|------|
| [Name] | [Functional/Data/Integration/Infrastructure] | [S/M/L] | [List] | [Risk factors] |

## 7. User Stories

### Summary
- Must Have: [X] stories
- Should Have: [X] stories
- Could Have: [X] stories
- Won't Have (this iteration): [X] stories

### [Component Name]

**US-001: [Story title]**
As a [role], I want to [action], so that [benefit].
- **Priority:** [MoSCoW]
- **Size:** [S/M/L]

#### Acceptance Criteria

AC-001: [Title]
Given [precondition]
When [action]
Then [outcome]

AC-002: [Title]
Given [precondition]
When [action]
Then [outcome]

[Repeat for each story and component]

## 8. Edge Cases & Risk Register

### Summary
- Critical: [X] | High: [X] | Medium: [X] | Low: [X]

| ID | Dimension | Title | Severity | Recommendation |
|----|-----------|-------|----------|----------------|
| EC-001 | [Dimension] | [Title] | [Severity] | [Handle/Prevent/Defer/Accept] |

### Detail

**EC-001: [Title]**
- **Scenario:** [Description]
- **Expected behaviour:** [What should happen]
- **Recommendation:** [Detailed handling approach]

## 9. Dependency Map

```
[Component A] → [Component B] (depends_on)
[Component C] → [Component A] (depends_on)
[Component D] (no dependencies — can start immediately)
```

**Critical path:** [Component X] → [Component Y] → [Component Z]

## 10. Implementation Recommendations

### Suggested Build Order
1. [Component — rationale]
2. [Component — rationale]

### Key Technical Decisions
- [Decision needed — context and options]

### Recommended Spikes
- [Spike topic — what uncertainty it resolves]

### Effort Estimate
[Range in story points or team-days, with assumptions stated]

## Appendices

### A. Glossary
| Term | Definition |
|------|-----------|
| [Term] | [Definition] |

### B. Open Questions
| Question | Status | Owner | Due Date |
|----------|--------|-------|----------|
| [Question] | [Blocking/Important/Nice to know] | [Name] | [Date] |

### C. Change Log
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [Date] | [Author] | Initial specification |
