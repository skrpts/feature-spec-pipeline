---
type: source
id: feature-spec-standards
title: Feature Specification Standards
description: "Reference standards and industry best practices for feature specification writing"
tags: [Production, planning:product, design:product]
connections: []
metadata:
  source_type: "reference"
  last_updated: "2026-03-10"
---

## Feature Specification Standards

This source document codifies the standards and conventions that govern feature specification writing within this pipeline. All generated specifications must conform to these standards.

### User Story Standards

**Format:** All user stories must follow the Connextra format:

> As a [specific user role], I want to [specific action], so that [measurable benefit].

**Rules:**
- The user role must be a defined persona or role within the product, never "a user" generically
- The action must be singular — one verb, one object
- The benefit must be a genuine outcome, not a restatement of the action
- Stories must be independent (can be delivered in any order unless explicit dependencies exist), negotiable (details can be discussed), valuable (delivers user or business value), estimable (team can size it), small (fits within a single sprint), and testable (has clear pass/fail criteria)

### Acceptance Criteria Standards

**Format:** Given/When/Then (Gherkin-style):

```
Given [precondition]
When [action]
Then [observable outcome]
```

**Rules:**
- Each criterion tests exactly one behaviour
- Outcomes must be measurable — no subjective terms
- Performance thresholds follow the standard: page loads < 2s, API responses < 500ms, batch operations < 30s
- Error messages must be specified verbatim where user-facing
- Boundary values must be tested explicitly (minimum, maximum, and one beyond each)

### Edge Case Classification

**Severity Levels:**

| Level | Definition | Response Required |
|-------|-----------|-------------------|
| Critical | Data loss, security breach, or complete feature failure | Must be addressed before release |
| High | Significant user impact with no reasonable workaround | Should be addressed before release |
| Medium | Noticeable issue with a reasonable workaround available | Address in a fast-follow release |
| Low | Minor cosmetic or convenience issue | Backlog for future consideration |

### Specification Document Standards

**Required sections:** Executive Summary, Problem Statement, Solution Overview, User Stories, Acceptance Criteria, Edge Cases, Dependency Map, Implementation Recommendations, Glossary, Open Questions

**Versioning:** Specifications use semantic versioning. Major version changes indicate fundamental scope changes. Minor versions add stories or criteria. Patch versions fix errors or clarify wording.

**Review process:** Every specification must be reviewed by at least one engineer and one designer before moving to "Approved" status.

### MoSCoW Prioritisation Guidelines

| Priority | Criterion |
|----------|-----------|
| Must Have | Feature is unusable without this. Maximum 60% of total stories. |
| Should Have | Important for user satisfaction. 20-30% of total stories. |
| Could Have | Nice to have, first cut candidates. 10-20% of total stories. |
| Won't Have | Acknowledged and deferred. No limit, but must be documented. |
