# System Logic: Agentic Flow & AWS Integration

This document outlines the orchestration strategy and agentic behavior trees governing C3 Jr.'s AWS deployment.

## AWS Architecture Overview

- **AWS Bedrock** — Foundation model layer; hosts the governed LLM with applied system prompts and guardrails.
- **AWS Lambda** — Serverless compute handling individual agent invocations and routing logic.
- **AWS Step Functions** — Orchestrates multi-step agentic workflows; mirrors the behavioral prototypes defined in Figma.

## Agentic Behavior Trees

### Entry Flow
1. User submits a query via the museum interface.
2. Lambda triggers input validation (PII scan, content filter).
3. If clean, request is routed to Bedrock with the active system prompt.

### Response Flow
1. Bedrock applies Socratic Constraint (see PROMPT_LAWS.md).
2. Step Functions evaluates response against brand and tone guardrails.
3. Approved response is returned to the user interface.
4. Interaction is logged (anonymized) for institutional review.

## Scalability Design

The serverless architecture ensures the system scales horizontally without adding operational headcount. Each Lambda invocation is stateless, and Step Functions manage state transitions — keeping the system predictable and auditable.
