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
