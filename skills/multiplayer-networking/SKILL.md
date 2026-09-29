---
name: multiplayer-networking
description: Use when implementing or debugging multiplayer features — matchmaking, tick loops, realtime state sync, interest management, latency compensation, or authoritative validation. Triggered by 联机, 多人, multiplayer, netcode, 网络同步, matchmaking, 延迟补偿, 反作弊. Covers Godot/Unity authoritative-server patterns for OffByOne Studio.
---

# 多人联机网络（Multiplayer Networking）

## 适用
2D 独立游戏联机模式：合作/对战、房间制、权威服务器（自有轻量服务器 82.156.111.14 或第三方）。

## 核心模式
1. **权威服务器（Authoritative Server）**：所有关键状态（HP/位置/物品）以服务器为准，客户端只做预测与渲染；反作弊靠"服务器不信任客户端输入"。
2. **Tick Loop**：固定 20-30Hz 逻辑 tick（不随帧率漂移），渲染帧插值；Godot 用 `NetworkSynchronizer`/`MultiplayerSpawner`，Unity 用 Mirror/Netcode for GameObjects。
3. **实时状态同步**：
   - 快照同步：服务器定期广播快照（tick 号+状态），客户端插值。
   - 增量同步：只同步变化字段（用 dirty flag）。
   - 输入同步：客户端只发输入，服务器回放（适合格斗/精确类）。
4. **兴趣管理（Interest Management）**：只给玩家同步其视野内实体（AOI 网格/距离），大世界必备。
5. **延迟补偿**：
   - 客户端预测 + 服务器回滚（客户端预测自己的移动，收到快照回滚校正）。
   - 命中判定用服务器时间回放（延迟补偿 100-150ms 窗口）。
6. **验证与反作弊**：服务器校验输入速率（防加速）、状态合法性（防瞬移）、关键操作加权限校验。

## 匹配与房间
- 房间制优先：房间码 + 主机迁移（Godot 内置 relay 或自建）；匹配服务（若需要）先做"房间列表 + 快速加入"。

## 调试
- 网络面板：显示 RTT、丢包率、同步带宽、tick 偏差。
- 用模拟丢包（10-30ms 抖动 + 5% 丢包）做本地联调。

## 检查清单
- [ ] 服务器权威：客户端改不了 HP/位置（关键包走服务器验证）
- [ ] 快照带 tick 号，过期快照丢弃
- [ ] 断线重连：状态恢复（重新快照 + 平滑插值）
- [ ] 兴趣管理开启（实体数>20 时）
- [ ] 带宽预算：每个玩家 ≤ 20KB/s（2D 游戏典型值）

## 交接
- 产出：同步协议说明（字段/tick/带宽）+ 联调测试结果（延迟/丢包场景）+ 反作弊校验点清单。
