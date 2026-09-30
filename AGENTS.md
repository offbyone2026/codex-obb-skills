# AGENTS.md —— 用户级技能索引（部署到 ~/.codex/AGENTS.md 或项目根）

本文件每次会话恒定加载，作为“可用技能总表”，配合 Agent Skills 的初始列表注入，确保 Agent 在用户不指名时也能主动发现并调用合适技能。

## 可用技能总表

以下技能已安装为本机 Codex 技能包（~/.codex/skills/），任务命中时**必须主动选择并调用**对应技能，无需用户指名：

| 技能名 | 何时使用（触发词） |
|--------|--------------------|
| video-generation | 生成视频、视频剪辑、宣传片、Sora、图生视频、remix |
| game-asset-pipeline | 素材生成、精灵图、3D模型、动画、音效、配音、TTS、UI素材 |
| pixel-art-design | 像素画、像素风、spritesheet、调色板、帧动画 |
| game-audio-design | 音效、BGM、背景音乐、配音、音频设计、声音风格 |
| game-localization | 本地化、翻译、多语言、文案适配、i18n |
| level-design | 关卡设计、关卡流程、难度曲线、地图布局 |
| playtesting | 测试、试玩、反馈、bug 收集、内测 |
| performance-optimization | 性能优化、卡顿、帧率、剖析、profiling、内存 |
| steam-release | Steam、商店页、构建、上传、发行、成就、更新 |
| indie-project-planning | 项目规划、GDD、里程碑、需求拆分、排期 |
| combat-system-design | 战斗、伤害、命中、hitbox、打击感、连招、平衡、combat |
| multiplayer-networking | 联机、多人、netcode、同步、匹配、matchmaking、延迟补偿、反作弊 |
| godot-4-specialist | Godot、GDScript、场景架构、信号、状态机、tilemap、像素渲染、Mono、C# |
| unity-ecs-specialist | Unity、ECS、DOTS、Burst、JobSystem、数据导向、批量实体 |
| engine-selection | 引擎选择、技术选型、which engine、用什么引擎 |
| game-jam-workflow | Game Jam、游戏开发挑战赛、48小时、72小时、jam、冲刺、itch |
| narrative-design | 剧情、叙事、对话、世界观、角色设定、narrative、story、dialogue |
| shader-and-vfx | shader、GLSL、着色器、特效、VFX、后处理、bloom、粒子、流光 |

## 引擎/工具路由（MCP）

| 需求 | 工具 |
|------|------|
| Godot 场景/脚本/项目 | Godot MCP（端口 9080） |
| Unity 编辑器 | Unity MCP |
| Unreal 蓝图/材质/粒子 | Unreal MCP（TCP 55557） |
| Blender 建模/贴图/渲染 | Blender MCP（socket 9876） |
| Steam 数据/发行 | Steam MCP（端口 11020） |
| 视频生成（文本/图像/remix） | Sora MCP |
| 素材全栈（sprite/3D/动画/音频/TTS） | Ludo MCP |

## 工作约定

1. 新任务先看“可用技能总表”，命中即加载对应 SKILL.md 执行；
2. 多个技能同时命中时，按“素材 -> 制作 -> 测试 -> 发布”流程顺序编排；
3. 需要引擎操作时按上表路由对应 MCP，不手写底层命令。
