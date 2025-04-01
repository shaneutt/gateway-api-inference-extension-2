# Inference Routing Rules

Authors: @kfswain, @shaneutt

## Proposal Status

 ***Provisional***

## Table of Contents

<!-- toc -->

-   [Summary](#summary)
-   [Motivation](#motivation)
-   [Goals](#goals)
-   [Non-Goals](#non-goals)
-   [Proposal](#proposal)

<!-- /toc -->

## Summary

This proposal defines the API for "Inference Routing Rules."

## Motivation

Current AI Gateway configurations with the Gateway API Inference Extension (GIE)
allow model-based routing and optimize endpoint selection using advertised
metrics and capabilities. However, users need more complex and declarative
routing rules—rules that can be chained, composed, or overridden via plugins.
This proposal defines these rules, their required behaviors for different user
roles, and the API that implements them.

## Goals

- Define a clear API for inference routing rules.
- Keep the core API simple and focused.
- Allow custom rules through expressive extension points.

## Non-goals

- Do not include every possible routing rule—only a core, essential set.

## User Stories

### Explicit Model Routing

As an AI Gateway operator, I want to route requests to endpoints serving a
specified model. If the model isn't available, the request should fail.

### Model Type Routing

As an AI Gateway operator, I want to route requests based on model type. For
example: directing LLM traffic to LLM endpoints and image generation requests
to image models.

### Fallback Models

As an AI Gateway operator, I want to designate fallback models with specific
conditions and thresholds. For instance, use "coding-expert" unless its
endpoints exceed 98% resource utilization or average latencies exceed 15
seconds; then switch to "coding-adept".

### Traffic Control

As an AI Gateway operator, I want to filter prompts through a semantic layer
before inference, blocking requests that contain PII, violate policies, or are
generally unsafe (e.g. "How do I brush my teeth with a cactus?").

### Semantic Cache

As an AI Gateway operator, I want to check inference requests against a semantic
caching system to return cached results when available and cache new ones,
either globally or on a per-model basis.

## Proposal

These user stories define specific inference routing rules which should be
expressible in a variety of combinations, and custom conditions.

**TODO**: initially focused on consensus around the "_what_?" and "_why_?"
          before addressing the "_how_?". The full proposal will be expanded
          upon in future iterations.
