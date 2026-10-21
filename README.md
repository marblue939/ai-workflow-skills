# Game Dev Skills · 游戏开发/AI 协作工作流 skill 库

做游戏时反复用到的流程，被我写成了 skill。每个 skill 是一个 `SKILL.md`，描述**什么情况触发、按什么步骤做、怎么算完成**——能被 Claude Code、Codex、DSH 等支持该约定的 agent 直接加载，也可以当人工检查清单照着走。

来源是两款自研项目：Unity 6 + C# 的 3D 派对桌游（15 款小游戏、4 人联机、卡牌经济与数值、约 519 条自动化断言），以及 Godot 4.7 + GDScript 的 2D 肉鸽射击（6 关卡、2 场 BOSS、词条构筑与波次成长曲线）。

## 目录

| skill | 用途 |
|---|---|
| [unity-editor-verify](skills/unity-editor-verify/SKILL.md) | 用命令行跑 Unity 编辑器任务（场景重建 / 冒烟测试 / HUD 校验），并核验 PASS 证据，处理 License 抖动 |
| [ai-output-verify](skills/ai-output-verify/SKILL.md) | 验收 AI 生成的代码与文档：假完成、报告失真、跨模块回归三类失效的识别与门禁 |
| [gameplay-breakdown](skills/gameplay-breakdown/SKILL.md) | 写或审一份游戏品类/竞品拆解：报告骨架、证据要求与质量检查 |
| [codex-rules-verify](skills/codex-rules-verify/SKILL.md) | 把一版规则装进全局配置并验证它真的被加载（新旧会话都要验） |

## 安装

- **Claude Code**：把 `skills/<name>/` 放到项目的 `.claude/skills/`。
- **Codex / DSH 等**：把目录加入对应的 skills 搜索路径，或在会话里显式引用该文件。
- **不想装**：每个 `SKILL.md` 本身就是一份检查清单，直接照着做。

## 设计原则

1. **每个 skill 都要有验收口**：不写"尽量做好"，写"怎么算对"。
2. **只信证据**：日志时间戳、报告尾部统计、实际跑通的输出，而不是模型或脚本的自述。
3. **改动可回滚**：先跑基线，改完再跑全量；出问题能定位到具体模块。
4. **踩过的坑要留下来**：一次翻车 → 写进对应 SKILL.md 的"坑"，而不是记在脑子里。

## 许可

MIT，见 [LICENSE](LICENSE)。
