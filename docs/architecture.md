# System Architecture

Gurwi's architecture is designed for scalability, real-time collaboration, and high-performance AI inference.

## High-Level Overview

```mermaid
graph TD
    Client[Client Application] -->|HTTPS/WSS| LB[Load Balancer]
    LB --> API[API Gateway]
    API --> Auth[Auth Service]
    API --> Core[Core Service]
    API --> AI[AI Engine]
    
    Core --> DB[(PostgreSQL)]
    Core --> Cache[(Redis)]
    
    AI --> LLM[LLM Provider]
    AI --> VectorDB[(Vector Database)]
```

## Data Flow

The following sequence diagram illustrates how a user request is processed when generating a new product plan.

```mermaid
sequenceDiagram
    participant User
    participant Client
    participant API
    participant AI
    participant DB

    User->>Client: Request Learning Module
    Client->>API: POST /api/v1/modules/generate
    API->>AI: Process Topic & Preferences
    AI->>AI: RAG Retrieval (VectorDB)
    AI->>AI: LLM Inference
    AI-->>API: Generated Module
    API->>DB: Save Module
    API-->>Client: Return Module ID
    Client->>User: Display Interactive Module
```
