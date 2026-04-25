# 前端设计专业名词大全

> 持续更新的前端设计术语参考，用于编写高质量 AI Prompt。
> 术语越精准，AI 输出的视觉质量越高。

---

## 一、视觉风格 / Design Style

### 1.1 拟态家族

| 术语   | 英文                    | 说明                          |
| ---- | --------------------- | --------------------------- |
| 玻璃拟态 | Glassmorphism         | 半透明背景 + 高斯模糊 + 微妙边框，模拟毛玻璃质感 |
| 新拟态  | Neumorphism / Soft UI | 柔和的凸起/凹陷阴影，模拟物理按键的浮雕质感      |
| 黏土拟态 | Claymorphism          | 膨胀圆角 + 大面积柔和内阴影，模拟黏土/橡皮泥质感  |
| 极简拟物 | Skeuomorphism 2.0     | 在扁平化基础上保留微妙的物理世界暗示（纹理、光影）   |
| 纸张拟态 | Papermorphism         | 层叠纸张效果，通过阴影和微旋转模拟真实纸张堆叠     |
| 金属拟态 | Metallicmorphism      | 金属质感表面，带高光反射和拉丝纹理           |

### 1.2 现代风格

| 术语      | 英文                    | 说明                          |
| ------- | --------------------- | --------------------------- |
| 扁平化 2.0 | Flat 2.0              | 在纯扁平基础上加入微妙阴影和层次暗示          |
| 野性主义    | Brutalism             | 粗犷、无装饰、大字号、强对比，反精致的叛逆风格     |
| 极简主义    | Minimalism            | 大量留白，极少元素，呼吸感强，less is more |
| 极繁主义    | Maximalism            | 丰富装饰、多层叠加、信息密集，more is more |
| 千禧复古风   | Y2K Aesthetic         | 霓虹色、金属质感、像素字体，致敬 2000 年代视觉  |
| 赛博朋克    | Cyberpunk             | 霓虹色、暗色基底、故障效果、未来科技感         |
| 蒸汽波     | Vaporwave             | 粉紫渐变、希腊雕塑、复古网格、怀旧迷幻感        |
| 包豪斯风格   | Bauhaus               | 几何图形、三原色、功能主义、网格对齐          |
| 瑞士风格    | Swiss Style           | 严格网格、无衬线字体、不对称布局、客观摄影       |
| 孟菲斯风格   | Memphis Style         | 波普色彩、几何图案、波浪线、活泼俏皮          |
| 有机设计    | Organic Design        | 曲线、不规则形状、自然流动的边界，模仿自然界形态    |
| 工业风     | Industrial Design     | 暴露结构、粗粝质感、单色调、功能性优先         |
| 像素风     | Pixel Art             | 复古像素图形、8-bit 色彩、网格对齐        |
| 手绘风     | Hand-drawn / Sketchy  | 不规则线条、涂鸦感、白板笔记风格            |
| 编辑设计    | Editorial Design      | 杂志排版风格、大标题、多栏布局、图文混排        |
| 极致留白    | Extreme Whitespace    | 内容极度稀疏，超大行距和边距，奢侈品感         |
| 数据可视化风  | Data-driven Aesthetic | 以图表和数据为核心视觉元素，科技感十足         |

---

## 二、动效 / Animation & Motion

### 2.1 物理动效

| 术语   | 英文                         | 说明                     |
| ---- | -------------------------- | ---------------------- |
| 弹簧物理 | Spring Physics             | 基于弹力和阻力的缓动，带自然回弹和过冲    |
| 弹性回弹 | Elastic Snap / Rubber Band | 拖拽/滑动到边界后弹回，带橡皮筋般的物理手感 |
| 惯性滚动 | Momentum Scrolling         | 松手后内容按惯性继续滑动，逐渐减速停止    |
| 阻尼效果 | Damping                    | 运动逐渐减速的自然衰减效果          |
| 重力模拟 | Gravity Simulation         | 元素受重力影响下落、弹跳的物理效果      |
| 流体动画 | Liquid / Fluid Animation   | 模拟水/液体的流动、融合、分裂效果      |
| 布料模拟 | Cloth Simulation           | 元素像布料一样飘动、折叠、拉伸        |
| 粒子系统 | Particle System            | 漂浮的光点/星尘/粒子背景，增加梦幻感    |
| 磁力吸附 | Magnetic Snap              | 鼠标靠近时元素被"吸引"偏移，增强交互感   |
| 弹性过冲 | Overshoot                  | 动画超过目标位置再回弹，模拟弹性物理     |
| 摩擦力  | Friction                   | 滑动时模拟摩擦力导致的减速效果        |

### 2.2 入场/退场动效

| 术语      | 英文                               | 说明                               |
| ------- | -------------------------------- | -------------------------------- |
| 交错动画    | Stagger Animation                | 列表项依次延迟触发，形成波浪式入场节奏              |
| 滚动揭示    | Reveal on Scroll / Scroll Reveal | 元素滚入视口时才渐显/滑入，营造叙事节奏             |
| 交叉观察器动画 | Intersection Observer Animation  | 基于 Intersection Observer 的视口触发动画 |
| 淡入淡出    | Fade In / Fade Out               | 透明度渐变的经典入场/退场方式                  |
| 缩放入场    | Scale In / Pop In                | 从小到大缩放出现，带弹性更佳                   |
| 滑入滑出    | Slide In / Slide Out             | 从某个方向滑入/滑出画面                     |
| 翻转入场    | Flip In                          | 元素以 3D 翻转方式出现                    |
| 打字机效果   | Typewriter Effect                | 文字逐字出现，模拟打字输入                    |
| 揭幕效果    | Curtain Reveal                   | 像拉开幕布一样揭示下方内容                    |
| 逐一显现    | Sequential Reveal                | 子元素按顺序一个接一个出现                    |
| 爆炸式入场   | Burst / Explosion                | 元素从中心向四周爆散出现                     |
| 聚合入场    | Converge                         | 元素从四面八方汇聚到目标位置                   |

