---
name: cascading-causal-cockpit
description: |
  多层级联系统的交互式因果可视化驾驶舱设计器。把任何"输入→处理→中间→输出"3-5 层级联的复杂系统，用专业 SVG 流程图 + 点击高亮全路径 + 贡献度矩阵 + 配方卡四件套呈现。让读者能"点击任意输出节点反追到根因数据源"。
  典型场景：量化基金（因子→域→产品）/ 业务模式（渠道→产品→客群→收入）/ 供应链（原料→工序→组件→成品）/ 软件架构（数据源→服务→API→客户端）/ 战略分解（能力→策略→项目→KPI）/ 因果归因（基因→通路→疾病→治疗）。
  与父 skill 边界：high-info-density-dashboard-designer 管"展示什么数据"，high-density-mckinsey-report-designer 管"如何论证"，本 skill 管"如何把多层级联的因果用一张可交互图说清楚"。
triggers:
  - "把这个复杂系统做成可点击的因果图"
  - "做个能点击高亮路径的流程图"
  - "多层级联可视化"
  - "交互式因果驾驶舱"
  - "Sankey 进阶 / 加权多层流向"
  - "层级因果归因图"
  - "数据→中间→产品 全链路可视"
  - "点击节点高亮上下游"
  - "cascading flowchart"
  - "click to highlight causal path"
  - "multi-layer causal map"
maturity: experimental
status: n=1-completed
created: 2026-05-23
license: MIT
distilled_from:
  - "Quant Fund N=1 (private case): factor → domain → product 4-layer cascade"
parent:
  - high-info-density-dashboard-designer
  - high-density-mckinsey-report-designer
---

# Cascading Causal Cockpit · 多层级联因果驾驶舱设计器

> **N=1 dry-run 完成**（匿名量化基金案例 · 因子→域→产品 4 层级联，2026-05-23）
> N=2 候选：业务模式分解 / 供应链 / 战略 KPI 树 / 软件架构 / 风险传导
>
> **核心信念 · 第一性原理**：
> 1. **复杂多层系统不能用线性叙述讲清** —— 必须用空间+颜色+交互三重维度同时呈现。
> 2. **点击 = 反追** —— 任何输出节点的"为什么"，都应能 1 次点击在 200ms 内追溯到根源数据。
> 3. **金色脉冲是因果终点的视觉锚** —— 用动画区分"被波及的"和"被精确选中的"。
> 4. **矩阵+流程图二者缺一不可** —— 流程图给方向感，矩阵给定量感。
> 5. **配方卡是产品/输出的解构** —— 每个输出都是 archetype 的加权组合，明示主菜/配菜/点缀。

---

## 何时启用

| 信号 | 是否启用本 skill |
|---|---|
| 系统有 3-5 个清晰层次（如：输入→处理→中间→输出） | ✅ |
| 层与层之间是 many-to-many 加权传导（不是 1:1） | ✅ |
| 输出节点有"健康度"差异（好/中/差），用户想知道为什么 | ✅ |
| 用户想"点任意输出 → 看完整因果路径" | ✅ |
| 仅 2 层（输入→输出）的扁平关系 | ❌ 用普通流程图即可 |
| 层间只是 1:1（每个输入对应唯一输出） | ❌ 用 sequence 图 |
| 系统是循环/反馈结构（如生态系统） | ❌ 本 skill 不擅长，建议系统动力学图 |

---

## 5 大支柱（不可省）

### 支柱 1 · 四层级联结构（3-5 层）
读者从左到右扫过去能看见完整因果链。最常见：

```
Layer 1: 数据源/输入        (4-6 个节点)
Layer 2: 中间转换/archetype  (8-12 个节点) ← 这是 alpha 的核心，节点最多
Layer 3: 分组/域/通道        (3-5 个节点)
Layer 4: 输出/产品/KPI       (4-8 个节点)
```

