<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multi-Agent WeChat</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; color: #24292e; background: #f6f8fa; padding: 20px; }
        .container { max-width: 900px; margin: 0 auto; background: #fff; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); overflow: hidden; }
        .header { background: linear-gradient(135deg, #11998e 0%, #ec38bc 100%); color: #fff; padding: 40px; text-align: center; }
        .header h1 { font-size: 2.5em; margin-bottom: 10px; }
        .header p { font-size: 1.2em; opacity: 0.9; }
        .lang-switch { display: flex; justify-content: center; gap: 10px; padding: 20px; background: #f6f8fa; border-bottom: 1px solid #e1e4e8; }
        .lang-btn { padding: 10px 30px; border: 2px solid #ec38bc; background: #fff; color: #ec38bc; border-radius: 25px; cursor: pointer; font-weight: 600; transition: all 0.3s; }
        .lang-btn:hover { background: #ec38bc; color: #fff; }
        .lang-btn.active { background: #ec38bc; color: #fff; }
        .content { padding: 40px; }
        .content[lang="en"] { display: none; }
        h2 { color: #ec38bc; margin: 30px 0 15px; padding-bottom: 10px; border-bottom: 2px solid #ec38bc; }
        h3 { color: #333; margin: 20px 0 10px; }
        p { margin: 15px 0; }
        ul { margin: 15px 0; padding-left: 25px; }
        li { margin: 8px 0; }
        code { background: #f6f8fa; padding: 2px 6px; border-radius: 3px; font-family: Monaco, monospace; color: #e74c3c; }
        pre { background: #1e1e1e; color: #d4d4d4; padding: 20px; border-radius: 8px; overflow-x: auto; margin: 15px 0; font-size: 14px; }
        pre code { background: none; color: inherit; }
        table { width: 100%; border-collapse: collapse; margin: 15px 0; }
        th, td { border: 1px solid #e1e4e8; padding: 12px; text-align: left; }
        th { background: #ec38bc; color: #fff; }
        tr:nth-child(even) { background: #f6f8fa; }
        .badge { display: inline-block; padding: 4px 12px; border-radius: 20px; font-size: 0.85em; margin: 2px; }
        .badge-primary { background: #ec38bc; color: #fff; }
        .badge-success { background: #27ae60; color: #fff; }
        .badge-warning { background: #f39c12; color: #fff; }
        .footer { text-align: center; padding: 30px; color: #666; border-top: 1px solid #e1e4e8; }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Multi-Agent WeChat</h1>
            <p>多Agent协作微信公众号内容创作 | Multi-Agent WeChat Content Creation</p>
        </div>
        <div class="lang-switch">
            <button class="lang-btn active" onclick="switchLang('zh')">中文</button>
            <button class="lang-btn" onclick="switchLang('en')">English</button>
        </div>
        <div class="content" lang="zh">
            <h2>概述</h2>
            <p>Multi-Agent WeChat 是一个企业级微信公众号内容创作解决方案。通过主编调度调研员、评估员、写手、评审四个专业Agent并行协作，实现从主题到高质量HTML文章的端到端创作。</p>
            <h3>核心特性</h3>
            <ul>
                <li>多Agent并行工作，效率提升50%</li>
                <li>自动评分迭代，达标（≥90分）才交付</li>
                <li>符合微信公众号规范的HTML排版</li>
                <li>全内联CSS，适配微信编辑器</li>
            </ul>
            <h2>工作流程</h2>
            <pre><code>用户说"写一篇关于XX的文章"
         ↓
主编接收主题
         ↓
Step 1: 并行搜索（调研员 + 评估员同时工作）
         ↓
Step 2: 主编汇总素材，确定文章结构
         ↓
Step 3: 写手Agent出初稿
         ↓
Step 4: 评审Agent打分
         ↓
      ┌── 及格（≥90分）──┐
      ↓              ↓
  交付        不及格 → 返回Step 3 修改
                                  ↑
                          （循环直到达标或达到6轮上限）
         ↓
Step 5: HTML排版（参照template.html版式）
         ↓
Step 6: 输出HTML文件，告知用户完成</code></pre>
            <h2>Agent团队</h2>
            <table>
                <tr><th>Agent</th><th>输出</th><th>职责</th></tr>
                <tr><td>调研员</td><td>素材汇总</td><td>搜索三类素材（人→人、人→Agent、Agent↔Agent）</td></tr>
                <tr><td>评估员</td><td>受众分析与结构建议</td><td>分析目标读者、写作时机、结构建议</td></tr>
                <tr><td>写手</td><td>完整文章</td><td>根据素材和结构要求撰写文章</td></tr>
                <tr><td>评审</td><td>评分报告</td><td>从5个维度打分，满分100，目标≥90</td></tr>
            </table>
            <h2>评审维度</h2>
            <table>
                <tr><th>维度</th><th>分值</th><th>说明</th></tr>
                <tr><td>主题契合度</td><td>20分</td><td>是否准确围绕主题，三个阶段是否清晰体现进化逻辑</td></tr>
                <tr><td>结构清晰度</td><td>20分</td><td>三段式结构是否合理，过渡是否流畅</td></tr>
                <tr><td>案例质量</td><td>20分</td><td>案例是否具体、有说服力，有细节和数据</td></tr>
                <tr><td>洞察深度</td><td>20分</td><td>每个阶段的洞察是否到位，是否有独特思考角度</td></tr>
                <tr><td>可读性与传播性</td><td>20分</td><td>语言是否生动，是否让人想转发</td></tr>
            </table>
            <h2>评分迭代规则</h2>
            <table>
                <tr><th>轮次</th><th>及格线</th><th>结果</th></tr>
                <tr><td>第1-5轮</td><td><90分</td><td>写手根据评审意见修改</td></tr>
                <tr><td>第6轮</td><td><90分</td><td>结束迭代，输出当前最高分版本</td></tr>
                <tr><td>≥90分</td><td>≥90分</td><td><span class="badge badge-success">达标，立即交付</span></td></tr>
            </table>
            <h2>HTML排版规范</h2>
            <p><span class="badge badge-warning">重要：HTML必须全内联CSS</span> - 微信编辑器会过滤`<style>`标签，所有样式必须写在style属性里。</p>
            <h3>template.html结构</h3>
            <ul>
                <li>封面：`<div>` 含 标签`<p>` + 主标题`<h1>` + 副标题`<p>` + 描述`<p>` + 核心命题引用块</li>
                <li>章节：`<h2>` + 底部2px黑线</li>
                <li>引用块：浅蓝背景 `#f5f8ff` + 左侧4px蓝线</li>
                <li>金句块：深色背景 `#1a1a1a` + 白色文字</li>
                <li>表格：浅灰表头 `#f5f5f5`</li>
                <li>分隔符：`━━━━━ ● ━━━━━`</li>
            </ul>
        </div>
        <div class="content" lang="en">
            <h2>Overview</h2>
            <p>Multi-Agent WeChat is an enterprise-level WeChat public account content creation solution. Through Editor-in-Chief orchestrating four specialized agents - Researcher, Evaluator, Writer, and Reviewer - working in parallel, it achieves end-to-end creation from topic to high-quality HTML article.</p>
            <h3>Core Features</h3>
            <ul>
                <li>Multi-agent parallel work, 50% efficiency improvement</li>
                <li>Automatic scoring iteration, only delivers when score ≥90</li>
                <li>WeChat-compliant HTML formatting</li>
                <li>Full inline CSS, compatible with WeChat editor</li>
            </ul>
            <h2>Workflow</h2>
            <pre><code>User says "Write an article about XX"
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
  Deliver    Not passed → Return to Step 3
                                    ↑
                          (loop until qualified or 6-round limit)
         ↓
Step 5: HTML formatting (refer to template.html style)
         ↓
Step 6: Output HTML file, notify user of completion</code></pre>
            <h2>Agent Team</h2>
            <table>
                <tr><th>Agent</th><th>Output</th><th>Responsibilities</th></tr>
                <tr><td>Researcher</td><td>Material summary</td><td>Search three types of materials</td></tr>
                <tr><td>Evaluator</td><td>Audience analysis & structure suggestions</td><td>Analyze target readers, writing timing</td></tr>
                <tr><td>Writer</td><td>Complete article</td><td>Write based on materials and structure</td></tr>
                <tr><td>Reviewer</td><td>Scoring report</td><td>Score from 5 dimensions, total 100, target ≥90</td></tr>
            </table>
            <h2>Review Dimensions</h2>
            <table>
                <tr><th>Dimension</th><th>Score</th><th>Description</th></tr>
                <tr><td>Topic fit</td><td>20pts</td><td>Accurately centered on topic, three stages reflect evolution logic</td></tr>
                <tr><td>Structure clarity</td><td>20pts</td><td>Three-part structure reasonable, transitions smooth</td></tr>
                <tr><td>Case quality</td><td>20pts</td><td>Cases specific and persuasive, with details and data</td></tr>
                <tr><td>Insight depth</td><td>20pts</td><td>Insights at each stage on point, unique perspective</td></tr>
                <tr><td>Readability & shareability</td><td>20pts</td><td>Language vivid, makes people want to share</td></tr>
            </table>
            <h2>Scoring Iteration Rules</h2>
            <table>
                <tr><th>Round</th><th>Pass Threshold</th><th>Result</th></tr>
                <tr><td>Round 1-5</td><td><90pts</td><td>Writer revises based on reviewer comments</td></tr>
                <tr><td>Round 6</td><td><90pts</td><td>End iteration, output current highest score version</td></tr>
                <tr><td>≥90pts</td><td>≥90pts</td><td><span class="badge badge-success">Qualified, deliver immediately</span></td></tr>
            </table>
            <h2>HTML Formatting Standards</h2>
            <p><span class="badge badge-warning">Important: HTML must use full inline CSS</span> - WeChat editor filters `<style>` tags, all styles must be written in style attributes.</p>
            <h3>template.html Structure</h3>
            <ul>
                <li>Cover: `<div>` with tag `<p>` + main title `<h1>` + subtitle `<p>` + description `<p>` + core proposition quote</li>
                <li>Sections: `<h2>` + bottom 2px black line</li>
                <li>Quote blocks: Light blue background `#f5f8ff` + left 4px blue line</li>
                <li>Highlight blocks: Dark background `#1a1a1a` + white text</li>
                <li>Tables: Light gray header `#f5f5f5`</li>
                <li>Separators: `━━━━━ ● ━━━━━`</li>
            </ul>
        </div>
        <div class="footer">
            <p>Multi-Agent WeChat | MIT License</p>
        </div>
    </div>
    <script>
        function switchLang(lang) {
            document.querySelectorAll('.content').forEach(el => {
                el.style.display = el.getAttribute('lang') === lang ? 'block' : 'none';
            });
            document.querySelectorAll('.lang-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
        }
    </script>
</body>
</html>