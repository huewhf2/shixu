sequenceDiagram
    participant Player1 as 玩家1
    participant Server as 游戏服务器
    participant Player2 as 玩家2

    Player1 ->> Server: 发起连接请求
    Server -->> Player1: 验证连接信息，允许连接，返回连接成功响应
    Player1 ->> Server: 发送玩家角色初始化信息（位置、外观等）
    Server ->> Player2: 转发玩家1的初始化信息给其他在线玩家（如玩家2）
    Player2 ->> Server: 发送自身角色初始化信息
    Server ->> Player1: 转发玩家2的初始化信息给玩家1

    loop 游戏进行中
        Player1 ->> Server: 发送操作信息（移动、射击等）
        Server ->> Player2: 同步玩家1的操作信息给其他玩家
        Player2 ->> Server: 发送操作信息（移动、射击等）
        Server ->> Player1: 同步玩家2的操作信息给玩家1
    end

    Player1 ->> Server: 发送断开连接请求
    Server -->> Player1: 确认断开连接，执行清理相关操作