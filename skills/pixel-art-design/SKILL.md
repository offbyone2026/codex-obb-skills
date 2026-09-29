---
name: pixel-art-design
description: Use when creating pixel art assets, pixel-style graphics, sprite sheets, or when the user mentions pixel art, retro style, palettes, tilemaps, or frame-by-frame animation. Provides pixel art conventions: canvas sizes, palettes, outlines, shading, and sprite sheet frame rules.
---

# 像素画设计规范

## 画布与规格
- 常见画布：16/32/64/128（角色），128/256（场景/UI）；竖屏角色通常高约 1.5-2x 宽。
- 导出尺寸 = 像素尺寸整数倍（1x/2x/4x），避免插值模糊。

## 调色板
- 单场景限 8-16 色；先定主色/辅色/高光/阴影/描边 5 档。
- 描边：深色半透明描边提升辨识度；避免纯黑大范围使用。

## 结构与细节
- 明暗用**分层色块**而非渐变/模糊；光源方向全场一致。
- 细节从大到小：剪影 → 大色块 → 次要结构 → 高光点缀；禁止每像素堆噪点。

## 帧动画
- sprite sheet 帧：4 帧（待机循环）/ 6-8 帧（走路）/ 8-12 帧（攻击/施法）。
- 帧尺寸固定、锚点一致；导出时按引擎要求留 1px 边距或紧凑排布。
- 动画曲线：待机用呼吸/飘带微动；攻击前摇-命中-收招三段。

## 引擎接入
- Godot：`AnimatedSprite2D` + SpriteFrames；缩放取整。
- Unity：`Sprite Editor` 切帧 + `Animator`。

## 交接
- 产出：png 文件 + 帧布局说明（行×列、帧率、锚点）。
