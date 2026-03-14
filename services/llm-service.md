---
type: service
id: llm-service
title: LLM Service
description: "Language model service providing feature specification and edge-case analysis capabilities"
tags: [Production]
connections: []
metadata:
  serviceType: llm
  auth_type: api_key
---

## Service Description

Provides access to a large language model for feature specification and edge-case analysis. Used by all skills in this skrpt.

## Configuration

The LLM provider is configured in the skrptiq app settings. This skrpt works with any supported provider — no specific vendor is required.

## Usage Notes

- All requests include a system prompt tailored to the specific skill being invoked
- The service does not retain any data from requests — all analysis is stateless
