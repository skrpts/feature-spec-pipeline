# Release Notes

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
Initial catalogue release with full structural and content-quality validation. All scanner checks pass.
