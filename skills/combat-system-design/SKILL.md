---
name: combat-system-design
description: Use when designing, implementing, or balancing a combat system — attack graphs, hit detection, damage pipelines, hitboxes, animation timings, or balance tuning. Triggered by combat, hitbox, hit detection, damage, attack, 战斗, 伤害, 命中, 打击感, 平衡. Covers OffByOne Studio's 2D game combat needs in Godot/Unity.
---

# 战斗系统设计（Combat System）

## 适用
2D 独立游戏（Godot/Unity）的战斗模块：玩家攻击、敌人 AI 反击、连招、打击判定。

## 核心流程
1. **攻击图（Attack Graph）**：定义攻击状态机——Idle → Startup → Active → Recovery → Idle；每个状态带持续帧数与可取消点。
2. **命中检测（Hitbox/Hurtbox）**：
   - 攻击帧用 Hitbox（只读可判定），受击体用 Hurtbox；禁用"攻击帧里同时改两个 box"。
   - 每帧检测一次，避免漏帧（tunneling）用 swept/shapecast 或 120Hz 采样。
3. **伤害管线（Damage Pipeline）**：Hitbox 命中 → 伤害事件（含方向/硬直/击退）→ 伤害修正（连击加成/防御）→ HP 变更 → 受击表现（闪白/顿帧/击退）→ 死亡判定。
4. **打击感**：顿帧（hitstop 40-80ms）、命中音效、粒子、屏幕震动、受击闪白，至少 3 项同帧触发。
5. **连招/取消**：Recovery 可取消点白名单（Jump/Attack/Special）；连招表用表格维护（输入+状态+优先级）。

## 平衡调优（数据驱动）
- 所有数值（伤害/帧数/判定框/硬直）放配置表（JSON/CSV），代码只读表。
- 用 mcp-game-helper 或脚本批量模拟：输出每秒伤害（DPS）、连招收益、克制矩阵。
- 每次改表后跑回归：单次攻击收益 vs 资源消耗（耐力/冷却）。

## 检查清单
- [ ] Hitbox 生命周期不跨状态泄漏（Active 帧结束即失效）
- [ ] 伤害事件只发一次（加 event id 去重）
- [ ] 顿帧不冻结 UI/输入（只冻结战斗实体）
- [ ] 连招表无死循环引用
- [ ] 数值表字段与代码字段一一对应（缺字段即报错）

## 交接
- 产出：攻击图/连招表/数值表文件路径 + 回归测试结果 + 手感验收项。
