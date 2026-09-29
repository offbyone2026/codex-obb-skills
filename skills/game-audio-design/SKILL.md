---
name: game-audio-design
description: Use when designing or generating game audio — sound effects, background music (BGM), character voice lines, ambient sound, or when the user mentions audio, music, SFX, voices, TTS, or sound style. Covers audio asset specs, batch generation via Ludo MCP, and engine integration (Godot/Unity).
---

# 游戏音频设计

## 音频资产规格
| 类型 | 格式 | 时长 | 采样率 |
|------|------|------|--------|
| UI 音效 | wav/ogg | 0.1-0.5s | 44.1kHz 16bit |
| 动作/战斗音效 | wav/ogg | 0.3-1.5s | 44.1kHz 16bit |
| 环境音 loop | ogg | 5-30s（无缝循环） | 44.1kHz |
| BGM 分段 | ogg/mp3 | 每段 15-60s（状态切换用） | 48kHz |
| 角色语音 | ogg/mp3 | 按台词 | 44.1kHz |

## 风格定调
- 先定音色关键词：暖/冷、明亮/低沉、有机/电子、卡通/写实。
- UI 音效统一“家族”：同风格音色、同响度（-18 ~ -12 LUFS）。
- 战斗音效分层：命中(短促)+受击(低频)+反馈(音调上行)。

## 生成工作流（Ludo MCP）
1. 每类音效用独立 prompt：`[类型] [情绪] [音色参考] [时长]`；
2. BGM 先生成主旋律变体 2-3 版，选一版再做分段；
3. TTS 配音：角色-台词-语气参数批量；先出 1-2 句样音确认再全量；
4. 生成后统一响度标准化（可交给引擎音频总线处理）。

## 引擎接入
- Godot：AudioStreamPlayer / AudioStreamPlayer2D（空间）；BGM 用 Bus 分组，UI/战斗各分 Bus 便于调平衡。
- Unity：AudioMixer + Snapshot 切换（战斗/探索）；AudioSource 3D 衰减。

## 交接
- 产出：音频文件清单 + 用途标注（UI/战斗/环境/BGM/语音）+ 建议 Bus 分组。
