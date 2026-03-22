---
type: document
id: feature-spec-guide
title: Feature Specification Guide
description: "Guide to writing effective feature specifications using this pipeline"
tags: [Production, Customer-Facing]
connections:
  - target: feature-spec-standards
    type: references
metadata:
  document_type: "guide"
  audience: "product-managers"
---

## Guide to Writing Effective Feature Specifications

This guide walks you through the process of creating feature specifications using the Feature Spec Pipeline. Whether you are specifying a small UI enhancement or a major platform capability, this pipeline will help you produce thorough, implementation-ready documentation.

### Before You Start

**Gather your raw inputs.** The pipeline works best when you provide:

- A clear description of the feature idea (even rough notes work)
- Context about the product or system the feature will live in
- Knowledge of who the target users are
- Any known constraints (technical, timeline, regulatory)

You do not need a polished brief. The pipeline's first stage handles structuring your raw thoughts. The more context you provide upfront, the better the output quality.

### Understanding the Pipeline Stages

**Stage 1: Feature Brief.** This stage takes your rough idea and produces a structured brief with a problem statement, solution overview, scope boundaries, and a decomposition into components. Review the output carefully — the rest of the pipeline builds on this foundation. If the decomposition misses a major component, add it here before proceeding.

**Stage 2: User Stories.** Each component from the brief generates user stories in standard format. Stories are prioritised using MoSCoW. Review the priorities — they determine what gets built first. Challenge any "Must Have" label that does not genuinely block the feature from being usable.

**Stage 3: Acceptance Criteria.** Each user story receives testable criteria in Given/When/Then format. These become the contract with your engineering team. If a criterion feels too vague to test, it needs rewriting. If you cannot imagine a QA engineer executing the test, the criterion is not specific enough.

**Stage 4: Edge Cases.** The pipeline systematically searches for scenarios outside the happy path. Review the severity classifications — a "Critical" edge case that is marked "Medium" will cause problems. Pay particular attention to data integrity and permission edge cases, as these tend to be the most costly when missed.

**Stage 5: Assembly.** All outputs are compiled into a single specification document with a dependency map and implementation recommendations. This is the document you share with your engineering team.

### Tips for Better Specifications

1. **Be specific about who.** "Users" is too broad. "Free-tier users on mobile devices" gives the pipeline much better context for story writing and edge case analysis.

2. **State what is out of scope.** Explicitly excluding things prevents scope creep and helps the pipeline focus its analysis on what matters for this iteration.

3. **Provide technical context.** If you know the feature will interact with a specific API, database, or service, mention it. The edge case analysis is significantly better with technical context.

4. **Review iteratively.** Do not wait until the final document to review. Check each stage's output before moving to the next. It is far cheaper to fix a decomposition error in Stage 1 than to redo acceptance criteria in Stage 3.

5. **Use the specification as a living document.** Update it as decisions are made during implementation. The version history should reflect the evolution of your understanding.

### Common Pitfalls

- **Over-specifying implementation details.** The spec should describe what and why, never how. Leave implementation decisions to engineering.
- **Under-specifying error handling.** If the spec does not say what happens when something goes wrong, engineering will make their own decisions — and they may not match your expectations.
- **Ignoring existing patterns.** Check how similar features work in your product. Consistency matters more than local optimisation.
- **Skipping the edge case review.** Edge cases feel theoretical until they become production incidents. Review them seriously.
