[English](README.md) | [中文](README.zh.md)

# fireworks-tech-graph

> 不用手画图了。用中文描述你的系统，几秒钟得到可直接发布的 SVG + PNG 技术图。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://claude.ai/code)
[![7 种视觉风格](https://img.shields.io/badge/风格-7种-purple)]()
[![14 种图类型](https://img.shields.io/badge/图类型-14种-green)]()
[![UML 支持](https://img.shields.io/badge/UML-完整支持-orange)]()

## 概述

`fireworks-tech-graph` 将自然语言描述转化为精美的 SVG 技术图，并通过 `rsvg-convert` 导出高分辨率 PNG。内置 **7 种视觉风格**，深度覆盖 AI/Agent 领域常见图类型（RAG、Agentic Search、Mem0、Multi-Agent、Tool Call 流程等），并完整支持全部 14 种 UML 图类型。

```
用户: "画一张 Mem0 的架构图，暗黑风格"
  → Skill 识别：Memory Architecture Diagram，Style 2
  → 生成含泳道、圆柱体、语义箭头的 SVG
  → 导出 1920px PNG
  → 输出路径：mem0-architecture.svg / mem0-architecture.png
```

---

## 效果展示

> 所有示例图均以 1920px 宽度（2× 视网膜分辨率）通过 `rsvg-convert` 导出为 **PNG 格式**。技术图应选 PNG（无损），JPG 有损压缩会在文字和线条边缘产生噪点。

### 风格 1 — 扁平图标风（默认）
*Mem0 记忆架构图 — 白底，语义箭头，分层记忆系统*
![风格 1 — 扁平图标风](assets/samples/sample-style1-flat.png)

### 风格 2 — 暗黑极客风
*Tool Call 流程图 — 暗色背景、霓虹强调色、等宽字体*
![风格 2 — 暗黑极客风](assets/samples/sample-style2-dark.png)

### 风格 3 — 工程蓝图风
*微服务架构图 — 深蓝背景、网格、青色描边*
![风格 3 — 工程蓝图风](assets/samples/sample-style3-blueprint.png)

### 风格 4 — Notion 极简风
*Agent 记忆类型图 — 极简白底、单一强调色*
![风格 4 — Notion 极简风](assets/samples/sample-style4-notion.png)

### 风格 5 — 玻璃态卡片风
*多 Agent 协作图 — 深色渐变背景、磨砂玻璃卡片*
![风格 5 — 玻璃态卡片风](assets/samples/sample-style5-glass.png)

### 风格 6 — Claude 官方风格
*系统架构图 — 暖米色背景（#f8f6f3）、Anthropic 品牌色、专业克制美学*
![风格 6 — Claude 官方风格](assets/samples/sample-style6-claude.png)

### 风格 7 — OpenAI 官方风格
*API 集成流程图 — 纯白背景、OpenAI 品牌配色、现代极简设计*
![风格 7 — OpenAI 官方风格](assets/samples/sample-style7-openai.png)

---

## 稳定提示词模板

当你希望模型尽量贴近仓库里已经回归验证过的高质量示例时，可以直接使用这些 prompt：

### 风格 1 — 扁平图标风
```text
画一张 Mem0 memory architecture diagram，使用 style 1（Flat Icon）。
分四个横向层：Input Layer、Memory Manager、Storage Layer、Output / Retrieval。
包含 User、AI App / Agent、LLM、mem0 Client、Memory Manager、Vector Store、Graph DB、Key-Value Store、History Store、Context Builder、Ranked Results、Personalized Response。
箭头要区分 read / write / control / data flow，整体适合产品文档展示。
```

### 风格 2 — 暗黑极客风
```text
画一张 tool call flow diagram，使用 style 2（Dark Terminal）。
展示 User query、Retrieve chunks、Generate answer、Knowledge base、Agent、Terminal、Source documents、Grounded answer。
要有 terminal chrome、霓虹强调色、等宽字体，以及 retrieval / synthesis / embedding update 三类语义箭头。
```

### 风格 3 — 工程蓝图风
```text
画一张 microservices architecture diagram，使用 style 3（Blueprint）。
做成工程分区标题：01 // EDGE、02 // APPLICATION SERVICES、03 // DATA + EVENT INFRA、04 // OBSERVABILITY。
包含 Client Apps、API Gateway、Auth / Policy、三个 service、Event Router、Postgres、Redis Cache、Warehouse、Metrics / Traces。
使用 blueprint grid、青色描边，以及右下角 title block。
```

### 风格 4 — Notion 极简风
```text
画一张 agent memory types diagram，使用 style 4（Notion Clean）。
围绕一个 central Agent core，对比 Sensory Memory、Working Memory、Episodic Memory、Semantic Memory、Procedural Memory。
整体用极简白底、浅边框、单一强调色箭头，并给每种 memory 标出简短存储标签。
```

### 风格 5 — 玻璃态卡片风
```text
画一张 multi-agent collaboration diagram，使用 style 5（Glassmorphism）。
分三个区块：Mission Control、Specialist Agents、Synthesis。
包含 User brief、Coordinator Agent、Research Agent、Coding Agent、Review Agent、Shared Memory、Synthesis Engine、Final response。
使用 frosted glass 卡片、轻微 glow，以及 delegation、shared memory write、synthesis output 三类语义箭头。
```

### 风格 6 — Claude 官方风格
```text
画一张 system architecture diagram，使用 style 6（Claude Official）。
左侧有层标签：Interface Layer、Core Layer、Foundation Layer。
包含 Client Surface、Gateway、Task Planner、Model Runtime、Policy Guardrails、Memory Store、Tool Runtime、Observability、Registry。
整体要用暖米色背景、克制的品牌感配色、大量留白，以及右下角 legend。
```

### 风格 7 — OpenAI 官方风格
```text
画一张 API integration flow diagram，使用 style 7（OpenAI Official）。
分三个区块：Entry、Model + Tools、Delivery。
包含 Application、OpenAI SDK Layer、Prompt Builder、Model Runtime、Tool Calls、Response Formatter、Observability、Release Control。
整体要极简、白底、精确、现代，箭头强调 OpenAI 风格的绿色点缀。
```

---

## 特性

- **7 种视觉风格** — 从文档友好的白底，到暗黑霓虹，再到玻璃态和品牌官方风格
- **可执行风格系统** — style guide 不只存在于 markdown，生成器会真正消费这些规则
- **14 种图类型** — 全 UML 支持（Class、Component、Deployment、Package、Composite Structure、Object、Use Case、Activity、State Machine、Sequence、Communication、Timing、Interaction Overview、ER Diagram）以及 AI/Agent 领域常见图
- **AI/Agent 场景内建** — RAG、Agentic Search、Mem0、Multi-Agent、Tool Call 等模式开箱即用
- **语义形状库** — LLM 用双边框框、Agent 用六边形、Vector Store 用带内圈圆柱
- **语义箭头系统** — 颜色 + 虚线样式表达读写 / 控制 / 异步 / 回路
- **产品图标** — 40+ 产品内建品牌色：OpenAI、Anthropic、Pinecone、Weaviate、Kafka、PostgreSQL…
- **泳道/分层布局** — 复杂架构图可自动加 layer label
- **SVG + PNG 输出** — SVG 便于编辑，PNG 适合文档嵌入
- **rsvg-convert 兼容** — 纯内联 SVG，不依赖外部字体，渲染稳定

---

## 安装

```bash
npx skills add yizhiyanhua-ai/fireworks-tech-graph
```

这个 skill 通过 GitHub 仓库安装；npm 页面是公开的包/分发页：

```text
https://www.npmjs.com/package/@yizhiyanhua-ai/fireworks-tech-graph
```

不要把 npm 包名直接传给 `skills add`，因为 CLI 会把安装源解析成 GitHub/local path。

## 更新

```bash
npx skills add yizhiyanhua-ai/fireworks-tech-graph --force -g -y
```

重新执行 `add --force` 即可拉取最新版本。

或者直接 clone：

```bash
git clone https://github.com/yizhiyanhua-ai/fireworks-tech-graph.git ~/.claude/skills/fireworks-tech-graph
```

---

## 依赖

```bash
# macOS
brew install librsvg

# Ubuntu/Debian
sudo apt install librsvg2-bin

# 验证
rsvg-convert --version
```

---

## 为什么不用 Mermaid 或 draw.io？

| | Mermaid | draw.io | **fireworks-tech-graph** |
|--|---------|---------|--------------------------|
| 自然语言输入 | ✗ | ✗ | ✅ |
| AI/Agent 模式内建 | ✗ | ✗ | ✅ |
| 多种视觉风格 | ✗ | 手工调 | ✅ 7 种内建 |
| 高分辨率 PNG 导出 | ✗ | 手工导出 | ✅ 自动 1920px |
| 语义箭头颜色 | ✗ | 手工配 | ✅ 自动 |
| 不依赖在线工具 | ✅ | ✗ | ✅ |

Mermaid 适合在 markdown 里快速内嵌图。draw.io 适合手工精修。`fireworks-tech-graph` 的目标是：**你只需要描述系统，就能立刻拿到一张完成度很高的图**，不用写 DSL，也不用手点 GUI。

---

## 使用方式

### 触发词

遇到这些表达时会自动触发：

```
generate diagram / draw diagram / create chart / visualize
architecture diagram / flowchart / sequence diagram / data flow
```

### 基础用法

```
画一张 RAG pipeline flowchart
```

```
生成一个 Agentic Search 的架构图
```

### 指定风格

```
画一张微服务架构图，style 2（暗黑极客风）
```

```
画一张多 Agent 协作图 --style glassmorphism
```

### 指定输出路径

当前这个本地项目默认输出目录：`/Users/bytedance/Downloads/`

```
生成 Mem0 架构图，输出到 /Users/bytedance/Downloads/
```

```
画一张 Tool Call 流程图 --output /Users/bytedance/Downloads/
```

---

## 场景示例集

### AI/Agent 系统

```
比较 Agentic RAG vs standard RAG，做成 feature matrix，Notion clean style
```
→ 对比矩阵：检索策略、agent loop、tool use 等维度并排呈现

```
画一个 Mem0 memory architecture，包含 vector store、graph DB、KV store、memory manager
```
→ Memory Architecture，按 Input → Manager → Storage tiers → Retrieval 分层

```
画一个 Multi-Agent 图：Orchestrator 分发给 3 个 SubAgent（search / compute / code execution），结果汇总
```
→ Agent Architecture，六边形 Agent 组件 + 工具层 + 汇总层

```
可视化 Tool Call 执行流程：LLM → Tool Selector → Execution → Parser → back to LLM
```
→ 带循环箭头的流程图，强调 tool invocation cycle

```
画 5 种 agent memory：Sensory、Working、Episodic、Semantic、Procedural
```
→ 可做成心智图或分层架构图，展示不同记忆层

### 基础设施 / 云架构

```
画一个微服务架构：Client → API Gateway → [User Service / Order Service / Payment Service] → PostgreSQL + Redis
```
→ 横向分层架构图，服务集群可放在同一泳道

```
生成一张数据流水线图：Kafka → Spark processing → write to S3 → Athena query
```
→ Data Flow 图，箭头标注 stream / batch / query 等数据类型

```
画一个 Kubernetes deployment：Ingress → Service → [Pod × 3] → ConfigMap + PersistentVolume
```
→ 带 namespace 容器边框的架构图，箭头表示流量方向

### API / 时序类

```
画一个 OAuth2 authorization code flow 的 sequence diagram：User → Client → Auth Server → Resource Server
```
→ 标准时序图，纵向 lifeline + 横向 message

```
画 ChatGPT Plugin 的调用时序图
```
→ Sequence: User → ChatGPT → Plugin Manifest → API → Response chain

### 决策 / 流程类

```
画一个 AI app pre-launch QA flowchart：Code Review → Security Scan → Performance Test → Manual Approval → Deploy
```
→ 带 decision diamond 和并行分支的流程图

```
生成 feature comparison matrix：RAG vs Fine-tuning vs Prompt Engineering
```
→ 对比矩阵，按 cost / latency / accuracy / flexibility 等维度比较

### 概念图 / 技术地图

```
可视化 LLM application tech stack：从 foundation model 到 SDK 到 app framework 到 deployment
```
→ 分层架构图或心智图，展示技术栈层次

```
画一个 AI Agent capability map：Perception / Memory / Reasoning / Action / Learning
```
→ 以 AI Agent 为中心的 radial concept map

---

## 风格

| # | 名称 | 背景 | 字体 | 适用场景 |
|---|------|------|------|----------|
| 1 | **扁平图标风** *(默认)* | `#ffffff` | Helvetica | 博客、幻灯片、文档 |
| 2 | **暗黑极客风** | `#0f0f1a` | SF Mono / Fira Code | GitHub README、技术文章 |
| 3 | **工程蓝图风** | `#0a1628` | Courier New | 架构文档、工程方案 |
| 4 | **Notion 极简风** | `#ffffff` | system-ui | Notion、Confluence、Wiki |
| 5 | **玻璃态卡片风** | 深色渐变 | Inter | 官网、演示、Keynote |
| 6 | **Claude 官方风格** | 暖米色 `#f8f6f3` | system-ui | Anthropic / Claude 风格图 |
| 7 | **OpenAI 官方风格** | 纯白 `#ffffff` | system-ui | OpenAI 风格图 |

每种 style 在 `references/` 中都有对应参考文档，里面包含精确颜色、SVG 模式和版式规则。
生成器也会消费 `containers`、语义 `nodes[].kind`、`arrows[].flow`、端口锚点等结构字段，以提高复现样例级布局的稳定性。

一些高杠杆的字段：
- `style_overrides`：在不 fork 整个风格的前提下微调 title 对齐或 palette token
- `containers[].header_prefix` / `containers[].header_text`：工程蓝图风编号式标题，如 `01 // EDGE`
- `containers[].side_label`：Claude 风格左侧 layer label
- `window_controls`, `meta_left`, `meta_center`, `meta_right`：终端 / 文档 chrome
- `blueprint_title_block`：style 3 右下角工程 title block

### 风格选择建议

**做 UML 图时：**
- **Class / Component / Package**：优先 Style 1（扁平图标风）或 Style 4（Notion 极简风）—— 结构清晰、易读
- **Sequence / Timing**：优先 Style 2（暗黑极客风）—— 等宽字体更适合对齐
- **State Machine / Activity**：优先 Style 3（工程蓝图风）—— 更像工程图纸
- **Use Case / Interview**：优先 Style 1（扁平图标风）—— 更亲和

**做 AI/Agent 图时：**
- **RAG / Agentic Search**：优先 Style 2（暗黑极客风）或 Style 5（玻璃态卡片风）—— 技术感强
- **Memory Architecture**：优先 Style 3（工程蓝图风）—— 更适合分层记忆系统
- **Multi-Agent**：优先 Style 5（玻璃态卡片风）—— 卡片感适合区分 Agent 边界

**做文档配图时：**
- **内部文档**：优先 Style 4（Notion 极简风）—— 极简、适合 wiki
- **博客配图**：优先 Style 1（扁平图标风）—— 更有视觉吸引力
- **GitHub README**：优先 Style 2（暗黑极客风）—— 更贴近深色主题
- **演示材料**：优先 Style 5（玻璃态卡片风）或 Style 6（Claude 官方风格）—— 更 polished

**品牌风格场景：**
- **Anthropic / Claude 项目**：Style 6（Claude 官方风格）—— 暖米色背景、Anthropic 感知强
- **OpenAI 项目**：Style 7（OpenAI 官方风格）—— 纯白、简洁、品牌感强

---

## 图类型

| 类型 | 描述 | 核心布局规则 |
|------|------|--------------|
| **Architecture** | 服务、组件、云基础设施 | 横向分层，自上而下 |
| **Data Flow** | 数据如何流动 | 每条箭头都标注数据类型 |
| **Flowchart** | 决策、流程步骤 | 菱形表示 decision，整体上到下 |
| **Agent Architecture** | LLM + tools + memory | 5 层模型：Input / Agent / Memory / Tool / Output |
| **Memory Architecture** | Mem0 / MemGPT 风格 | 区分 read path 和 write path，分层存储 |
| **Sequence** | API 调用链、时间顺序 | 竖向 lifeline，横向消息 |
| **Comparison** | 对比矩阵、左右比较 | 列 = 系统，行 = 维度 |
| **Mind Map** | 概念图、发散图 | 中心节点 + 曲线分支 |

### UML 图支持（14 种）

| UML 类型 | 说明 | 推荐风格 |
|----------|------|----------|
| **Class Diagram** | 类、属性、方法、关系 | Style 1, 4 |
| **Component Diagram** | 软件组件和依赖 | Style 1, 3 |
| **Deployment Diagram** | 硬件节点和软件部署 | Style 3 |
| **Package Diagram** | 包组织和依赖关系 | Style 1, 4 |
| **Composite Structure** | 类/组件内部结构 | Style 1, 3 |
| **Object Diagram** | 对象实例和关系 | Style 1, 4 |
| **Use Case Diagram** | Actor、用例、系统边界 | Style 1 |
| **Activity Diagram** | 工作流、并行流程 | Style 3 |
| **State Machine** | 状态转换和事件 | Style 2, 3 |
| **Sequence Diagram** | 按时间的消息交换 | Style 2 |
| **Communication Diagram** | 对象之间的交互和消息 | Style 1, 2 |
| **Timing Diagram** | 随时间变化的状态 | Style 2 |
| **Interaction Overview** | 高层交互流程 | Style 1, 2 |
| **ER Diagram** | 实体关系数据模型 | Style 1, 3 |

---

## AI/Agent 场景知识

内建模式：

```
RAG Pipeline         → Query → Embed → VectorSearch → Retrieve → LLM → Response
Agentic RAG          → 在 Query 和 LLM 之间增加 Agent loop + Tool use
Agentic Search       → Query → Planner → [Search/Calc/Code] → Synthesizer
Mem0 Memory Layer    → Input → Memory Manager → [Write: VectorDB + GraphDB] / [Read: Retrieve+Rank] → Context
Agent Memory Types   → Sensory（原始输入）→ Working（上下文窗口）→ Episodic（交互历史）→ Semantic（事实）→ Procedural（技能）
Multi-Agent          → Orchestrator → [SubAgent×N] → Aggregator → Output
Tool Call Flow       → LLM → Tool Selector → Tool Execution → Result Parser → LLM（loop）
```

---

## 形状语义

同一种概念在所有风格中尽量保持一致：

| 概念 | 形状 |
|------|------|
| User / Human | 人物圆形头像/身体 |
| LLM / Model | 圆角矩形 + 双边框 + ⚡ |
| Agent / Orchestrator | 六边形 |
| Memory（短期） | 虚线边框圆角框 |
| Memory（长期） | 实心圆柱 |
| Vector Store | 带内圈的圆柱体 |
| Graph DB | 3 个重叠圆节点 |
| Tool / Function | 带 ⚙ 或工具语义的矩形 |
| API / Gateway | 单边框六边形 |
| Queue / Stream | 水平管道/胶囊管 |
| Document / File | 折角矩形 |
| Browser / UI | 顶部 3 个点的窗口框 |
| Decision | 菱形 |
| External Service | 虚线边框矩形 |

---

## 箭头语义

| 流程类型 | 线条 | 虚线 | 含义 |
|---------|------|------|------|
| 主数据流 | 2px 实线 | — | 主请求 / 响应链 |
| 控制 / 触发 | 1.5px 实线 | — | 系统 A 触发 B |
| Memory read | 1.5px 实线 | — | 从存储读取 |
| Memory write | 1.5px | `5,3` | 写入存储 |
| Async / event | 1.5px | `4,2` | 非阻塞 / 事件驱动 |
| Feedback / loop | 1.5px 曲线 | — | 推理或迭代回路 |

---

## 文件结构

```
fireworks-tech-graph/
├── SKILL.md                      # 主 Skill：图类型、布局规则、形状语义
├── README.md                     # 英文说明
├── README.zh.md                  # 中文说明
├── references/
│   ├── style-1-flat-icon.md      # 白底 + 彩色强调
│   ├── style-2-dark-terminal.md  # 暗色背景 + 霓虹强调 + 等宽字体
│   ├── style-3-blueprint.md      # 蓝图网格 + 青色描边
│   ├── style-4-notion-clean.md   # 白底极简 + 单一箭头色
│   ├── style-5-glassmorphism.md  # 深色渐变 + 玻璃卡片
│   ├── style-6-claude-official.md # 暖米色背景 + Anthropic 品牌感
│   ├── style-7-openai.md      # 纯白 + OpenAI 品牌配色
│   └── icons.md                  # 40+ 产品图标 + 语义形状
├── agents/
│   └── openai.yaml              # 兼容运行时的 agent 元信息
├── fixtures/
│   ├── mem0-style1.json         # Style 1 回归测试样例
│   ├── tool-call-style2.json    # Style 2 回归测试样例
│   └── ...                      # 每种风格的更多 sample-grade fixtures
├── scripts/
│   ├── generate-diagram.sh       # SVG 验证 + PNG 导出
│   ├── generate-from-template.py # 用模板创建起始 SVG
│   ├── validate-svg.sh           # 验证 SVG 语法
│   └── test-all-styles.sh        # 批量测试所有风格
├── assets/
│   └── samples/                  # 展示效果图 PNG
├── templates/
│   ├── architecture.svg         # 架构图模板
│   ├── data-flow.svg            # 数据流模板
│   └── ...                      # 其他图类型模板
└── agentloop-core.svg           # 仓库自带示例 SVG
```

---

## 覆盖的产品图标

**AI/ML：** OpenAI、Anthropic/Claude、Google Gemini、Meta LLaMA、Mistral、Cohere、Groq、Hugging Face

**AI Framework：** Mem0、LangChain、LlamaIndex、LangGraph、CrewAI、AutoGen、DSPy、Haystack

**Vector DB：** Pinecone、Weaviate、Qdrant、Chroma、Milvus、pgvector、Faiss

**数据库：** PostgreSQL、MySQL、MongoDB、Redis、Elasticsearch、Neo4j、Cassandra

**消息系统：** Kafka、RabbitMQ、NATS、Pulsar

**云服务：** AWS、GCP、Azure、Cloudflare、Vercel、Docker、Kubernetes

**可观测性：** Grafana、Prometheus、Datadog、LangSmith、Langfuse、Arize

---

## Troubleshooting

| 症状 | 原因 | 修复 |
|------|------|------|
| PNG 全黑或空白 | SVG 中使用了 `@import url()`，rsvg-convert 无法拉取外部资源 | 改用系统字体栈，不要用 `@import` |
| PNG 没生成 | 未安装 `rsvg-convert` | `brew install librsvg`（macOS）或 `apt install librsvg2-bin` |
| 图底部被截断 | `viewBox` 高度太小 | 提高 `viewBox="0 0 960 <height>"` 中的高度 |
| 文本超出框外 | label 太长 | 用 `text-anchor="middle"` + `<clipPath>`，或缩短文案 |
| 图标不显示 | 在 `rsvg-convert` 上下文使用了外部 CDN URL | 使用 `references/icons.md` 中的 inline SVG path |

---

## 许可证

MIT © 2025 fireworks-tech-graph contributors
