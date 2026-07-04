# 移动端 App

> 移动端交互范式:iOS/安卓原生、卡片流、底部弹层、小组件等触屏优先的风格。
>
> 共 14 种风格。每种含:精髓 / 配色 / 字体 / 视觉特征 / 复刻要点 / 即用 Prompt,并附配套实践 demo 路径。
> 配色与字体仅供快速参考,完整数据见根目录 `styles.json`(机器可读,AI 可直接引用)。

---

### 1. iOS / HIG Native · iOS 原生
> 年代 常青　·　关键词:iOS HIG 苹果 系统原生

**精髓**:遵循 Apple Human Interface Guidelines：圆角卡片、SF 字体、克制配色、毛玻璃导航栏，原生、精致、高一致性。

**配色 Palette**: `#f2f2f7` `#ffffff` `#007aff` `#1c1c1e`

**推荐字体**:`SF Pro Text / SF Pro Display（系统字体）`

**视觉特征**

- 圆角卡片（12~16px）+ 系统阴影
- SF 字体，字重层级清晰
- 分组列表（inset grouped）
- 毛玻璃 TabBar/NavigationBar

**复刻要点**

- 圆角 12~16px，卡片白底 + 柔和阴影
- 配色 #f2f2f7 底 + #ffffff 卡 + #007aff 强调
- 列表用 grouped table，section header 大写灰
- TabBar 用 blur + 半透明白

**范例与适用**:iOS 系统应用（设置、App Store）、Apple 自家 App、大量遵循 HIG 的第三方 App。

**即用 Prompt**

```text
Build a page in "iOS / HIG Native" (iOS 原生) style. 遵循 Apple Human Interface Guidelines：圆角卡片、SF 字体、克制配色、毛玻璃导航栏，原生、精致、高一致性。 Visual: 圆角卡片（12~16px）+ 系统阴影; SF 字体，字重层级清晰; 分组列表（inset grouped）; 毛玻璃 TabBar/NavigationBar. Replicate: 圆角 12~16px，卡片白底 + 柔和阴影; 配色 #f2f2f7 底 + #ffffff 卡 + #007aff 强调; 列表用 grouped table，section header 大写灰; TabBar 用 blur + 半透明白. Palette: #f2f2f7, #ffffff, #007aff, #1c1c1e. Font: SF Pro Text / SF Pro Display（系统字体）.
```

> 实践 demo:[查看 `实践/demos/ios.html`](./实践/demos/ios.html) — 配色可在 demo 内点击复制 hex

---

### 2. Android Material · 安卓 Material
> 年代 2021+　·　关键词:安卓 materialyou 动态色

**精髓**:Android 原生遵循 Material You：动态取色、大圆角、FAB、手势导航，强调个性、表达与流畅手势。

**配色 Palette**: `#6750a4` `#eaddff` `#21005d` `#fef7ff`

**推荐字体**:`Roboto（M3 默认）`

**视觉特征**

- 动态色取自壁纸
- 大圆角卡片 + FAB 悬浮按钮
- 底部手势条 + 顶部大型应用栏
- 表达力强：Chip、Card、Bottom Sheet

**复刻要点**

- 配色 M3 tonal，圆角 16~28px
- FAB 在右下，Bottom Sheet 常驻手势
- 顶部 Large Top App Bar 可滚动收起
- 间距用 4dp 基准，间距 16/24dp

**范例与适用**:Android 系统应用、Google 全家桶、Material You 主题第三方 App。

**即用 Prompt**

```text
Build a page in "Android Material" (安卓 Material) style. Android 原生遵循 Material You：动态取色、大圆角、FAB、手势导航，强调个性、表达与流畅手势。 Visual: 动态色取自壁纸; 大圆角卡片 + FAB 悬浮按钮; 底部手势条 + 顶部大型应用栏; 表达力强：Chip、Card、Bottom Sheet. Replicate: 配色 M3 tonal，圆角 16~28px; FAB 在右下，Bottom Sheet 常驻手势; 顶部 Large Top App Bar 可滚动收起; 间距用 4dp 基准，间距 16/24dp. Palette: #6750a4, #eaddff, #21005d, #fef7ff. Font: Roboto（M3 默认）.
```

> 实践 demo:[查看 `实践/demos/android.html`](./实践/demos/android.html) — 配色可在 demo 内点击复制 hex

---

### 3. Fluent Design · Fluent 设计
> 年代 2017+　·　关键词:fluent 亚克力 微软 mica reveal

