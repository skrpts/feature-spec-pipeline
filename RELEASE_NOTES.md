# Release Notes

## v1.1.30
GH#863 Wave 1 (#858-A1 class) — fix the intent/output mismatch (K-045). The bundle shipped `user-story-writer` and `feature-spec-assembler` prompts, and the docs said to run them, but the `execution:` block never did — so the workflow emitted polished intermediate analysis (stakeholder + risk) instead of the promised feature specification. Restored the intended bound graph: added a **User Story Writer** step and a **Feature Spec Assembler** step (each with a backing skill so they are `from_step`-addressable — `user-story-writing`, `feature-spec-assembly`), ordered `feature-decomposition → user-story-writing → acceptance-criteria-writing → edge-case-analysis → stakeholder-analysis → risk-assessment → feature-spec-assembly`, placing the assembler as the last content step before `language-polish`. Rewired every cross-step input to an **explicit `from_step` binding** via `context_params`/`{{step.context.*}}` instead of positional or mis-pointed `{{steps.<Title>.output}}` refs — user stories now feed acceptance criteria, edge cases, and the assembler; the assembler consumes the feature brief, user stories, acceptance criteria, edge cases, and risk assessment. Completed the tail: repinned `polish-language` 1.0.1→1.0.6 (the version exposing the bindable `source` slot) and bound `language-polish`'s `source` ← the assembled feature spec, so the `output_step` polishes the actual specification rather than its positional previous. Added 2 skills (skills 3→5, total 12→14). No new required inputs.

## v1.1.29
GH#845 — republish with American English (en-US) content, completing the source-only GH#805 flip that never reached the Hub. Copy only — no functional or behaviour change.

## v1.1.28
GH#745 — declare per-step `output: {name, type}` on every execution step (feature_brief/text, acceptance_criteria/list, edge_cases/list, stakeholder_analysis/text, polished_spec/text, compliance_verdict/decision, consistency_verdict/decision, input_gaps/decision, risk_assessment/text). Lights up the #744 rich flow-map with named, typed outputs. **Also corrects the input-gap-check step to its intended `validation` type** — its `step_type` was mis-indented (outside the parallel item) and dropped at parse time, so the step previously ran untyped; it is now a validation gate. Content + structural fix (GH#748); no bindings changes.

## v1.1.27
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 14 inline shared-content files and declare 14 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Closes pre-Step-3 inline-vendoring for this bundle.

## v1.1.26
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.25
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.24
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.23
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.22
Initial catalog release with full structural and content-quality validation. All scanner checks pass.
