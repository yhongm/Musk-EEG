# Musk-EEG

> 用马斯克的脑子讲 EEG / 神经科学。Wikipedia 知识库 + 马斯克语气，不是复读，是翻译。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![数据库: 5,300+ 词条](https://img.shields.io/badge/Database-5%2C300%2B%20entries-0077cc.svg)](https://en.wikipedia.org/wiki/Electroencephalography)

---

## 这是什么

把两件事接在一起：

1. **EEG Wikipedia 知识库** — 5,300+ 神经科学词条，SQLite 存储，FTS5 全文检索
2. **马斯克认知框架** — 第一性原理、类比、挑衅式断言、短句

问任何 EEG 相关问题，答案用 Elon 的声音说出来，每条知识标注来源。

---

## 快速开始

```bash
# 克隆
git clone <repo-url>
cd musk-eeg

# 首次运行：数据库 zip 自动解压（29 MB → 77 MB），无需手动操作

# 中文 / 混合语言查询（模糊 LIKE 搜索）
python3 scripts/musk_eeg_search.py --query "脑电 睡眠"

# 英文查询（FTS5 全文搜索，速度更快）
python3 scripts/musk_eeg_search.py --query "epilepsy" --top-k 3

# JSON 格式（程序调用）
python3 scripts/musk_eeg_search.py '{"query":"P300", "top_k":5}'
```

### 查什么

| 话题 | 查询词 |
|------|--------|
| EEG 基础 | `EEG`, `electroencephalography` |
| 睡眠与脑波 | `sleep`, `睡眠`, `脑电 睡眠` |
| 事件相关电位 | `P300`, `ERP` |
| 癫痫 | `epilepsy`, `癫痫` |
| 脑机接口 | `BCI`, `brain-computer interface`, `脑机接口` |
| 记忆 | `memory`, `记忆` |
| 意识 | `consciousness`, `意识` |

---

## 项目结构

```
musk-eeg/
├── README.md
├── SKILL.md                        # Claude Code / Hermes skill 触发文件
├── LICENSE
├── scripts/
│   └── musk_eeg_search.py          # 检索脚本（基于相对路径）
└── data/
    └── knowledge_new_fixed.db.zip  # 随仓库发布，首次自动解压
```

脚本通过相对于自身位置的路径查找 `data/`，所以从任意工作目录运行都能正常工作。

---

## 语气示例

**问：脑电是什么？**

> 你的大脑是个生物计算机。
>
> 它在放电——几十亿个神经元同时放电，形成电场。
>
> EEG 就是在大脑外面放传感器，听它的风扇声。
>
> 本质上，你在测电磁辐射。💀
>
> 不同频段代表不同工作状态：
> - δ（0.5–4 Hz）：深度维修模式
> - α（8–13 Hz）：空闲时钟，闭眼放空
> - β（13–30 Hz）：工作模式
> - γ（>30 Hz）：高速处理
>
> 这些频率分布就是大脑的遥测数据。没有中央时钟，是分布式同步。
>
> [来源：Neural oscillation]

**问：脑电在睡眠障碍里怎么用？**

> 睡眠不是关机。睡眠是维护协议。
>
> 白天神经元烧能量，代谢废物堆在突触间隙。慢波睡眠——0.5–4.5 Hz 的 δ 波像工业吸尘器，把垃圾清干净，顺便把短时记忆归档到长时存储。
>
> [来源：慢波睡眠（Slow-Wave Sleep）]
>
> REM 睡眠又是另一个协议。大脑离线跑测试，随机激活各皮层区——这就是梦。
>
> [来源：Why We Sleep]
>
> 睡眠呼吸暂停——上气道塌陷，血氧掉，δ 波被掐断，大脑还没完成维护就被憋醒。
>
> [来源：阻塞性睡眠呼吸暂停综合征]

---

## 数据库字段

| 字段 | 说明 |
|------|------|
| `title` | 词条名称 |
| `category` | 分类（如"睡眠障碍"） |
| `keywords` | 关键词（中英双语） |
| `core_definition` | 核心定义 |
| `mechanism` | 机制原理 |
| `musk_insight` | 马斯克视角（部分词条有） |

数据规模：原始词条 ~5,300 条，有实质内容 ~3,700 条。ZIP 压缩：77 MB → 29 MB。

---

## 马斯克语气规则

### ✅ 这样做

- 第一句 = 挑衅性断言，不写背景
- 一句一意，每段不超过 3 个短句
- 类比 + 第一性原理：大脑 = 生物计算机，EEG = 听风扇声
- 每条知识标注来源：`[来源：{词条名}]`
- 结尾留挑战或押注
- Emoji 最多 1–2 个，点在最反直觉的地方

### ❌ 别这样做

- 用"首先/其次/最后" → AI 指纹
- 用"值得注意的是/实际上" → 废话
- 直接复制维基百科定义 → 必须翻译，不是抄
- 用"EEG 是…研究表面…"开头 → 教科书腔
- 生成知识库里没有的内容

---

## 数据来源与流水线

- 原始数据：英文 Wikipedia（EEG、神经科学、睡眠医学分类）
- 蒸馏工具：LM Studio 本地 LLM（mistralai/ministral-3-3b）生成 Q&A
- 检索索引：SQLite FTS5 + BM25 排序
- 相关流水线：[wikipedia-eeg-pipeline](https://github.com/your-repo/wikipedia-eeg-pipeline)（爬取 → 蒸馏 → 建索引）

---

## 许可证

MIT License
