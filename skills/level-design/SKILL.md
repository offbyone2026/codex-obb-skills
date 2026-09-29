---
name: level-design
description: Use when designing game levels, maps, level flow, difficulty curves, pacing, or when the user mentions level design, map layout, stage, dungeon, or mission structure. Covers level goals, flow/blockout, difficulty pacing, and checklist validation.
---

# 关卡设计

## 设计输入
1. 确认核心玩法句：玩家**做X**（移动/战斗/解谜/收集），关卡目标是什么；
2. 收集参数：时长预算、敌人/障碍种类与数量、资源产出点、检查点位置。

## 流程设计（Flow）
- 三段式节奏：**引入（教学/低压力）→ 发展（难度上升/新要素）→ 高潮（Boss/密集挑战）→ 收尾（奖励/剧情）**；
- 每 30-60 秒给一个“高光时刻”（新机制首次登场/大事件/奖励）；
- 路径选择：主线明确 + 1-2 条支线/秘密区（奖励非关键资源）。

## 难度曲线
- 新机制先低压力示范 → 再组合应用 → 最后压力测试；
- 敌人强度用“密度 × 组合 × 地形”调节，不只堆数值；
- 失败容忍：允许 1-2 次失误；检查点间隔 ≤ 2-3 分钟；死亡后信息不丢失。

## Blockout 与验证
1. 用灰盒（Godot 占位网格 / Unity Probuilder）跑通流程再填美术；
2. 试玩检查清单：目标可达性、无死路/软锁、相机不穿墙、性能基线（目标平台帧率）；
3. 迭代：按 playtesting 反馈调整位置/密度/节奏，一次只改一个变量。

## 交接
- 产出：关卡布局描述/灰盒场景路径 + 节奏表（时间轴：事件-难度-奖励）+ 待填美术清单。
