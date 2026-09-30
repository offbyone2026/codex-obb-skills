# Codex OBB Skill 库

本仓库收录 OffByOne Studio 多功能开发平台（Codex 改壳版）可用的 Skill（SKILL.md 技能包），聚焦 2D 独立游戏开发工作流、全栈工程、GTM 与学术研究等场景。客户端 obb_agent.py 依据主仓 manifest.json 自动拉取本仓库内容。

## 规模与分级（当前实际值）

- **技能总数：1153 条**（skills/ 目录 1145 个技能包 + 根目录参考文档技能 8 条）
- **core=true（自动安装）：904 条** —— 游戏开发、全栈/Web 工程、文档处理、工程方法论、GTM 等成熟技能，客户端默认部署
- **core=false（可选 skill 集）：249 条** —— 学术研究（243）、知识管理（6）等按需安装，可在「安装可选 skill 集」中拉取
- **自研技能包：18 个**（保留原有命名）；**外部收录：1127 条**（统一 `源标识-技能名` 前缀命名，如 `gamedev-godot-2d-movement`），与自研包无命名冲突

> 数量说明：外部技能均从公开源仓库真实 clone 并核对 `SKILL.md` 后收录，frontmatter 与完整内容原样保留，无虚构条目。

## 收录来源清单（12 个公开源 + 自研）

