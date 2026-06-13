# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

世界杯赛事分析工作台 — 使用三个独立足球预测仓库作为方法论框架，通过三分析师团队（MonteCarlo / ScoutTactical / StatsMarkets）生成结构化比赛分析报告，经过交叉辩论后输出最终共识预测。

## Repository Layout

```
worldcup-analysis/
├── 2026-world-cup-predictor/       # Elo + Monte Carlo + ML集成预测框架 (Python)
├── ScoutFootball_for_World_Cup/    # 球员评分 + 战术匹配 + Poisson/Dixon-Coles (Python)
├── Football-2026/                  # 泊松模型 + 博彩市场信号 + 凯利公式 (Chrome扩展/JS)
├── reports/                        # 📁 所有分析报告（按比赛分文件夹）
│   ├── templates/                  # 报告模板
│   ├── <TeamA>_vs_<TeamB>/         # 每场比赛一个文件夹
│   │   ├── montecarlo_report.md    # 分析师一号独立报告
│   │   ├── scouttactical_report.md # 分析师二号独立报告
│   │   ├── statsmarkets_report.md  # 分析师三号独立报告
│   │   └── <TeamA>_vs_<TeamB>_WorldCup2026_Analysis.md  # 最终共识合成报告
│   └── ...
├── ANALYSIS_CHECKLIST.md
├── CLAUDE.md
└── datafix_corrected_elo.md
```

## 三大分析工具方法论

### 1. 2026-world-cup-predictor (Analyst-MonteCarlo)
- **核心**: `src/models/team_scoring.py` — Elo锚点(35%) + 年龄结构 + 大赛经验 + 近期状态 + 教练 + 玄学因子的多因子修正
- **模拟**: `src/simulation/monte_carlo.py` — Bradley-Terry淘汰赛模型; Poisson xG (`lambda = 1.3 + (elo-1700)/500`) 用于小组赛
- **阵容**: `src/models/player_scoring.py` — 4年周期球员评分, 首发/替补深度指数
- **数据**: `data/elo_cache_2026.json` (52队Elo), `data/wc2026_players_processed.json` (913球员)
- **已知限制**: 土耳其有"未进决赛0.65x惩罚"; 阵容数据仅覆盖28/48队
- **关键文件**: `config.py` (权重配置), `scripts/report.py` (CLI报告), `src/dashboard/mobile_ui.py` (看板)

### 2. ScoutFootball_for_World_Cup (Analyst-ScoutTactical)
- **核心**: `src/scoutfootball/models/match_prediction.py` — Independent Poisson + Dixon-Coles 比分预测
- **球员评分**: 8位置细化(ST/W/AM/CM/DM/FB/CB/GK), 5维度百分位评估
- **战术板**: `frontend/` — 电子战术白板, 支持阵型预设、动画导出
- **世界杯**: `src/scoutfootball/worldcup/data.py` — 48队1104球员真实阵容
- **数据管道**: `scoutfootball ingest → build-features → train` (uv + DuckDB + Parquet)
- **关键文件**: `docs/ALGORITHM.md` (740行中文算法详解), `docs/MODEL_CARD.md`, `AGENTS.md`

### 3. Football-2026 (Analyst-StatsMarkets)
- **核心**: `js/quant-engine.js` — Poisson进球模型 + 去水概率(deMargin) + 凯利公式 + 赔率异动检测
- **数据源**: 球探网(titan007.com) DOM注入采集欧赔/亚盘/大小球/角球
- **AI集成**: `js/ai-client.js` — OpenAI/Claude/自定义 快速+深度预测模式
- **联网搜索**: `js/web-search.js` — Tavily→DuckDuckGo→Bing降级链路, 4维度情报检索
- **报告生成**: `js/report.js` — 16节结构化Markdown报告
- **注意**: 这是Chrome MV3扩展, 不可直接命令行运行; 分析时手动应用其量化模型公式

---

## 强制数据验证规则

以下规则是生成任何分析报告的强制前提条件，必须在**任何分析工作开始之前**完成。

### 规则 1: Elo 数据必须从数据文件读取

必须在 `2026-world-cup-predictor/data/elo_cache_2026.json` 中查询比赛双方的 Elo 值。禁止从记忆中估算 Elo。记录精确到一位小数的值并注明文件路径。

```
# 正确做法:
读取 data/elo_cache_2026.json -> 找到 Team_A: 1654.8, Team_B: 1640.0
```

### 规则 2: 所有提及的球员必须通过 squad JSON 验证

在报告中写入任何球员名字之前，必须在球队阵容 JSON 文件中通过 grep 确认其存在。ScoutFootball 阵容数据位于 `ScoutFootball_for_World_Cup/src/scoutfootball/worldcup/data.py` 或相关的 JSON 文件。对于 `wc2026_players_processed.json` 中覆盖的球队，也必须交叉检查。

