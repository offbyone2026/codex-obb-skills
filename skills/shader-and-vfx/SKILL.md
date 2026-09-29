---
name: shader-and-vfx
description: Use when writing shaders or visual effects — GLSL, Godot shader language, post-processing (bloom, god rays, depth of field, glitch), particles, instancing, or draw-call optimization. Triggered by shader, GLSL, 着色器, 特效, VFX, 后处理, bloom, 粒子, 流光. For OffByOne Studio's Godot 2D/3D and Three.js web experiments.
---

# 着色器与视觉特效（Shader & VFX）

## 适用
Godot 4（2D/3D）与 Three.js Web 项目的特效：后处理、粒子、程序化几何。

## 基础规范
1. **结构**：uniform 参数集中在顶部（颜色/强度/时间缩放），便于调参不重编；避免硬编码魔法数。
2. **时间**：统一用全局时间 uniform（`TIME`/u_time），特效节奏与游戏节奏解耦。
3. **性能**：
   - 全屏后处理 ≤ 3 个 pass（EffectComposer 按需挂载）。
   - 粒子用 GPU 粒子/Instancing（Godot GPUParticles3D、Three.js Points），避免逐粒子 CPU 更新。
   - 重复绘制合并：同材质同网格走 Instancing/BatchedMesh。

## 常见特效配方
- **Bloom/辉光**：下采样 + 高斯模糊 + 叠加；强度控制在 ≤ 0.8，避免糊。
- **God Rays（体积光）**：径向模糊 + 遮罩乘法，2D 用遮罩精灵模拟。
- **Depth of Field**：基于深度 buffer 的模糊；近景/远景分 pass。
- **Glitch**：行偏移 + RGB 分裂 + 噪声遮罩；只在关键帧触发。
- **像素风 2D 特效**：Godot CanvasItem shader + 色盘替换（palette swap）实现变身/受伤闪白。

## Godot 专项
- 2D 后处理：WorldEnvironment + CanvasLayer shader；像素完美需保持整数缩放。
- Shader 编辑器内 `--headless` 校验：`godot --headless --script` 跑 shader 编译检查。

## 检查清单
- [ ] uniform 参数集中、无魔法数
- [ ] 全屏后处理 pass ≤ 3
- [ ] 粒子走 GPU/Instancing
- [ ] 移动/低端机上关闭高开销特效（降级路径）
- [ ] 特效不遮挡游戏信息（可读性验收）

## 交接
- 产出：shader 文件/资源路径 + 参数表 + 性能测量（帧耗时）+ 降级方案。
