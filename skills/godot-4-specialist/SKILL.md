---
name: godot-4-specialist
description: Use when writing Godot 4 code or scenes — GDScript patterns, scene architecture, signals, state machines, 2D pixel rendering, tilemaps, physics, or C#/.NET. Triggered by Godot, GDScript, 场景架构, 信号, 状态机, tilemap, 像素渲染, 物理. Deep patterns for OffByOne Studio's Godot 4.7.2 Mono (C#) and 4.4 projects.
---

# Godot 4 专精（GDScript/C# 工程模式）

## 适用
本机 Godot 4.7.2 Mono（C# 项目）与 4.4 共存；2D 为主（像素风）。

## 架构模式
1. **场景即模块**：一个场景 = 一个可复用模块；节点树层级 3-5 层，避免过深。资源用 .tscn 手写规范（indent/属性）。
2. **信号（Signal）驱动**：子节点只发信号，父节点订阅；避免 get_parent() 链式耦合。
3. **状态机**：玩家/敌人用 FSM（Idle/Run/Attack/Hurt/Dead），状态切换走信号或直接引用；复杂行为用 StateChart（Godot 4 官方插件）或自写状态表。
4. **类型安全**：GDScript 全程类型注解（`var hp: int`、`-> void`）；C# 项目用强类型 + 依赖注入（Autoload 服务）。
5. **Autoload 服务**：GameState / SaveSystem / AudioManager / NetworkManager 作为单例服务；避免把业务逻辑塞进节点脚本。

## 2D 像素渲染
- 像素完美：纹理 filter=Nearest、viewport 缩放整数倍、Camera 位置取整（防像素抖动）。
- TileMap：TileSet 组织物理/遮挡/自动 tile；大关卡用 TileMapLayer 分层。

## 物理与碰撞
- 用 Physics Layers 管理碰撞矩阵（玩家/敌人/地形/触发器），避免逻辑层混用。
- KinematicBody2D/CharacterBody2D 手动移动前先 `move_and_slide` 前保存状态，命中检测用 Area2D 触发器。

## C# 注意（本机 Mono 版本）
- 4.7.2 Mono 用 C#：`dotnet` 构建；场景内 C# 脚本命名空间与类名一致。
- 热重载有限，改 C# 需停止运行；批量逻辑优先 GDScript 原型，稳定后转 C#。

## 检查清单
- [ ] 无 get_parent() 链（信号替代）
- [ ] 场景文件手写规范通过（`godot --headless --editor --quit` 校验无错误）
- [ ] 像素渲染四项（filter/camera/缩放/取整）达标
- [ ] Autoload 顺序正确（无循环依赖）
- [ ] 物理层矩阵与实际检测一致

## 交接
- 产出：场景/脚本改动文件列表 + 校验输出 + 未决问题。
