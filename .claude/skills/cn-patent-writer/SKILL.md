---
name: cn-patent-writer
description: Use when the user asks to write a Chinese invention patent (发明专利), patent application, or patent draft in Chinese. Triggers on keywords like 写专利, 发明专利, 专利申请, 撰写专利, 专利交底书. Generates complete patent documents following CNIPA format including claims (权利要求书), description (说明书), and abstract (摘要).
---

# Chinese Patent Writer (中国发明专利撰写)

## Overview

Generate complete Chinese invention patent applications (发明专利) in the CNIPA (国家知识产权局) standard format. Target: **≥15,000 Chinese characters** in the final document. Output includes the full set of required documents.

## When to Use

- User says "写专利", "写发明专利", "撰写专利", "专利申请"
- User provides a technical description and asks for a patent draft
- User has a paper/thesis and wants to extract patentable content

## Core Structure

A Chinese invention patent MUST include ALL of the following sections, in this exact order:

### 说明书标题行

在 "## 说明书" 后，正文第一行为发明名称（独立文本行，非标题级），与权利要求书中的发明名称完全一致：

```
说   明   书
基于XXX的XXX方法及装置
```

### 权利要求书 (Claims) — Most Important

**Rule: Method claims first, then device claims, then system/platform claims.**

```
1. 一种[技术方案名称]方法，其特征在于，包括：
   [步骤S10描述]；
   [步骤S20描述]；
   [步骤S30描述]。

2. 如权利要求1所述的方法，其特征在于，[对步骤S10的具体限定]。

3. 如权利要求1所述的方法，其特征在于，[对步骤S20的具体限定]。

...

N. 一种[技术方案名称]装置，其特征在于，包括：
   [模块T10]，用于[功能1]；
   [模块T20]，用于[功能2]；

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
- **Generate ≥10 claims**
- Electronic device, storage medium, program product are MANDATORY boilerplate (claims N+1, N+2, N+3)

### 说明书 (Description)

**MANDATORY: After "## 说明书" header, first line is the invention name as plain text.**

```
技术领域
本发明涉及[大领域]技术领域，具体涉及[细分领域]。

背景技术
[现有技术描述]
[现有技术的缺陷和不足：逐条列出，用"其一/其二/其三"编号]
[每条缺陷与有益效果一一对应，数量相等]

发明内容
[要解决的技术问题：一句话概括]
[技术方案：对应权利要求1的方法论描述。禁止出现具体公式、具体参数值、英文缩写]
[有益效果：列出N条，N必须等于背景技术缺陷条数，顺序一一对应]

附图说明
图1是本发明实施例提供的[方法名称]的流程示意图；
图2是本发明实施例提供的[架构/模型]示意图；
图3是本发明实施例提供的[装置名称]的模块结构示意图；
图4...[列出所有图号，至少5张，覆盖至少4种类型]

具体实施方式
[以标准术语定义段开头（见下方模板）]
[每个主步骤拆分为≥3个子段落，每段落以过渡用语开头]
[每个主步骤末尾有小结句]
[每个可量化参数至少1次"在一实施例中，[参数]取值为[数值]"]
[技术效果的对比说明，含量化数据和结果图引用]

说明书附图
[列出所有图号]
```

### 发明内容 vs 具体实施方式 的严格分离

| | 发明内容 | 具体实施方式 |
|---|---------|------------|
| 可否包含公式 | ❌ 禁止 | ✅ 可以（用 $$...$$ 独立块） |
| 可否包含具体参数值 | ❌ 禁止 | ✅ 可以（"在一实施例中，取值为X"） |
| 可否包含英文缩写 | ❌ 禁止 | ⚠️ 仅公式块中允许必要数学符号 |
| 子步骤划分 | 不需要 | ✅ 必须（每步骤≥3子段落） |

### 说明书摘要 (Abstract)

```
本申请属于[技术领域]技术领域，具体公开了一种[技术方案名称]。通过本申请，[核心手段概述]。通过上述方式，[主要效果概述]。
```

## 具体实施方式标准模板

### 术语定义段（MANDATORY — 具体实施方式开头）

```
为了使本申请的目的、技术方案及优点更加清楚明白，以下结合附图及实施例，对本申请进行进一步详细说明。应当理解，此处所描述的具体实施例仅用以解释本申请，并不用于限定本申请。

本文中术语"和/或"，是一种描述关联对象的关联关系，表示可以存在三种关系，例如，A和/或B，可以表示：单独存在A，同时存在A和B，单独存在B这三种情况。本文中符号"/"表示关联对象是或者的关系，例如A/B表示A或者B。

本文中的说明书和权利要求书中的术语"第一"和"第二"等是用于区别不同的对象，而不是用于描述对象的特定顺序。

