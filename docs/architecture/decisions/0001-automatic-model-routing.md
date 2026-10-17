# ADR 0001: Automatic model routing with manual override

- **Status:** Accepted
- **Date:** 2026-10-17
- **Scope:** Future Sage inference architecture (not yet implemented)

## Context

Sage is a self-hosted AI application expected to support general chat, coding assistance, document retrieval, multimodal understanding, and specialist agents. A single fixed model or serving runtime would limit adaptability and benchmarking.

## Decision

Sage will implement a **model-router abstraction** in its application backend. **Automatic routing is the default**, and the user can **manually override** the model and inference backend. Specialist agents may define preferred model profiles and explicit fallbacks, without bypassing user overrides or resource/security rules.

### Selection criteria

- Task type and required modality (text, vision, embeddings, tools)
- Model capability, context requirements, and compatibility
- Current availability, GPU/CPU memory budget, concurrency and power constraints
- Privacy/security requirements and explicit user policies
- Measured quality, latency and reliability from reproducible evaluations

Selection decisions should be explainable and auditable, including fallback reasons. Do not silently send private data to an external provider.

## Proposed interfaces

- **Auto:** router selects an appropriate registered model and engine.
- **Manual:** user selects a specific model and engine; return a clear compatibility/availability error rather than secretly overriding the selection.
- **Agent preference:** agent profiles provide preferred models and fallbacks within central policy and resource constraints.

The router should not couple client UI or business logic to a single inference engine. Use adapters for engines such as Ollama, llama.cpp, vLLM, and SGLang **where supported and validated**. Their model formats, APIs, quantization, scheduling and hardware support differ and must be tested individually.

## Rollout and dependencies

1. Finish foundation milestone: host, rootless Podman, NVIDIA CDI, service management and persistent storage.
2. Establish a baseline model and inference backend.
3. Build repeatable evaluations of accuracy, tool use, latency, VRAM, power and recovery.
4. Add embeddings and additional model families with explicit GPU allocations.
5. Implement a capability registry, routing policies and manual UI/API overrides.
6. Introduce engine adapters and specialist agent profiles.
7. Test resource contention, GPU index/UUID handling, unavailable models and fallback behavior.

Avoid concurrent high-load GPU experiments until electrical power constraints are resolved.

## Consequences

- **Benefits:** flexible models, reproducible comparisons, specialization, backend independence and clear overrides.
- **Costs:** more operational complexity, model lifecycle management, resource budgeting, extra testing and observability.

This ADR records an architecture choice only. It does not imply that any proposed model, engine, routing logic or benchmark is currently deployed.
