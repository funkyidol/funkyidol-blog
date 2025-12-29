---
title: "Observability pipeline for product teams"
date: 2025-11-12
summary: "Unified tracing, metrics, and logs with opinionated dashboards so product teams can debug without SRE handoffs."
draft: false
tags: ["observability", "otel", "sre"]
---

## Problem

Fragmented telemetry made it hard to correlate frontend errors, edge behavior, and backend performance during incidents.

## Approach

- Standardized OpenTelemetry instrumentation across services and edge functions with shared semantic conventions.
- Built a collector pipeline that enriches events with request IDs, user context, and deployment metadata.
- Shipped curated Grafana dashboards and SLOs per service; alerts route via PagerDuty with runbook links.
- Added sampling rules to keep costs predictable while preserving tail-latency visibility.

## Outcome

- Median time-to-detect cut by ~40% and time-to-mitigate by ~25%.
- Engineers can trace a user journey end-to-end (edge → API → browser) from one place.
- Predictable telemetry spend through adaptive sampling and retention policies.