**精髓**:微软设计语言：Acrylic 亚克力半透明 + Reveal 高光 + 深度层次，统一 Win/Mobile，通透、连贯、轻盈。

**配色 Palette**: `#005fb8` `#ffffff` `#f3f3f3` `#202020`

**推荐字体**:`Segoe UI（系统字体）`

**视觉特征**

- Acrylic 半透明背景（亚克力模糊）
- Reveal：边框随鼠标/触摸高亮
- 深度：元素有 z 层与视差
- Mica 不透明材质用于窗口

**复刻要点**

- 背景 Acrylic：blur(30px) + 5~15% 着色
- 边框用 Reveal：border-image 或光感渐变
- 配色以系统强调色 #005fb8 为准
- 圆角 4~8px，比苹果小

**范例与适用**:Windows 11、Microsoft 365、Edge、部分跨平台 App。

**即用 Prompt**

```text
Build a page in "Fluent Design" (Fluent 设计) style. 微软设计语言：Acrylic 亚克力半透明 + Reveal 高光 + 深度层次，统一 Win/Mobile，通透、连贯、轻盈。 Visual: Acrylic 半透明背景（亚克力模糊）; Reveal：边框随鼠标/触摸高亮; 深度：元素有 z 层与视差; Mica 不透明材质用于窗口. Replicate: 背景 Acrylic：blur(30px) + 5~15% 着色; 边框用 Reveal：border-image 或光感渐变; 配色以系统强调色 #005fb8 为准; 圆角 4~8px，比苹果小. Palette: #005fb8, #ffffff, #f3f3f3, #202020. Font: Segoe UI（系统字体）.
```

> 实践 demo:[查看 `实践/demos/fluent.html`](./实践/demos/fluent.html) — 配色可在 demo 内点击复制 hex

---

### 4. Card Feed · 卡片信息流
> 年代 2020+　·　关键词:卡片流 feed tiktok 小红书 瀑布流

**精髓**:以卡片为基本单元的滚动信息流：瀑布流/单列卡片承载图文，沉浸、可滑动、内容为王，是内容 App 主流。

**配色 Palette**: `#ffffff` `#161823` `#ff2d55` `#f1f1f2`

**推荐字体**:`Inter / 系统默认（高可读）`

**视觉特征**

- 卡片为基本单元，圆角图片
- 瀑布流（两列不等高）或单列大卡
- 顶导航 + 底 Tab，沉浸式滚动
- 点赞/评论/收藏等高频微交互

**复刻要点**

- 瀑布流：CSS columns 或 grid + masonry
- 卡片圆角 12~16px，图片占主面积
- 滚动时顶/底栏可隐藏增强沉浸
- 加载用骨架屏，下拉刷新

**范例与适用**:小红书、TikTok、抖音、Instagram、Pinterest、大部分内容社区 App。

**即用 Prompt**

```text
Build a page in "Card Feed" (卡片信息流) style. 以卡片为基本单元的滚动信息流：瀑布流/单列卡片承载图文，沉浸、可滑动、内容为王，是内容 App 主流。 Visual: 卡片为基本单元，圆角图片; 瀑布流（两列不等高）或单列大卡; 顶导航 + 底 Tab，沉浸式滚动; 点赞/评论/收藏等高频微交互. Replicate: 瀑布流：CSS columns 或 grid + masonry; 卡片圆角 12~16px，图片占主面积; 滚动时顶/底栏可隐藏增强沉浸; 加载用骨架屏，下拉刷新. Palette: #ffffff, #161823, #ff2d55, #f1f1f2. Font: Inter / 系统默认（高可读）.
```

> 实践 demo:[查看 `实践/demos/cardfeed.html`](./实践/demos/cardfeed.html) — 配色可在 demo 内点击复制 hex

---

### 5. Bottom Sheet / Half-sheet · 底部半屏页
> 年代 2018+　·　关键词:底部弹层 bottomsheet 半屏 sheet

**精髓**:从底部滑出的半屏/全屏面板，用于次级操作、选择、表单，模态轻量、手势自然、不阻断上下文，移动端主流交互。

**配色 Palette**: `#ffffff` `#f2f2f7` `#1c1c1e` `#007aff`

**推荐字体**:`SF Pro / 系统默认`

**视觉特征**

- 底部滑出，可拖拽改变高度
- 顶部 grabber 拖把（圆角小条）
- 背景半透明遮罩，点击/下拉关闭
- 可堆叠：detents 多档高度（medium/large）

**复刻要点**

