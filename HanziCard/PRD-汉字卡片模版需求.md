# Anki 汉字卡片模版需求

ANKI 汉字卡片模版卡片字段包含`汉字`、`拼音`、`音节`、`声调`、`笔画`、`备注`，请对现有的卡片内容模版进行如下修改，使得卡片美观漂亮，适应手机、平板等多种设备，界面让小学生更加喜欢，并包含动态效果，最终生成优化后的`front_template.html`、`back_template.html`、`styles.css`、`preview.html`文件（参考Card templates - FAQ），用于创建ANKI汉字卡片。

## 卡片内容现有模版如下

### 正面模板内容

文件名：`front_template.html`

```html
{{笔画}}
```

### 背面模板内容

文件名：`back_template.html`

```html
{{FrontSide}}

<hr id="answer" />

<audio
  controls="controls"
  autoplay="autoplay"
  src="https://hanyu-word-pinyin-short.cdn.bcebos.com/{{音节}}{{声调}}.mp3"
  controls="controls"
></audio>

<br />

{{拼音}}
```
### 样式模版内容
```css
.card {
  font-family: arial;
  font-size: 100px;
  text-align: center;
  color: black;
  background-color: #fdf6e3;
}

img {
 width: 80%;
}
```
