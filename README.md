# cn-patent-writer

中文发明专利撰写助手 — 将技术方案转化为符合 CNIPA 格式的完整发明专利申请。

## 安装

### 方式一：Claude Code Plugin Marketplace

**前置步骤**（首次安装自定义 marketplace 需执行，仅需一次）：

如果你的电脑未配置 GitHub SSH key，先让 Git 走 HTTPS：

```bash
git config --global url."https://github.com/".insteadOf git@github.com:
```

然后安装：

```text
/plugin marketplace add Chuangwei-Liu/cn-patent-writer
/plugin install cn-patent-writer@cn-patent-writer-marketplace
```

> **常见问题**：执行 `/plugin marketplace add` 时若报 `SSH authentication failed`，说明 Git 默认走 SSH 协议但本机未配置 SSH key。运行上述 `git config` 命令后重试即可。

### 方式二：直接复制

将 `.claude/skills/cn-patent-writer/SKILL.md` 复制到 `~/.claude/skills/cn-patent-writer/` 目录下（全局）或项目根目录 `.claude/skills/cn-patent-writer/`（项目级）。

## 功能

- **权利要求书**：独立方法权利要求 + 从属权利要求 + 装置权利要求 + 电子设备/存储介质/程序产品
- **说明书**：技术领域、背景技术、发明内容、附图说明、具体实施方式
- **说明书摘要**：核心手段 + 主要效果概述
- **信息收集**：输入不完整时自动提问补全
- **专利风格**：自动使用"所述"、"其特征在于"、"在一实施例中"等标准表述

## 触发条件

Claude 在以下情况自动加载此技能：
- 用户说"写专利"、"写发明专利"、"撰写专利"、"专利申请"
- 用户提供技术方案并要求生成专利文档

## 输出结构

```
[说明书摘要]

[权利要求书]
  1. 独立方法权利要求
  2-N. 从属方法权利要求
  N+1. 装置权利要求
  N+2. 电子设备权利要求
  N+3. 计算机可读存储介质权利要求
  N+4. 计算机程序产品权利要求

[说明书]
  技术领域
  背景技术
  发明内容（技术问题 + 技术方案 + 有益效果）
  附图说明
  具体实施方式
```

## 示例

输入：
> 一种基于贝叶斯神经网络的材料性能预测方法，通过异方差输出头获得偶然不确定性，通过MC-Dropout获得认知不确定性，将总不确定性作为多目标优化的独立目标函数

输出：完整的中国发明专利申请（15条权利要求 + 完整说明书 + 摘要）

## 限制

- 生成内容仅供发明人审核和专利代理人参考
- 不提供专利检索功能
- 不替代专业专利代理人的法律意见
- 不保证专利申请的授权

## License

MIT