### 2.3 过渡/转场动效

| 术语       | 英文                                          | 说明                        |
| -------- | ------------------------------------------- | ------------------------- |
| 形态渐变     | Morphing                                    | 一个形状平滑变形为另一个形状            |
| 共享元素过渡   | Shared Element Transition / Hero Transition | 点击卡片后卡片"飞"到详情页，元素在页面间连贯流动 |
| 页面翻页     | Page Flip                                   | 3D 翻转式内容切换，模拟真实翻页         |
| 视图过渡 API | View Transitions API                        | 浏览器原生支持的页面/元素状态过渡         |
| 交叉淡入淡出   | Cross-fade                                  | 旧内容淡出的同时新内容淡入             |
| 擦除转场     | Wipe Transition                             | 新内容从一侧"擦除"覆盖旧内容           |
| 缩放转场     | Zoom Transition                             | 放大/缩小实现页面间的视觉连接           |
| 变形转场     | Shape Morph Transition                      | 通过形状变形连接两个页面状态            |
| 色彩过渡     | Color Transition                            | 通过颜色变化平滑连接不同状态            |
| 液态转场     | Liquid Transition                           | 像水滴融合一样的有机形态过渡            |

### 2.4 微交互

| 术语   | 英文                        | 说明                                  |
| ---- | ------------------------- | ----------------------------------- |
| 微交互  | Micro-interaction         | 按钮 hover、点赞心跳等细微但反馈感强的交互            |
| 点击涟漪 | Ripple Effect             | 点击位置扩散出水波纹效果（Material Design 标志性效果） |
| 悬停浮起 | Hover Lift                | 鼠标悬停时元素轻微上浮并增加阴影                    |
| 按压缩放 | Press Scale               | 按下时元素缩小，松开恢复，模拟物理按压                 |
| 心跳动效 | Heart Beat / Pulse        | 元素像心跳一样有节奏地缩放                       |
| 抖动反馈 | Shake Feedback            | 操作错误时元素左右抖动，提供直观的负面反馈               |
| 发光反馈 | Glow Feedback             | hover/click 时元素边缘发光，提供视觉确认          |
| 旋转加载 | Spinner / Rotating Loader | 旋转的加载指示器                            |
| 进度动画 | Progress Animation        | 填充进度条或环形进度指示                        |
| 计数滚动 | Count Up / Rolling Number | 数字从旧值滚动到新值，常用于仪表盘                   |
| 复选打勾 | Checkmark Animation       | 选中时打勾动画从无到有绘制出来                     |
| 开关切换 | Toggle Switch             | 滑块平滑过渡到另一端                          |

### 2.5 缓动函数

| 术语     | 英文                  | 说明                                        |
| ------ | ------------------- | ----------------------------------------- |
| 缓入     | Ease In             | 慢启动加速，如 ease-in、cubic-bezier(0.42,0,1,1)  |
| 缓出     | Ease Out            | 快启动减速，如 ease-out、cubic-bezier(0,0,0.42,1) |
| 缓入缓出   | Ease In Out         | 慢启动→加速→慢停止，最自然的运动曲线                       |
| 线性     | Linear              | 匀速运动，通常只适合进度条等少数场景                        |
| 弹性缓动   | Elastic Ease        | 带弹性回弹的缓动，超出目标后振荡归位                        |
| 回弹缓动   | Back Ease           | 启动前先略微反向运动，增加蓄力感                          |
| 弹跳缓动   | Bounce Ease         | 到达终点后多次弹跳衰减                               |
| 自定义贝塞尔 | Custom Cubic-bezier | 精确控制加速减速曲线                                |
| 弹簧阻尼   | Spring Damping      | 指定 stiffness、damping、mass 的物理弹簧模型         |

---

## 三、布局 / Layout

### 3.1 网格与分区

| 术语      | 英文                    | 说明                      |
| ------- | --------------------- | ----------------------- |
| 便当盒网格   | Bento Grid            | 不等大小的卡片网格拼合，类似苹果产品展示页   |
| 瀑布流     | Masonry Layout        | Pinterest 式不等高卡片流式排列    |
| 12列栅格   | 12-Column Grid        | 传统网格系统，灵活的列组合           |
| 圣杯布局    | Holy Grail Layout     | 头部、底部、中间三栏（侧边+主内容）的经典布局 |
| 不对称布局   | Asymmetric Layout     | 刻意打破对称，制造动感和视觉张力        |
| 分屏布局    | Split Screen          | 左右/上下各占一半，常用于对比展示       |
| 全出血通栏   | Full-bleed Section    | 内容延伸到屏幕边缘，无左右留白         |
| 通栏 + 居中 | Full-width + Centered | 背景通栏但内容居中，兼顾视觉冲击与阅读舒适度  |
| Z型浏览路径  | Z-Pattern             | 视觉引导呈 Z 字形，适合信息展示页      |
| F型浏览路径  | F-Pattern             | 视觉引导呈 F 字形，适合文本密集型页面    |
| 黄金比例    | Golden Ratio Layout   | 基于 1:1.618 比例划分空间       |
| 模块化布局   | Modular Layout        | 将页面拆分为独立可复用的功能模块        |

### 3.2 响应式与自适应

