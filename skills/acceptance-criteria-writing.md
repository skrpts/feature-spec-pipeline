---
type: skill
id: acceptance-criteria-writing
title: Acceptance Criteria Writing
description: "Writing precise, testable acceptance criteria in Given/When/Then format with measurable outcomes"
tags: [Production, Tested]
connections:
  - target: claude-service
    type: runs_on
  - target: feature-spec-standards
    type: references
metadata:
  estimated_duration: "3 minutes"
  avg_tokens: 2500
  trigger: manual
---

## Acceptance Criteria Writing

This skill produces acceptance criteria that are precise enough to serve as the contract between product and engineering. Every criterion written using this skill is testable, unambiguous, and directly tied to a user story.

### Core Capability

Given a user story in standard format (As a... I want... So that...), this skill generates a set of acceptance criteria that define exactly what "done" means. The criteria serve three audiences simultaneously: developers implementing the feature, QA engineers testing it, and product managers verifying it meets the original intent.

### Format

All criteria follow the Given/When/Then structure:

- **Given** — the precondition or context (system state, user role, data present)
- **When** — the action the user takes or the event that occurs
- **Then** — the observable, measurable outcome

Each criterion is a single, atomic statement. Compound criteria (those using "and" in the Then clause to describe multiple outcomes) are split into separate criteria.

### Writing Principles

1. **Measurability over subjectivity.** Never write "the page loads quickly." Write "the page loads within 2 seconds on a 3G connection." Every criterion must have an observable pass/fail condition.

2. **Specificity over generality.** Never write "the user sees an error message." Write "the user sees a red inline validation message reading 'Email address is required' below the email input field."

3. **Completeness over brevity.** Each criterion must be self-contained. A tester should be able to execute it without referring to other criteria or asking clarifying questions.

4. **Positive and negative paths.** For each user story, include criteria for:
   - The happy path (everything works as expected)
   - Validation failures (invalid input, missing data)
   - Permission boundaries (unauthorised access attempts)
   - State transitions (what changes in the system after success)

5. **Boundary conditions.** Explicitly state behaviour at boundaries:
   - Empty states (no data, first-time use)
   - Maximum limits (character counts, file sizes, list lengths)
   - Concurrent access (two users editing simultaneously)

### Quantity Guidelines

- **Simple stories** (single interaction, no state change): 3-4 criteria
- **Standard stories** (form submission, CRUD operation): 5-6 criteria
- **Complex stories** (multi-step flow, integrations, permissions): 6-7 criteria

More than 7 criteria per story suggests the story should be split.

### Anti-Patterns to Avoid

- **Implementation criteria:** "The system uses a Redis cache" is an implementation detail, not acceptance criterion. Focus on behaviour, not architecture.
- **Duplicate coverage:** If two criteria test the same behaviour with different wording, consolidate them.
- **Assumed context:** Never assume the reader knows the domain. Spell out what "active user" or "valid input" means in the Given clause.
- **Untestable criteria:** "The system is secure" or "The UX is intuitive" are not criteria. They are aspirations.
