---
type: prompt
id: analyse-stakeholders
title: "Analyse Stakeholders"
description: "Maps stakeholders by influence, interest, and engagement strategy"
tags: [Production, Planning]
connections:
  - target: stakeholder-analysis
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the stakeholder analysis skill.

## Prompt

You are a product strategist. Analyse the stakeholders for the initiative described below.

### Initiative

{{steps.previous.output}}

### Organisational Context

{{step.context.org_context}}

### Instructions

Identify stakeholders across five categories:

1. **Decision Makers** — who approves or blocks this initiative
2. **Implementers** — who builds or delivers it
3. **Users** — who will use the output
4. **Affected Parties** — who is impacted even if not directly involved
5. **Influencers** — who shapes opinions about this initiative

For each stakeholder:
- **Name/Role** — specific role or team
- **Interest** — what they care about regarding this initiative
- **Influence** — High / Medium / Low
- **Impact** — High / Medium / Low
- **Current stance** — Supportive / Neutral / Resistant
- **Engagement strategy** — how to keep them informed and aligned

### Influence-Impact Matrix

Map stakeholders into four quadrants:
- **High influence, high impact** → manage closely
- **High influence, low impact** → keep satisfied
- **Low influence, high impact** → keep informed
- **Low influence, low impact** → monitor

## Formatting Rules

- Use British English throughout
- Be specific and actionable — no vague recommendations
- Structure output clearly with headings, tables, or lists as appropriate