**3 条质检**：
- 每层语义明确（"原料"vs"加工"vs"组件"vs"成品" 清晰可名）
- 每层节点数 ≥ 3（< 3 视为单点，无可视化价值）
- 层与层确实是 many-to-many（否则降级为简单流程图）

### 支柱 2 · 颜色 ∝ 健康度（4 态状态机）

| 状态 | 边框颜色 | 适用 |
|---|---|---|
| 🟢 现役主力 / 健康 | `#3dd68c` | 当前正贡献、值得保持 |
| 🟡 震荡 / 攻坚中 | `#f5b53a` | 介于好坏之间或在迭代 |
| 🔴 待加固 / 走弱 | `#e5484d` | 当前负贡献、需要修 |
| 🔵 在研增量 | `#6aa6e8` | 还没有结果但在试 |

**重要纪律**：状态判定要有客观依据（实测数据 / 当事人确认），不能凭直觉染色。

### 支柱 3 · 连接线 = 加权传导（Bezier 曲线）

| 视觉属性 | 编码什么 |
|---|---|
| **粗细** | 贡献权重（主导 2.4-2.8、次要 1.2-1.8、边缘 0.7-1.0） |
| **颜色** | 多用源节点颜色（绿/红/蓝），中性用金色 |
| **虚线** | 中性化关系 / 非贡献性连接 / 反馈 |
| **方向曲线** | Bezier `C` 控制点放在两端 50% 处保证视觉柔和 |

### 支柱 4 · 点击交互（核心创新点）

**交互规约**：
- 点击 Layer 2 中任意节点（最丰富的那层）
- 自动 dim 其余节点和连接到 10% opacity
- 高亮该节点 + 它接入的 Layer 1 数据源 + 它流向的 Layer 3 分组
- 追到 Layer 4：精确识别该 archetype 经分组所到达的具体输出节点
- **输出节点加金色脉冲光环**（1.6s 周期，区分"在路径上"vs"被精确选中"）
- 信息面板自动浮现：完整链路文字描述 + 注记
- 再点击同一节点 / 点击空白处 → 全部 reset

### 支柱 5 · 矩阵 + 配方卡（流程图的两个解构视图）

流程图给方向感，但定量感弱。需补两个视图：

**B · 贡献度矩阵**：行 = archetype，列 = 输出节点，单元格 = 占比（%），主菜用 ★ 标记，背景颜色编码

**C · 配方卡**：每个输出节点一张卡，列出"主菜（最大贡献 archetype）/ 配菜 / 点缀"，附当前状态

**D · 动态调整层**（可选）：宏观信号 → 因子权重的反馈，4-6 行表

---

## 12 维信息密度 rubric（适配级联系统）

继承自父 skill `high-info-density-dashboard-designer` 的 12 维 rubric，本 skill 重点关注：

| # | 维度 | 在级联图谱中的实现 | 满分典型 |
|---|---|---|---|
| **D1** 时间密度 | 数据 as-of 标注、节点状态当前性 | "数据 as-of [日期]" 显式 |
| **D2** 判定密度 | 节点颜色直接给判定，不只是描述 | 红 = 待加固，绿 = 主力 |
| **D7** 状态机化 | 4 态颜色编码（不是连续色谱） | 现役/震荡/待加固/在研 |
| **D8** 高维降维 | 几百节点 → ~10 archetype → 少量分组 → 输出 | 4352 项归 9 archetype |
| **D9** 行动建议 | 配方卡末尾给 Action | 具体改进方向 + 预期效果 |
| **D11** 历史轨迹 | 节点边框宽度/颜色随版本演化 | （可选）每版高亮新增/退出节点 |

≥ 9/10 平均分 = 咨询级专业图谱。

---

## 8 反模式扫描

