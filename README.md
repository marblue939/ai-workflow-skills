# Game Dev Skills · 游戏开发工作流 skill 库

做游戏时反复用到的流程，被写成了 skill。每个 skill 是一份 `SKILL.md`：说明**什么情况触发、按什么步骤做、怎么算完成**——能被 Claude Code、Codex、DSH 等支持该约定的 agent 直接加载，也可以当人工检查清单照做。

来源是两款自研项目：Unity 6 + C# 的 3D 派对桌游（15 款小游戏、4 人联机、卡牌经济与数值、约 519 条自动化断言、三端构建），以及 Godot 4.7 + GDScript 的 2D 肉鸽射击（6 关卡、2 场 BOSS、词条构筑与波次成长曲线）。

## 目录

| skill | 用途 |
|---|---|
| [unity-editor-verify](skills/unity-editor-verify/SKILL.md) | 命令行跑 Unity 编辑器任务（场景重建 / 冒烟 / HUD 校验）并核验 PASS 证据，处理 License 抖动 |
| [unity-commandline-playtest](skills/unity-commandline-playtest/SKILL.md) | 不打开界面直入小游戏/关卡跑一遍并截帧取证，识别空跑与假成功 |
| [unity-smoke-assertions](skills/unity-smoke-assertions/SKILL.md) | 维护自动化冒烟断言基线：写一条可回归的断言、判定全绿、失败归因 |
| [unity-build-matrix](skills/unity-build-matrix/SKILL.md) | PC / Android / 小程序多端构建与产物自检（防「构建成功但跑不起来」） |
| [spec-card-authoring](skills/spec-card-authoring/SKILL.md) | 写规格卡：总则铁律 + 逐条规格 + 演出双栏 + 边界与验收 |
| [bug-diagnosis-chain](skills/bug-diagnosis-chain/SKILL.md) | 实机反馈诊断：结论摘要表 + 逐环证据链（文件:行号）+ 修复计划 + 复验清单 |
| [visual-evidence-review](skills/visual-evidence-review/SKILL.md) | 截图取证与判读：同机位对比、提问方式、结论回写与误判防范 |
| [gameplay-breakdown](skills/gameplay-breakdown/SKILL.md) | 品类/竞品拆解骨架与质量检查（避免写成玩法介绍） |
| [ai-output-verify](skills/ai-output-verify/SKILL.md) | 验收 AI 产出：假完成、报告失真、跨模块回归三类失效与门禁 |
| [codex-rules-verify](skills/codex-rules-verify/SKILL.md) | 规则装载与验证：作用域、新会话实测、旧会话不生效的判断与回滚 |

## 安装

- **Claude Code**：把 `skills/<name>/` 放到项目的 `.claude/skills/`。
- **Codex / DSH 等**：把目录加入对应 skills 搜索路径，或在会话里显式引用该文件。
- **不想装**：每个 `SKILL.md` 本身就是检查清单，直接照着做。

## 设计原则

1. **每个 skill 都要有验收口**：不写「尽量做好」，写「怎么算对」。
2. **只信证据**：日志时间戳、报告尾部统计、实机画面，而不是模型或脚本的自述。
3. **改动可回滚**：先跑基线，改完再跑全量；出问题能定位到具体模块。
4. **踩过的坑要留下来**：一次翻车 → 写进对应 SKILL.md 的「坑」，而不是记在脑子里。

## 许可

MIT，见 [LICENSE](LICENSE)。