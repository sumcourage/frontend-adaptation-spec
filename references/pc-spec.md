---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: b21004edebe357441e3d410f977e7c81_d449cbb7753711f1aabe5254007bceed
    ReservedCode1: nLqOpq1f8vH9a+e64kdcvj1W38yv9Q9nHLNK2zv9S3Ac5iI+vJLE0IrD3hh+8T1KvYrX8FAXnjOCnVkmpv+DxphIx6XsGDpCdv+JIHyGeb9YE2cmpFaOl6y3eIWyDkwFmADhrfnQ2kUDN8G38f72dmnsqZi7/yPNXSksSSrt1fxggWVRbPciEwGwQCY=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: b21004edebe357441e3d410f977e7c81_d449cbb7753711f1aabe5254007bceed
    ReservedCode2: nLqOpq1f8vH9a+e64kdcvj1W38yv9Q9nHLNK2zv9S3Ac5iI+vJLE0IrD3hh+8T1KvYrX8FAXnjOCnVkmpv+DxphIx6XsGDpCdv+JIHyGeb9YE2cmpFaOl6y3eIWyDkwFmADhrfnQ2kUDN8G38f72dmnsqZi7/yPNXSksSSrt1fxggWVRbPciEwGwQCY=
---

# PC 端适配完整规范

## 一、响应式断点

| 断点 | 范围 | 典型设备 |
|------|------|----------|
| 超大屏 | >= 1920px | 2K/4K 显示器 |
| 标准桌面 | 1280px ~ 1919px | 常规笔记本/台式机（设计基准 1440px） |
| 小型桌面 | 1024px ~ 1279px | 小型笔记本 / 平板横屏 |
| 平板/手机 | < 1024px | 平板竖屏 / 手机（降级为移动端布局） |

### CSS 变量管理断点

```css
:root {
  --breakpoint-xl: 1920px;
  --breakpoint-lg: 1280px;
  --breakpoint-md: 1024px;
  --content-max-width: 1400px;
  --content-min-width: 1024px;
}
```

## 二、布局规范

### 内容区域

```css
.page-container {
  max-width: var(--content-max-width);
  min-width: var(--content-min-width);
  margin: 0 auto;
  padding: 0 24px;
}
```

### 布局方案选择

| 场景 | 方案 |
|------|------|
| 后台管理系统 | 左侧固定导航 + 右侧自适应（Flexbox） |
| 官网 / 展示页 | 内容居中 + 多栏 Grid |
| 数据看板 | CSS Grid 栅格 |
| 表单页 | 固定宽度 600-800px 居中 |

### 经典后台布局

```css
.admin-layout {
  display: flex;
  min-height: 100vh;
}
.admin-sidebar {
  width: 240px;
  flex-shrink: 0;
}
.admin-main {
  flex: 1;
  overflow: auto;
  padding: 24px;
}
```

## 三、字体规范

### 字体栈

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI',
               'PingFang SC', 'Hiragino Sans GB',
               'Microsoft YaHei', 'Helvetica Neue', Helvetica,
               Arial, sans-serif;
}
```

优先级：macOS 苹方 → Windows 微软雅黑 → 兜底 sans-serif

### 字号体系

| 用途 | 字号 | 行高 |
|------|------|------|
| 大标题 | 24px | 1.4 |
| 页面标题 | 20px | 1.4 |
| 卡片标题 | 16px | 1.5 |
| 正文 | 14px | 1.6 |
| 辅助文字 | 12px | 1.5 |

## 四、CSS 变量体系

```css
:root {
  /* 主题色 */
  --color-primary: #1677ff;
  --color-primary-hover: #4096ff;
  --color-primary-active: #0958d9;
  --color-success: #52c41a;
  --color-warning: #faad14;
  --color-error: #ff4d4f;
  --color-info: #1677ff;

  /* 中性色 */
  --color-text: #1f1f1f;
  --color-text-secondary: #666;
  --color-text-placeholder: #999;
  --color-border: #e8e8e8;
  --color-bg: #f5f5f5;
  --color-bg-white: #fff;

  /* 字号 */
  --font-size-xl: 24px;
  --font-size-lg: 20px;
  --font-size-md: 16px;
  --font-size-base: 14px;
  --font-size-sm: 12px;

  /* 间距 */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 12px;
  --spacing-base: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;

  /* 圆角 */
  --radius-sm: 4px;
  --radius-base: 6px;
  --radius-lg: 8px;
  --radius-round: 50%;

  /* 阴影 */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.06);
  --shadow-base: 0 2px 8px rgba(0,0,0,0.08);
  --shadow-lg: 0 4px 16px rgba(0,0,0,0.12);
}
```

## 五、滚动条美化（Windows 必需）

```css
::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}
::-webkit-scrollbar-thumb {
  background: #c1c1c1;
  border-radius: 3px;
}
::-webkit-scrollbar-thumb:hover {
  background: #a8a8a8;
}
::-webkit-scrollbar-track {
  background: transparent;
}
```

## 六、PC 端 CSS Reset 关键差异

与移动端不同的地方：
1. 不需要 `overflow-x: hidden`（桌面端可能需要横向滚动，如表哥）
2. 不需要 `-webkit-overflow-scrolling: touch`
3. 不需要 `-webkit-text-size-adjust`
4. 需要设置 `min-width` 防止布局崩溃
5. 需要统一滚动条样式
*（内容由AI生成，仅供参考）*
