# 荐股文体检 · a-share-fact-check

> **真数据，不一定是真逻辑。**
> 荐股文里每个数字都能查证，骗局藏在它们被拼起来的方式里。

一个 Claude Skill：把一篇荐股文，一键体检成——**哪些数字是真的、哪些查无此据、哪些是把真事实剪成假结论的"蒙太奇谎言"、哪些是把你导向匿名标的的付费漏斗。**

它不预测股票、不生成研报、不替你做判断。它只做一件事：**对着 A 股官方披露，审计一篇投资内容里的每一条断言，然后告诉你这篇文章该信几分。**

---

### 这是给谁的

**如果你会看公众号、雪球、小红书或群里转的荐股文**，心里犯嘀咕"这靠谱吗"，却没工具、没时间去核对里面的数字和故事——这个就是帮你把那篇文章拆开、看清楚的。

**如果你是研究员、金融学生、投顾合规、财经内容审核**——它是一个"信息进入决策之前"的核验层：在你相信一篇内容之前，先机械地过一遍它的事实、证据、推理结构和营销意图。

它不是交易工具，是**投资内容的信息完整性工具**。

---

### 为什么需要它：你真正的对手不是数据造假

跑了六篇真实荐股文测试后，一个反直觉的结论：**真·硬数据造假极少。** 荐股文的谎言几乎都不在单个数字里，而在数字被拼起来的方式里——

```
真实A  +  真实B  +  真实C   ──▶   虚假的D
```

每个事实单独查都是真的，把一个大模型直接叫来"核实一下"，它会一路返回"✅ 都是真的"，然后**完美错过真正的骗局**。这就是本 Skill 存在的理由：它把核验从"逐条查真假"上移到"查组合是否误导"。

---

### 四个它能、别的工具不能的事

**1. 真事实 ≠ 真结论（最大差异）**
ChatGPT 能帮你查一个数字。但几乎没有工具会检查**"这些真数字被组合起来，是否推出了一个它们支撑不了的结论"**。本 Skill 有一套专门的「蒙太奇谎言」分析层（幸存者偏差 / 虚假因果 / 指标混用 / 时间窗口操纵 / 主体替换 / 暴富个例→你也能六类），个案照样判真，但会为被拼出的那个结论**单独立一条断言判存疑**——警告直接进判定表，不藏在附注里。

**2. "查无此据"是一等公民**
荐股文里最毒的，是一个年报里**根本不存在**的数字（"在手订单30亿"）。生成类 AI 查不到就是不写，于是这个红旗被悄悄咽掉。本 Skill 把"官方披露里查不到"做成一个显式判定态（⚠️），专门抓这种编造。

**3. 识别匿名标的与付费导流漏斗**
很多荐股内容的商业模式是：**免费内容给你 90% 的确定感，把真正的"核心标的"藏起来，让你付费/进私域才拿到名字。** 隐藏不是缺陷，隐藏本身就是产品机制。本 Skill 会识别这种结构——凡是给你一堆诱人线索却全程不具名的推荐，可信度**直接封顶**，并点破整条转化漏斗。它也绝不替你猜标的（**推断 ≠ 核验**）。

**4. 不替你投资，只审计信息**
它永远不出"买/卖/值得"的结论。所有报告以"判断权在你、不构成投资建议"收尾。它的立场是：**把内容拆开给你看，你自己决定。**

---

### 实例：一篇荐股文进去，一份体检报告出来

下面两组 **Before（荐股文片段）/ After（体检报告片段）** 均为本 Skill 最新版真实跑出的结果，节选、已脱敏。它们覆盖两种最典型的场景：**最标准的事实核验**，和**真数据的假逻辑**。

---

#### 例① · 估值型荐股 —— 最标准的"事实核验"，也是"不乱判"的分寸感

**Before（荐股文片段）**
> 目前紫金的滚动市盈率（PE-TTM）跌到了 13.2 倍左右，**处于过去 5 年极低的 10% 分位点**。……市场目前的定价，已经提前消化了悲观预期，属于典型的**下行有底**。……这笔配置目前占我整体资产的 7% 左右……在绝对底部去捡便宜的血筹。

