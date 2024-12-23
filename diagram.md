# FPS Multiplayer Game Sequence Diagram

```mermaid
sequenceDiagram
    participant Player1 as Player 1
    participant Player2 as Player 2
    participant Server as Game Server
    participant DB as Database

    Player1->>Server: Connect to Server
    Server->>DB: Authenticate Player 1
    DB-->>Server: Authentication Success
    Server-->>Player1: Connection Acknowledged

    Player2->>Server: Connect to Server
    Server->>DB: Authenticate Player 2
    DB-->>Server: Authentication Success
    Server-->>Player2: Connection Acknowledged

    Player1->>Server: Send Player State (Position, Health, etc.)
    Player2->>Server: Send Player State (Position, Health, etc.)

    Server->>Player1: Update Other Players' States
    Server->>Player2: Update Other Players' States

    Player1->>Server: Shoot
    Server->>Player2: Notify Hit
    Player2->>Server: Send Updated State (Health, etc.)
    Server->>Player1: Update Player2's State

    Player1->>Server: Disconnect
    Server->>DB: Save Player 1 State
    Server-->>Player1: Disconnect Acknowledged