| 术语     | 英文                   | 说明                             |
| ------ | -------------------- | ------------------------------ |
| 容器查询   | Container Query      | 根据父容器而非视口响应式适配                 |
| 移动优先   | Mobile First         | 从移动端开始设计，逐步增强到桌面端              |
| 桌面优先   | Desktop First        | 从桌面端开始设计，逐步适配移动端               |
| 流式布局   | Fluid Layout         | 使用百分比/rem/vw 等相对单位，尺寸随视口平滑变化   |
| 自适应断点  | Adaptive Breakpoints | 在特定断点切换不同的固定布局                 |
| 响应式图片  | Responsive Images    | picture 元素 + srcset 根据设备加载不同尺寸 |
| 内容重排   | Content Reflow       | 不同屏幕下内容顺序和排列方式重新组织             |
| 优先内容可见 | Above the Fold       | 确保首屏可见区域包含最重要内容                |

### 3.3 特殊布局模式

| 术语      | 英文                           | 说明                      |
| ------- | ---------------------------- | ----------------------- |
| 粘性堆叠    | Sticky Stack                 | 滚动时卡片堆叠吸附在顶部，逐层覆盖       |
| 粘性侧边栏   | Sticky Sidebar               | 滚动时侧边栏固定不动，保持导航可见       |
| 首屏大图区   | Hero Section                 | 页面第一屏的核心视觉区域，大图+主标题+CTA |
| 固定底部操作栏 | Fixed Bottom Bar             | 底部固定的操作/导航栏，移动端常见       |
| 浮动操作按钮  | FAB (Floating Action Button) | 悬浮在右下角的主操作按钮            |
| 抽屉/侧滑面板 | Drawer / Side Panel          | 从侧边滑出的面板，不遮挡主内容         |
| 底部弹出面板  | Bottom Sheet                 | 从底部滑出的面板，移动端常见          |
| 手风琴     | Accordion                    | 点击展开/折叠内容区域             |
| 标签页切换   | Tabs                         | 通过标签切换不同内容面板            |
| 轮播图     | Carousel / Slider            | 自动或手动滑动的图片/卡片序列         |
| 时间线     | Timeline                     | 按时间顺序排列的垂直/水平轴内容        |
| 看板      | Kanban Board                 | 多列拖拽式任务管理布局             |
| 无限滚动    | Infinite Scroll              | 滚动到底部自动加载更多内容           |
| 虚拟滚动    | Virtual Scrolling            | 只渲染可视区域 DOM，优化长列表性能     |

---

## 四、色彩与光影 / Color & Light

### 4.1 色彩模式与风格

| 术语    | 英文                              | 说明                   |
| ----- | ------------------------------- | -------------------- |
| 暗色优先  | Dark Mode First                 | 以深色为基底设计，强调发光元素和对比度  |
| 暗色模式  | Dark Mode                       | 深色背景+浅色文字的低亮度配色方案    |
| 亮色模式  | Light Mode                      | 浅色背景+深色文字的传统配色方案     |
| 双色调   | Duotone                         | 只用两种颜色渲染图像，强烈的视觉冲击力  |
| 单色调   | Monotone                        | 只用一种颜色的不同明度/饱和度      |
| 渐变    | Gradient                        | 两种或多种颜色平滑过渡          |
| 极光渐变  | Aurora Gradient / Gradient Mesh | 多色渐变叠加流动，模拟北极光的色彩过渡  |
| 网格渐变  | Mesh Gradient                   | 多控制点的复杂渐变，色彩过渡如油画般柔和 |
| 同色系配色 | Analogous Colors                | 色轮上相邻颜色的和谐配色         |
| 互补色配色 | Complementary Colors            | 色轮上对立颜色的强烈对比         |
| 三角色配色 | Triadic Colors                  | 色轮上等距三种颜色的平衡配色       |
| 撞色    | Color Blocking                  | 大面积高饱和对比色块拼接         |
| 莫兰迪色系 | Morandi Palette                 | 低饱和度灰调色系，优雅柔和        |
| 赛博霓虹  | Cyber Neon                      | 高饱和度荧光色 + 深色背景       |
| 色相偏移  | Hue Rotation / Color Shift      | 颜色随时间/交互缓慢变化，梦幻迷幻感   |
| 彩虹渐变  | Rainbow Gradient                | 全色谱渐变，常用于进度条或装饰元素    |

### 4.2 光影效果

| 术语    | 英文             | 说明                       |
| ----- | -------------- | ------------------------ |
| 环境光晕  | Ambient Glow   | 元素周围的柔和发光，营造氛围感          |
| 霓虹发光  | Neon Glow      | 多层 box-shadow 叠加模拟霓虹灯管光晕 |
| 柔和投影  | Soft Shadow    | 大扩散、低透明度阴影，让元素"浮"起来      |
| 硬阴影   | Hard Shadow    | 锐利边缘的投影，增加对比度和层次感        |
| 长阴影   | Long Shadow    | 向某个方向延伸的长条阴影，扁平化设计的经典元素  |
| 内发光   | Inner Glow     | inset box-shadow 制造内发光效果 |
| 多层阴影  | Layered Shadow | 多个不同参数的阴影叠加，比单阴影更自然      |
| 文字阴影  | Text Shadow    | 文字上的投影，增加可读性或装饰感         |
| 玻璃着色  | Glass Tint     | 半透明层叠加带色底色，增加层次和色彩氛围     |
| 暗角    | Vignette       | 画面四角渐暗，聚焦中心内容，增加电影感      |
| 焦散光   | Caustics       | 水面折射产生的光斑效果              |
| 镜头光晕  | Lens Flare     | 模拟相机镜头的眩光效果              |
| 丁达尔效应 | Tyndall Effect | 模拟光线穿过雾气/灰尘的光柱效果         |
| 焦点光   | Spot Light     | 聚光灯式的高亮区域，强调特定内容         |

---

## 五、质感与纹理 / Texture & Pattern

