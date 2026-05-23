# 微信公众号HTML排版规范（微信编辑器兼容性）

## 核心原则

**所有CSS必须内联到style属性中**。微信编辑器会完全过滤掉`<style>`标签和外部样式表，这是最高频的排版踩坑点。

## 必须遵守的规则

### 1. 样式内联（最重要）
```html
<!-- ❌ 错误：会被微信编辑器完全移除 -->
<style>
  .highlight { background: #1a1a1a; color: #fff; }
</style>

<!-- ✅ 正确：所有样式写在style属性里 -->
<p style="background:#1a1a1a;color:#fff;padding:14px 16px;">内容</p>
```

### 2. 字体设置
```html
<!-- 使用系统字体栈，微信渲染环境有限 -->
style="font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Microsoft YaHei',sans-serif;"
```

### 3. 常用样式值

| 用途 | 推荐值 |
|------|--------|
| 正文颜色 | #555 / #333 |
| 辅助文字 | #666 / #999 |
| 强调色 | #3b82f6（蓝色） |
| 背景色 | #fafafa / #f5f8ff |
| 金句背景 | #1a1a1a（深色）+ 白色文字 |
| 边框色 | #e0e0e0 |
| 表头背景 | #f5f5f5 |

### 4. 结构规范
- 最大宽度：680px，居中
- 段落间距：margin-bottom: 16px
- 行高：line-height: 2（约26px）
- 正文字号：13-14px
- 一级标题：18px，加粗，下边框2px solid #1a1a1a
- 封面标题：26px，加粗

### 5. 表格写法
```html
<table style="width:100%;border-collapse:collapse;font-size:12px;border:1px solid #e0e0e0;margin-bottom:16px;">
  <tr>
    <td style="padding:8px 10px;background:#f5f5f5;color:#666;font-weight:600;border-bottom:1px solid #e0e0e0;">表头</td>
  </tr>
  <tr>
    <td style="padding:8px 10px;border-bottom:1px solid #eee;color:#333;">内容</td>
  </tr>
</table>
```

### 6. 分隔符
```html
<p style="font-size:11px;color:#ccc;text-align:center;margin:40px 0 0;padding:16px 0;">━━━━━ ● ━━━━━</p>
```

### 7. 金句块（深色背景）
```html
<p style="font-size:14px;color:#fff;font-weight:700;margin:0 0 16px;padding:14px 16px;background:#1a1a1a;">
  金句内容
</p>
```

### 8. 引用块（浅蓝背景+左侧蓝线）
```html
<p style="font-size:13px;color:#333;line-height:2;margin:0 0 16px;padding:12px;background:#f5f8ff;border-left:4px solid #3b82f6;">
  引用内容
</p>
```

### 9. emoji使用
- 可以使用emoji，但不要过度
- 常见：🏢 🚀 🔄 🌐 📊 ✅ ❌
- 在iOS和Android上显示效果较好，Windows端可能显示异常

### 禁止使用的特性
- CSS变量（var()）
- CSS动画（@keyframes）
- Flexbox/Grid（部分支持，但容易出错，用float或block替代）
- 外部字体加载（@font-face）
- 背景图（background-image）
- 透明色（rgba，部分支持）
- CSS渐变（background: linear-gradient(...)）—— 部分Android机型微信不渲染

### 复制到微信公众号草稿的正确方式

1. 用浏览器打开生成的HTML文件，全选复制（`Ctrl+A` → `Ctrl+C`）
2. 打开微信公众平台 → 素材管理 → 新建图文消息
3. 点击顶部工具栏的**"源码"按钮**（`<>` 图标）
4. 粘贴进去（`Ctrl+V`）
5. 切回富文本模式查看效果

**注意**：不是直接粘贴到正文，而是先点"源码"按钮进入HTML编辑模式粘贴，否则样式会乱。

## 验证方法

发布前在微信公众平台后台用**群发助手**预览，检查：
1. 样式是否移位
2. 表格是否对齐
3. 金句背景是否显示
4. emoji是否正常

## 快速检查清单

- [ ] 所有样式都在style属性里，没有<style>标签
- [ ] 字体使用系统字体栈
- [ ] 最大宽度不超过680px
- [ ] 表格有边框和padding
- [ ] 金句块用深色背景+白色文字
- [ ] 用微信编辑器预览验证
