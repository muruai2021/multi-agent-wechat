# Multi-Agent WeChat — 多Agent协作微信公众号内容创作

> 一键触发多Agent协作：选题→调研→评估→撰写→评审→HTML排版，循环迭代直到评分达标（≥90分）。

---

# English Version

# Multi-Agent WeChat — Multi-Agent WeChat Public Account Content Creation

> One-click triggers multi-agent collaboration: topic selection → research → evaluation → writing → review → HTML formatting, iterative loop until score reaches ≥90.

## Overview

Multi-Agent WeChat is an enterprise-level WeChat public account content creation solution. Through Editor-in-Chief orchestrating four specialized agents - Researcher, Evaluator, Writer, and Reviewer - working in parallel, it achieves end-to-end creation from topic to high-quality HTML article.

**Core Features:**
- Multi-agent parallel work, 50% efficiency improvement
- Automatic scoring iteration, only delivers when score ≥90
- WeChat-compliant HTML formatting
- Full inline CSS, compatible with WeChat editor

## Workflow

```
User says "Write an article about XX"
         ↓
Editor receives topic
         ↓
Step 1: Parallel search (Researcher + Evaluator work simultaneously)
         ↓
Step 2: Editor summarizes materials, determines article structure
         ↓
Step 3: Writer agent produces initial draft
         ↓
Step 4: Reviewer agent scores
         ↓
      ┌── Passed (≥90)? ──┐
      ↓              ↓
  ✅ Deliver    ❌ Not passed → Return to Step 3 for revision
                                    ↑
                              (loop until qualified or 6-round limit)
         ↓
Step 5: HTML formatting (refer to template.html style)
         ↓
Step 6: Output HTML file, notify user of completion
```

## Agent Team

| Agent | Output | Responsibilities |
|-------|--------|------------------|
| Researcher | Material summary | Search three types of materials (person→person, person→Agent, Agent↔Agent) |
| Evaluator | Audience analysis & structure suggestions | Analyze target readers, writing timing, structure suggestions |
| Writer | Complete article | Write article based on materials and structure requirements |
| Reviewer | Scoring report | Score from 5 dimensions, total 100, target ≥90 |

## Review Dimensions

| Dimension | Score | Description |
|-----------|-------|-------------|
| Topic fit | 20pts | Accurately centered on topic, three stages reflect evolution logic clearly |
| Structure clarity | 20pts | Three-part structure reasonable, transitions smooth |
| Case quality | 20pts | Cases specific and persuasive, with details and data |
| Insight depth | 20pts | Insights at each stage on point, unique perspective |
| Readability & shareability | 20pts | Language vivid, makes people want to share |

## Scoring Iteration Rules

| Round | Pass Threshold | Result |
|-------|----------------|--------|
| Round 1-5 | <90pts | Writer revises based on reviewer comments |
| Round 6 | <90pts | End iteration, output current highest score version |
| ≥90pts | ≥90pts | Qualified, deliver immediately |

## HTML Formatting Standards

**Important: HTML must use full inline CSS** - WeChat editor filters `<style>` tags, all styles must be written in style attributes.

### template.html Structure

- Cover: `<div>` with tag `<p>` + main title `<h1>` + subtitle `<p>` + description `<p>` + core proposition quote block
- Sections: `<h2>` + bottom 2px black line `border-bottom:2px solid #1a1a1a`
- Quote blocks: Light blue background `#f5f8ff` + left 4px blue line `border-left:4px solid #3b82f6`
- Highlight blocks: Dark background `#1a1a1a` + white text `<span style="color:#fff;">`
- Tables: Light gray header `#f5f5f5` + `border:1px solid #e0e0e0`
- Separators: `━━━━━ ● ━━━━━`

Output filename: `{article title}.html`
Storage path: `/mnt/c/Users/Administrator/Desktop/` (Windows desktop)

## Trigger Words

- "写文章" / "Write an article"
- "创作内容" / "Create content"
- "帮我写一篇" / "Help me write one"
- "/创作 [主题]" / "/create [topic]"

## Quick Commands

```
/创作 [主题] [字数要求] [目标读者]
/create [topic] [word count] [target readers]
```

Example: `/创作 商业模式进化：从人到AI Agent 2000字 创业者` / `/create Business model evolution: from human to AI Agent 2000 words entrepreneurs`

## Directory Structure

```
multi-agent-wechat/
├── SKILL.md              ← Main entry
└── references/
    ├── agents.md                   ← 4 Agent templates
    ├── article_draft.md            ← Article draft
    ├── article-writing-principles.md ← Writing principles (required reading)
    ├── content-data-sources.md     ← Data source reliability reference
    ├── subagent-output-handling.md ← Sub-agent output handling spec
    ├── template.html              ← HTML formatting template
    ├── templates.md               ← Review/delivery report templates
    ├── test_pool.md               ← Test cases
    └── wechat-html-guidelines.md  ← Formatting standards (required reading)
```

## Related Skills

- `skill-factory` - Skill packaging basics
- `scale-factory` - AI employee creation

## License

MIT
