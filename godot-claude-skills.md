# Skill: Godot Claude Skills（Godot 4.x 专项）

来源：alexmeckes/godot-claude-skills

Godot 4.x 游戏开发技能包，提供可复用的知识与工作流，与 godot-mcp 配合使用（技能提供最佳实践，MCP 提供场景/脚本/着色器读写与实时编辑器控制）。

## 包含技能

| 技能 | 说明 |
|------|------|
| godot-code-gen | GDScript 最佳实践：类型提示、信号、状态机、async/await、tweens |
| godot-live-edit | 基于 AI Bridge 插件的轻量实时编辑器引导 |
| godot-interactive | godot-mcp + AI Bridge 的持续 inspect/edit/run/debug 工作流 |
| godot-scene-design | 场景文件（.tscn）、节点层级、关卡布局设计 |
| godot-shader | 2D/3D 特效与后处理着色器编写 |

## 使用方式

- 处理 Godot 项目时自动加载对应技能
- 编辑器联动场景：godot-interactive（完整工作流）或 godot-live-edit（轻量引导）
- 写 GDScript/场景/着色器时加载对应专项技能

## 安装

```bash
/plugin marketplace add alexmeckes/godot-claude-skills
/plugin install godot-claude-skills
```