| 术语    | 英文                            | 说明                             |
| ----- | ----------------------------- | ------------------------------ |
| 噪点叠加  | Noise Overlay / Grain Texture | 全屏叠加极淡噪点，增加肌理质感避免"太干净"         |
| 胶片颗粒  | Film Grain                    | 模拟胶片相机的颗粒质感                    |
| 微光边框  | Subtle Border                 | 1px 半透明白色/深色边框，区分层级但不突兀        |
| 渐变边框  | Gradient Border               | 用渐变色做边框，通过 border-image 或伪元素实现 |
| 虚线边框  | Dashed Border                 | 虚线样式边框，常用于拖拽区域或占位区域            |
| 发光边框  | Glowing Border                | 动态发光的边框效果，强调聚焦状态               |
| 磨砂模糊  | Frosted Blur                  | backdrop-filter: blur() 的核心效果  |
| 拉丝金属  | Brushed Metal                 | 金属表面的拉丝纹理                      |
| 大理石纹理 | Marble Texture                | 天然大理石的流动纹理质感                   |
| 水磨石纹理 | Terrazzo Pattern              | 彩色碎片嵌入基底的水磨石图案                 |
| 波点图案  | Polka Dot Pattern             | 规则排列的圆点图案背景                    |
| 条纹图案  | Stripe Pattern                | 横向/纵向/对角线条纹背景                  |
| 棋盘格   | Checkerboard                  | 经典黑白交替的棋盘格图案                   |
| 等高线纹理 | Topographic Lines             | 地形图等高线风格的曲线纹理                  |
| 碳纤维纹理 | Carbon Fiber                  | 碳纤维编织纹理，科技感强                   |
| 编织纹理  | Woven Pattern                 | 交织编织效果的纹理                      |
| 半调图案  | Halftone Pattern              | 印刷网点效果的图案                      |
| 水彩晕染  | Watercolor Wash               | 模拟水彩画的不规则边缘和晕染效果               |

---

## 六、排版 / Typography

### 6.1 字体风格

| 术语    | 英文                | 说明                                 |
| ----- | ----------------- | ---------------------------------- |
| 衬线体   | Serif             | 笔画末端有装饰线的经典字体（如宋体、Times New Roman） |
| 无衬线体  | Sans-serif        | 笔画简洁无装饰的现代字体（如黑体、Helvetica）        |
| 等宽字体  | Monospace         | 每个字符等宽，常用于代码展示                     |
| 展示字体  | Display Font      | 用于大标题的装饰性字体，个性强                    |
| 可变字体  | Variable Font     | 单一字体文件包含多轴变化（粗细、宽度等）               |
| 网络字体  | Web Font          | 通过 @font-face 或 CDN 加载的自定义字体       |
| 系统字体栈 | System Font Stack | 使用操作系统原生字体，零加载延迟                   |
| 像素字体  | Pixel Font        | 像素风格的复古字体                          |
| 手写体   | Handwriting Font  | 模拟手写风格的字体                          |
| 黑板体   | Chalkboard Font   | 模拟粉笔/黑板书写风格                        |

### 6.2 排版技巧

| 术语       | 英文                          | 说明                               |
| -------- | --------------------------- | -------------------------------- |
| 文字渐变     | Text Gradient               | background-clip: text 实现文字填充渐变色  |
| 描边文字     | Outline / Stroke Typography | -webkit-text-stroke 实现只有描边没有填充的字 |
| 文字描边发光   | Neon Text                   | 文字带发光描边效果                        |
| 镂空文字     | Knockout Text               | 文字部分透明，露出下方背景/图片                 |
| 竖排文字     | Vertical Text               | 竖向排列的文字，中日韩排版或装饰用途               |
| 首字下沉     | Drop Cap                    | 段落首字母放大并下沉，经典编辑排版                |
| 文字裁切     | Text Clipping               | 文字形状作为蒙版裁切背景                     |
| 大字报排版    | Big Type / Gigantic Heading | 超大字号标题，标题即视觉                     |
| 行宽控制     | Measure / Line Length       | 控制 45-75 字符的最佳阅读行宽               |
| 行高 / 行间距 | Line Height / Leading       | 行与行之间的间距                         |
| 字间距      | Letter Spacing / Tracking   | 字符之间的水平间距                        |
| 词间距      | Word Spacing                | 英文单词之间的间距                        |
| 段间距      | Paragraph Spacing           | 段落之间的垂直间距                        |
| 两端对齐     | Justified Text              | 文本左右两端都对齐                        |
| 渐显文字     | Text Reveal                 | 文字逐字/逐行渐显的效果                     |
| 高亮标记     | Highlight / Mark            | 荧光笔标记效果，用于强调关键词                  |
| 混排大小写    | Mixed Case                  | 标题中混合使用大小写，增加视觉层次                |

---

## 七、3D 与沉浸式 / 3D & Immersive

### 7.1 3D 效果

| 术语        | 英文                      | 说明                                  |
| --------- | ----------------------- | ----------------------------------- |
| 倾斜陀螺仪效果   | Tilt / Gyroscope Effect | 鼠标移动时元素微微 3D 倾斜，模拟卡片悬浮              |
| 深度分层      | Depth Layering          | 多层 z 轴叠加 + 视差，制造空间纵深                |
| 3D 翻转卡片   | 3D Card Flip            | CSS perspective + rotateY 实现卡片正反面翻转 |
| WebGL 着色器 | WebGL Shader            | 基于 GPU 的实时渲染效果，如波浪、扭曲、热力图           |
| 3D 产品展示   | 3D Product Viewer       | 可旋转、缩放的 3D 产品模型展示                   |
| 视差景深      | Parallax Depth          | 背景层移动慢、前景层移动快的 3D 纵深感               |
| 3D 透视走廊   | Perspective Tunnel      | 向远方延伸的透视走廊效果                        |
| 3D 粒子场景   | 3D Particle Scene       | Three.js 等创建的 3D 粒子效果               |
| 球面映射      | Sphere Mapping          | 在球体表面映射纹理/内容                        |
| 环境贴图      | Environment Map         | 模拟周围环境在物体表面的反射                      |
| 体素风       | Voxel Style             | 3D 像素方块风格                           |
| 低多边形      | Low Poly                | 低面数的几何风格化 3D 模型                     |

