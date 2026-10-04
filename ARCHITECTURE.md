# JANCH AI - Architecture

## Prototype architecture

```text
                +---------------------+
                |  Message / Link     |
                |  Screenshot / Voice |
                +----------+----------+
                           |
                           v
                +---------------------+
                | Input Normalisation |
                +----------+----------+
                           |
        +------------------+-------------------+
        |                  |                   |
        v                  v                   v
   Text pattern       URL heuristics       Context cues
    detection          (domain/link)       (pay/KYC/etc.)
        |                  |                   |
        +------------------+-------------------+
                           v
                +---------------------+
                | Explainable Scoring |
                | + signal extraction |
                +----------+----------+
                           |
                           v
                +---------------------+
                |  Evidence Routing   |
                | official resources  |
                +----------+----------+
                           |
                           v
                +---------------------+
                |     Safety Card     |
                | score + reason +    |
                | action + sources    |
                +---------------------+
```

## Production-ready extension

```text
Client -> Secure API -> Classifier -> Claim Extraction
                     -> Approved-source Retrieval (RAG)
                     -> Evidence linker
                     -> Guardrail / policy layer
                     -> Safety Card
```

The prototype intentionally keeps analysis local. Sensitive data should not be collected unless explicitly required, authorized and protected in a production deployment.
