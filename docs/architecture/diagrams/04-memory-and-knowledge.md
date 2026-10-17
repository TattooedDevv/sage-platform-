# Memory, Documents, and Retrieval

**Status:** Target architecture.

This diagram separates durable memory from document ingestion and retrieval. The goal is to make knowledge traceable, reviewable, and controllable rather than treating every uploaded document as trusted memory.

```mermaid
flowchart LR
    INPUT[User-Approved Documents] --> INGEST[Ingestion Pipeline]
    INGEST --> EXTRACT[Text / Metadata / OCR Extraction]
    EXTRACT --> CHUNK[Chunking and Source References]
    CHUNK --> INDEX[Search and Retrieval Index]

    QUESTION[User Question] --> RETRIEVE[Retrieve Relevant Passages]
    INDEX --> RETRIEVE
    RETRIEVE --> ANSWER[Answer with Source References]

    CONVO[Conversation and Tool Outcomes] --> CANDIDATE[Memory Candidate]
    CANDIDATE --> REVIEW[Review, Policy, and Conflict Checks]
    REVIEW --> WORKING[Working Memory]
    REVIEW --> EPISODIC[Episodic Memory]
    REVIEW --> SEMANTIC[Semantic Memory]
    REVIEW --> PROCEDURAL[Procedural Memory]

    WORKING --> CONTROLS[User Memory Controls]
    EPISODIC --> CONTROLS
    SEMANTIC --> CONTROLS
    PROCEDURAL --> CONTROLS
    CONTROLS --> RETAIN[Retention / Edit / Delete / Expire]
```

## Trust and lifecycle rules

- Preserve source references for retrieved claims wherever possible.
- Treat document contents and retrieved text as data, not as executable instructions.
- Keep memory candidates separate from approved durable memory.
- Support user review, correction, retention limits, and deletion workflows.
- Separate model-generated summaries from facts directly supported by source documents.
- Do not publish private user documents or memory content in public project artifacts.
