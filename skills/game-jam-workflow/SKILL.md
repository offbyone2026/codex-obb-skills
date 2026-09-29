---
name: game-jam-workflow
description: Use when participating in a game jam or time-boxed 48-72h game sprint — compressed scope, rapid prototyping, playable vertical slice, submission. Triggered by Game Jam, 游戏开发挑战赛, 48小时, 72小时, 冲刺, jam. Applies to OffByOne Studio's jam participation (e.g. itch.io jams via itch-jams-mcp).
---

# Game Jam 冲刺流程（48-72h）

## 时间分配（72h 模板）
- 第 0-6h：主题解析 + 脑暴 + 一句话概念锁定（写完 GDD 骨架就冻结范围）
- 第 6-18h：垂直切片（核心循环可玩，丑但完整）
- 第 18-48h：内容填充（1-3 关/机制变体）+ 手感打磨
- 第 48-66h：美术/音频收尾、菜单/结算/失败态补齐
- 第 66-72h：打包测试、itch.io 页面上传、截图/预告图、提交

## 范围纪律（关键）
- 概念一句话能讲清，否则砍。
- 垂直切片优先：先让"核心循环"能玩，再谈"更多内容"。
- 冻结清单：美术规格（分辨率/风格）、音频数量上限（≤10 个音效）、关卡数量上限（≤3）。
- 备份：每 6h 提交一次 git；最后 3h 只修 P0 bug 不新增功能。

## 分工（5 人团队）
- CEO：概念/范围/决策
- 工程师：核心循环 + 打包
- 画师+副画师：美术规格内批量产出（可用 game-asset-pipeline 技能加速）
- 剧本师：文案/世界观/叙事点缀（沿用 narrative-design 技能）
- 全员最后 3h：测试 + 修 P0

## 提交清单（itch.io）
- [ ] 可玩构建（WebGL/桌面包，注明平台与操作）
- [ ] 截图 ≥ 3 张 + 封面图
- [ ] 页面文案：玩法一句话 + 操作说明 + 制作名单
- [ ] 无已知 P0 bug（卡死/无法开始/无法提交分数）
- [ ] 游戏可在他人机器/浏览器直接运行

## 交接
- 产出：游戏包 + itch.io 页面 URL + jam 提交状态 + 复盘要点（哪些可复用）。
