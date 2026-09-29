---
name: indie-project-planning
description: Use when planning an indie game project, creating a Game Design Document (GDD), defining milestones, breaking down tasks, scoping, or when the user mentions project plan, roadmap, GDD, milestone, scope, or sprint. Covers the OffByOne Studio 5-person team planning workflow.
---

# 独立游戏项目规划

## 输入
- 一句话概念：核心玩法句 + 目标平台 + 目标时长；
- 团队能力盘点（OffByOne Studio：CEO/画师/副画师/剧本师/工程师）；
- 约束：预算（时间/资金）、Steam 发行节点、引擎（Godot 4.7.2 Mono / 4.4）。

## GDD 骨架
1. 概念（Elevator Pitch、目标玩家、卖点 3 条）
2. 玩法（核心循环、操作、系统清单、难度曲线）
3. 内容量（关卡数/敌人/Boss/物品/成就估算）
4. 艺术方向（风格参考、角色、UI、音视频基调）
5. 技术方案（引擎、关键系统、风险点）
6. 里程碑与预算表

## 里程碑（3-4 个阶段）
| 阶段 | 内容 | 验收 |
|------|------|------|
| Pre-Production | GDD、垂直切片（核心玩法可玩） | 核心循环被内部试玩认可 |
| Alpha | 全系统打通、主要关卡灰盒 | 可玩全流程（含临时美术） |
| Beta | 内容填满、平衡、本地化、性能达标 | playtesting 无 S 级问题 |
| Gold | 商店页、构建、认证、发布 | Steam 上线 |

## 任务拆解
- 每个里程碑拆为 1-2 周任务，按依赖排序；画师/工程师并行不阻塞；
- 用技能路由：素材→game-asset-pipeline，关卡→level-design，测试→playtesting，发行→steam-release；
- 风险登记：技术验证先行（最难系统第一个做）、外部依赖（API/权限）提前申请。

## 迭代节奏
- 周会：进度 vs 里程碑 + 阻塞项；每日站立可省；
- 范围控制：新点子进“冰盒”，当前里程碑冻结；砍内容优先于砍质量。

## 交接
- 产出：GDD 文档路径 + 里程碑表 + 任务拆分清单 + 风险登记。
