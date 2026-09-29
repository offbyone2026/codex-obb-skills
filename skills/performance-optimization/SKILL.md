---
name: performance-optimization
description: Use when optimizing game performance, fixing lag, low frame rate, memory issues, loading times, or when the user mentions performance, FPS, lag, stutter, profiling, frame time, or optimization. Covers profiling-first workflow and engine-specific optimization checklists (Godot/Unity).
---

# 性能优化

## 铁律：先剖析，后优化
1. 用 Profiler 定位瓶颈（CPU/GPU/内存/IO 分开看），禁止盲改；
2. 记录基线（场景、设备、帧率、帧耗时 P95、内存峰值）再动手；
3. 一次只改一个变量，改完复测对比基线。

## Godot 4.x
- 场景树：隐藏远离视锥的节点（`set_visible(false)` + 暂停处理）；复用池化敌人/子弹；
- 渲染：检查 V-Sync/降采样/阴影（DirectionalShadow 距离）；2D 用 LightOccluder2D 控制光照范围；纹理开 Mipmaps + 压缩（VRAM）；
- 脚本：热路径避免每帧分配（GetNode 缓存）、信号优于轮询；`Physics` 层减少碰撞种类；`Engine.time_scale` 慎用；
- 内存：资源本地化到场景（Local to Scene）避免跨场景保留；纹理按需加载。

## Unity
- Profiler + Frame Debugger 定位；Canvas 合并/图集（Sprite Atlas）、禁用多余 Raycast；
- 渲染：SRP Batcher/GPU Instancing、LOD、遮挡剔除（Occlusion Culling）、阴影距离裁剪；
- 脚本：避免每帧 `Find*`/`GetComponent`、对象池（ObjectPool）、Job System + Burst 处理密集计算；
- 内存：Addressables 按需加载、贴图压缩格式按平台（ASTC/BC）、清泄漏（Leak Detection）。

## 通用清单
- 三角面/绘制调用预算（移动端：DC<100-200；桌面：DC<1000）；
- 音频/物理/导航每帧开销；GC 分配率（热路径 0 分配）；
- 加载时间：分场景加载、异步加载、启动只加载必选资源。

## 交接
- 产出：基线-改动-结果对比表 + 剩余瓶颈清单。