### 7.2 沉浸式体验

| 术语      | 英文                      | 说明                              |
| ------- | ----------------------- | ------------------------------- |
| 沉浸式滚动   | Immersive Scroll        | 全屏分章节，滚动驱动叙事，类似 Apple 产品页       |
| 滚动劫持    | Scroll Jacking          | 接管滚动行为，每次滚动对齐到下一屏/章节            |
| 全屏故事    | Full-screen Story       | 类似 Instagram/Snapchat 的全屏垂直滑动故事 |
| 自定义鼠标跟随 | Custom Cursor Follow    | 自定义光标或光晕跟随鼠标移动                  |
| 鼠标追踪光效  | Mouse-tracked Lighting  | 光源跟随鼠标位置，照亮/投射阴影                |
| 磁力按钮    | Magnetic Button         | 鼠标靠近时按钮被"吸引"偏移                  |
| 交互式背景   | Interactive Background  | 背景随鼠标/滚动/点击实时变化                 |
| 滚动驱动动画  | Scroll-driven Animation | 动画进度与滚动位置绑定                     |
| 视差滚动    | Parallax Scrolling      | 不同层以不同速度移动，制造深度感                |
| 缩放式滚动   | Zoom Scrolling          | 滚动时画面逐渐放大/缩小，推进或拉远镜头            |
| 水平滚动    | Horizontal Scroll       | 鼠标滚轮或拖拽实现横向滚动                   |
| 全景浏览    | Panoramic View          | 360度全景图片/视频浏览体验                 |

---

## 八、组件模式 / Component Patterns

### 8.1 卡片与容器

| 术语     | 英文                           | 说明                   |
| ------ | ---------------------------- | -------------------- |
| 可展开卡片  | Expandable Card              | 点击后卡片展开显示更多内容        |
| 悬浮卡片   | Floating Card                | 带柔和阴影的浮动卡片，hover 时提升 |
| 玻璃卡片   | Glass Card                   | 玻璃拟态风格的半透明卡片         |
| 个人资料卡  | Profile Card                 | 展示头像、姓名、简介的卡片        |
| 统计卡片   | Stat Card / KPI Card         | 展示关键指标的数字卡片          |
| 预览卡片   | Preview Card                 | 带缩略图和摘要的内容预览         |
| 可拖拽卡片  | Draggable Card               | 支持拖拽排序或移动的卡片         |
| 翻转卡片   | Flip Card                    | 正反面可翻转的卡片            |
| 堆叠卡片   | Stacked Cards / Card Stack   | 像扑克牌一样堆叠，可滑动切换       |
| 横向滚动卡片 | Horizontally Scrolling Cards | 卡片列表横向滑动浏览           |

### 8.2 导航

| 术语     | 英文                            | 说明               |
| ------ | ----------------------------- | ---------------- |
| 汉堡菜单   | Hamburger Menu                | 三横线图标展开的导航菜单     |
| 底部导航栏  | Bottom Navigation             | 移动端底部的标签式导航      |
| 顶部导航栏  | Top Navbar / Header           | 页面顶部固定的导航栏       |
| 面包屑    | Breadcrumb                    | 显示当前页面在层级中的路径    |
| 侧边栏导航  | Sidebar Navigation            | 侧边的垂直导航菜单        |
| 标签式导航  | Tab Navigation                | 水平标签页切换          |
| 全屏导航覆盖 | Full-screen Nav Overlay       | 点击后全屏覆盖的导航菜单     |
| 进度导航   | Progress Nav / Step Indicator | 显示多步骤流程进度的导航     |
| 锚点导航   | Anchor Navigation             | 点击滚动到页面内对应锚点位置   |
| 下拉菜单   | Dropdown Menu                 | 点击/hover 展开的二级菜单 |
| 超大菜单   | Mega Menu                     | 多列复杂下拉菜单，常见于电商   |

### 8.3 表单与输入

| 术语     | 英文                           | 说明                 |
| ------ | ---------------------------- | ------------------ |
| 浮动标签   | Floating Label               | 输入时标签上浮到输入框上方，节省空间 |
| 内联验证   | Inline Validation            | 实时在输入框旁显示验证结果      |
| 自动补全   | Autocomplete                 | 输入时弹出建议列表          |
| 步进器    | Stepper                      | 增减数字的 +/- 按钮       |
| 范围滑块   | Range Slider                 | 拖动选择数值范围的滑块        |
| 切换开关   | Toggle Switch                | 开/关状态的滑动切换         |
| 复选框组   | Checkbox Group               | 多选选项组              |
| 单选按钮组  | Radio Button Group           | 单选选项组              |
| 搜索框    | Search Bar                   | 带搜索图标的输入框，可带下拉建议   |
| 多步表单   | Multi-step Form              | 分步引导填写的表单，降低认知负荷   |
| 标签输入   | Tag Input                    | 输入后生成标签芯片的输入方式     |
| 文件上传区域 | File Upload Zone / Drop Zone | 拖拽上传文件的区域          |
| 颜色选择器  | Color Picker                 | 可视化选择颜色的控件         |
| 日期选择器  | Date Picker                  | 日历式日期选择控件          |
| 评分组件   | Rating / Star Rating         | 星级或其他形式的评分控件       |

### 8.4 反馈与状态