- 用 transform: translateY + 触摸拖拽
- detents：medium(50%)/large(95%) 两档
- 背景遮罩 rgba(0,0,0,.4)，随高度渐显
- 圆角顶部 20px + grabber 36x5

**范例与适用**:iOS 16+ 原生 sheet、Google Maps 选择面板、打车/支付确认、大部分 App 次级流程。

**即用 Prompt**

```text
Build a page in "Bottom Sheet / Half-sheet" (底部半屏页) style. 从底部滑出的半屏/全屏面板，用于次级操作、选择、表单，模态轻量、手势自然、不阻断上下文，移动端主流交互。 Visual: 底部滑出，可拖拽改变高度; 顶部 grabber 拖把（圆角小条）; 背景半透明遮罩，点击/下拉关闭; 可堆叠：detents 多档高度（medium/large）. Replicate: 用 transform: translateY + 触摸拖拽; detents：medium(50%)/large(95%) 两档; 背景遮罩 rgba(0,0,0,.4)，随高度渐显; 圆角顶部 20px + grabber 36x5. Palette: #ffffff, #f2f2f7, #1c1c1e, #007aff. Font: SF Pro / 系统默认.
```

> 实践 demo:[查看 `实践/demos/bottomsheet.html`](./实践/demos/bottomsheet.html) — 配色可在 demo 内点击复制 hex

---

### 6. Gesture-first Minimal · 手势优先极简
> 年代 2020+　·　关键词:手势极简 无按钮 全屏 swipable

**精髓**:极简到几乎无按钮，靠手势（滑动、长按、捏合）驱动，全屏沉浸、内容至上，是新一代「无感」设计。

**配色 Palette**: `#000000` `#ffffff` `#ff375f` `#f5f5f7`

**推荐字体**:`SF Pro / 系统默认（超克制）`

**视觉特征**

- 全屏沉浸，隐藏导航
- 手势驱动：左右滑切换、长按操作
- 极少的可见控件，浮于内容之上
- 动画跟手、有物理感

**复刻要点**

- 隐藏 TabBar/NavBar，手势替代
- 关键操作浮层化，闲置时淡出
- 手势配 spring 物理动效
- 内容铺满全屏，安全区留白

**范例与适用**:TikTok（全屏滑动）、Instagram Reels、Apple Books、Arc 移动版。

**即用 Prompt**

```text
Build a page in "Gesture-first Minimal" (手势优先极简) style. 极简到几乎无按钮，靠手势（滑动、长按、捏合）驱动，全屏沉浸、内容至上，是新一代「无感」设计。 Visual: 全屏沉浸，隐藏导航; 手势驱动：左右滑切换、长按操作; 极少的可见控件，浮于内容之上; 动画跟手、有物理感. Replicate: 隐藏 TabBar/NavBar，手势替代; 关键操作浮层化，闲置时淡出; 手势配 spring 物理动效; 内容铺满全屏，安全区留白. Palette: #000000, #ffffff, #ff375f, #f5f5f7. Font: SF Pro / 系统默认（超克制）.
```

> 实践 demo:[查看 `实践/demos/gestureminimal.html`](./实践/demos/gestureminimal.html) — 配色可在 demo 内点击复制 hex

---

### 7. Glass Mobile · 毛玻璃移动
> 年代 iOS 14+　·　关键词:毛玻璃移动 渐变背景 半透明卡 控制中心

**精髓**:彩色渐变背景上漂浮半透明毛玻璃卡片，iOS 控制中心那种感觉，通透、年轻、有层次，是 iOS 14+ 的标志风格。

**配色 Palette**: `#5e5ce6` `#ff9f0a` `#ff375f` `#0a0a0f`

**推荐字体**:`SF Pro Text（系统圆润）`

**视觉特征**

- 彩色渐变背景 + 半透明卡片漂浮
- backdrop-filter blur 毛玻璃
- 圆角大、卡片有层次阴影
- 年轻、通透、活力

**复刻要点**

- 背景 linear-gradient 多彩
- 卡片 rgba 半透明 + blur(20px)
- 圆角 16-20px + 柔和阴影
- 强调色用系统色

**范例与适用**:iOS 控制中心、天气/音乐 App、年轻向工具、小组件界面。

**即用 Prompt**