**After（体检报告片段）**
> **⚡ 速读**：★★★☆☆ · 可核荐股文 · 一句话：核心财务与行情数据大体属实，但"5 年 10% 分位"的极值表述偏激进——**数据准但叙事略激进**。
>
> | # | 原文断言 | 官方/行情数据 | 判定 |
> |---|---|---|---|
> | 1 | "PE-TTM 13.2 倍" | 推算约 13.0–13.3 | ✅ 一致（容差内） |
> | 2 | "过去 5 年极低的 10% 分位" | 搜索区间推算约 15–25% | ⚠️ **存疑（估算提示）**：偏激进但非不可能，需自算序列复核，**暂不定性为矛盾** |
>
> **为什么这条是 ⚠️ 不是 ❌**：方向完全对（确实在历史低位），只是数字偏紧。没有精确自算序列，就绝不把"我查到的和你不一样"升级成"官方证明你错"。**它能抓，但不乱抓。**

---

#### 例② · 产业故事型荐股 —— 30 条真事实，最后引向一个不具名的标的

**Before（荐股文片段）**
> 华为每次大动作，必有翻倍股诞生！2021 鸿蒙→某润和涨近 5 倍，2024 海思→某华强 17 天 16 板、**从 8 块涨到 48 块**……（随后是 Atlas 950 参数、大厂锁单、券商研报等约 30 条真实行业数据）……尤其有一家堪称"**核心中的核心**"：是华为超节点"神经网络"的关键供应商、业绩已实现 200% 以上增长、获 35 家机构密集调研……**机会就摆在这，你自己决定。**

**After（体检报告片段）**
> **⚡ 速读**：★★★★☆ · 混合体（A 主 B 辅）· 一句话：**可核部分属实 ≠ 全文可信。** 30 条周边事实是真的，但真正要推给你的那个标的——全文从头到尾没说过名字。
>
> **总评：⚠️ 部分存疑**（匿名标的封顶规则触发：核心推荐标的全程匿名，无论周边事实多精确，全局封顶 ⚠️）
>
> | # | 原文断言 | 核验 | 判定 |
> |---|---|---|---|
> | 4 | "某华强从 8 块涨到 48 块，17 天 16 板" | 实际最高 41.55 元，**48 元这个点位行情里查无此数** | ❌ **矛盾**（编造的具体点位；"翻倍"是修辞、48 元是可证伪的数字） |
> | ⑤-A | "华为每次大动作必有翻倍股"（配 5 案例） | 只举 5 个赢家、隐去大量未涨/下跌的同类 | ⚠️ **NE-1 幸存者偏差**（个案真≠规律成立） |
> | ⑤-C | 30 条真数据 → 匿名"核心供应商" | 真数据是包装、匿名标的才是产品 | ⚠️ **NE-5 真事实→匿名跃迁** |
>
> 报告能查到那条匿名线索**高度指向某连接器供应商**，但明确写：**"这不代表本报告推荐该标的，我们只核验线索真伪，判断权在你。"** ——指认出来、却不推荐，恰恰拆穿了"匿名钓鱼"的套路。

> 💡 **两个例子的对比**：例①是"抓得准且不乱抓"（真核验工具的分寸感），例②是"真数据里的假逻辑"（别的工具会一路判 ✅ 而错过的骗局）。此外，对于**通篇没有可核标的、纯人设+战绩+导流**的投顾获客广告，Skill 会在入口分诊时直接识别为"**这是广告，不是分析**"，拆解其转化漏斗而非逐条核验诱饵。

---

<p align="center">
  <img src="https://img.shields.io/badge/status-v1.0-blue" alt="status" />
  <img src="https://img.shields.io/badge/platform-Claude%20Skill-8A63D2" alt="platform" />
  <img src="https://img.shields.io/badge/market-A--share%20%7C%20HK%20%7C%20NEEQ-green" alt="market" />
  <img src="https://img.shields.io/badge/lang-中文-red" alt="lang" />
  <img src="https://img.shields.io/badge/license-MIT-lightgrey" alt="license" />
</p>

## Overview

**a-share-fact-check** (荐股文体检) is a Claude Skill that audits Chinese stock-pitch articles ("荐股文") against official disclosure — instead of generating stock research, it verifies the claims in content someone else already wrote.

