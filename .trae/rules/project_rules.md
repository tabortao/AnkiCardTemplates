Anki is a program which makes remembering things easy. Because it is a lot more efficient than traditional study methods, you can either greatly decrease your time spent studying, or greatly increase the amount you learn.

Card templates tell Anki which fields should appear on the front and back of your card, and control which cards will be generated when certain fields have text in them. By adjusting your card templates, you can alter the design and styling of many of your cards at once.

# 卡片制作步骤：
1. 工具-管理笔记模板-添加，设置一个模板。
2. 选择该模板，点击字段，对模板进行字段设计。
3. 选择该模板，点击卡片，对卡片进行设计。

# Card templates compilation principle(卡片模板编制原则)

- 字段应该保持简洁，样式应该在CSS中控制，而不是在HTML内联样式中。
- Anki 卡片模板包含:正面内容模板、背面内容模板、样式
- 正面内容模板使用的是 html 语言
- 背面内容模板使用的是 html 语言
- 样式使用的是 css 语言
- 编写的卡片模板，需分别编写正面内容模板、背面内容模板、样式
- 卡片需要满足黑暗模式和手机端的显示
- 卡片的样式需要满足响应式设计，能够在不同设备上正常显示
- 模板中使用的字段要前后对应，不能使用不存在的字段，字段名称是区分大小写的，而且需要与你在 Anki 中创建的字段完全匹配。具体查看：Reference\fields.md。

# 常见问题与解决方案 (FAQ) 📋

## 🔧 技术问题

### 1. 移动端显示问题
**问题描述**：AnkiDroid 和移动端显示不全，内容被顶部和底部按钮遮挡
**解决方案**：
- 添加 viewport 元标签：`<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">`
- 使用响应式设计，设置多个断点适配不同屏幕尺寸
- 为 AnkiDroid 特殊适配：减少边距，使用 `calc(100% - 2px)` 宽度设置
- 添加 `overflow-x: hidden` 防止水平滚动

### 2. 桌面端响应式问题
**问题描述**：桌面端非全屏状态下显示不完整
**解决方案**：
- 使用百分比宽度而非固定像素值
- 设置多个媒体查询断点：大屏幕(1201px+)、中等屏幕(769px-1200px)、小屏幕(769px-1024px)
- 添加 `max-height: calc(100vh - 20px)` 防止内容溢出

### 3. 字段名称不匹配
**问题描述**：模板中使用的字段在 Anki 中不显示
**解决方案**：
- 确保字段名称完全匹配，区分大小写
- 常用字段：`{{图片}}`、`{{音频}}`、`{{句子}}`、`{{翻译}}`
- 检查字段是否在笔记类型中正确创建

### 4. CSS 样式冲突
**问题描述**：样式在不同设备上显示不一致
**解决方案**：
- 使用 `box-sizing: border-box` 统一盒模型
- 避免内联样式，统一在 CSS 中管理
- 使用相对单位（em、rem、%）而非绝对单位（px）

## 🎨 设计优化

### 1. 色彩搭配建议
- 主色调：渐变背景 `linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)`
- 文字颜色：深色背景用白色 `#fff`，浅色背景用深灰 `#333`
- 强调色：蓝色系 `#2196f3`、绿色系 `#4caf50`

### 2. 字体设置最佳实践
- 中文优先：`"Microsoft YaHei", "Segoe UI", Arial, sans-serif`
- 移动端字体大小：标题 16-20px，内容 12-14px
- 桌面端字体大小：标题 24-32px，内容 16-18px

### 3. 间距和布局
- 卡片内边距：桌面端 20-25px，移动端 8-12px
- 元素间距：使用 margin-bottom 统一控制
- 圆角设置：桌面端 20px，移动端 8-12px

## 📱 设备适配

### 1. AnkiDroid 特殊适配
```css
/* AnkiDroid 专用样式 */
.ankidroid .card, .mobile .card {
    margin: 0 !important;
    padding: 8px !important;
    width: 100% !important;
    max-width: 100% !important;
    border-radius: 8px !important;
}
```

### 2. 响应式断点设置
- 超小屏幕：`@media (max-width: 480px)` - AnkiDroid 专用
- 移动端：`@media (max-width: 768px)` - 手机和小平板
- 桌面端小屏：`@media (min-width: 769px) and (max-width: 1024px)`
- 桌面端中屏：`@media (min-width: 769px) and (max-width: 1200px)`
- 桌面端大屏：`@media (min-width: 1201px)`

### 3. 图片适配
```css
.main-image {
    max-width: 100%;
    height: auto;
    object-fit: contain;
    /* 不同屏幕的最大高度 */
    max-height: 400px; /* 桌面端 */
    max-height: 200px; /* 移动端 */
    max-height: 150px; /* 超小屏幕 */
}
```