在本申请实施例中，"示例性的"或者"例如"等词用于表示作例子、例证或说明。本申请实施例中被描述为"示例性的"或者"例如"的任何实施例或设计方案不应被解释为比其它实施例或设计方案更优选或更具优势。确切而言，使用"示例性的"或者"例如"等词旨在以具体方式呈现相关概念。
```

### 步骤结构模板

**步骤编码**: 使用 `S10/S20/S30...` 格式（间隔10以便插入子步骤）。子步骤用 `S11/S12` 或 `S101/S102`。

**每个主步骤的内部结构**：

```
步骤S10：[步骤名称]。

[过渡用语] [核心描述段落，≥100字]。

需要说明的是，[补充解释段落，≥80字]。

应当理解的是，[原理/必要性段落，≥80字]。

在一实施例中，[具体参数/数值示例]。

本步骤通过[核心手段]，实现[技术效果]。
```

### 过渡用语强制列表

**每个正文段落必须以以下过渡用语之一开头**：

| 用语 | 使用场景 | 要求频率 |
|------|---------|---------|
| 需要说明的是 | 对前述概念的补充解释 | 每个步骤≥1次 |
| 应当理解的是 | 从原理层面解释必要性 | 每个步骤≥1次 |
| 可以理解的是 | 技术推论和延伸 | 每2个步骤≥1次 |
| 进一步地 | 引入下一层技术细节 | 每个步骤≥1次 |
| 还需要强调的是 | 强调关键区别或要点 | 每3个步骤≥1次 |
| 在一实施例中 | 引入具体参数/数值 | 全文≥10次 |
| 在一具体实施例中 | 引入更具体的数据案例 | 全文≥2次 |

### 步骤小结

**每个主步骤末尾必须有小结句**，格式为：

```
本步骤通过[核心手段]，[技术效果描述]。
```

或

```
通过上述方式，[总结性描述]，[解决的问题或带来的好处]。
```

### 装置实施例模板

每个模块必须包含：编号（T10/T20/T30...）、至少3句功能描述。

```
本实施例提供了一种[装置名称]，包括：

确定模块T10，用于[功能]。所述确定模块T10具体用于：[功能细节1]；[功能细节2]；[功能细节3]。

融入模块T20，用于[功能]。所述融入模块T20具体用于：[功能细节1]；[功能细节2]。

输出模块T30，用于[功能]。所述输出模块T30具体用于：[功能细节1]；[功能细节2]。

可以理解的是，上述各个模块可以以硬件、软件、固件或其任意组合的方式实现。上述各个模块的划分仅为功能逻辑上的划分，在实际物理实现中，多个模块可以集成在同一个处理器或存储器件中。
```

### 电子设备/存储介质/程序产品模板

实施例3（电子设备）**必须包含完整的处理器类型枚举**：

```
本实施例提供了一种电子设备，包括至少一个存储器和至少一个处理器。所述存储器用于存储计算机程序。所述处理器用于执行所述存储器存储的程序，当所述存储器存储的程序被执行时，所述处理器用于执行如实施例1中所述的方法。

可以理解的是，本实施例中的处理器可以是中央处理单元（Central Processing Unit, CPU），还可以是其他通用处理器、数字信号处理器（Digital Signal Processor, DSP）、专用集成电路（Application Specific Integrated Circuit, ASIC）、现场可编程门阵列（Field-Programmable Gate Array, FPGA）或者其他可编程逻辑器件、晶体管逻辑器件、硬件部件或者其任意组合。通用处理器可以是微处理器，也可以是任何常规的处理器。
```

实施例4（存储介质）**必须包含完整的存储介质类型枚举**：

```
本实施例提供了一种计算机可读存储介质，所述计算机可读存储介质存储有计算机程序。当所述计算机程序在处理器上运行时，使得所述处理器执行如实施例1中所述的方法。

