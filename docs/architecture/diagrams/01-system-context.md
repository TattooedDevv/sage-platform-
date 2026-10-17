# Sage System Context and Major Layers

**Status:** Target architecture; components are implemented incrementally.

This view shows how a user-facing Sage experience can connect to orchestration, model runtimes, tools, knowledge services, and operations. It is intentionally technology-neutral where implementation decisions are still evolving.

```mermaid
flowchart TD
    USER[User] --> CLIENT[Web / Mobile Client]
    CLIENT --> API[Sage API]
    API --> AUTH[Identity and Permission Checks]
    AUTH --> ORCH[Request Orchestration]

    ORCH --> ROUTER[Model Router]
    ORCH --> AGENTS[Sage Council]
    ORCH --> TOOLS[Tool and Integration Layer]
    ORCH --> MEMORY[Memory Services]
    ORCH --> KNOWLEDGE[Document and Retrieval Services]

    ROUTER --> LOCAL[Local Model Runtimes]
    ROUTER --> OPTIONAL[Optional External Model Providers]
    TOOLS --> WEB[Web Research]
    TOOLS --> HOME[Homelab Operations]
    TOOLS --> VOICE[Voice and Audio]
    KNOWLEDGE --> DOCS[Approved Documents and Knowledge Sources]
    MEMORY --> STORE[Structured Memory Store]

    API --> OBS[Observability and Audit]
    ORCH --> OBS
    ROUTER --> OBS
    TOOLS --> OBS
```

## Design principles

- Keep the client separate from backend orchestration and model runtimes.
- Apply authentication, authorization, and tool-specific permissions before sensitive actions.
- Treat local and external model providers as interchangeable routing targets only when policy permits.
- Keep memory, retrieval, and auditability explicit rather than burying them inside one model prompt.
- Record which components are implemented, experimental, or planned in the relevant project documentation.