## 🛠️ 开发工具和调试

### 1. 本地预览设置
```bash
# 启动本地服务器
python -m http.server 3000
# 访问地址：http://localhost:3000
```

### 2. 浏览器调试技巧
- 按 F12 打开开发者工具
- 使用设备模拟器测试不同屏幕尺寸
- 检查元素样式和响应式断点

### 3. 常用测试设备尺寸
- iPhone SE: 375x667px
- iPhone 12: 390x844px
- iPad: 768x1024px
- 桌面端: 1920x1080px

## 📝 模板结构最佳实践

### 1. HTML 结构规范
```html
<!-- 添加 viewport 元标签 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<!-- 使用语义化的 class 名称 -->
<div class="card english-learning">
    <div class="title-section">
        <div class="title-icon">📚</div>
        <h2 class="card-title">标题</h2>
    </div>
    
    <div class="content-section">
        {{字段内容}}
    </div>
</div>
```

### 2. CSS 组织结构
```css
/* 1. 全局设置 */
html, body { /* 基础设置 */ }

/* 2. 基础卡片样式 */
.card { /* 主要样式 */ }

/* 3. 组件样式 */
.title-section { /* 标题区域 */ }
.content-section { /* 内容区域 */ }

/* 4. 响应式设计 */
@media (max-width: 768px) { /* 移动端 */ }
@media (min-width: 769px) { /* 桌面端 */ }
```

## 🚀 性能优化建议

### 1. CSS 优化
- 避免过深的选择器嵌套
- 使用 CSS 变量管理颜色和尺寸
- 合理使用 CSS 动画，避免影响性能

### 2. 图片优化
- 推荐使用 SVG 格式的图标
- 图片压缩和适当的尺寸设置
- 使用 `object-fit: contain` 保持比例

### 3. 代码维护
- 保持代码注释的完整性
- 使用一致的命名规范
- 定期检查和更新响应式断点

# 卡片模板编写示例 1

## 正面内容模板
字段有：字、Image、组词、例句

```html
<div style='font-family: "Arial"; font-size: 100px;'>{{字}}</div>
```

## 背面内容模板

```html
<div style="font-family: 'Arial'; font-size: 20px">{{Image}}</div>
<div style="font-family: 'Arial'; font-size: 50px">{{组词}}</div>

<div style="font-family: 'Arial'; font-size: 50px">{{例句}}</div>
```

## 样式

```css
.card {
  font-family: arial;
  font-size: 50px;
  text-align: center;
  color: black;
  background-color: white;
}
```

# 卡片模板编写示例 2

字段有：问题、选择题选项、原始内容、正确答案、我的回答、AI评估

## 正面内容模板

```html
<div class="question">{{问题}}</div>

<div class="options">{{选择题选项}}</div>
```

## 背面内容模板

```html
<div class="original-content">
  <div class="label">原始内容：</div>
  <div class="content">{{原始内容}}</div>
</div>

<hr />

<div class="answer">
  <div class="label">正确答案：</div>
  <div class="content">{{正确答案}}</div>
</div>

<hr />

<div class="my-answer">
  <div class="label">我的回答：</div>
  <div class="content">{{我的回答}}</div>
</div>

<hr />

<div class="ai-feedback">
  <div class="label">AI评估：</div>
  <div class="content">{{AI评估}}</div>
</div>
```

## 样式

```css
.card {
  font-family: "Microsoft YaHei", Arial, sans-serif;
  font-size: 16px;
  text-align: left;
  color: #333;
  line-height: 1.5;
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
  background-color: #fff;
}

.question {
  font-size: 18px;
  color: #2196f3;
  margin-bottom: 20px;
  padding: 15px;
  border-left: 4px solid #2196f3;
  background-color: #e3f2fd;
}

.options {
  margin: 15px 0;
}

.option-group {
  margin: 10px 0;
  padding: 8px 15px;
  background-color: #f5f5f5;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.option-group:hover {
  background-color: #e3f2fd;
}

.label {
  font-weight: bold;
  color: #1976d2;
  margin-bottom: 5px;
}

.content {
  white-space: pre-wrap;
  padding: 5px 0;
}

.original-content {
  background-color: #f5f5f5;
  padding: 10px;
  border-radius: 4px;
  margin-bottom: 15px;
}

.answer,
.my-answer {
  padding: 10px;
  border-radius: 4px;
  margin-bottom: 15px;
}

.answer {
  background-color: #e8f5e9;
}

.my-answer {
  background-color: #fff3e0;
}

.ai-feedback {
  background-color: #f3e5f5;
  padding: 10px;
  border-radius: 4px;
  margin-bottom: 15px;
}

hr {
  border: none;
  border-top: 1px solid #e0e0e0;
  margin: 15px 0;
}
```
