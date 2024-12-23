# 基于Unity实现的多人联机FPS游戏时序图

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#FFFFFF', 'primaryColor': '#000000', 'edgeLabelBackground': '#FFFFFF', 'tertiaryColor': '#000000', 'primaryTextColor': '#000000', 'labelTextColor': '#000000', 'sequence': {'participantBkg': '#FFFFFF', 'participantTextColor': '#000000', 'participantBorder': '#000000', 'actorBkg': '#FFFFFF', 'actorTextColor': '#000000', 'actorBorder': '#000000', 'actor': {'Player1': {'bkg': '#FFFFFF'}}}}}}%%
sequenceDiagram
    participant Player1 as 玩家 1
    participant Player2 as 玩家 2
    participant Server as 游戏服务器
    participant DB as 数据库

    Player1->>Server: 连接到服务器
    Server->>DB: 验证玩家 1
    DB-->>Server: 验证成功
    Server-->>Player1: 连接确认

    Player2->>Server: 连接到服务器
    Server->>DB: 验证玩家 2
    DB-->>Server: 验证成功
    Server-->>Player2: 连接确认

    Player1->>Server: 发送玩家状态（位置、健康等）
    Player2->>Server: 发送玩家状态（位置、健康等）

    Server->>Player1: 更新其他玩家状态
    Server->>Player2: 更新其他玩家状态

    Player1->>Server: 射击
    Server->>Player2: 通知击中
    Player2->>Server: 发送更新状态（健康等）
    Server->>Player1: 更新玩家 2 的状态

    Player1->>Server: 断开连接
    Server->>DB: 保存玩家 1 的状态
    Server-->>Player1: 断开连接确认