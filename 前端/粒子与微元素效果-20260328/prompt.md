# 粒子与微元素效果

> 适用平台：Flutter / 移动端应用
> 核心原则：克制使用，锦上添花，不喧宾夺主

---

## 适用场景（不滥用）

仅在以下场景使用粒子/微元素效果：

- 空状态页面背景（无数据时的占位画面）
- 加载等待页面（数据加载中的过渡画面）
- 特殊节日/活动主题页面
- 个人中心头部背景装饰
- 首页 Banner 背景装饰

**禁止在以下场景使用：**
- 列表页（影响滚动性能）
- 表单页面（分散用户注意力）
- 高频操作页面（如搜索、设置）

---

## 粒子效果规范

### 数量控制

| 场景 | 粒子数量 | 说明 |
|------|---------|------|
| 空状态背景 | 20-30 个 | 轻盈点缀 |
| 加载等待页 | 30-50 个 | 适度丰富 |
| Banner 背景 | 15-25 个 | 不干扰前景内容 |
| 活动主题页 | 40-60 个 | 营造氛围 |

### 粒子属性

| 属性 | 规范 |
|------|------|
| 大小 | 1-4px，带模糊效果 |
| 透明度 | 10%-40%，避免遮挡内容 |
| 颜色 | 取当前页面主色或强调色的低透明度版本 |
| 形状 | 圆形为主（80%），可少量混入菱形、三角形（20%） |

### 粒子运动

| 运动类型 | 说明 | 速度 |
|---------|------|------|
| 缓慢漂浮 | 从底部缓慢上升或水平漂浮 | 0.2-0.5 px/frame |
| 随机扰动 | 布朗运动式微随机偏移 | ±0.1 px/frame |
| 呼吸闪烁 | 透明度周期性变化 | 周期 2-4s |
| 连线效果 | 相近粒子之间绘制半透明连线（可选） | 距离 < 100px 时连线 |

### Flutter 实现

```dart
// 使用 CustomPaint + Canvas 绘制粒子
class ParticlePainter extends CustomPainter {
  final List<Particle> particles;

  @override
  void paint(Canvas canvas, Size size) {
    for (final particle in particles) {
      final paint = Paint()
        ..color = particle.color.withOpacity(particle.opacity)
        ..maskFilter = MaskFilter.blur(BlurStyle.normal, particle.blur);

      canvas.drawCircle(
        Offset(particle.x, particle.y),
        particle.radius,
        paint,
      );
    }
  }
}

// 使用 RepaintBoundary 隔离重绘区域
RepaintBoundary(
  child: CustomPaint(
    painter: ParticlePainter(particles: particles),
    size: Size.infinite,
  ),
)
```

### 性能优化
- 粒子系统必须使用 `RepaintBoundary` 隔离
- 使用 `ValueNotifier` 仅在粒子状态变化时触发重绘
- 粒子数量根据设备性能动态调整
- 页面不可见时暂停粒子动画（`WidgetsBindingObserver`）
- 优先使用 GPU 加速（`Canvas` 而非 `Widget`）

---

## 微元素效果

### 1. 几何线条装饰
- 半透明细线条（0.5px，5-15% 透明度）
- 常见形态：圆形、三角形、六边形轮廓
- 缓慢旋转或脉动动画
- 用途：背景纹理、角落装饰

### 2. 光斑/光晕效果
- 使用 `RadialGradient` 绘制
- 颜色：强调色的极低透明度版本（5-15%）
- 大小：100-300px
- 位置：通常在页面角落或重要内容后方
- 可缓慢移动或脉动

### 3. 网格点阵（背景纹理）
- 正方形网格，间距 20-40px
- 点大小 1-2px，透明度 5-10%
- 颜色：当前主题的灰色调
- 用途：技术感背景、数据面板背景
- 可在特定区域使用渐变淡出

### 4. 流动渐变色块
- 大面积低透明度渐变色块
- 缓慢平移或形变动画
- 颜色：取配色方案中 2-3 种颜色的极低透明度（5-10%）
- 用途：页面背景氛围营造
- 必须使用 `RepaintBoundary` 隔离

---

## 微元素与内容的层级关系

```
Layer 4 (最底层)  │ 背景色 / 背景渐变
Layer 3           │ 流动渐变色块 / 网格点阵
Layer 2           │ 粒子效果 / 光晕
Layer 1           │ 页面内容（文字、卡片、按钮）
Layer 0 (最顶层)  │ 弹窗 / Toast / 导航
```

- 微元素永远在内容下方（Layer 2-3）
- 确保微元素不影响文字可读性
- 内容区域可使用半透明遮罩与微元素隔离
