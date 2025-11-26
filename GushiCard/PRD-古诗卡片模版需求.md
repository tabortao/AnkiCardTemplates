# Anki 古诗卡片模版需求

ANKI 古诗卡片模版卡片字段包含`序号`、`诗名`、`作者`、`朝代`、`古诗内容`、`古诗音频`、`古诗解读`、`创作背景`、`作者简介`，请对现有的卡片内容模版进行如下修改，使得卡片美观漂亮，适应手机、平板等多种设备，界面让小学男生更加喜欢，并包含动态效果，最终生成优化后的`front_template.html`、`back_template.html`、`styles.css`、`preview.html`文件（参考Card templates - FAQ），用于创建ANKI古诗卡片。

- 正面可以显示`诗名`,有个按钮，点击后显示不完整的`古诗内容`，对古诗中个别字随机添加下划线，不显示对应的字。
- 背面内容可以显示`作者`、`朝代`、`古诗内容`、`古诗解读`、`创作背景`、`作者简介`、`序号`。

## 卡片内容现有模版如下

### 正面模板内容

文件名：`front_template.html`

```html
{{诗名}}
```

### 背面模板内容

文件名：`back_template.html`

```html
{{FrontSide}}

<hr id=answer>

{{朝代}}·{{作者}}
<br><br>
{{古诗内容}}
<br><br>
{{古诗解读}}
<br><br>
{{创作背景}}
<br><br>
{{作者简介}}
```
### 样式模版内容
```css
.card {
 font-family: "Microsoft YaHei", Arial, sans-serif;
 font-size: 5vw;
 text-align: center;
 color: black;
 line-height: 1.5;
 padding: 20px;
 max-width: 800px;
 margin: 0 auto;
 background-color: #DCEDC8;
}

```