| 反模式 | 是否中招？ | 修法 |
|---|---|---|
| ❌ 节点太多视觉过载 | 单层 > 12 节点 | 收敛到 ≤ 10 |
| ❌ 所有连线一样粗细颜色 | 没有 weight 编码 | 按支柱 3 重做 |
| ❌ 没有图例 | 颜色含义猜不到 | 底部加颜色 + 线型图例 |
| ❌ 只有静态图、没有交互 | 缺点击高亮 | 按支柱 4 注入 |
| ❌ 配方比例全是猜的 | 没说明定性还是定量 | 显式标注 "比例为定性估算" |
| ❌ 点击后视觉差异不显著 | dim 不够、active 不够亮 | dim → 10% opacity，active 加 drop-shadow |
| ❌ 反馈延迟 > 200ms | JS 实现重 | CSS 动画 + transition |
| ❌ 信息面板不更新 | 状态变化没同步文字 | innerHTML 跟着 active 状态变 |

---

## 5 步流程

### Step 1 · 系统分解（30 分钟）

回答 4 个问题：

| 问题 | 示例答案 |
|---|---|
| 系统的最左是什么？（数据/原料/输入） | （6 类原始数据来源）|
| 系统的最右是什么？（输出/成品/KPI） | （7 个产品/KPI） |
| 中间最关键的层是什么？ | （9 个 archetype 类别）|
| 是否还有第二个中间层？ | 是 → 4 个分组 |

输出：4-layer 草图 + 每层节点清单。

### Step 2 · 健康度标注 + 权重映射（30-60 分钟）

- 给每个节点定 4 态状态（绿/黄/红/蓝），写依据
- 列连接关系（哪个连哪个），估权重（主导 / 次要 / 边缘 / 中性化）
- ⚠️ 如无定量数据，明确标注"定性估算"

输出：节点 × 节点的邻接矩阵 + 权重列。

### Step 3 · 矩阵 + 配方卡（1 小时）

- 行 = archetype，列 = 输出
- 单元格填 % 估算，主菜加 ★
- 末行加"当前 KPI"
- 每个输出做一张配方卡（主菜 / 配菜 / 点缀）
- 卡片状态彩边对应输出健康度

### Step 4 · SVG 流程图 + 交互（2-3 小时）

参考 [templates/scaffold.html](templates/scaffold.html) 直接 fork：
- 4 列布局，1180×600 viewBox
- 节点用 `<rect>` + `<text>`，加 class + data 属性
- 连接用 `<path>` + Bezier，加 class + data-arch / data-dom
- CSS：`.svg-dimmed { opacity: 0.10 }` + `.svg-active-ring { drop-shadow }` + `@keyframes prod-pulse`
- JS：监听 `.arch-rect` 点击，根据 `ARCH_MAP` 字典 dim/highlight

### Step 5 · 深度结论 + 改进路径（30 分钟）

每张图谱配 2 个 callout：
- **深度结论**：图谱回答了什么具体问题？为什么 X 输出健康、Y 输出待加固？
- **改进路径**：基于矩阵看出来的 1-2 个工程可加固方向（含预期效果）

---

## SVG + JS 标准模板（可直接 fork）

### 节点最小标记

```xml
<!-- Layer 2 archetype 节点（可点击）-->
<rect class="arch-rect" data-arch="1"
      x="290" y="60" width="220" height="38" rx="6"
      fill="#0f2a1d" stroke="#3dd68c" stroke-width="1.2"/>
<text x="400" y="76" fill="#ececed" font-size="11" text-anchor="middle">① archetype 健康</text>
<text x="400" y="90" fill="#7fe0ad" font-size="10" text-anchor="middle">现役主力</text>
```

### Layer 4 输出节点（接受脉冲高亮）

```xml
<rect class="prod-rect" data-doms="L,M,S" data-prod="输出 X"
      x="970" y="60" width="180" height="42" rx="6"
      fill="#0f2a1d" stroke="#3dd68c" stroke-width="1.4"/>
```

### 连接线