| 来源仓库 | 收录数 | 主要 domain |
|----------|-------:|-------------|
| [gooseworks-ai/goose-skills](https://github.com/gooseworks-ai/goose-skills) | 286 | go-to-market |
| [mindrally/skills](https://github.com/mindrally/skills) | 265 | web-development |
| [AlterLab-IEU/AlterLab-Academic-Skills](https://github.com/AlterLab-IEU/AlterLab-Academic-Skills) | 243 | academic-research（可选） |
| [gamedev-skills/awesome-gamedev-agent-skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills) | 75 | game-development |
| [donchitos/claude-code-game-studios](https://github.com/donchitos/claude-code-game-studios) | 74 | game-development |
| [Jeffallan/claude-skills](https://github.com/Jeffallan/claude-skills) | 67 | full-stack-development |
| [AlterLab-IEU/AlterLab_GameForge](https://github.com/AlterLab-IEU/AlterLab_GameForge) | 34 | game-development |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | 25 | engineering-practices |
| [anthropics/skills](https://github.com/anthropics/skills) | 20 | office-documents |
| [maystudios/claude-skills](https://github.com/maystudios/claude-skills) | 17 | game-development |
| [obra/superpowers](https://github.com/obra/superpowers) | 15 | engineering-methodology |
| [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | 6 | knowledge-management（可选） |
| OffByOne Studio 自研 | 18 包 + 8 根 md | game-development 等 |

## 自动发现机制（重要）

Codex 官方 **Agent Skills** 机制：每次会话自动把已安装技能的 name+description+path 注入上下文，任务与 description 匹配即**隐式自动调用**，无需用户指名。详见 [AUTO_SKILL_DISCOVERY.md](AUTO_SKILL_DISCOVERY.md)；常驻索引模板见 [AGENTS.md](AGENTS.md)（部署到 `~/.codex/AGENTS.md` 后每次会话必载，作为兜底索引）。

## 标准技能包（skills/ 目录，可直接部署 ~/.codex/skills/）

### 自研核心包（18 个）

| 技能包 | 触发场景 |
|--------|----------|
| [skills/video-generation/SKILL.md](skills/video-generation/SKILL.md) | 视频生成/宣传片（Sora MCP 官方 Sora 2 API） |
| [skills/game-asset-pipeline/SKILL.md](skills/game-asset-pipeline/SKILL.md) | 素材批量生成：sprite/3D/动画/音频/TTS（Ludo MCP） |
| [skills/pixel-art-design/SKILL.md](skills/pixel-art-design/SKILL.md) | 像素画规范与帧动画 |
| [skills/game-audio-design/SKILL.md](skills/game-audio-design/SKILL.md) | 音效/BGM/配音设计与生成 |
| [skills/game-localization/SKILL.md](skills/game-localization/SKILL.md) | 多语言本地化流程 |
| [skills/level-design/SKILL.md](skills/level-design/SKILL.md) | 关卡设计与难度曲线 |
| [skills/playtesting/SKILL.md](skills/playtesting/SKILL.md) | 测试/试玩/问题分级/反馈闭环 |
| [skills/performance-optimization/SKILL.md](skills/performance-optimization/SKILL.md) | 性能剖析与优化（Godot/Unity） |
| [skills/steam-release/SKILL.md](skills/steam-release/SKILL.md) | Steam 商店页/构建/上传/发布 |
| [skills/indie-project-planning/SKILL.md](skills/indie-project-planning/SKILL.md) | GDD/里程碑/任务拆解/风险登记 |
| [skills/combat-system-design/SKILL.md](skills/combat-system-design/SKILL.md) | 战斗系统：攻击图/命中检测/伤害管线/打击感/平衡 |
| [skills/multiplayer-networking/SKILL.md](skills/multiplayer-networking/SKILL.md) | 多人联机：权威服务器/同步/延迟补偿/反作弊 |
| [skills/godot-4-specialist/SKILL.md](skills/godot-4-specialist/SKILL.md) | Godot 4 专精（架构/信号/状态机/2D 像素/C#） |
| [skills/unity-ecs-specialist/SKILL.md](skills/unity-ecs-specialist/SKILL.md) | Unity ECS/DOTS 数据导向架构 |
| [skills/engine-selection/SKILL.md](skills/engine-selection/SKILL.md) | 引擎与技术栈选型决策树 |
| [skills/game-jam-workflow/SKILL.md](skills/game-jam-workflow/SKILL.md) | Game Jam 48-72h 冲刺流程与提交清单 |
| [skills/narrative-design/SKILL.md](skills/narrative-design/SKILL.md) | 叙事/剧情/对话/世界观设计 |
| [skills/shader-and-vfx/SKILL.md](skills/shader-and-vfx/SKILL.md) | 着色器与特效（GLSL/后处理/粒子/Instancing） |

### 外部收录包（1127 个）

以 `源标识-技能名` 命名，完整清单见 [skills.json](skills.json)（含 name/description/domain/source/core 字段）。按 domain 汇总：

| domain | 数量 | 分级 |
|--------|-----:|------|
| go-to-market | 286 | core |
| web-development | 265 | core |
| academic-research | 243 | optional |
| game-development | 200 | core |
| full-stack-development | 67 | core |
| engineering-practices | 25 | core |
| office-documents | 20 | core |
| engineering-methodology | 15 | core |
| knowledge-management | 6 | optional |

## 参考文档（根目录 md）

| 文件 | 内容 |
|------|------|
| [game-developer.md](game-developer.md) | 通用游戏开发技能（Unity/Unreal，性能优化/多人联网） |
| [godot-claude-skills.md](godot-claude-skills.md) | Godot 4.x 专项技能（GDScript/场景/着色器/实时工作流） |
| [game-studios.md](game-studios.md) | 全流程游戏工作室技能集（49 agents/73 skills） |
| [game-development-orchestrator.md](game-development-orchestrator.md) | 按平台/维度路由的游戏开发编排技能 |
| [skills-gamedev.md](skills-gamedev.md) | 26 项游戏开发工程技能（建模/构建/反作弊/版本控制） |
| [skills.json](skills.json) | 汇总清单（1153 条，含分级字段 core，供客户端自动部署） |

> 客户端部署：拉取 skills.json → 下载 `skills/<name>/SKILL.md` 到 `~/.codex/skills/<name>/` → 生成 AGENTS.md 索引 → 重启 Codex 生效。core=true 的技能自动安装；core=false 为可选 skill 集，按需安装。
