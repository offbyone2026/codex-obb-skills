---
name: video-generation
description: Use when generating or editing videos, game trailers, cinematics, promotional clips, or when the user mentions Sora, text-to-video, image-to-video, video remix, or needs a video from a script/storyboard. Covers Sora MCP workflows: prompt engineering, model/size/duration selection, job polling, and asset handoff.
---

# 视频生成（Sora MCP）

## 前置
- 确认 Sora MCP 已接入（`mcp_servers.sora`），`OPENAI_API_KEY` 已开通 Sora 权限。
- 先向用户确认用途（宣传片/过场/素材测试）与时长预算；长任务先出 5s 测试帧再上正式帧。

## 工作流
1. **拆脚本**：把用户脚本/文案拆成镜头序列（每镜头一个 prompt）。
2. **写 prompt（五要素）**：镜头类型 + 主体 + 动作 + 场景 + 光照/氛围。
   - 示例：`Wide tracking shot of a teal coupe driving through a desert highway, heat ripples visible, hard sun overhead.`
3. **选参数**：
   - model：sora-2（常规）/ sora-2-pro（高质量）
   - size：1920x1080（横）/ 1080x1920（竖）/ 1280x720 / 720x1280 / 1024x1024
   - seconds：5 / 10 / 15 / 20
4. **图生视频保一致**：用已有角色/场景图（imagegen 产出）作为首帧 → `create_video_with_image`。
5. **轮询**：`wait_for_video`（默认 10s 间隔，600s 超时）；失败先查 status 原因再重试，不要盲目重发。
6. **下载与归档**：`download_video` 存到 `DOWNLOAD_DIR`；缩略图/spritesheet 同步取。

## 内容红线
- 禁止版权角色/音乐、真实人物、18 岁以下不适内容；参考图禁含人脸。

## 交接
- 产出：视频文件路径 + 使用的 model/size/seconds + prompt 原文。
- 与 imagegen 协同：图片 → 图生视频；视频帧 → 回注素材管线。
