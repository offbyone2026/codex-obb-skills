---
name: engine-selection
description: Use when choosing a game engine or tech stack — platform, genre, architecture (full canvas vs hybrid DOM+guest), Web (Phaser/Pixi/Three/Babylon), Godot/Unity, or narrative runtimes (Ink/Twine). Triggered by 引擎选择, 技术选型, which engine, engine selection, 用什么引擎. Decision tree for OffByOne Studio's 2D indie + web experiments.
---

# 引擎与技术栈选型（Engine Selection）

## 决策起点（先问再选）
- 平台：Web / 移动 / PC / 主机 / VR？
- 核心循环：动作/物理、回合制、叙事分支、管理 UI、混合？
- 呈现方式：全屏 canvas、DOM/UI 并存、混合？
- 工具链：无构建（ESM 直跑）还是 bundler + 编辑器？
- 制作方式：纯代码，还是策划需要 Twine/Ink/Godot/Unity 编辑器？

## 决策树
```
游戏类型?
├── 偏 DOM/面板/表单/文本 UI（如经营模拟后台）
│   └── 加小游戏 → 混合壳：Phaser/Pixi 挂载在视图区
├── 全屏 2D 游戏
│   ├── 完整功能（场景/物理/输入）→ Phaser 4 或 Kaplay
│   └── 重渲染/自绘 → PixiJS 8 或裸 Canvas
├── 全屏 3D 游戏
│   ├── 完整引擎/物理/XR → Babylon.js
│   └── 渲染为主 → Three.js
├── 叙事分支（文字量大）→ Ink (inkjs) / Twine
└── 原生桌面/移动独立游戏
    ├── PC 独立/开源 → Godot 4（2D 首选）
    ├── 大团队/多平台 → Unity
    └── 极致画面 → Unreal 5
```

## 反模式
- 表单/UI 重的浏览器工具选 Unity/Godot → 应选 DOM/混合
- 用 Ink 跑实时多实体模拟 → 叙事工具只做分支
- 2D 像素游戏选 Unreal → 资源浪费

## 本工作室倾向
- 2D 像素独立游戏：Godot 4（已有 4.7.2 Mono + 4.4 双版本）。
- Web 实验/原型：Phaser 4（DOM 混合壳）或 PixiJS 8。
- 叙事向实验：Ink/Twine 导出到 Web。

## 交接
- 产出：选型结论表（引擎/理由/替代项/风险）+ 最小可运行原型路径。
