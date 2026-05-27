---
name: cn-patent-writer
description: Use when the user asks to write a Chinese invention patent (发明专利), patent application, or patent draft in Chinese. Triggers on keywords like 写专利, 发明专利, 专利申请, 撰写专利, 专利交底书. Generates complete patent documents following CNIPA format including claims (权利要求书), description (说明书), and abstract (摘要).
---

# Chinese Patent Writer (中国发明专利撰写)

## Overview

Generate complete Chinese invention patent applications (发明专利) in the CNIPA (国家知识产权局) standard format. Output includes the full set of required documents: abstract (说明书摘要), claims (权利要求书), description (说明书), and figure descriptions (附图说明).

## When to Use

- User says "写专利", "写发明专利", "撰写专利", "专利申请"
- User provides a technical description and asks for a patent draft
- User has a paper/thesis and wants to extract patentable content

## Core Structure

A Chinese invention patent MUST include ALL of the following sections:

### 权利要求书 (Claims) — Most Important

**Rule: Method claims first, then device claims, then system/platform claims.**

```
1. 一种[技术方案名称]方法，其特征在于，包括：
   [步骤1描述]；
   [步骤2描述]；
   [步骤N描述]。

2. 如权利要求1所述的方法，其特征在于，[对步骤1的具体限定]。

3. 如权利要求1所述的方法，其特征在于，[对步骤2的具体限定]。

...

N. 一种[技术方案名称]装置，其特征在于，包括：
   [模块1]，用于[功能1]；
   [模块2]，用于[功能2]；

N+1. 一种电子设备，其特征在于，包括：
   至少一个存储器，用于存储计算机程序；
   至少一个处理器，用于执行所述存储器存储的程序，当所述存储器存储的程序被执行时，所述处理器用于执行如权利要求1-[N-1]任一所述的方法。

N+2. 一种计算机可读存储介质，所述计算机可读存储介质存储有计算机程序，其特征在于，当所述计算机程序在处理器上运行时，使得所述处理器执行如权利要求1-[N-1]任一所述的方法。

N+3. 一种计算机程序产品，其特征在于，当所述计算机程序产品在处理器上运行时，使得所述处理器执行如权利要求1-[N-1]任一所述的方法。
```

**Claim writing rules:**
- Independent claim 1: broadest protection, no optional features
- Dependent claims 2+: narrow down with "如权利要求1所述的方法，其特征在于"
- Method claim steps use "；" separator, final step uses "。"
- Device claims mirror method claims: method step → device module
- Generate 10 claims minimum
- Electronic device, storage medium, program product are MANDATORY boilerplate (claims N+1, N+2, N+3)

### 说明书 (Description)

```
技术领域
本发明涉及[大领域]技术领域，具体涉及[细分领域]。

背景技术
[现有技术描述]
[现有技术的缺陷和不足：逐条列出，每条对应一项有益效果]

发明内容
[要解决的技术问题：一句话概括]
[技术方案：对应权利要求1的方法论描述。禁止出现具体公式、具体参数值、英文缩写]
[有益效果：列出3-5条，每条与背景技术缺陷一一对应]

附图说明
图1是本发明实施例提供的[方法名称]的流程示意图；
图2是本发明实施例提供的[架构/模型]示意图；
图3是本发明实施例提供的[装置名称]的模块结构示意图；
图4...图N：[预测结果图、对比图、实验验证图等，至少覆盖4种类型]

具体实施方式
[对技术方案的详细说明，此处可包含公式、实施例、参数范围]
[至少一个具体实施例，采用步骤一至步骤N的编号]
[技术效果的对比说明]
```

### 发明内容 vs 具体实施方式 的严格分离

| | 发明内容 | 具体实施方式 |
|---|---------|------------|
| 可否包含公式 | ❌ 禁止 | ✅ 可以 |
| 可否包含具体参数值 | ❌ 禁止 | ✅ 可以（"在一实施例中，取值为X"） |
| 可否包含英文缩写 | ❌ 禁止 | ⚠️ 仅公式中允许必要数学符号 |
| 语言风格 | 方法论描述 | 技术细节展开 |
| 作用 | 确定保护范围 | 支撑权利要求 |

### 说明书摘要 (Abstract)

```
本申请属于[技术领域]技术领域，具体公开了一种[技术方案名称]。通过本申请，[核心手段概述]。通过上述方式，[主要效果概述]。

[可选：摘要附图说明]
```

### 具体实施方式标准结构

```
步骤一：[名称]。 [详细描述，可含子步骤、公式、参数范围]。

步骤二：[名称]。 [详细描述]。

...

步骤N：[名称]。 [详细描述]。

[技术效果验证段落]

实施例2
参照图M，本实施例提供了一种[装置]，包括[模块列表]。各模块功能简述。

实施例3
本实施例提供了一种电子设备，包括至少一个存储器和至少一个处理器...

实施例4
本实施例提供了一种计算机可读存储介质...

实施例5
本实施例提供了一种计算机程序产品...
```

## Writing Style Rules (MANDATORY)

### 专利标准用语