```
# 正确做法:
grep -i "player_name" ScoutFootball_for_World_Cup/src/scoutfootball/worldcup/data.py
# 确认球员存在于阵容中，否则删除引用
```

### 规则 3: 实际运行模型代码，避免人工估算

只要可能，应实际运行模型代码生成数值，而非手动估算：
- Elo 修正: 运行 `_compute_modified_elo()` 来自 `src/models/team_scoring.py`
- Poisson xG: 使用公式 `lambda = 1.3 + (modified_elo - 1700) / 500`
- 球员评分: 从 squad JSON 中读取实际评分，而非凭空创造

如果无法运行代码，必须在报告中记录原因并说明使用了替代方法。

### 规则 4: 实时新闻和赔率必须附带来源

所有新闻和赔率引用必须附带具体来源名称和 URL（如 Bet365, Pinnacle, 预赛发布会报道）。禁止使用"多家媒体"或"FIFA历史统计"等无来源的笼统表述。

### 规则 5: 三名分析师必须独立生成报告

必须通过 TeamCreate 创建三分析师团队，每位分析师**独立**生成报告。禁止在同一会话中模拟多个分析师视角。每位分析师报告必须以独立文件保存。

---

## 分析前检查清单

`ANALYSIS_CHECKLIST.md` 是本项目的强制检查清单文件，涵盖以下维度：

| 检查阶段 | 覆盖范围 | 优先级 |
|---------|---------|:------:|
| PRE-FLIGHT | Elo 读取, 阵容验证, 新闻搜索, 赔率采集, 交锋记录 | P0 (必做) |
| Monte Carlo | Poisson lambda, P(k;λ) 表, 比分矩阵, 三模型对比, 深度分析, 敏感性分析 | P0 (必做) |
| ScoutTactical | 球员存在性验证, ASCII 阵型, 关键对位表, 三条比赛路径, Poisson 预测 | P0 (必做) |
| StatsMarkets | lambda 计算, xG 校准, deMargin, Kelly, 情绪分析, 赔率异动 | P0 (必做) |
| 交叉验证 | 独立报告保存, 概率三元组标准化, 共识度量化, 投资评级 | P0 (必做) |

在开始新比赛分析前，打开 `ANALYSIS_CHECKLIST.md` 并逐项确认。每位分析师在提交报告时，必须在报告末尾附上已完成的检查清单签收表。

---

## 生成分析报告的标准流程

### 0. 数据验证 (任何分析之前)

在开始任何分析之前，必须完成以下数据验证：

- [ ] 从 `data/elo_cache_2026.json` 读取双方 Elo 值，写入 `PRE-FLIGHT` 检查清单
- [ ] 从 ScoutFootball squad JSON / `wc2026_players_processed.json` 读取双方阵容数据
- [ ] grep 确认所有将要在报告中提及的球员存在于 squad JSON 中
- [ ] 记录实际博彩赔率（来源、时间戳、具体赔率值）
- [ ] 搜索并记录实时新闻（伤病、阵容、热身赛结果）
- [ ] 参考 `ANALYSIS_CHECKLIST.md` 完成所有 PRE-FLIGHT 检查项

### 1. 搜索实时新闻
在生成分析前, 必须搜索以下维度的最新信息:
- 双方伤病/阵容更新 (赛前发布会确认)
- 近期热身赛结果和表现
- 博彩赔率数据 (1X2, 亚盘, 大小球)
- 交锋历史和球队近况对比

### 2. 创建三分析师团队并启动分析

```
Step 2a: TeamCreate(team_name="worldcup-analysis")
Step 2b: 创建3个任务分别分配给 Analyst-MonteCarlo, Analyst-ScoutTactical, Analyst-StatsMarkets
         它们的 blockedBy 为空（可并行执行）
Step 2c: 第4个任务(最终合成)用 addBlockedBy 指向前3个任务
Step 2d: 每位分析师收到的指令必须包含:
         - 比赛基本信息（对阵、时间、场地、小组）
         - 从 elo_cache_2026.json 读取的 Elo 值（精确到一位小数）
         - 从 squad JSON 提取的关键球员评分（Top 5 per team）
         - 实时新闻摘要（伤病、阵容、热身赛结果）
         - 实时博彩赔率（1X2, 亚盘, 大小球）
         - 方法论指导（指明其仓库中的关键文件和公式）
         - 标准化输出格式要求: 概率三元组 {TeamA_win%, Draw%, TeamB_win%}
Step 2e: 等待前三名分析师完成任务，获取他们的独立报告
```

每位分析师完成后必须：
1. 将独立报告保存到 `reports/<TeamA>_vs_<TeamB>/<analyst>_report.md`（如 `reports/Canada_vs_Bosnia/montecarlo_report.md`）
2. 输出标准化的概率三元组 `{TeamA_win%, Draw%, TeamB_win%}`
3. 在报告末尾附上 `ANALYSIS_CHECKLIST.md` 的签收表