| 术语       | 英文                         | 说明                  |
| -------- | -------------------------- | ------------------- |
| 骨架屏      | Skeleton Loading           | 用灰色占位块预演布局，加载后再渐显内容 |
| 加载动画     | Loading Spinner / Progress | 各种形式的加载状态指示         |
| 进度条      | Progress Bar               | 线性进度指示器             |
| 环形进度     | Circular Progress          | 环形/圆形进度指示器          |
| Toast 通知 | Toast / Snackbar           | 底部或角落弹出的短暂提示信息      |
| 模态对话框    | Modal Dialog               | 覆盖在页面上的居中对话框        |
| 确认对话框    | Confirmation Dialog        | 要求用户确认操作的弹窗         |
| 行内提示     | Inline Toast               | 在操作位置附近显示的行内反馈      |
| 空状态      | Empty State                | 无数据时展示的引导性空状态画面     |
| 错误状态     | Error State                | 出错时的友好错误展示          |
| 成功状态     | Success State              | 操作成功后的确认反馈          |
| 脉冲指示器    | Pulse Indicator            | 有节奏地闪烁/脉动的状态指示      |
| 数字徽标     | Badge / Dot Indicator      | 红点或数字角标，提示未读/更新     |

### 8.5 数据展示

| 术语    | 英文                  | 说明              |
| ----- | ------------------- | --------------- |
| 数据表格  | Data Table          | 可排序、筛选、分页的数据表格  |
| 迷你图   | Sparkline           | 内嵌在文本/卡片中的微型趋势图 |
| 仪表盘   | Gauge / Dashboard   | 关键指标的仪表盘展示      |
| 热力图   | Heatmap             | 用颜色深浅表示数据密度/强度  |
| 树状图   | Treemap             | 用嵌套矩形表示层级数据     |
| 桑基图   | Sankey Diagram      | 展示流量/资源流向的可视化   |
| 雷达图   | Radar Chart         | 多维度对比的蛛网图       |
| 环形图   | Donut Chart         | 空心饼图，中间可显示汇总数据  |
| 面积图   | Area Chart          | 带填充面积的趋势图       |
| 柱状图   | Bar Chart           | 垂直/水平柱状对比图      |
| 折线图   | Line Chart          | 趋势变化的折线图        |
| 可视化面板 | Visualization Panel | 综合多种图表的数据面板     |

---

## 九、CSS 技术术语 / CSS Techniques

### 9.1 现代 CSS 特性

| 术语         | 英文                         | 说明                                  |
| ---------- | -------------------------- | ----------------------------------- |
| CSS 变量     | CSS Custom Properties      | --var-name 定义的可复用设计令牌               |
| 容器查询       | Container Query @container | 根据父容器尺寸响应式适配                        |
| 子网格        | Subgrid                    | 子元素继承父网格的轨道定义                       |
| 级联层        | CSS Layers @layer          | 控制样式的优先级层级                          |
| 逻辑属性       | Logical Properties         | 根据书写方向定义的属性（inline-size 等）          |
| 色彩空间       | Color Functions            | oklch()、lab() 等新色彩函数                |
| 滚动驱动动画     | Scroll-driven Animations   | animation-timeline: scroll()        |
| 视图过渡       | View Transitions           | document.startViewTransition() 页面过渡 |
| 选择器嵌套      | CSS Nesting                | 原生 CSS 嵌套写法                         |
| :has() 选择器 | :has() Pseudo-class        | 父元素根据子元素状态选择（CSS 中的"如果"）            |
| 容器查询单位     | Container Query Units      | cqw、cqh 等基于容器尺寸的单位                  |
| 动态视口单位     | Dynamic Viewport Units     | dvh、dvw 自动排除浏览器地址栏                  |

### 9.2 经典 CSS 技巧

| 术语           | 英文                    | 说明                                  |
| ------------ | --------------------- | ----------------------------------- |
| Flexbox 弹性布局 | Flexbox               | 一维弹性布局，擅长行/列排列                      |
| Grid 网格布局    | CSS Grid              | 二维网格布局，擅长行列同时控制                     |
| 多栏布局         | Multi-column Layout   | CSS columns 报纸式多栏文本                 |
| 吸附滚动         | CSS Scroll Snap       | 滚动自动吸附到指定位置                         |
| 粘性定位         | Sticky Position       | 滚动到阈值后固定在指定位置                       |
| 背景模糊         | Backdrop Filter Blur  | 毛玻璃效果的核心 CSS 属性                     |
| 混合模式         | Blend Mode            | mix-blend-mode 实现颜色混合叠加             |
| 裁切蒙版         | Clip-path             | CSS 裁切元素为各种形状                       |
| 遮罩           | CSS Mask              | 用图片/渐变作为遮罩控制元素可见区域                  |
| 形状浮动         | CSS Shape             | shape-outside 让文本环绕自定义形状            |
| 滚动条样式        | Custom Scrollbar      | 自定义滚动条的外观样式                         |
| 文字描边         | -webkit-text-stroke   | 为文字添加描边                             |
| 文字裁切         | background-clip: text | 用渐变/图片填充文字                          |
| 多行省略         | Line Clamping         | -webkit-line-clamp 多行文本截断省略         |
| 响应式字体        | Fluid Typography      | clamp() 实现字体大小随视口平滑变化               |
| 全屏溢出隐藏       | Overscroll Behavior   | overscroll-behavior: contain 防止滚动穿透 |

---

## 十、设计系统 / Design System

### 10.1 设计令牌

| 术语   | 英文                   | 说明                               |
| ---- | -------------------- | -------------------------------- |
| 设计令牌 | Design Tokens        | 颜色、间距、字号等可复用的设计原子变量              |
| 颜色令牌 | Color Tokens         | 语义化颜色变量（primary、surface、error 等） |
| 间距令牌 | Spacing Tokens       | 统一的间距梯度（xs、sm、md、lg、xl）          |
| 字体令牌 | Typography Tokens    | 字号、行高、字重等排版变量                    |
| 圆角令牌 | Border Radius Tokens | 统一的圆角梯度                          |
| 阴影令牌 | Shadow Tokens        | 统一的阴影层级（sm、md、lg）                |
| 动效令牌 | Motion Tokens        | 统一的时长和缓动曲线变量                     |
| 断点令牌 | Breakpoint Tokens    | 统一的响应式断点值                        |
| Z轴令牌 | Z-index Tokens       | 统一的层级梯度                          |