可以理解的是，本实施例中的计算机可读存储介质可以是随机存取存储器（Random Access Memory, RAM）、闪存（Flash Memory）、只读存储器（Read-Only Memory, ROM）、可编程只读存储器（Programmable ROM, PROM）、可擦除可编程只读存储器（Erasable PROM, EPROM）、电可擦除可编程只读存储器（Electrically EPROM, EEPROM）、寄存器、硬盘、移动硬盘或者本领域熟知的任何其它形式的存储介质。一种示例性的存储介质耦合至处理器，从而使处理器能够从该存储介质读取信息，且可向该存储介质写入信息。当然，所述存储介质也可以是处理器的组成部分。
```

### 技术效果验证段落

技术效果验证段落**必须包含**：
1. 具体测试案例名称和参数
2. 至少1个量化对比数据
3. 至少引用2张结果图

### 说明书附图

文档末尾必须有独立的 "说明书附图" 章节，列出所有图号：

```
说   明   书   附   图
图1
图2
图3
图4
图5
图6
图7
```

## Minimum Length Requirements (MANDATORY)

| 区域 | 最低要求 |
|------|---------|
| 总文档 | ≥ 15,000 字符 |
| 权利要求书 | ≥ 2,000 字符 |
| 背景技术 | ≥ 800 字符（含≥3条缺陷） |
| 发明内容 | ≥ 1,500 字符（含≥3条有益效果） |
| 具体实施方式 | ≥ 5,000 字符 |
| 每个主步骤 | ≥ 200 字 |
| 每个主步骤子段落 | ≥ 3 个 |
| 装置实施例每个模块 | ≥ 3 句描述 |
| "在一实施例中" | 全文 ≥ 10 次 |
| 附图数量 | ≥ 5 张 |
| 附图类型 | ≥ 4 种（流程/架构/模块/结果/对比/验证） |

## Writing Style Rules (MANDATORY)

### 专利标准用语

| 用途 | 表述 |
|------|------|
| 指代前述元素 | 所述 |
| 引入关键特征 | 其特征在于 |
| 强调区别 | 不同于现有技术 |
| 效果对比 | 相较于现有技术 |
| 概括总结 | 总体而言 / 综上 |
| 引出附图 | 参照图X，图X是... |

**Never use:**
- Academic paper language ("我们提出了", "本文", "研究表明")
- Casual language ("很", "非常", "特别")
- Vague claims without technical specificity

### 英文和符号禁用规则

**权利要求书：零英文符号。** 全部变量和算法名称用中文描述。

**说明书正文：仅公式块中允许必要数学符号。** 运行文字中禁止英文缩写。

**发明内容：完全禁止英文。**

### 公式格式规则

- 所有公式**独立成行**，用 `$$...$$` 块
- **禁止 `$...$` 行内公式**
- 公式中的变量后跟中文说明（"其中 N 为训练样本数..."）

### 灰度附图规则

- 所有附图为**黑白或灰度**
- 用**形状**（圆○、方■、三角▲）、**纹样**（斜线、十字纹、点纹）和**灰度深浅**区分不同系列
- 坐标轴标签、图例文字全部为中文

## Information Gathering

Before writing, check if user has provided:

1. **Technical problem**: What specific problem does it solve?
2. **Existing solutions' defects**: What's wrong with current approaches? (≥3 items)
3. **Core technical solution**: What are the key steps/modules?
4. **Distinctive features**: What makes it different from existing methods?
5. **Measurable effects**: What concrete improvements does it achieve?

If ≥2 of these are missing, ask the user. If 4+ are provided, proceed directly.

## Generation Process

### Step 1: Abstraction

Abstract implementation details to patent-level language:
- "用Python的sklearn训练RF模型" → "利用随机森林算法构建预测模型"
- "BNN输出logvar" → "通过贝叶斯神经网络输出预测方差"
- "NSGA-II + TOPSIS" → "采用多目标遗传算法结合多属性决策方法"

### Step 2: Claims First

Write 权利要求书 before 说明书. Claims define protection scope; description supports claims.

### Step 3: Description from Claims

- Claim 1 → 技术方案 in 发明内容 (method-level, no formulas)
- Dependent claims → specific implementations in 具体实施方式 (with formulas, sub-steps, numerical examples)
- Benefits → 有益效果 (条数 = 背景技术缺陷条数)

### Step 4: Abstract Last

Compressed version of claim 1 + key benefit.

## Pre-Submission Checklist

- [ ] 总字符数 ≥ 15,000
- [ ] 权利要求书全文零英文符号
- [ ] 发明内容零公式、零具体参数值、零英文缩写
- [ ] 附图说明列出全部图号，数量 ≥ 5
- [ ] 所有公式独立成行（$$...$$），无行内公式
- [ ] 背景技术缺陷条数 = 有益效果条数，一一对应
- [ ] 具体实施方式以4段术语定义开头
- [ ] 每个主步骤拆分为 ≥ 3 个子段落，均有过渡用语开头
- [ ] 每个主步骤末尾有小結句
- [ ] "在一实施例中" 出现 ≥ 10 次
- [ ] 装置模块每模块 ≥ 3 句描述，带 T10/T20 编号
- [ ] 电子设备实施例含完整处理器类型枚举
- [ ] 存储介质实施例含完整存储介质类型枚举
- [ ] 技术效果验证含量化数据和 ≥ 2 张结果图引用
- [ ] 说明书附图章节列出所有图号
- [ ] 步骤编号使用 S10/S20 格式