```xml
<!-- Layer 1 → Layer 2，标 data-arch=目标节点ID -->
<path class="conn" data-arch="1"
      d="M 180 90 C 235 90, 235 79, 290 79"
      stroke="#c8a05a" stroke-width="2.4" fill="none" opacity="0.7"/>

<!-- Layer 3 → Layer 4，标 data-dom=源域 -->
<path class="conn-dp" data-dom="L"
      d="M 830 105 C 900 105, 900 81, 970 81"
      stroke="#3dd68c" stroke-width="2.6" fill="none" opacity="0.75"/>
```

### CSS

```css
rect.arch-rect { cursor: pointer; transition: opacity .25s, filter .15s; }
rect.arch-rect:hover { filter: brightness(1.35) drop-shadow(0 0 4px rgba(200,160,90,.5)); }
path.conn, path.conn-dp { transition: opacity .25s; }
.svg-dimmed { opacity: .10 !important; }
.svg-active-ring { filter: drop-shadow(0 0 6px rgba(200,160,90,.9)); }

rect.prod-active {
  stroke: #c8a05a !important; stroke-width: 2.5 !important;
  animation: prod-pulse 1.6s ease-in-out infinite;
}
@keyframes prod-pulse {
  0%, 100% { filter: drop-shadow(0 0 4px rgba(200,160,90,.5)); }
  50% { filter: drop-shadow(0 0 10px rgba(216,189,134,1)) drop-shadow(0 0 3px rgba(200,160,90,.8)); }
}
```

### JS 交互核心（核心代码 ~50 行）

```javascript
(function() {
  var ARCH_MAP = {
    1: { name: "① archetype A", sources: ["数据A"], doms: ["L","M","S"], note: "现役主力" },
    2: { name: "② archetype B", sources: ["数据A","数据B"], doms: ["L","M"], note: "..." },
    // ... 其他 archetype
  };
  var DOM_NAMES = { "L":"Large","M":"Mid","S":"Small","Mi":"Micro" };
  var svg = document.querySelector("#causal-map svg");
  var info = document.getElementById("causal-info");
  var infoText = document.getElementById("causal-info-text");
  var allDimable = svg.querySelectorAll(
    "rect.arch-rect, rect.dat-rect, rect.dom-rect, rect.prod-rect, path.conn, path.conn-dp"
  );
  var activeArch = null;

  function reset() {
    activeArch = null;
    allDimable.forEach(function(el) {
      el.classList.remove("svg-dimmed", "svg-active-ring", "prod-active");
    });
    info.classList.remove("show");
  }

  function activate(archId) {
    var m = ARCH_MAP[archId]; if (!m) return;
    allDimable.forEach(function(el) { el.classList.add("svg-dimmed"); });
    // 高亮选中 archetype
    svg.querySelectorAll('rect.arch-rect[data-arch="' + archId + '"]').forEach(function(el) {
      el.classList.remove("svg-dimmed"); el.classList.add("svg-active-ring");
    });
    // 高亮数据源
    m.sources.forEach(function(s) {
      svg.querySelectorAll('rect.dat-rect[data-src="' + s + '"]').forEach(function(el) {
        el.classList.remove("svg-dimmed");
      });
    });
    // 高亮域 + 域→产品路径
    m.doms.forEach(function(d) {
      svg.querySelectorAll('rect.dom-rect[data-dom="' + d + '"]').forEach(function(el) {
        el.classList.remove("svg-dimmed");
      });
      svg.querySelectorAll('path.conn-dp[data-dom="' + d + '"]').forEach(function(el) {
        el.classList.remove("svg-dimmed");
      });
    });
    // 精确高亮：基于 archetype 所连域，识别下游产品（金色脉冲）
    var activeDomSet = new Set(m.doms);
    svg.querySelectorAll("rect.prod-rect").forEach(function(el) {
      var pdoms = (el.dataset.doms || "").split(",");
      var matched = pdoms.some(function(d) { return activeDomSet.has(d); });
      if (matched) {
        el.classList.remove("svg-dimmed");
        el.classList.add("svg-active-ring", "prod-active");
      }
    });
    // 高亮 data→arch 路径
    svg.querySelectorAll('path.conn[data-arch="' + archId + '"]').forEach(function(el) {
      el.classList.remove("svg-dimmed");
    });

    // 信息面板
    info.classList.add("show");
    var domsName = m.doms.map(function(d) { return DOM_NAMES[d]; }).join(" / ");
    var prodList = [];
    svg.querySelectorAll('rect.prod-rect.prod-active').forEach(function(el) {
      prodList.push(el.dataset.prod);
    });
    infoText.innerHTML =
      '<b style="color:var(--gold-s)">' + m.name + '</b>' +
      ' · 数据源 [' + m.sources.join(" · ") + ']' +
      ' → 域 [' + domsName + ']' +
      ' → <b style="color:#d8bd86">产品 [' + (prodList.join(' / ') || '—') + ']</b>' +
      '<br><span style="color:var(--txt3);font-size:12px">' + m.note + '</span>';
  }

  svg.querySelectorAll("rect.arch-rect").forEach(function(r) {
    r.addEventListener("click", function(e) {
      e.stopPropagation();
      var id = r.dataset.arch;
      if (activeArch === id) { reset(); return; }
      reset(); activeArch = id; activate(id);
    });
  });

  document.addEventListener("click", function(e) {
    if (activeArch && !e.target.closest("rect.arch-rect")) { reset(); }
  });
})();
```