### 3. 交叉辩论与合成报告格式
三位分析师完成后，进入合成阶段。合成报告必须遵循以下 7 部分结构（以 `Canada_vs_Bosnia_WorldCup2026_Analysis.md` 为参考）:
1. **赛事背景与实时新闻摘要** — 新闻表格(影响评级/来源方向) + 双方近况对比表
2. **分析师一号: Monte Carlo报告** — Elo调整表→深度指数→Poisson xG→比分TOP10→MC模拟→多模型对比→市场分析→敏感性分析→结论
3. **分析师二号: 球探战术报告** — 阵型博弈(含ASCII图)→关键对位(5+组评分表)→战术X因素→三条比赛路径→Poisson预测→结论
4. **分析师三号: 统计市场报告** — Poisson模型(完整比分矩阵)→历史基准评分→去水概率+凯利价值→赔率异动→情绪分析→冷门风险→结论
5. **三方交叉辩论** — 3个核心分歧的三方立场(用ASCII框), 交叉验证共识表(含共识度%)
6. **最终共识预测** — 加权概率表(权重: 一号35%/二号35%/三号30%)→比分排名→ASCII预测框→时间线→投资建议(⭐评级)→组内展望→三大决定因素
7. **附录** — 工具方法说明 + 新闻来源 + 免责声明

### 4. 分析师权重分配
| 分析师 | 权重 | 理由 |
|--------|:--:|------|
| MonteCarlo | 35% | 量化模型最全面, Elo+Poisson+MC三重验证 |
| ScoutTactical | 35% | 战术洞察最深, 球员级对位+路径分析 |
| StatsMarkets | 30% | 市场信号最准确, 去水概率+凯利+情绪量化 |

### 5. 输出文件
- 每位分析师的独立报告: `reports/<TeamA>_vs_<TeamB>/<analyst>_report.md`
- 最终合成报告: `reports/<TeamA>_vs_<TeamB>/<TeamA>_vs_<TeamB>_WorldCup2026_Analysis.md`

## 投资价值建议评级体系

| 评级 | 条件 |
|:--:|------|
| ⭐⭐⭐ 强烈推荐 | 三方100%共识 + 优势值 >5% |
| ⭐⭐ 推荐 | 两方共识 + 优势值 >2% |
| ⭐ 参考 | 单方信号, 需独立判断 |
| ❌ 回避 | 深度负EV或三方一致否定 |

---

## 质量标准基准

每位分析师的报告在细节深度和量化严格性上必须达到或超过以下基准报告的水平：

| 分析师 | 基准报告 | 关键指标 |
|--------|---------|---------|
| Analyst-MonteCarlo | `reports/<Match>/montecarlo_report.md` | 16 节完整结构, 含 Elo 基础/因子修正/伤病影响/球员评分/Poisson xG/比分分布/三模型对比/深度分析/敏感性分析/结论 |
| Analyst-ScoutTactical | `reports/<Match>/scouttactical_report.md` | 6 组量化关键对位表, ASCII 阵型图, 三条路径分析(含触发条件/分阶段时间线/概率), 量化 X 因素分析, set-piece 身高对比表 |
| Analyst-StatsMarkets | `reports/<Match>/statsmarkets_report.md` | lambda 攻防交叉计算, xG 校准, 完整 16+ 行比分矩阵, deMargin 过程展示, Kelly 仓位计算, 情绪-历史相关性(128 场数据), 赔率异动分析 |

### 最低容忍标准

| 维度 | 不可接受的做法 | 正确做法 |
|------|--------------|---------|
| Elo 数据 | 从记忆估算, 或未引用 elo_cache_2026.json | 从 JSON 文件读取并记录精确值 |
| Poisson lambda | 仅给出最终 lambda 值, 无计算过程 | 展示公式 + 代入值 + 结果 |
| 三模型对比 | 仅展示单一模型输出 | Poisson xG / Simple Elo / Bradley-Terry 三表对比 + 市场/外部参考 |
| 球员引用 | 引用不存在于 squad JSON 的球员 | 用 grep 验证后再引用,或删除 |
| 赔率引用 | "博彩公司赔率 1.85" 无来源 | "Bet365 2026-06-13 12:00 UTC, 土耳其 1.78" |
| 投资建议 | 仅定性"推荐" | 展示 Kelly 分数 + 预期值计算 + 仓位比例 |
| 概率输出 | 粗粒度范围 ("~30%") | 精确到小数点的百分比三元组 |

## 团队管理

- 团队配置文件: `~/.claude/teams/worldcup-analysis/config.json`
- 任务列表: `~/.claude/tasks/worldcup-analysis/`
- 分析师通过 `SendMessage` 通信, 报告写入项目目录
- 换比赛时: 更新 config.json 的 description, 发送新指令给现有分析师
- 清理团队: `TeamDelete` (需先 shutdown 所有成员)
