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
[现有技术的缺陷和不足]

发明内容
[要解决的技术问题]
[技术方案：对应权利要求1的详细展开]
[有益效果：列出3-5条]

附图说明
图1是本发明实施例提供的[方法名称]的流程示意图；
图2是本发明实施例提供的[装置名称]的模块结构示意图；

具体实施方式
[对技术方案的详细说明，可包含公式、实施例、参数范围]
[至少一个具体实施例]
[技术效果的对比说明]
```

### 说明书摘要 (Abstract)

```
本申请属于[技术领域]技术领域，具体公开了一种[技术方案名称]。通过本申请，[核心手段概述]。通过上述方式，[主要效果概述]。

[可选：摘要附图说明]
```

## Writing Style Rules (MANDATORY)

**Use these phrases throughout:**

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
- Claim 1 → 技术方案 in 发明内容
- Dependent claims → specific implementations in 具体实施方式
- Benefits → 有益效果 (quantify where possible)

### Step 4: Abstract Last

The abstract is a compressed version of claim 1 + key benefit. Write it last.

## Common Mistakes (from baseline testing)

| Mistake | Fix |
|---------|-----|
| Only method claims, no device/medium claims | ALWAYS add claims N+1, N+2, N+3 (device, storage medium, program product) |
| Uncertainty described as "constraint" when it's an "optimization objective" | Match the paper's actual technical contribution |
| Using generic descriptions ("纤维种类", "基体配合比") instead of specific features | Use specific technical terms from the provided material |
| Academic writing style ("我们提出", "本文") | Replace with patent style ("本申请", "本发明") |
| Too few claims (<10) | Aim for 10 claims minimum |
| Missing boilerplate electronic device + storage medium claims | These are ALWAYS required for method patents |

## Real-World Examples

Reference patent structure (Chinese patent HPACN20251268): See the reference document at `Reference/基于物理信息神经网络的结构数值仿真与优化一体化方法/` for complete formatting, paragraph structure, and claim chain design.
