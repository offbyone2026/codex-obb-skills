---
name: game-localization
description: Use when localizing or translating a game, preparing multi-language text, adapting UI copy for locale, managing i18n keys, or when the user mentions localization, translation, languages, i18n, or locale support. Covers text pipeline, string keys, locale files, and culture-sensitive adaptation.
---

# 游戏本地化流程

## 文本管线
1. **提取**：所有玩家可见字符串抽离为 key-value（禁止硬编码）；key 语义化：`ui.btn.start` / `dlg.npc.greet` / `item.potion.name`。
2. **占位与复数**：统一用 ICU MessageFormat 或引擎原生占位（`{0}`、`{name}`）；复数用 ICU plural 而非拼接。
3. **翻译批次**：先核心 UI（按钮/菜单/教程）→ 剧情 → 物品/成就；每批交返审校。

## Locale 文件
- Godot：`ProjectSettings -> Localization`，CSV 或 .po；`tr()` 引用。
- Unity：`Localization` 包 + Locale Table（.csv 导入）；字体 Fallback 处理 CJK。
- 文件名规范：`<lang>.json`（en/zh-Hans/ja/ko 等），仓库内 `locales/` 目录。

## 文化适配
- 数字/日期/货币用 locale 格式；竖排、换行宽度按语言复核 UI 布局；
- 敏感词/符号按目标地区过滤（左到右/右到左、禁忌色、手势图等）；
- 人名/专有名词保留原文+音译对照表。

## 质检清单
- 字符串未翻译率 = 0；占位符数量一致；截断检查（日文最易溢出）；编码 UTF-8。

## 交接
- 产出：locale 文件路径 + 覆盖率统计 + 待审校清单。
