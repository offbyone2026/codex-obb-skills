---
name: playtesting
description: Use when testing or playtesting a game, gathering feedback, triaging bugs, running internal playtests, or when the user mentions testing, playtest, QA, bugs, feedback, or internal test. Covers test session setup, observation, issue triage, and feedback loop into development.
---

# 游戏测试与反馈闭环

## 测试准备
1. 明确测试目标（新关卡/新机制/性能/平衡）；
2. 准备测试版本：可执行 + 版本号 + 已知问题清单；
3. 定义数据采集：日志（错误/事件）、录屏、问卷。

## 测试会话
- 引导语：不提示答案，观察自然行为；记录时间戳+操作+情绪；
- 观察重点：卡住点、误解点、挫败点、爽快点；
- 每场 20-40 分钟，样本 3-5 人即可暴露主要问题（小型团队够用）。

## 问题分级与分类
| 级别 | 定义 | 处理 |
|------|------|------|
| S | 阻塞主线/崩溃/存档丢失 | 立即修复 |
| A | 严重体验问题/频繁死循环 | 本轮迭代修复 |
| B | 体验瑕疵/文案错误 | 排期修复 |
| C | 风格建议/优化项 | 记录备选 |

- 分类维度：崩溃 / 逻辑 / 平衡 / 可用性 / 美术 / 音频 / 性能 / 文案。

## 反馈闭环
1. 测试后 24h 内出报告：Top 问题 + 建议改动（附证据时间戳）；
2. 改动一次只验证一个变量，复测确认修复且无回归；
3. 保留测试版本归档，便于回归对比。

## 交接
- 产出：测试报告（版本号、样本、问题分级清单、建议优先级）+ 复测结果。