### 10.2 组件体系

| 术语    | 英文                   | 说明                    |
| ----- | -------------------- | --------------------- |
| 原子组件  | Atomic Components    | 最小不可拆分的 UI 元素（按钮、输入框） |
| 分子组件  | Molecular Components | 原子组合的功能单元（搜索栏=输入框+按钮） |
| 有机体组件 | Organism Components  | 分子组合的复杂区块（导航栏、页脚）     |
| 模板    | Template             | 页面骨架布局，定义内容区域         |
| 页面    | Page                 | 填充真实内容的最终页面           |
| 变体    | Variant              | 组件的不同状态/样式版本          |
| 复合组件  | Compound Component   | 通过上下文共享状态的组件模式        |
| 无头组件  | Headless Component   | 只提供逻辑不提供样式的组件         |
| 受控组件  | Controlled Component | 状态由外部控制的组件            |
| 插槽    | Slot / Children      | 组件中可自定义内容的占位区域        |

---

## 十一、性能与体验 / Performance & UX

### 11.1 性能优化

| 术语        | 英文                              | 说明                     |
| --------- | ------------------------------- | ---------------------- |
| 首屏渲染      | FCP (First Contentful Paint)    | 首次有内容渲染的时间点            |
| 最大内容渲染    | LCP (Largest Contentful Paint)  | 最大内容元素渲染完成的时间          |
| 首次输入延迟    | FID (First Input Delay)         | 用户首次交互的响应延迟            |
| 累积布局偏移    | CLS (Cumulative Layout Shift)   | 页面视觉稳定性指标              |
| 交互到下一次绘制  | INP (Interaction to Next Paint) | 交互响应速度指标               |
| 懒加载       | Lazy Loading                    | 滚动到可视区域再加载图片/内容        |
| 预加载       | Prefetch / Preload              | 提前加载即将需要的资源            |
| 代码分割      | Code Splitting                  | 按路由/功能拆分加载代码           |
| 图片优化      | Image Optimization              | WebP/AVIF 格式、响应式尺寸、懒加载 |
| 关键 CSS 内联 | Critical CSS Inlining           | 首屏 CSS 直接内联到 HTML      |
| 虚拟列表      | Virtual List                    | 只渲染可视区域的列表项            |

### 11.2 无障碍

| 术语      | 英文                     | 说明                        |
| ------- | ---------------------- | ------------------------- |
| 无障碍     | Accessibility / a11y   | 确保所有用户都能使用                |
| ARIA 标签 | ARIA Labels            | 为辅助技术提供的语义标签              |
| 键盘导航    | Keyboard Navigation    | 仅用键盘完成所有操作                |
| 焦点管理    | Focus Management       | 控制焦点顺序和位置                 |
| 颜色对比度   | Color Contrast         | 文字与背景的对比度满足 WCAG 标准       |
| 屏幕阅读器友好 | Screen Reader Friendly | 语义化 HTML + ARIA 确保屏幕阅读器可用 |
| 减少动效偏好  | prefers-reduced-motion | 尊重用户的减少动效系统设置             |
| 高对比模式   | High Contrast Mode     | 为视力障碍用户提供高对比选项            |
| 跳过导航    | Skip Navigation        | 跳过重复导航直达内容的快捷链接           |

### 11.3 用户体验模式

| 术语    | 英文                                | 说明                 |
| ----- | --------------------------------- | ------------------ |
| 渐进增强  | Progressive Enhancement           | 基础功能优先，逐步增强体验      |
| 优雅降级  | Graceful Degradation              | 高级功能不可用时优雅回退       |
| 乐观更新  | Optimistic Update                 | 操作后立即更新 UI，不等服务端响应 |
| 防抖    | Debounce                          | 延迟执行，只在停止操作后触发一次   |
| 节流    | Throttle                          | 限制执行频率，固定间隔执行一次    |
| 就地编辑  | Inline Edit                       | 点击文本直接在原位编辑        |
| 拖拽排序  | Drag and Drop Sort                | 通过拖拽重新排列元素顺序       |
| 下拉刷新  | Pull to Refresh                   | 移动端下拉手势触发刷新        |
| 骨架占位  | Skeleton Placeholder              | 加载前展示页面结构的灰色骨架     |
| 占位符内容 | Lorem Ipsum / Placeholder Content | 设计时使用的临时填充内容       |

---

## 十二、特定场景 / Domain-specific

### 12.1 电商

| 术语      | 英文                    | 说明                 |
| ------- | --------------------- | ------------------ |
| 商品卡片    | Product Card          | 展示商品图片、名称、价格、操作的卡片 |
| 加入购物车动画 | Add to Cart Animation | 商品飞入购物车的微交互        |
| 价格标签    | Price Tag             | 带删除线的原价 + 促销价      |
| 评分星标    | Star Rating           | 五星评价展示             |
| 商品画廊    | Product Gallery       | 多图缩略图 + 主图预览       |
| 规格选择器   | Variant Selector      | 颜色/尺码等规格选择控件       |
| 购物车抽屉   | Cart Drawer           | 侧滑出的购物车面板          |
| 快速预览    | Quick View            | 弹窗快速查看商品详情         |
| 倒计时计时器  | Countdown Timer       | 限时促销的倒计时           |
| 库存指示    | Stock Indicator       | "仅剩X件"的库存紧张提示      |
| 愿望清单按钮  | Wishlist Button       | 收藏/加入心愿单的心形按钮      |
| 优惠券条    | Coupon Bar            | 可展开的优惠券/促销信息条      |

### 12.2 SaaS / Dashboard