完整可 fork 的 HTML 见 [templates/scaffold.html](templates/scaffold.html)。

---

## 适配其他领域的速查表

| 领域 | Layer 1 | Layer 2（最丰富层） | Layer 3 | Layer 4 |
|---|---|---|---|---|
| **量化基金（N=1）** | 数据源 | ~9 archetype | 分域 | 产品 |
| **业务模式** | 资源/能力 | 12-15 战术动作 | 渠道/产品线 | 4-6 客群 |
| **供应链** | 原料/零部件 | 加工工序 | 组件/半成品 | 成品 SKU |
| **软件架构** | 数据源 | 服务/微服务 | API gateway | 客户端/终端 |
| **战略 KPI 树** | 北极星指标 | 杠杆点 | 季度举措 | 团队 KR |
| **生物医药** | 基因/靶点 | 通路 | 疾病机制 | 治疗方案 |
| **风险传导** | 威胁源 | 攻击向量 | 控制薄弱点 | 业务影响 |
| **能源系统** | 能源输入 | 转换设施 | 配送网络 | 终端用户 |

---

## 关联

- `[[high-info-density-dashboard-designer]]` 父 skill（12 维 rubric 来源）
- `[[high-density-mckinsey-report-designer]]` 兄弟 skill（用于报告版本）
- `[[architecture-diagram]]` 适合静态系统架构图（无加权传导）

## 边界 · 不要越界

- ❌ **不替代领域知识** —— 节点权重要靠对系统的真实理解
- ❌ **不用于 1-2 层扁平关系** —— 用 sequence / flow 图即可
- ❌ **不用于循环系统** —— 用系统动力学图
- ❌ **不要让节点 > 12 个一层** —— 视觉过载
- ✅ **诚实标注权重的来源**：精确披露 vs 定性估算
- ✅ **跨载体配套**：HTML 主交付 + PNG 嵌 docx + （可选）静态 SVG 嵌 PPT
- ✅ **N=1 状态显式**：本 skill 目前 N=1，N=2 之前请标注实验性

## N=1 已实测

| 案例 | 日期 | 评分 | 载体 | 链路深度 |
|---|---|---|---|---|
| 匿名量化基金 · 因子→产品 4 层级联 | 2026-05-23 | 95/120 | HTML + 嵌 PNG docx | 4 层 / 30 节点 / 50+ 路径 |

完整匿名化案例结构见 [references/n1-quant-fund-anonymous.md](references/n1-quant-fund-anonymous.md)。