Point it at a WeChat / Xueqiu / Xiaohongshu stock pitch and it returns a **"health-check report"**: which numbers are true, which are **not found in any official filing**, which are **montage lies** (true facts spliced into a false conclusion), and which are **funnels** routing you toward an anonymized ticker behind a paywall.

**It never tells you to buy or sell.** It audits the information; the judgment stays yours.

> Your real competitor isn't another GitHub repo — it's the base model itself. A retail user can paste the article straight into Claude and say "check this." This Skill's entire value is constraining the base model into a verification discipline it won't follow on its own: only trust official disclosure, flag fabricated figures, and never fabricate a source link.

### Why it's different

Most financial AI runs **company → research** (ticker in, report out: company-research-agent, FinRobot, AlphaAnalyst…). This Skill runs the opposite direction — **content → audit** (an existing article in, a verdict on it out). That's a category difference, not a feature difference.

Three moats, deepest first:
1. **Direction** — audit side vs. generation side.
2. **Source discipline** — verify only against official A-share disclosure & exchange market data; never against "web consensus."
3. **Montage-lie detection** — real hard data fabrication is rare; the lie is almost always in how true facts are assembled. Per-claim checking returns all-✅ and misses it. This is the most distinctive capability.

## How it works

```
Article
  → Triage (A: verifiable pitch | B: lead-gen ad | Hybrid: A-primary + B-module)
  → Claim extraction & typing
  → Normalization (5-tuple Claim Schema; colloquial → GAAP-term mapping)
  → Route to 7 playbooks
  → Three-state verification (✅ match / ❌ contradiction / ⚠️ not-found)  [structured-first]
  → Montage-layer scan (6 narrative-error types)
  → Two-tier report (retail quick-read + expert per-claim table)
```

Three shared foundations under `references/`:
- `normalization.md` — 5-tuple Claim Schema + closed colloquial→GAAP-term map + caliber/tolerance rules
- `evidence-rules.md` — source priority P1–P7 + conflict resolution + **anti-fabrication source-link rule**
- `narrative-errors.md` — the six montage / narrative-construction error types (NE-1 ~ NE-6)

## Repository structure

```
a-share-fact-check/
├── SKILL.md                       # Dispatch core: 3 iron laws + triage + 6-step flow + report templates
├── references/                    # 3 shared foundations (read these first)
│   ├── normalization.md
│   ├── evidence-rules.md
│   └── narrative-errors.md
├── playbooks/                     # 7 verification playbooks (unified 5-step contract)
│   ├── 01-financial-figures.md    ├── 05-policy-existence.md
│   ├── 02-equity-structure.md     ├── 06-red-flags.md
│   ├── 03-fundraising-capacity.md └── 07-valuation-market-data.md
│   └── 04-industry-position.md
├── sources/official-channels.md   # Data-source inventory + retrieval paths
└── tools/mcp.md                   # MCP combo (企查查 MCP + AKShare + source-routing doc)
```

## Installation & usage

1. Download `a-share-fact-check.skill` (or clone this repo).
2. Install the Skill in Claude (or drop the folder into your skills directory).
3. Paste a stock-pitch article / investment commentary into Claude and ask it to fact-check — the Skill triggers automatically.

> Optional: wiring up **AKShare** (self-computed valuation percentiles) and the **企查查 MCP** (corporate/equity data) raises precision. Without them, affected claims are honestly downgraded to "pending verification" — the Skill never fabricates data or source links.

## Status — v1.0

Core framework converged over **six rounds of real stock-pitch testing** (紫金 / 德源 / 华为 / 船长 / siRNA …): entry triage, seven claim types, three shared foundations, A/B dual output, montage-layer verification, anonymized-target credibility cap.

Items marked `TODO` (Error Taxonomy finalization, whether to split routing, red-flag/montage pattern-library expansion) are **deliberately locked pending a real-corpus survey** — not stacked from single-article guesses.

## Contributing

The single most useful contribution right now is **corpus**: typical stock pitches, investment-advisor ads, day-trader recaps — especially any article this framework mishandles. Open an issue with the text and (if you have it) the correct verdict. Real corpus is exactly what the next step (batch survey + benchmark) needs most.

---

*本工具仅就公开信息一致性进行核验，不构成任何投资建议。 This tool verifies public-information consistency only and does not constitute investment advice.*
