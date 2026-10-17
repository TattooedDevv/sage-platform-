# Sage Council and Sage Quant

**Status:** Target architecture; agent roles and coordination are planned to be implemented in stages.

Sage Council is intended to coordinate specialized agents under a central orchestrator. Sage Quant is a domain-focused capability for financial research and analysis, not an autonomous authority for financial decisions.

```mermaid
flowchart TD
    USER[User Goal] --> SAGE[Sage Orchestrator]
    SAGE --> PLAN[Task Plan and Scope]
    PLAN --> RESEARCH[Research Agent]
    PLAN --> ENGINEERING[Engineering Agent]
    PLAN --> SECURITY[Security / Blue Team Agent]
    PLAN --> INFRA[Infrastructure Agent]
    PLAN --> DATA[Data Agent]
    PLAN --> CRITIC[Independent Critic]
    PLAN --> TUTOR[Tutor Agent]

    RESEARCH --> EVIDENCE[Evidence and Findings]
    ENGINEERING --> EVIDENCE
    SECURITY --> EVIDENCE
    INFRA --> EVIDENCE
    DATA --> EVIDENCE
    CRITIC --> REVIEW[Challenge Assumptions and Review]
    EVIDENCE --> REVIEW
    TUTOR --> REVIEW

    SAGE --> QUANT[Sage Quant]
    QUANT --> MARKET[Market and Company Research]
    QUANT --> SCENARIOS[Scenario and Risk Analysis]
    QUANT --> TRACK[Prediction and Thesis Tracking]
    MARKET --> QUANTRESULT[Evidence-Based Quant Output]
    SCENARIOS --> QUANTRESULT
    TRACK --> QUANTRESULT

    REVIEW --> GATE[Policy, Permission, and Human Review]
    QUANTRESULT --> GATE
    GATE --> OUTPUT[Final Answer or Proposed Action]
```

## Coordination and safety

- Agents should have scoped roles, independent task context where useful, and limited tool permissions.
- The critic should examine evidence, uncertainty, and conflicting conclusions rather than simply vote with other agents.
- External actions require authorization appropriate to their risk.
- Financial outputs should distinguish sourced facts, assumptions, scenarios, and uncertainty. They should not promise returns or replace the user's judgment.
- Agent count and concurrency should adapt to available compute rather than assume every agent runs simultaneously.