| 用途 | 表述 |
|------|------|
| 指代前述元素 | 所述 |
| 引入关键特征 | 其特征在于 |
| 引入实施例 | 在一实施例中 / 在一个具体实施方式中 |
| 强调区别 | 不同于现有技术 |
| 解释必要性 | 可以理解的是 / 需要说明的是 |
| 效果对比 | 相较于现有技术 |
| 概括总结 | 总体而言 / 综上 |
| 引出附图 | 参照图X，图X是... |

**Never use:**
- Academic paper language ("我们提出了", "本文", "研究表明")
- Casual language ("很", "非常", "特别")
- Vague claims without technical specificity

### 英文和符号禁用规则 (MANDATORY)

**权利要求书：零英文符号。** 全部变量和算法名称用中文描述：
- σ²_data → "第一不确定性"或"数据固有噪声"
- NSGA-II → "非支配排序遗传算法"
- TOPSIS → "优劣解距离法"
- I_f → "纤维综合指标"
- FA/C, W/B → "粉煤灰与胶凝材料的质量比"、"水胶比"

**说明书正文：仅公式块中允许必要数学符号。** 运行文字中禁止英文缩写。

**发明内容：完全禁止英文。** 初次出现的术语必须给出中文全称。

### 公式格式规则 (MANDATORY)

- 所有公式**独立成行**，不杂糅在文字段落中
- Word 输出用 OMML 格式，Markdown 输出用 `$$...$$` 块
- 公式中的变量后跟中文说明
- 禁止 `$...$` 行内公式

### 灰度附图规则 (MANDATORY)

- 所有附图为**黑白或灰度**，不使用彩色区分
- 用**形状**（圆○、方■、三角▲）、**纹样**（斜线、十字纹、点纹）和**灰度深浅**区分不同模型或数据系列
- 坐标轴标签、图例文字全部为中文

## Information Gathering

Before writing, check if user has provided:

1. **Technical problem**: What specific problem does it solve?
2. **Existing solutions' defects**: What's wrong with current approaches?
3. **Core technical solution**: What are the key steps/modules?
4. **Distinctive features**: What makes it different from existing methods?
5. **Measurable effects**: What concrete improvements does it achieve?

If ≥2 of these are missing, ask the user before proceeding. Use the following questions (pick the most critical gaps):

- "要解决什么技术问题？"
- "现有方案有什么缺陷？"
- "技术方案的核心步骤是什么？"
- "有哪些区别于现有方法的关键技术特征？"
- "能达到什么定量效果（如精度提升X%、效率提高Y倍）？"

If 4+ are provided, proceed directly to generate the complete patent.

## Generation Process

### Step 1: Abstraction

Abstract implementation details to patent-level language:
- "用Python的sklearn训练RF模型" → "利用随机森林算法构建预测模型"
- "BNN输出logvar" → "通过贝叶斯神经网络输出预测方差"
- "NSGA-II + TOPSIS" → "采用多目标遗传算法结合多属性决策方法"

### Step 2: Claims First

Write 权利要求书 before 说明书. Claims define the protection scope; the description supports the claims.

### Step 3: Description from Claims

Expand each claim element into prose sections in the description:
- Claim 1 → 技术方案 in 发明内容 (method-level, no formulas)
- Dependent claims → specific implementations in 具体实施方式 (can include formulas)
- Benefits → 有益效果 (quantify where possible)

### Step 4: Abstract Last

The abstract is a compressed version of claim 1 + key benefit. Write it last.

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Only method claims, no device/medium claims | ALWAYS add claims N+1, N+2, N+3 (device, storage medium, program product) |
| Formulas and specific values in 发明内容 | Move all formulas and values to 具体实施方式 |
| English abbreviations in claims or 发明内容 | Replace ALL with Chinese descriptions |
| Inline formulas in text ($...$) | Put ALL formulas on separate lines ($$...$$ or OMML) |
| Color-dependent figures | Use grayscale with distinct shapes, hatch patterns, and line styles |
| 附图说明 only lists flowcharts | Include 4+ figure types: flowchart, architecture, module, prediction result, comparison, experimental validation |
| 发明内容残留英文缩写 (e.g., "FRCC") | Expand to full Chinese name on first occurrence |
| 实施例2-5 missing headers | Add explicit 实施例 headers for each embodiment |
| Academic writing style ("我们提出", "本文") | Replace with patent style ("本申请", "本发明") |
| Too few claims (<10) | Aim for 10 claims minimum |

## Pre-Submission Checklist (MANDATORY)

Before finalizing the patent document, verify ALL of the following:

- [ ] 权利要求书全文零英文符号
- [ ] 发明内容零公式、零具体参数值、零英文缩写
- [ ] 附图说明列出全部图号及描述，数量与正文引用一致
- [ ] 所有公式独立成行，无行内公式
- [ ] 所有附图为黑白/灰度
- [ ] 附图至少覆盖4种类型（流程图+架构图+模块图+结果图+对比图+验证图任选其四）
- [ ] 背景技术缺陷条数 = 发明内容有益效果条数
- [ ] 实施例2-5均有明确标题
- [ ] 全文无"FRCC"等英文缩写（除公式块中必要数学符号）
- [ ] 说明书附图区域列出的图号与正文引用完全一致
