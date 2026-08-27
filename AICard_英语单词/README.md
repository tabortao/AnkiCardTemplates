# AICard_英语单词 卡片模板使用指南

`AICard_英语单词` 是一套专为英语词汇与句型记忆设计的 Anki 卡片模板。采用柔和的**豆沙绿（Sage Green）**商务极简设计风格，集成了 **VoiceCraft 在线 TTS 引擎**，无需在本地保存音频文件，即可实现单词、例句的流式发音与翻面自动连播。

---

## 🌟 核心特性

- **商务极简设计**：采用护眼的低饱和度豆沙绿主题，去除冗余装饰与动画，排版清晰居中，提升沉浸专注度。
- **在线 TTS 动态发音**：集成 VoiceCraft（基于 Edge TTS）接口，点击播放图标即可实时流式发音，大幅节省本地存储空间。
- **背面自动连播序列**：翻至卡片背面时，系统会自动按顺序连播 **“英文单词 ➔ 中文释义 ➔ 英文例句”**，并同步高亮当前朗读项。
- **全平台自适应**：完美兼容 Anki Desktop（Windows / macOS / Linux）、AnkiDroid（Android）以及 AnkiMobile（iOS）。

![AICard_英语单词_正面](..\docs\image\AICard_英语单词_正面.png)
![AICard_英语单词_背面](..\docs\image\AICard_英语单词_背面.png)

---

## 📋 字段列表

创建卡片笔记类型（Note Type）时，请确保包含以下 **5 个字段**（字段名称需完全一致）：

| 字段名称 | 类型 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| `英语` | 必填 | 目标英文单词或短语 | `serendipity` |
| `汉语` | 必填 | 对应的中文释义 | `意外发现美好事物的机缘` |
| `图片` | 选填 | 辅助记忆的示意图 | `<img src="sample.jpg">` |
| `英语句子` | 选填 | 英文例句 | `Finding this book was pure serendipity.` |
| `英语句子翻译` | 选填 | 英文例句的中文翻译 | `找到这本书完全是一次意外的惊喜。` |

---

## 🛠️ 安装与配置步骤

### 第一步：新建笔记类型 (Note Type)
1. 打开 Anki 电脑端，点击顶部菜单栏的 **工具** ➔ **管理笔记类型**。
2. 点击右侧 **添加** ➔ 选择 **添加: 基础** ➔ 命名为 `AICard_英语单词`。
3. 选中新创建的类型，点击右侧 **字段**，添加/修改字段为：`英语`、`汉语`、`图片`、`英语句子`、`英语句子翻译`。

### 第二步：导入模板代码
1. 选中 `AICard_英语单词`，点击右侧 **卡片** 进入代码编辑页面。
2. **正面模板 (Front Template)**：清空并粘贴 `front_template.html` 代码。
3. **背面模板 (Back Template)**：清空并粘贴 `back_template.html` 代码。
4. **样式 (Styling)**：清空并粘贴 `styles.css` 代码。
5. 点击 **保存** 即可完成配置。

---

## ⚙️ TTS 引擎配置与自定义

模板默认调用 `https://tts.wangwangit.com/v1/audio/speech` 接口。

### 1. 声音模型配置
在正面与背面模板的 JavaScript 中，您可以根据偏好调整发音人角色：

| 语言 | 默认声音角色 | 常用可选角色 |
| :--- | :--- | :--- |
| **英文** (`voice`) | `en-US-AriaNeural` (自然美式女声) | `en-US-GuyNeural` (美式男声)<br>`en-GB-SoniaNeural` (英式女声)<br>`en-GB-RyanNeural` (英式男声) |
| **中文** (`voice`) | `zh-CN-XiaoxiaoNeural` (温和女声) | `zh-CN-YunxiNeural` (男声)<br>`zh-CN-YunjianNeural` (沉稳男声) |

### 2. 语速调节
若需调整朗读语速，可修改脚本中的 `speed` 参数（默认值为 `1.0`）：
```javascript
body: JSON.stringify({
    input: text,
    voice: voice,
    speed: 0.95, // 0.5 ~ 2.0，0.95 适合单词精听
    pitch: "0",
    style: "general"
})
```

### 3. 自动连播延时控制
背面模板通过 `autoPlayBackSequence()` 控制播放节奏。若希望调整单词与句子之间的停顿间隔，可修改延时毫秒数：
```javascript
await new Promise(r => setTimeout(r, 260)); // 260毫秒停顿
```

---

## 💡 注意事项与常见问题

1. **网络连接**：
   - 在线 TTS 发音依赖实时网络请求。如需完全离线复习，请在有网络时复习或借助批量工具生成本地音频。
2. **AnkiDroid 自动播放权限**：
   - 若在部分安卓设备上未触发自动连播，请检查 AnkiDroid 设置中的“高级 ➔ 启用 JavaScript”是否已开启。
3. **空白字段容错**：
   - 模板使用了 `{{#字段名}}...{{/字段名}}` 条件标签，例句或图片留空时，界面会自动收起对应区块，不会出现空白占位。