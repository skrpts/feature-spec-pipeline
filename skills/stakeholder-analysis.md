---
type: skill
id: stakeholder-analysis
title: Stakeholder Analysis
description: "Identifying stakeholders, their needs, influence levels, and impact on product decisions"
tags: [Production, Tested]
connections:
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "4 minutes"
  avg_tokens: 3000
  trigger: manual
---

## Stakeholder Analysis

This skill identifies all stakeholders relevant to a product initiative, maps their interests and influence, and produces a stakeholder management strategy that informs communication and approval approaches.

### Core Capability

Given a product initiative description and organisational context, this skill produces a detailed stakeholder map that identifies who cares about the initiative, what they care about, how much influence they have, and how to engage them.

### Stakeholder Identification

Stakeholders are identified across five categories:

**1. Decision Makers**
People who must approve the initiative before work begins. They have budget authority, strategic oversight, or organisational accountability. Missing a decision maker means work may be rejected after significant effort.

- Typical roles: VP Product, CTO, Business Unit Lead, Budget Owner
- Key question: "Who can say no to this initiative and make it stick?"

**2. Implementers**
People who will build, design, test, or deploy the initiative. Their feasibility assessment and effort estimates are critical inputs.

- Typical roles: Engineering Lead, Design Lead, QA Lead, DevOps
- Key question: "Whose work changes as a result of this initiative?"

**3. Users**
People who will directly use the product or feature being specified. Their needs are the foundation of the requirements.

- Typical roles: End users, administrators, internal operations team
- Key question: "Who interacts with this feature daily?"

**4. Affected Parties**
People who do not use the feature directly but are affected by its existence. Their concerns may surface as constraints or requirements.

- Typical roles: Customer Support, Sales, Legal, Finance
- Key question: "Whose work is indirectly affected by this initiative?"

**5. Influencers**
People who shape opinions about the initiative without having formal authority.

- Typical roles: Key customers, industry analysts, internal thought leaders, board advisors
- Key question: "Who could build momentum for or against this initiative through informal influence?"

### Stakeholder Mapping

For each identified stakeholder, capture:

| Attribute | Description |
|-----------|-------------|
| **Name/Role** | Specific individual or role |
| **Category** | Decision Maker, Implementer, User, Affected Party, or Influencer |
| **Interest** | What they care about regarding this initiative |
| **Influence** | High (can block or accelerate), Medium (can shape direction), Low (limited ability to affect outcome) |
| **Impact** | High (significantly affected), Medium (moderately affected), Low (minimally affected) |
| **Current stance** | Supportive, Neutral, Sceptical, or Opposed |
| **Engagement strategy** | How and when to involve them (Inform, Consult, Collaborate, or Empower) |

### The Influence-Impact Matrix

Plot stakeholders on a 2x2 matrix:

| | High Impact | Low Impact |
|---|-----------|-----------|
| **High Influence** | **Manage Closely:** Full engagement, regular updates, active collaboration | **Keep Satisfied:** Regular updates, address concerns promptly |
| **Low Influence** | **Keep Informed:** Periodic updates, solicit input on relevant topics | **Monitor:** Occasional updates, available for questions |

### Engagement Planning

For each quadrant, define:
- **Communication frequency:** Daily, weekly, biweekly, or milestone-based
- **Communication format:** One-on-one meetings, group reviews, written updates, async comments
- **Involvement points:** Which stages require their input
- **Escalation path:** What to do if this stakeholder raises a blocking concern

### Conflict Resolution

When stakeholders have conflicting needs:
1. Identify the specific conflict (what each party wants and why)
2. Assess which stakeholder's need is more closely aligned with the user need and business objective
3. Propose a resolution that addresses the higher-priority need while mitigating the impact on the other party
4. Document the trade-off decision for transparency

### Output Structure

The stakeholder analysis produces:
- A stakeholder register (table listing all stakeholders with their attributes)
- An influence-impact matrix visualisation (narrative description)
- An engagement plan (who is involved at which stage, how, and why)
- A conflict register (known disagreements, proposed resolutions, decision status)
