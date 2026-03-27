# 8pt 网格与色彩体系

> **适用场景**：UI 设计与开发中的间距、圆角、颜色管理
> **核心理念**：所有数值都是基础单位的倍数，色彩按功能分层
> **参考来源**：Apple HIG、Material Design、8-Point Grid

---

## 一、8pt 网格体系

### 1.1 基础规则

```
基础单位 = 4px
常用单位 = 8px（基础单位的 2 倍）

铁律：所有间距、圆角、内边距、外边距、元素尺寸必须是 4 的倍数。
     优先使用 8 的倍数。
     4px 仅用于精细微调，使用时需说明理由。
```

### 1.2 间距标尺（Spacing Scale）

| Token | 值 | 常用名 | 典型用途 |
|-------|-----|--------|----------|
| `space-0` | 0px | none | 重置间距 |
| `space-1` | 4px | micro | 图标与文字最小间距、紧凑列表项 |
| `space-2` | 8px | xs | 组内元素间距、输入框内边距 |
| `space-3` | 12px | sm | 标签与内容间距 |
| `space-4` | 16px | md | 卡片内边距、列表项间距、按钮组间距 |
| `space-5` | 20px | lg | 段落间距 |
| `space-6` | 24px | xl | 区块间距、内容与操作区间距 |
| `space-8` | 32px | 2xl | 卡片间距、大区块分隔 |
| `space-10` | 40px | 3xl | 内容与页面边缘安全距离 |
| `space-12` | 48px | 4xl | 页面级大间距 |
| `space-16` | 64px | 5xl | 章节/模块分隔 |

### 1.3 间距使用规则

```
规则 1：同一组件内元素间距 ≤ space-4（16px）
规则 2：组件之间间距 ≥ space-6（24px）
规则 3：页面左右安全边距 = space-4（移动端）或 space-10（桌面端）
规则 4：页面顶部安全边距 = space-6 ~ space-8
规则 5：重复元素间距使用同一 Token（如所有卡片间距都是 space-8）
规则 6：禁止出现 3px、5px、7px、9px、11px 等非 4 倍数值
```

---

## 二、圆角标尺（Border Radius Scale）

| Token | 值 | 典型用途 |
|-------|-----|----------|
| `radius-none` | 0px | 全角按钮、分割线 |
| `radius-sm` | 4px | 小标签、Badge、代码块 |
| `radius-md` | 8px | 输入框、小卡片、下拉菜单 |
| `radius-lg` | 12px | 卡片、弹窗、对话框 |
| `radius-xl` | 16px | 底部弹窗、大面板、模态框 |
| `radius-2xl` | 20px | 大型卡片、特殊容器 |
| `radius-full` | 9999px | 胶囊按钮、头像、药丸标签 |

### 圆角使用规则

```
规则 1：同一层级元素使用相同圆角（如所有卡片都是 radius-lg）
规则 2：容器圆角 ≥ 内部元素圆角（外圆内不圆）
规则 3：圆角值不随意创新，只从标尺中选择
规则 4：小元素用小圆角，大元素用大圆角（比例协调）
规则 5：方形元素（如图片）使用 radius-md 或 radius-lg 即可软化视觉
```

---

## 三、色彩层级体系

### 3.1 四层色彩架构

```
┌──────────────────────────────────┐
│     Brand Color（品牌色）         │  ← 1 个主色 + 1 个辅色
│  ┌────────────────────────────┐  │
│  │   Neutral Palette（中性色） │  │  ← 10 级灰阶
│  │  ┌──────────────────────┐  │  │
│  │  │ Semantic（语义色）    │  │  │  ← 成功/警告/错误/信息
│  │  │ ┌────────────────┐  │  │  │
│  │  │ │ Surface（表面色）│  │  │  │  ← Z 轴层次
│  │  │ └────────────────┘  │  │  │
│  │  └──────────────────────┘  │  │
│  └────────────────────────────┘  │
└──────────────────────────────────┘
```

### 3.2 品牌色（Brand Color）

```
定义规则：
- 主色（Primary）：1 个，用于最重要的操作和元素
- 辅色（Secondary）：1 个，用于辅助强调（可选）
- 生成方式：从主色生成 10 级色阶（50 → 950）

示例（以 #6366F1 Indigo 为例）：
  indigo-50   #EEF2FF
  indigo-100  #E0E7FF
  indigo-200  #C7D2FE
  indigo-300  #A5B4FC
  indigo-400  #818CF8
  indigo-500  #6366F1  ← 主色
  indigo-600  #4F46E5
  indigo-700  #4338CA
  indigo-800  #3730A3
  indigo-900  #312E81
```

