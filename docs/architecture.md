# Architecture

```mermaid
flowchart TB
    subgraph Frontend
      UI[Product modules]
      EVT[Analytics client]
      API[Server-side proxy routes]
    end
    subgraph Local validation environment
      BE[Express contract backend]
      DB[(Prisma state store)]
      SIM[Lifecycle controls]
      LOG[Event mirror]
    end
    MP[Analytics destination]
    UI --> EVT --> MP
    UI --> API --> BE --> DB
    SIM --> BE
    EVT -. optional QA mirror .-> LOG
```

The frontend owns event intent and typed payload construction. Proxy routes preserve the product's API boundary. The mock backend reproduces state transitions needed to test event sequences without production dependencies.