| 术语     | 英文                            | 说明              |
| ------ | ----------------------------- | --------------- |
| 数据面板   | Dashboard                     | 多指标综合展示页面       |
| 侧边栏菜单  | Sidebar Menu                  | 固定在左侧的导航菜单      |
| 顶部命令栏  | Command Bar / Command Palette | Cmd+K 弹出的快速命令面板 |
| 通知铃铛   | Notification Bell             | 带红点的通知入口        |
| 用户头像菜单 | Avatar Menu                   | 点击头像展开的用户操作菜单   |
| 活动流    | Activity Feed                 | 按时间排列的活动/事件流    |
| 看板视图   | Kanban View                   | 多列拖拽看板          |
| 表格视图   | Table View                    | 可排序筛选的数据表格      |
| 日历视图   | Calendar View                 | 日历形式的事件展示       |
| 图表视图   | Chart View                    | 图表化的数据展示        |
| 全屏模式   | Fullscreen Mode               | 隐藏导航进入沉浸模式      |
| 键盘快捷键  | Keyboard Shortcuts            | 高效操作的键盘快捷方式     |

### 12.3 社交 / 内容

| 术语         | 英文                | 说明                   |
| ---------- | ----------------- | -------------------- |
| 信息流        | Feed / Timeline   | 按时间排列的内容流            |
| 故事条        | Stories Bar       | 顶部横向滑动的故事圆形头像列表      |
| 点赞动效       | Like Animation    | 点赞时的心形爆炸/弹跳动效        |
| 评论线程       | Comment Thread    | 嵌套的评论回复树             |
| 分享面板       | Share Sheet       | 分享到各平台的面板            |
| 标签云        | Tag Cloud         | 大小不一的标签集合            |
| 用户卡片       | User Card         | 展示用户信息的卡片            |
| 关注按钮       | Follow Button     | 关注/取消关注的状态切换         |
| 图片网格       | Image Grid        | 类似 Instagram 的方形图片网格 |
| 无限瀑布流      | Infinite Masonry  | 无限滚动加载的瀑布流           |
| 双列/三列 Feed | Multi-column Feed | 多列并排的信息流             |

---

## 十三、动效库与框架术语 / Animation Libraries

| 术语            | 英文                | 说明                        |
| ------------- | ----------------- | ------------------------- |
| Lottie 动画     | Lottie Animation  | After Effects 导出的矢量动画     |
| GSAP 动画       | GSAP (GreenSock)  | 高性能专业动画库                  |
| Framer Motion | Framer Motion     | React 生态的声明式动画库           |
| React Spring  | React Spring      | 基于弹簧物理的 React 动画库         |
| Motion One    | Motion One        | 轻量级 Web Animations API 封装 |
| Anime.js      | Anime.js          | 轻量级通用动画库                  |
| Three.js      | Three.js          | WebGL 3D 渲染库              |
| R3F           | React Three Fiber | React 封装的 Three.js        |
| Drei          | Drei              | R3F 的常用辅助组件集              |
| Theater.js    | Theater.js        | 序列动画/滚动动画编排库              |
| Lenis         | Lenis             | 平滑滚动库                     |
| Swiper        | Swiper            | 现代化的滑动/轮播组件               |

---

## Prompt 使用示例

### 示例 1: 产品展示页

> 做一个暗色优先的便当盒网格产品展示页。卡片使用玻璃拟态风格，带柔和投影和微光边框。hover 时有磁力按钮效果和悬浮浮起动效。首屏为全出血通栏 Hero Section，带极光渐变背景和噪点叠加。页面加载时卡片采用交错动画入场，标题使用文字渐变效果，数字采用计数滚动动效。

### 示例 2: SaaS Dashboard

> 做一个亮色模式的数据面板。左侧固定侧边栏导航，使用便当盒网格展示 KPI 统计卡片。图表区包含环形图和折线图。顶部有命令栏（Cmd+K 触发）。表格支持排序和筛选，空数据时展示友好的空状态。所有数据加载时使用骨架屏。数字变化带计数滚动效果。

### 示例 3: 沉浸式品牌页

> 做一个沉浸式滚动品牌介绍页，暗色优先。每屏全屏展示，采用滚动劫持对齐到章节。首屏有粒子系统背景，鼠标追踪光效。各屏幕间使用共享元素过渡。文字采用打字机效果逐字揭示。产品图使用 3D 倾斜陀螺仪效果，跟随鼠标微倾斜。色调整体为莫兰迪色系，配合环境光晕和暗角效果。

---

| 类别       | 术语数 | 涵盖内容                          |
| -------- | --- | ----------------------------- |
| 视觉风格     | ~20 | 玻璃拟态、新拟态、赛博朋克、蒸汽波等            |
| 动效       | ~60 | 弹簧物理、交错动画、微交互、缓动函数等           |
| 布局       | ~40 | 便当盒网格、瀑布流、粘性堆叠、响应式等           |
| 色彩与光影    | ~30 | 极光渐变、霓虹发光、暗角、色相偏移等            |
| 质感与纹理    | ~20 | 噪点叠加、磨砂模糊、水彩晕染等               |
| 排版       | ~30 | 文字渐变、描边文字、首字下沉等               |
| 3D 与沉浸式  | ~25 | 倾斜陀螺仪、WebGL 着色器、滚动驱动动画等       |
| 组件模式     | ~60 | 卡片、导航、表单、数据展示等                |
| CSS 技术术语 | ~25 | 容器查询、子网格、滚动驱动动画等              |
| 设计系统     | ~20 | 设计令牌、原子组件、变体等                 |
| 性能与体验    | ~30 | LCP/CLS、无障碍、乐观更新等             |
| 特定场景     | ~35 | 电商、SaaS Dashboard、社交等         |
| 动效库与框架   | ~15 | GSAP、Framer Motion、Three.js 等 |

---

> 最后更新：2026-04-12
