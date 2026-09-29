---
name: steam-release
description: Use when preparing or releasing a game on Steam — store page, build preparation, upload, depot, branches, achievements, pricing, or when the user mentions Steam, store page, release, publish, depot, launch, or Steamworks. Covers Steamworks pipeline for the OffByOne Studio Steam developer account.
---

# Steam 发行流程（Steamworks）

## 前置
- 用工作室 Steamworks 账号（收信邮箱 zxyteam1234@qq.com）登录；国内网络需加速器访问 Steam 商店/社区域名。

## 商店页
1. 资产准备：库位图(600x800)、宣传图(616x353)、页头图(460x215)、宣传短片(≤30s)（用 video-generation 技能生成）、截图(≥5 张 1280x720)；
2. 文案：短描述（≤140 字符）、详细描述（Markdown，含玩法/GIF/FAQ）、标签 5 个以内（贴合类目）;
3. 定价与货币：设美元基准价，区域建议按官方表；发布日前 2-4 周提交商店页审核。

## 构建与上传
1. SteamPipe 流程：`depotbuild` 生成 manifest → 构建上传对应 branch（默认 main）；
2. 打包规范：exe 入口、依赖 DLL 同目录、禁用路径空格依赖；上传前本机全量回归；
3. 分支管理：main(正式) / beta(测试) / dev；测试用 beta 分支 + 测试账号。

## 发布清单
- [ ] 商店页审核通过（构建 4-5 项齐全）
- [ ] 成就/云存档配置并本地验证
- [ ] 定价确认、折扣计划（如有）
- [ ] 选择发布日期（建议避开大作撞期）并预约
- [ ] 发布日当天：确认构建可下载、商店可见、首发公告

## 发布后
- 监控崩溃报告（Crash Reporting）与差评；第一周集中修 S 级问题；
- 更新流程：修复 → bump 版本 → 上传 depot → 发布到 main（Steam 无需 MSIX 流程）。

## 交接
- 产出：Steamworks 后台完成项清单 + 构建分支状态 + 商店页链接。
