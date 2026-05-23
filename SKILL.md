---
name: multi-agent-wechat
description: Use when 需要创作微信公众号文章。一键触发多Agent协作工作流：选题→调研→评估→撰写→评审→HTML排版，循环迭代直到评分达标（≥90分）。
version: 1.0.0
author: Muru AI
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [multi-agent, wechat, article-writing, content-creation, html-formatting]
    related_skills: [skill-factory, scale-factory]
---

# 多Agent协作内容创作工作流

> 内容创作工作流的标准化封装，一键触发多Agent协作，循环迭代直到评分达标。

## Overview

用户指令 → 主编（我）调度 → 并行调研+评估 → 写手出稿 → 评审打分 → (循环修改) → HTML排版 → 交付

## When to Use

**触发词（满足任一即可）：**
- "写文章"
- "创作内容"
- "多Agent协作"
- "帮我写一篇"
- "多Agent工作流"
- "/创作 [主题]"

**不适用于：**
- "多Agent做项目" → 用 `delegate_task` 直连Agent，或 `kanban-orchestrator` 做任务分解
- "帮我建个Skill/技能" → 用 `skill-factory`
- "建一个Scale/AI员工" → 用 `scale-factory`
- "深化/重新解读已有素材" → 主编直接深度写作，不调用调研员

## Agent团队配置

| Agent | 模板 | 输出 | 职责 |
|-------|------|------|------|
| 调研员 | [references/agents.md](references/agents.md) | 素材汇总 | 搜索三类素材（人→人、人→Agent、Agent↔Agent） |
| 评估员 | [references/agents.md](references/agents.md) | 受众分析与结构建议 | 分析目标读者、写作时机、结构建议 |
| 写手 | [references/agents.md](references/agents.md) | 完整文章 | 根据素材和结构要求撰写文章 |
| 评审 | [references/agents.md](references/agents.md) | 评分报告 | 从5个维度打分，满分100，目标≥90 |

## 模板文件

| 文件 | 说明 |
|------|------|
| [references/agents.md](references/agents.md) | 4个Agent的系统提示词模板 |
| [references/templates.md](references/templates.md) | 评审报告模板、交付报告模板、评分规则 |
| [references/template.html](references/template.html) | HTML排版模板 |
| [references/wechat-html-guidelines.md](references/wechat-html-guidelines.md) | 微信公众号HTML排版规范（必读） |
| [references/subagent-output-handling.md](references/subagent-output-handling.md) | 子Agent输出处理规范 |
| [references/content-data-sources.md](references/content-data-sources.md) | 内容创作数据源可靠性参考 |
| [references/article-writing-principles.md](references/article-writing-principles.md) | 老石公众号写作原则（必读） |
| [references/article_draft.md](references/article_draft.md) | 文章草稿模板 |

## 核心工作流

### 标准流程（7步）

```
Step 1: 用户提供主题
         ↓
Step 2: 并行搜索（调研员 + 评估员同时工作）
         ↓
Step 3: 主编汇总素材，确定文章结构
         ↓
Step 4: 写手Agent出初稿
         ↓
Step 5: 评审Agent打分
         ↓
      ┌── 及格（≥90分）──┐
      ↓              ↓
  ✅ 交付        ❌ 不及格 → 返回Step 4 修改
                                  ↑
                              （循环直到达标或达到6轮上限）
         ↓
Step 6: HTML排版（参照 Skills_深度技术报告.html 版式）
         ↓
Step 7: 输出HTML文件路径，告知用户完成
```

### 评审维度（每项20分，满分100）

| 维度 | 说明 |
|------|------|
| 主题契合度 | 是否准确围绕主题，三个阶段是否清晰体现进化逻辑 |
| 结构清晰度 | 三段式结构是否合理，过渡是否流畅 |
| 案例质量 | 案例是否具体、有说服力，有细节和数据 |
| 洞察深度 | 每个阶段的洞察是否到位，是否有独特思考角度 |
| 可读性与传播性 | 语言是否生动，是否让人想转发 |