```text
Build a page in "Glass Mobile" (毛玻璃移动) style. 彩色渐变背景上漂浮半透明毛玻璃卡片，iOS 控制中心那种感觉，通透、年轻、有层次，是 iOS 14+ 的标志风格。 Visual: 彩色渐变背景 + 半透明卡片漂浮; backdrop-filter blur 毛玻璃; 圆角大、卡片有层次阴影; 年轻、通透、活力. Replicate: 背景 linear-gradient 多彩; 卡片 rgba 半透明 + blur(20px); 圆角 16-20px + 柔和阴影; 强调色用系统色. Palette: #5e5ce6, #ff9f0a, #ff375f, #0a0a0f. Font: SF Pro Text（系统圆润）.
```

> 实践 demo:[查看 `实践/demos/glassmobile.html`](./实践/demos/glassmobile.html) — 配色可在 demo 内点击复制 hex

---

### 8. Dark Mode Native · 原生暗色
> 年代 常青　·　关键词:原生暗色 oled纯黑 低对比 强调色 夜间

**精髓**:OLED 纯黑(#000)、低对比、强调色点缀、省电护眼，层级靠深浅灰而非阴影，夜间使用与媒体消费 App 的标配。

**配色 Palette**: `#000000` `#1c1c1e` `#0a84ff` `#f5f5f7`

**推荐字体**:`SF Pro Text（系统暗色适配）`

**视觉特征**

- OLED 纯黑 #000，省电
- 低对比，强调色点缀
- 层级靠深浅灰（#1c1c1e）而非阴影
- 减少蓝光，夜间友好

**复刻要点**

- 背景纯黑 #000，卡片 #1c1c1e
- 强调色单一（系统蓝/橙/绿）
- 不用黑阴影，用更深的灰做层级
- 文字 #f5f5f7，副文字 #8e8e93

**范例与适用**:夜间模式 App、媒体消费（视频/音乐）、开发者/极客向、社交媒体。

**即用 Prompt**

```text
Build a page in "Dark Mode Native" (原生暗色) style. OLED 纯黑(#000)、低对比、强调色点缀、省电护眼，层级靠深浅灰而非阴影，夜间使用与媒体消费 App 的标配。 Visual: OLED 纯黑 #000，省电; 低对比，强调色点缀; 层级靠深浅灰（#1c1c1e）而非阴影; 减少蓝光，夜间友好. Replicate: 背景纯黑 #000，卡片 #1c1c1e; 强调色单一（系统蓝/橙/绿）; 不用黑阴影，用更深的灰做层级; 文字 #f5f5f7，副文字 #8e8e93. Palette: #000000, #1c1c1e, #0a84ff, #f5f5f7. Font: SF Pro Text（系统暗色适配）.
```

> 实践 demo:[查看 `实践/demos/darknative.html`](./实践/demos/darknative.html) — 配色可在 demo 内点击复制 hex

---

### 9. Vibrant Gradient · 高饱和渐变卡
> 年代 2018+　·　关键词:高饱和渐变卡 vibrant 健身 金融 彩色卡 白字

**精髓**:彩色渐变卡片、白色文字、活力四射，健身/金融 App 常用数据卡用渐变提升情绪，激励、年轻、有能量。

**配色 Palette**: `#ff6a00` `#ee0979` `#2193b0` `#6dd5ed`

**推荐字体**:`Poppins / Inter（粗壮活力）`

**视觉特征**

- 卡片用饱和渐变填充
- 白字叠在渐变上
- 数据卡为主，激励感强
- 配色活力，情绪驱动

**复刻要点**

- 卡片 background: linear-gradient 饱和撞色
- 文字白色 + 微阴影保证可读
- 圆角 16-20px
- 配色橙红/蓝绿等活力对

**范例与适用**:健身（Keep/Nike）、金融/记账、运动、激励向产品。

**即用 Prompt**

```text
Build a page in "Vibrant Gradient" (高饱和渐变卡) style. 彩色渐变卡片、白色文字、活力四射，健身/金融 App 常用数据卡用渐变提升情绪，激励、年轻、有能量。 Visual: 卡片用饱和渐变填充; 白字叠在渐变上; 数据卡为主，激励感强; 配色活力，情绪驱动. Replicate: 卡片 background: linear-gradient 饱和撞色; 文字白色 + 微阴影保证可读; 圆角 16-20px; 配色橙红/蓝绿等活力对. Palette: #ff6a00, #ee0979, #2193b0, #6dd5ed. Font: Poppins / Inter（粗壮活力）.
```

> 实践 demo:[查看 `实践/demos/vibrant.html`](./实践/demos/vibrant.html) — 配色可在 demo 内点击复制 hex

---

### 10. Minimal Tab · 极简标签
> 年代 2020+　·　关键词:极简标签 纯图标 tab 大留白 独立app

**精髓**:底部纯图标 Tab（无文字或仅激活时显示）、大留白、极简，很多独立 App 和设计感强的应用采用，克制、优雅。

**配色 Palette**: `#ffffff` `#1a1a1a` `#007aff` `#f5f5f7`

**推荐字体**:`SF Pro / Inter（克制中性）`

**视觉特征**

- 底部 Tab 纯图标，激活时才显文字
- 大留白，内容呼吸
- 配色极简，零装饰
- 独立 App 设计感

**复刻要点**

- TabBar 纯图标，激活项加文字/颜色
- 背景近白，内容区大留白
- 强调色单一系统蓝
- 圆角克制，间距宽松

**范例与适用**:Things、独立 App、设计感工具、极简向效率产品。

**即用 Prompt**

```text
Build a page in "Minimal Tab" (极简标签) style. 底部纯图标 Tab（无文字或仅激活时显示）、大留白、极简，很多独立 App 和设计感强的应用采用，克制、优雅。 Visual: 底部 Tab 纯图标，激活时才显文字; 大留白，内容呼吸; 配色极简，零装饰; 独立 App 设计感. Replicate: TabBar 纯图标，激活项加文字/颜色; 背景近白，内容区大留白; 强调色单一系统蓝; 圆角克制，间距宽松. Palette: #ffffff, #1a1a1a, #007aff, #f5f5f7. Font: SF Pro / Inter（克制中性）.
```

> 实践 demo:[查看 `实践/demos/minimaltab.html`](./实践/demos/minimaltab.html) — 配色可在 demo 内点击复制 hex

---

### 11. Onboarding Story · 引导故事流
> 年代 常青　·　关键词:引导 onboarding 全屏插画 一句话 滑动 进度点

**精髓**:全屏插画 + 一句话、左右滑动、跳过按钮、进度点，首次启动引导的标准模式，讲故事、低门槛、建立第一印象。

**配色 Palette**: `#6c5ce7` `#fdcb6e` `#a29bfe` `#ffffff`

**推荐字体**:`Poppins / Nunito（友好圆润）`

**视觉特征**

- 全屏插画 + 一句话标题
- 左右滑动切换，进度点指示
- 跳过按钮始终可见
- 首次启动，建立认知

**复刻要点**

- 每屏：全屏插画 + 居中一句话
- 底部进度点 + 跳过按钮
- 滑动用 transform translateX
- 插画用 clay/扁平风格

**范例与适用**:所有 App 首次启动、功能介绍、权限请求引导。

**即用 Prompt**

```text
Build a page in "Onboarding Story" (引导故事流) style. 全屏插画 + 一句话、左右滑动、跳过按钮、进度点，首次启动引导的标准模式，讲故事、低门槛、建立第一印象。 Visual: 全屏插画 + 一句话标题; 左右滑动切换，进度点指示; 跳过按钮始终可见; 首次启动，建立认知. Replicate: 每屏：全屏插画 + 居中一句话; 底部进度点 + 跳过按钮; 滑动用 transform translateX; 插画用 clay/扁平风格. Palette: #6c5ce7, #fdcb6e, #a29bfe, #ffffff. Font: Poppins / Nunito（友好圆润）.
```

> 实践 demo:[查看 `实践/demos/onboarding.html`](./实践/demos/onboarding.html) — 配色可在 demo 内点击复制 hex

---

### 12. Widget / Glanceable · 小组件
> 年代 iOS 14+　·　关键词:小组件 widget glanceable 信息密度 即时 ios android

**精髓**:iOS/Android 桌面小组件，信息密度高、圆角、即时信息一览，强调"一眼获取"，是系统级的信息呈现方式。

**配色 Palette**: `#1c1c1e` `#0a84ff` `#34c759` `#ffd60a`

**推荐字体**:`SF Pro Text（紧凑系统字）`

**视觉特征**

- 小尺寸（2x2 / 4x2）信息卡
- 信息密度高但层级清晰
- 圆角（12-20px）
- 即时数据，一眼可读

**复刻要点**

- 卡片小尺寸 + 圆角 16px
- 信息分主次：大数字 + 小标签
- 配色深色卡 + 强调色数据
- 支持点击进 App 详情

**范例与适用**:iOS/Android 桌面小组件、天气/日历/健康/财务、系统工具。

**即用 Prompt**

```text
Build a page in "Widget / Glanceable" (小组件) style. iOS/Android 桌面小组件，信息密度高、圆角、即时信息一览，强调"一眼获取"，是系统级的信息呈现方式。 Visual: 小尺寸（2x2 / 4x2）信息卡; 信息密度高但层级清晰; 圆角（12-20px）; 即时数据，一眼可读. Replicate: 卡片小尺寸 + 圆角 16px; 信息分主次：大数字 + 小标签; 配色深色卡 + 强调色数据; 支持点击进 App 详情. Palette: #1c1c1e, #0a84ff, #34c759, #ffd60a. Font: SF Pro Text（紧凑系统字）.
```

> 实践 demo:[查看 `实践/demos/widget.html`](./实践/demos/widget.html) — 配色可在 demo 内点击复制 hex

---

### 13. Orbit / Bubble Nav · 悬浮气泡导航
> 年代 2020+　·　关键词:气泡导航 orbit 悬浮药丸 弹性 底部导航

**精髓**:底部导航栏变成悬浮的药丸/气泡形状，带弹性动画，脱离传统 Tab 栏，更年轻、更灵动、更有交互趣味。

**配色 Palette**: `#5b3fff` `#ffffff` `#7c5cff` `#0a0a0f`

**推荐字体**:`Inter / SF Pro（现代圆润）`

**视觉特征**

- 底部导航悬浮成药丸/气泡
- 与底部留间距，不贴边
- 弹性 spring 动画切换
- 选中项放大/变色

**复刻要点**

- TabBar position 绝对，底部留 16-24px 间距
- 圆角 999px 药丸形 + 阴影
- 切换用 spring 物理动效
- 选中项放大/背景色填充

**范例与适用**:部分潮流 App、Z 世代社交、设计感强的独立应用。

**即用 Prompt**

```text
Build a page in "Orbit / Bubble Nav" (悬浮气泡导航) style. 底部导航栏变成悬浮的药丸/气泡形状，带弹性动画，脱离传统 Tab 栏，更年轻、更灵动、更有交互趣味。 Visual: 底部导航悬浮成药丸/气泡; 与底部留间距，不贴边; 弹性 spring 动画切换; 选中项放大/变色. Replicate: TabBar position 绝对，底部留 16-24px 间距; 圆角 999px 药丸形 + 阴影; 切换用 spring 物理动效; 选中项放大/背景色填充. Palette: #5b3fff, #ffffff, #7c5cff, #0a0a0f. Font: Inter / SF Pro（现代圆润）.
```

> 实践 demo:[查看 `实践/demos/orbitnav.html`](./实践/demos/orbitnav.html) — 配色可在 demo 内点击复制 hex

---

### 14. Card Stack · 卡片堆叠
> 年代 2014+　·　关键词:卡片堆叠 cardstack tinder 透视 滑动 层级

**精髓**:卡片透视堆叠，滑动时带旋转和模糊层级，强力景深感，是 Tinder 式选择交互的视觉，沉浸、有趣、决策驱动。

**配色 Palette**: `#ff5a5f` `#ffffff` `#1a1a2e` `#ff6b6b`

**推荐字体**:`Inter / SF Pro（清晰）`

**视觉特征**

- 卡片层叠，下层缩小+模糊
- 滑动带旋转（如向右滑 +8deg）
- z-index 层级明确
- 强景深，决策感强

**复刻要点**

- 下层卡片 scale(.92) + translateY + blur(2px)
- 顶层卡片绝对定位居中
- 滑动用 transform rotate + translateX
- 左滑/右滑触发不同动作

**范例与适用**:Tinder、探探、内容浏览 App、选择/匹配类交互。

**即用 Prompt**

```text
Build a page in "Card Stack" (卡片堆叠) style. 卡片透视堆叠，滑动时带旋转和模糊层级，强力景深感，是 Tinder 式选择交互的视觉，沉浸、有趣、决策驱动。 Visual: 卡片层叠，下层缩小+模糊; 滑动带旋转（如向右滑 +8deg）; z-index 层级明确; 强景深，决策感强. Replicate: 下层卡片 scale(.92) + translateY + blur(2px); 顶层卡片绝对定位居中; 滑动用 transform rotate + translateX; 左滑/右滑触发不同动作. Palette: #ff5a5f, #ffffff, #1a1a2e, #ff6b6b. Font: Inter / SF Pro（清晰）.
```

> 实践 demo:[查看 `实践/demos/cardstack.html`](./实践/demos/cardstack.html) — 配色可在 demo 内点击复制 hex

---

*导航:返回 [README 索引](./README.md)*
