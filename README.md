# worldcup-analysis

世界杯赛事分析工作台 — 使用三个独立足球预测仓库作为方法论框架，通过三分析师团队（MonteCarlo / ScoutTactical / StatsMarkets）生成结构化比赛分析报告，并在交叉辩论后产出最终共识预测。

## 概览

本仓库包含三套互补的分析方法：

- `2026-world-cup-predictor`：基于 Elo、Poisson 与 Monte Carlo 的量化预测与模拟。
- `ScoutFootball_for_World_Cup`：球探/战术层面的球员评分与对位分析，包含阵型与路径推演工具。
- `Football-2026`：以博彩市场与赔率为核心的统计/量化引擎（去水、凯利、赔率异动检测）。

仓库目标是将三位分析师的独立结论整合为可复现、带来源与检验步骤的比赛报告，供策略决策和投资参考。

## 仓库结构（简要）

- `2026-world-cup-predictor/` — Elo 与 Monte Carlo 模型代码、模拟脚本与数据。
- `ScoutFootball_for_World_Cup/` — 球探模型、阵容数据与前端战术白板工具。
- `Football-2026/` — 浏览器扩展与量化引擎脚本（JS）。
- `reports/` — 各场比赛的三位分析师独立报告与最终合成报告。
- `ANALYSIS_CHECKLIST.md` — 分析前的强制检查清单（Elo 校验、阵容验证、赔率来源等）。

详细布局请参阅仓库内各子目录的 `README.md` 与 `CLAUDE.md`（方法论与操作规范）。

## 快速开始

先确保系统已安装 Python 3.8+ 与 Node.js（若需运行前端/扩展相关脚本）。

1. 克隆仓库：

```bash
git clone https://github.com/1561040647/worldcup-analysis.git
cd worldcup-analysis
```

2. Python 环境（示例）：

```bash
python -m venv .venv
source .venv/bin/activate   # Windows PowerShell: .\.venv\Scripts\Activate.ps1
pip install -r 2026-world-cup-predictor/requirements.txt
```

3. 运行 Monte Carlo 模拟（示例）：

```bash
cd 2026-world-cup-predictor
python scripts/report.py --match "TeamA vs TeamB"
```

（每个子项目有各自的运行说明，详见子目录下的 `README.md`。）

## 报告生成流程要点

- 在任何分析之前，必须从 `2026-world-cup-predictor/data/elo_cache_2026.json` 读取 Elo 值并记录来源。
- 所有在报告中引用的球员必须在 `wc2026_players_processed.json` 或相应 squad JSON 中验证存在。
- 实际运行模型生成数值（禁止凭经验手动估算），并在报告中附上数据来源与方法调用说明。

这些细则与模板已收录在 `CLAUDE.md` 与 `ANALYSIS_CHECKLIST.md`，请务必遵守。

## 贡献

欢迎贡献：提交 issue、PR 或者在 `reports/` 下添加新的分析报告。贡献前请先阅读 `CLAUDE.md` 中的数据验证与报告保存规范。

## 许可证

请在提交前确认各子项目的许可证（部分子模块可能有单独 LICENSE 文件）。

---

如果你希望我根据某个子项目补充更详细的使用示例或把 README 翻译为英文，我可以继续完善。