## 评分迭代规则

| 轮次 | 及格线 | 结果 |
|------|--------|------|
| 第1-5轮 | <90分 | 写手根据评审意见修改 |
| 第6轮 | <90分 | 结束迭代，输出当前最高分版本 |
| ≥90分 | ≥90分 | ✅ 达标，立即交付 |

## HTML排版规范

### 重要区分

| 场景 | 操作 |
|------|------|
| 用户提供主题，写手创作文章 | 写手输出内容 → 主编按template.html结构排版 |
| 用户已有内容，说"转html" | 直接从template.html生成，不保留之前迭代的HTML结构 |
| 用户说"参照模板排版" | 加载template.html，用其结构重新生成HTML |

### template.html结构速查

- 封面：`<div>` 含 标签`<p>` + 主标题`<h1>` + 副标题`<p>` + 描述`<p>` + 核心命题引用块
- 章节：`<h2>` + 底部2px黑线 `border-bottom:2px solid #1a1a1a`
- 引用块：浅蓝背景 `#f5f8ff` + 左侧4px蓝线 `border-left:4px solid #3b82f6`
- 金句块：深色背景 `#1a1a1a` + 白色文字 `<span style="color:#fff;">`
- 表格：浅灰表头 `#f5f5f5` + `border:1px solid #e0e0e0`
- 分隔符：`━━━━━ ● ━━━━━`
- 底部：文章标题 + 来源说明居中

**重要：HTML必须全内联CSS** - 微信编辑器会过滤`<style>`标签，所有样式必须写在style属性里。

输出文件名：`{文章标题}.html`
存放路径：`/mnt/c/Users/Administrator/Desktop/`（Windows桌面）

## 快捷指令

```
/创作 [主题] [字数要求] [目标读者]
```

示例：`/创作 商业模式进化：从人到AI Agent 2000字 创业者`

## 已知陷阱

1. **HTML必须全内联CSS** - 微信编辑器会过滤`<style>`标签，所有样式必须写在style属性里
2. **输出文件必须存放在Windows桌面** - 路径：`/mnt/c/Users/Administrator/Desktop/`
3. **子Agent不执行文件操作** - 写手Agent必须直接输出文章内容，禁止执行bash/PowerShell保存文件
4. **保持用户大纲** - 用户提供详细大纲/内容时，必须严格遵循
5. **评审≠写手反馈** - 评审是独立打分，只打分不同时给修改建议
6. **迭代卡点：洞察深度上不去** - 多次迭代后分数停滞（78-83分），洞察深度需要质的突破，不是加篇幅能解决的
7. **用户说"深化/重新解读"** - 这是一个高优先级信号，表示用户不想听素材里说了什么，而是想要独立分析和观点

## 最佳实践

1. 并行启动调研 - 调研员和评估员同时工作，节省一半时间
2. 明确指出所有问题 - 每轮评审列出所有需要改进的地方
3. 改进意见必须落实 - 修改稿要逐一回应上一轮评审意见
4. 达标立即交付 - 达到90分不继续修改，直接交付
5. 记录迭代历史 - 在交付报告中记录每轮评分，便于复盘
6. 一轮达标是常态 - 实测多篇文章第1轮直接过（95分、98分）
7. 禁止虚假完成步骤 - 评审未被调用时，必须如实告知用户

## 目录结构

```
multi-agent-content/
├── SKILL.md              ← 主入口
└── references/
    ├── agents.md                   ← 4个Agent模板
    ├── article_draft.md            ← 文章草稿
    ├── article-writing-principles.md
    ├── content-data-sources.md
    ├── subagent-output-handling.md
    ├── template.html              ← HTML排版模板
    ├── templates.md               ← 评审/交付报告模板
    ├── test_pool.md               ← 测试用例
    └── wechat-html-guidelines.md
```

## 验证清单

- [ ] description以"Use when"开头
- [ ] frontmatter包含完整字段
- [ ] 所有content文件在references/目录
- [ ] references/test_pool.md存在
- [ ] 内部链接已更新为references/路径
