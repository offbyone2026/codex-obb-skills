# Skill 自动发现与主动调用机制（官方 Agent Skills）

## 一句话结论

你记忆里那个“发消息时一定会附带过去的官方功能”叫 **Agent Skills（Codex Skills）**。
官方文档：https://developers.openai.com/codex/skills

它的核心机制就是：**Codex 每次会话开始时，把已安装技能的名称（name）、描述（description）和路径（path）自动注入上下文**，形成一个“可用技能初始列表”；当用户任务与某个技能的 description 匹配时，Codex 会**自动（隐式）选择并调用**该技能——完全不需要用户指名。这就是“不指定也会主动去找并调用”的官方实现。

## 机制细节（官方行为）

| 项目 | 说明 |
|------|------|
| 触发方式 1 | **隐式调用**：任务与技能 description 匹配时自动触发（默认即开启） |
| 触发方式 2 | **显式调用**：输入 `$技能名` 或 `/skills` 选择 |
| 上下文预算 | 初始技能列表上限约 **2% 上下文窗口，或 8000 字符**；技能过多时先截短 description，再多会省略并告警 |
| 渐进披露 | 只注入 name+description+path，**命中后才加载完整 SKILL.md**（不占常驻上下文） |
| 必填字段 | SKILL.md 的 YAML frontmatter 必须含 `name` 和 `description` |
| 技能结构 | 目录 + SKILL.md（可选 scripts/、references/、assets/、agents/openai.yaml） |

## 部署路径（按优先级）

| 作用域 | 路径 | 说明 |
|--------|------|------|
| 用户级（推荐） | `~/.codex/skills/<name>/SKILL.md` | 对本机所有项目生效，客户端自动拉取部署的目标位置 |
| 项目级 | `<repo>/.agents/skills/<name>/`（含上级目录至仓库根） | 跟随仓库分发 |
| 管理员级 | `/etc/codex/skills/<name>/` | 整机默认 |
| 系统级 | Codex 内置（`~/.codex/skills/.system/`） | 官方自带：imagegen、skill-creator、skill-installer 等 |

> 本机现状核对：`C:\Users\zl\.codex\skills\.system\` 下已有官方内置 `imagegen`（这就是现有“图片生成工具”）、`skill-creator`、`skill-installer` 等，说明改壳版已启用官方 Agent Skills 机制，直接复用即可。

## 如何保证“即使不指定也一定被找到”（三步）

1. **标准包格式**：每个技能写成 `skills/<name>/SKILL.md`，frontmatter 写清 `name` + `description`，正文是完整工作流指令。仓库内技能包已按此格式编写。
2. **description 就是触发信号**：写成 “Use when …” 条件句，触发关键词前置、范围边界明确。因为初始列表可能被截短，**描述前 40 字内必须包含最高频触发词**。
3. **AGENTS.md 常驻索引兜底**：Codex 每次会话都会读取 AGENTS.md（与任务无关、恒定加载）。把“已安装技能总表（名称 + 何时用）”写进用户级 `~/.codex/AGENTS.md`（模板见本仓 `AGENTS.md`），即使某条 description 匹配失败，Agent 也能从常驻索引里看到并主动去翻对应技能。

> ⚠️ 大库注意：本仓库技能总量已达 1153 条，全部注入会超出 8000 字符预算被截短/省略。因此**默认只自动安装 core=true 的 904 条**；core=false 的 249 条作为可选 skill 集按需安装。客户端部署时按 core 字段过滤，避免初始列表过载。

## 客户端 obb_agent.py 集成建议

```python
# 伪代码：拉取 skills 仓 -> 部署为 Codex 标准技能包
# 1. 拉取 https://raw.githubusercontent.com/offbyone2026/codex-obb-skills/main/skills.json
# 2. 对每条 skill：下载 skills/<name>/SKILL.md 及 scripts/references/assets
#    写入 C:\Users\<user>\.codex\skills\<name>\
# 3. 生成/更新用户级技能索引：
#    把 skills.json 的 name+trigger 渲染为 C:\Users\<user>\.codex\AGENTS.md 的“可用技能”章节
#    （只渲染 core=true 条目；core=false 在“安装可选 skill 集”时再部署）
# 4. 重启 Codex（技能变更需重启会话生效）
```

注意：
- 同名技能不合并，两个都会出现在选择器里——命名避免与官方内置冲突；
- 外部收录技能统一使用 `源标识-技能名` 前缀命名，避免跨源重名；
- 更新后重启 Codex 才生效。

## 本仓库技能包一览

### 自研核心包（18 个，core=true）

| 技能 | 触发场景（description 要点） |
|------|------------------------------|
| video-generation | 生成/编辑视频、宣传片、Sora |
| game-asset-pipeline | 素材批量生成：sprite/3D/动画/音频/TTS |
| pixel-art-design | 像素画规范：尺寸/调色板/帧动画 |
| game-audio-design | 音效/BGM/配音设计与生成 |
| game-localization | 多语言本地化与文案适配 |
| level-design | 关卡设计/难度曲线/流程 |
| playtesting | 测试/试玩/反馈闭环 |
| performance-optimization | 性能剖析与优化 |
| steam-release | Steam 商店页/构建/上传/发布 |
| indie-project-planning | 项目规划/GDD/里程碑 |
| combat-system-design | 战斗系统：攻击图/命中检测/伤害管线/打击感/平衡 |
| multiplayer-networking | 多人联机：权威服务器/同步/延迟补偿/反作弊 |
| godot-4-specialist | Godot 4 专精：架构/信号/状态机/2D 像素/C# |
| unity-ecs-specialist | Unity ECS/DOTS 数据导向架构 |
| engine-selection | 引擎与技术栈选型决策树 |
| game-jam-workflow | Game Jam 48-72h 冲刺流程与提交清单 |
| narrative-design | 叙事/剧情/对话/世界观设计 |
| shader-and-vfx | 着色器与特效（GLSL/后处理/粒子/Instancing） |

### 外部收录包（1127 个，core 分级见 skills.json）

- **core=true 自动安装（878 条）**：go-to-market(286)、web-development(265)、game-development(200)、full-stack-development(67)、engineering-practices(25)、office-documents(20)、engineering-methodology(15)
- **core=false 可选 skill 集（249 条）**：academic-research(243)、knowledge-management(6)

完整清单与每条 name/description/domain/source 见 [skills.json](skills.json)。
