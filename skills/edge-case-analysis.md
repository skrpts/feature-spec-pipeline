---
type: skill
id: edge-case-analysis
title: Edge Case Analysis
description: "Identifying edge cases, failure modes, and boundary conditions through systematic analysis across six dimensions"
tags: [Production, Tested, analysis:risk, planning:product, quality:testing, design:product]
connections:
  - target: llm-service
    type: runs_on
  - target: feature-spec-standards
    type: references
metadata:
  estimated_duration: "4 minutes"
  avg_tokens: 3000
  trigger: manual
---

## Edge Case Analysis

This skill systematically identifies edge cases, failure modes, and boundary conditions that are routinely missed during feature specification. It operates across six analysis dimensions to ensure thorough coverage.

### Core Capability

Given a feature's user stories and acceptance criteria, this skill produces a categorised inventory of edge cases — scenarios that fall outside the happy path but must be explicitly handled to avoid bugs, data corruption, or degraded user experience.

### The Six Dimensions

#### 1. Input Boundaries

Analyse every user input and data entry point for boundary behaviour:

- **Empty inputs:** What happens when required fields are left blank, optional fields are omitted, or arrays are empty?
- **Maximum values:** What happens at character limits, file size caps, numeric maximums?
- **Malformed data:** What happens with invalid email formats, SQL injection attempts, Unicode edge cases (zero-width characters, RTL text, emoji sequences)?
- **Type mismatches:** What happens when a number field receives text, or a date field receives an invalid format?

#### 2. Concurrency and Timing

Analyse scenarios where multiple actions occur simultaneously or in unexpected sequences:

- **Race conditions:** Two users editing the same record. A save request arriving after a delete.
- **Stale data:** User viewing data that has been modified by another process since page load.
- **Timeout scenarios:** What happens when an API call takes 30 seconds? When a background job never completes?
- **Retry behaviour:** What happens when a failed operation is retried — is it idempotent?

#### 3. Permission and Access Control

Analyse authorisation boundaries:

- **Role transitions:** What happens when a user's role changes mid-session?
- **Shared resources:** Can User A access User B's data through predictable URL patterns?
- **Token expiry:** What happens when authentication expires during a multi-step flow?
- **Elevated privileges:** Can admin-only actions be triggered through API calls by non-admin users?

#### 4. Data Integrity and State Transitions

Analyse data consistency across state changes:

- **Partial failures:** What happens if step 3 of a 5-step process fails? Is the data left in a consistent state?
- **Rollback scenarios:** Can a failed operation be cleanly reversed?
- **Orphaned records:** When a parent entity is deleted, what happens to child records?
- **Migration edge cases:** What happens to existing data when the schema changes?

#### 5. Integration Failure Modes

Analyse behaviour when external dependencies fail:

- **Service unavailability:** What happens when a third-party API is down?
- **Degraded responses:** What happens when an API returns a 200 but with incomplete data?
- **Rate limiting:** What happens when API quotas are exceeded?
- **Version mismatches:** What happens when an API changes its response format?

#### 6. Performance Under Load

Analyse behaviour at scale:

- **Large data sets:** What happens when a list contains 10,000 items instead of 10?
- **Burst traffic:** What happens when 100 users trigger the same action simultaneously?
- **Memory pressure:** What happens when the operation processes a 500MB file?
- **Cascading failures:** If one component slows down, does it create backpressure across the system?

### Severity Classification

Each identified edge case is classified:

- **Critical:** Data loss, security breach, or complete feature failure
- **High:** Significant user impact, workaround exists but is painful
- **Medium:** Noticeable degradation, reasonable workaround available
- **Low:** Minor inconvenience, cosmetic impact only

### Output Format

Each edge case entry contains: a descriptive title, the dimension it belongs to, a severity rating, a description of the scenario, expected behaviour (what should happen), and a recommended handling approach.
