**结果概述**

- 已在 `HanziCard` 目录生成并优化 `front_template.html`、`back_template.html`、`styles.css`、`preview.html`，符合 PRD 的字段与设计要求，适配手机/平板，加入动画与童趣风格。
- 预览页面已通过本地服务器验证可正常访问。

**文件说明**

- `HanziCard/front_template.html`：正面模板，展示汉字与笔画演示，配儿童友好提示与装饰动效
  - 显示主字：`HanziCard/front_template.html:10` 的 `{{汉字}}`
  - 笔画演示：`HanziCard/front_template.html:18` 的 `{{笔画}}`
- `HanziCard/back_template.html`：背面模板，包含正面内容、拼音、自动拼接音频、备注与动效
  - 合并正面：`HanziCard/back_template.html:12` 的 `{{FrontSide}}`
  - 音频播放：`HanziCard/back_template.html:21` 使用 `{{音节}}{{声调}}` 拼接 CDN 音频
  - 拼音显示：`HanziCard/back_template.html:34` 的 `{{拼音}}`
  - 备注显示：`HanziCard/back_template.html:42` 的 `{{备注}}`
- `HanziCard/styles.css`：统一样式与响应式、AnkiDroid 适配、黑暗模式与动画
  - 卡片主题：`HanziCard/styles.css:41` 的 `.hanzi-card` 渐变与主题色
  - 汉字大字展示：`HanziCard/styles.css:53` 的 `.character` 大字号与动画
  - 笔画区块：`HanziCard/styles.css:56` 的 `.stroke-section` 与占位符
  - 拼音区块：`HanziCard/styles.css:78` 的 `.pinyin-content`
  - 音频布局：`HanziCard/styles.css:71` 的 `.audio-section` 与 `HanziCard/styles.css:73` 的 `audio` 控件适配
  - 移动端适配：`HanziCard/styles.css:112` 起的媒体查询
  - 黑暗模式：`HanziCard/styles.css:133`
- `HanziCard/preview.html`：可视化预览（静态示例），帮助在浏览器直接检查呈现效果
  - 正面示例：`HanziCard/preview.html:45` 的 “学” 字、`HanziCard/preview.html:48` 的笔画图
  - 背面示例：`HanziCard/preview.html:63` 起；示例音频：`HanziCard/preview.html:76` 使用 `shi4.mp3`

**模板要点**

- 结构遵循 Anki 模板规范：只写片段，不包含完整 HTML 文档结构（参考 `Card templates - FAQ/front_template.html` 与 `back_template.html` 的写法），顶层添加 `meta viewport` 以适配移动端。
- 样式集中在 CSS，避免内联样式；并提供响应式断点与 AnkiDroid 特殊适配。
- 动效与童趣设计：标题图标弹跳、表情浮动、星星闪烁，提升小学阶段学习趣味性。
- 音频拼接与播放：后端模板用 `音节 + 声调` 直接生成 CDN 链接，简化使用（`HanziCard/back_template.html:21`）。

**字段与数据要求**

- 必需字段（名称严格匹配大小写）：`汉字`、`拼音`、`音节`、`声调`、`笔画`、`备注`
- 使用建议
  - `汉字`：单个汉字，正面大字显示
  - `笔画`：图片或 SVG 的内容（支持 `<img>` 标签），占位样式见 `HanziCard/styles.css:59`
  - `音节`/`声调`：如 `shi` + `4`，自动生成 `https://hanyu-word-pinyin-short.cdn.bcebos.com/shi4.mp3`
  - `拼音`：支持声调符号，背面大字号居中显示
  - `备注`：例词、语境补充，留空有占位提示（`HanziCard/styles.css:82`）

**预览验证**

- 本地服务器已运行，可直接打开：
  - `http://localhost:3000/HanziCard/preview.html`
- 已验证页面可正常加载并展示动效与布局（通过本地预览检查）。

**使用步骤**

- 在 Anki 创建“汉字学习卡片”笔记类型。
- 添加 6 个字段：`汉字`、`拼音`、`音节`、`声调`、`笔画`、`备注`。
- 打开模板编辑器，分别将 `HanziCard/front_template.html`、`HanziCard/back_template.html`、`HanziCard/styles.css` 内容复制到对应区域。
- 创建卡片时填写对应字段；音频将按 `音节 + 声调` 自动拼接播放。

**设计与实现对齐**

- 参考了项目规则与 `Card templates - FAQ` 的断点、AnkiDroid 适配与预览方式，统一了布局结构与样式组织，保持一致的体验。
- 模板片段与普通 HTML 的差异已遵循：仅卡片片段，不含 `<html>/<body>` 等骨架，样式集中在 CSS。

**预览链接**

- 预览地址：`http://localhost:3000/HanziCard/preview.html`

**后续建议**

- 若笔画为 SVG 动画资源，可在 `stroke-container` 中直接插入，配合现有样式获得更佳演示效果。
- 若 CDN 音频未覆盖所有音节/声调组合，可考虑在 Anki 字段中提供备用 `{{音频}}` 字段，并在模板内条件显示。
