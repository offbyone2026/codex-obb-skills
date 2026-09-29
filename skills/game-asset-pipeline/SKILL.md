---
name: game-asset-pipeline
description: Use when generating game assets in batch — sprites, icons, UI elements, textures, 2D-to-3D models, skeletal animations, sprite-sheet animations, short videos, sound effects, BGM, character voices, or TTS. Routes through Ludo MCP; coordinates with imagegen (images), Sora MCP (video), Blender MCP (detailed 3D).
---

# 游戏资产生成管线（Ludo MCP）

## 前置
- 确认 Ludo MCP 已接入且 `LUDO_API_KEY` 有效；**批量任务先查余额/额度**再开工。
- 明确资产清单与规格（类型、数量、风格、尺寸、帧数、时长）。

## 工作流
1. **拆清单**：把需求拆成可并行的生成任务（每任务独立 prompt）。
2. **逐类生成**：
   - 图片类：精灵/图标/背景/UI/贴图 → 图片生成接口；
   - 3D：2D 概念图 → 图转 GLB（含 PBR）→ 自动绑定 → 预设动画重定向；
   - 动画：静态精灵 → spritesheet（4-64 帧）/ 关键帧动画；
   - 视频：截图/视频 → 短视频（5-15s，可配乐）→ 2x 超分；
   - 音频：SFX/BGM 批量、角色配音、TTS。
3. **异步管理**：提交任务 → 轮询/长轮询 → 结果落盘；失败任务重试一次，仍失败换参数。
4. **质检与整理**：按 `Assets/<分类>/` 归档；命名规范 `类型_场景_编号`。

## 与其他工具分工
| 需求 | 工具 |
|------|------|
| 概念图/贴图 | imagegen skill |
| 3D 建模/雕刻细节 | Blender MCP |
| 宣传视频 | Sora MCP（video-generation 技能） |
| 其余素材 | 本技能（Ludo） |

## 交接
- 产出：资产文件路径清单 + 生成参数（模型/尺寸/帧数/seed）。
