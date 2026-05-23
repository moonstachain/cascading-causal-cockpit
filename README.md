# Cascading Causal Cockpit

> **多层级联系统的交互式因果可视化驾驶舱设计器**
> Interactive multi-layer causal flowchart designer for complex cascading systems.

把任何"输入 → 处理 → 中间 → 输出"3-5 层级联的复杂系统，用专业 SVG 流程图 + 点击高亮全路径 + 贡献度矩阵 + 配方卡四件套呈现。让读者能**点击任意输出节点反追到根因数据源**。

## 适用场景

| 领域 | Layer 1 | Layer 2（最丰富层） | Layer 3 | Layer 4 |
|---|---|---|---|---|
| 量化基金（N=1 案例） | 数据源 | ~9 archetype | 分域 | 产品 |
| 业务模式 | 资源/能力 | 12-15 战术动作 | 渠道/产品线 | 4-6 客群 |
| 供应链 | 原料/零部件 | 加工工序 | 组件/半成品 | 成品 SKU |
| 软件架构 | 数据源 | 服务/微服务 | API gateway | 客户端/终端 |
| 战略 KPI 树 | 北极星指标 | 杠杆点 | 季度举措 | 团队 KR |
| 生物医药 | 基因/靶点 | 通路 | 疾病机制 | 治疗方案 |
| 风险传导 | 威胁源 | 攻击向量 | 控制薄弱点 | 业务影响 |
| 能源系统 | 能源输入 | 转换设施 | 配送网络 | 终端用户 |

## 5 大支柱

1. **3-5 层级联结构** — 每层节点 3-12 个、层间 many-to-many 加权
2. **颜色 ∝ 健康度（4 态）** — 🟢 现役主力 / 🟡 震荡 / 🔴 待加固 / 🔵 在研增量
3. **连接线 = 加权传导** — 粗细∝权重，颜色∝源健康度，虚线=中性化
4. **点击交互** — dim 其余 + 高亮路径 + 输出节点金色脉冲动画
5. **矩阵 + 配方卡** — 流程图给方向感，矩阵给定量感，配方卡解构每个输出

## 快速开始

### 作为 Claude Code Skill 安装

```bash
git clone https://github.com/moonstachain/cascading-causal-cockpit \
  ~/.claude/skills/cascading-causal-cockpit
```

完成后，在 Claude Code 中说"做个能点击高亮路径的流程图"或"多层级联可视化"即会触发本 skill。

### 作为独立 HTML 模板使用

直接 fork [`templates/scaffold.html`](templates/scaffold.html)：

1. 改 `ARCH_MAP` 字典（最关键）—— 定义你的 9 个 archetype 与上下游连接
2. 改 SVG `<rect>` 节点的文字标签和 fill/stroke 颜色
3. 改 SVG `<path>` 的 d 属性 和 data-arch / data-dom
4. 浏览器打开 → 点击中间任意 archetype 验证完整路径高亮

模板**单文件零依赖**，复制 1100 行的 HTML 就能跑。

## 交互示意

点击中间任意 archetype 节点：

```
⊕ dim 其余节点 + 连线 → 10% opacity
⊕ 高亮选中的 archetype（金色描边）
⊕ 高亮其接入的左侧数据源（绿/黄/红边）
⊕ 高亮其流向的中间分组
⊕ 精确识别右侧下游产品 → 金色脉冲光环（1.6s 周期动画）
⊕ 底部 info 面板浮现：完整链路文字 + 注记
⊕ 再点同一节点 / 点击空白 → 全部 reset
```

## 仓库结构

```
cascading-causal-cockpit/
├── SKILL.md              ── 主方法论（5 大支柱、5 步流程、SVG/CSS/JS 标准模板）
├── templates/
│   └── scaffold.html     ── 最小可运行模板（3 archetype × 2 域 × 3 输出 demo）
├── references/
│   └── n1-quant-fund-anonymous.md  ── N=1 案例匿名化复盘
├── LICENSE               ── MIT
└── README.md
```

## 与父/兄弟 skill 的边界

```
┌─────────────────────────────────────────────────────────────────┐
│  数据展示 / 持续看 / 数据驱动                                      │
│  → high-info-density-dashboard-designer (12 维 rubric)          │
│                                                                  │
│  文档论证 / 一次性读 / 论证驱动                                    │
│  → high-density-mckinsey-report-designer (Pyramid + 12 维)      │
│                                                                  │
│  多层级联因果 / 交互追溯 / 加权传导                                │
│  → cascading-causal-cockpit (本仓库)                            │
│                                                                  │
│  静态系统架构 / 无加权传导                                         │
│  → architecture-diagram                                          │
└─────────────────────────────────────────────────────────────────┘
                       ↑ 同源信息密度方法论的不同载体
```

## 何时不要用本 skill

- ❌ 仅 2 层扁平关系（用普通流程图）
- ❌ 1:1 严格映射（用 sequence 图）
- ❌ 循环反馈结构（用系统动力学图）
- ❌ 单层节点超过 12 个（视觉过载，先做信息收敛）

## 边界声明

- 本 skill 不替代领域知识 —— 节点权重的判定必须基于对真实系统的理解
- 当前 N=1（experimental），N=2 / N=3 验证后会升级 production
- 节点 archetype 类目是行业通用知识（如"残差动量""量贝塔"为量化领域公开概念），无任何机构专有信息

## 鸣谢与方法论来源

- 父 skill：`high-info-density-dashboard-designer` 的 12 维信息密度 rubric
- 兄弟 skill：`high-density-mckinsey-report-designer` 的 Minto Pyramid 论证骨架
- 设计语言：黑金双色（深色科技感 + 古铜金强调），来自维护者自用 dashboard 系列

## License

MIT © 2026 moonstachain / liming