### 3.3 中性色系（Neutral Palette）

| Token | 色值 | 用途 |
|-------|------|------|
| `neutral-0` | #FFFFFF | 纯白，主背景 |
| `neutral-1` | #F7F8FA | 次级背景、卡片背景 |
| `neutral-2` | #EEF0F4 | 输入框背景、分割线 |
| `neutral-3` | #E2E5EB | 禁用状态背景 |
| `neutral-4` | #CDD1D9 | 占位符文字、次要边框 |
| `neutral-5` | #9BA1AD | 次要文字、禁用图标 |
| `neutral-6` | #6B7280 | 正文文字 |
| `neutral-7` | #4B5563 | 标题文字 |
| `neutral-8` | #374151 | 重要标题 |
| `neutral-9` | #111827 | 最高层级文字、纯黑替代 |

### 3.4 语义色（Semantic Color）

| 语义 | 主色 | 浅色背景 | 深色背景 | 用途 |
|------|------|----------|----------|------|
| **Success** | #10B981 | #ECFDF5 | #065F46 | 成功、已完成、在线 |
| **Warning** | #F59E0B | #FFFBEB | #92400E | 警告、即将过期、低电量 |
| **Error** | #EF4444 | #FEF2F2 | #991B1B | 错误、失败、不可用 |
| **Info** | #3B82F6 | #EFF6FF | #1E40AF | 提示、帮助、链接 |

### 3.5 表面色层级（Surface Color）

用于表达 Z 轴空间层次：

| 层级 | 亮色模式 | 暗色模式 | 用途 |
|------|----------|----------|------|
| **Surface 0** | #FFFFFF | #0A0A0A | 页面主背景 |
| **Surface 1** | #F7F8FA | #161616 | 卡片、列表容器 |
| **Surface 2** | #EEF0F4 | #1F1F1F | 弹窗、抽屉、浮层 |
| **Surface 3** | #FFFFFF + Shadow | #2A2A2A + Border | Toast、Tooltip、下拉菜单 |
| **Surface 4** | Black 50% | Black 70% | Modal 遮罩层 |

**规则：**
- 层级越高，Surface 越浅（亮色）或越深（暗色）
- 亮色模式可配合 Box-Shadow 加强层次
- 暗色模式用微妙的边框（1px neutral-3）替代阴影

---

## 四、阴影标尺（Box Shadow Scale）

| Token | 值 | 用途 |
|-------|-----|------|
| `shadow-sm` | 0 1px 2px rgba(0,0,0,0.05) | 微妙提升，卡片默认 |
| `shadow-md` | 0 4px 6px rgba(0,0,0,0.07) | 中等提升，悬浮卡片 |
| `shadow-lg` | 0 10px 15px rgba(0,0,0,0.1) | 明显提升，弹窗 |
| `shadow-xl` | 0 20px 25px rgba(0,0,0,0.1) | 强烈提升，模态框 |

**规则：** 阴影仅在亮色模式下显著使用，暗色模式下大幅减弱或用边框替代。

---

## 五、CSS 变量定义参考

```css
:root {
  /* === Spacing === */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
  --space-10: 40px;
  --space-12: 48px;
  --space-16: 64px;

  /* === Border Radius === */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-full: 9999px;

  /* === Neutral === */
  --neutral-0: #FFFFFF;
  --neutral-1: #F7F8FA;
  --neutral-2: #EEF0F4;
  --neutral-3: #E2E5EB;
  --neutral-4: #CDD1D9;
  --neutral-5: #9BA1AD;
  --neutral-6: #6B7280;
  --neutral-7: #4B5563;
  --neutral-8: #374151;
  --neutral-9: #111827;

  /* === Semantic === */
  --color-success: #10B981;
  --color-warning: #F59E0B;
  --color-error: #EF4444;
  --color-info: #3B82F6;

  /* === Surface === */
  --surface-0: #FFFFFF;
  --surface-1: #F7F8FA;
  --surface-2: #EEF0F4;
  --surface-3: #FFFFFF;
  --surface-4: rgba(0, 0, 0, 0.5);

  /* === Shadow === */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.07);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.1);
  --shadow-xl: 0 20px 25px rgba(0,0,0,0.1);
}
```
