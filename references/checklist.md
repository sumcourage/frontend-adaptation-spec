---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: b21004edebe357441e3d410f977e7c81_d53cb39b753711f1aabe5254007bceed
    ReservedCode1: 3DMaPgSURILS2nqggqYWVPWDz6vwld866LtqvSLLhSQfEbFOEBwIhjPNK7g3uKH0Pr02mg0UpsjhCFX4ASoG/PsxPpsaWuEfMDZhWY09qiHpg//wUJxOvOPMTBhOJCyIyYqrvcZYnEdr8HDW7SVLApFKZntoiSxqpGBpu/d+b/ja1Khd1UiogQ7Yz2c=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: b21004edebe357441e3d410f977e7c81_d53cb39b753711f1aabe5254007bceed
    ReservedCode2: 3DMaPgSURILS2nqggqYWVPWDz6vwld866LtqvSLLhSQfEbFOEBwIhjPNK7g3uKH0Pr02mg0UpsjhCFX4ASoG/PsxPpsaWuEfMDZhWY09qiHpg//wUJxOvOPMTBhOJCyIyYqrvcZYnEdr8HDW7SVLApFKZntoiSxqpGBpu/d+b/ja1Khd1UiogQ7Yz2c=
---

# 前端适配上线自查清单

## 移动端

### 必选项（上线前必须通过）
- [ ] viewport meta 包含 `viewport-fit=cover`
- [ ] CSS Reset 已引入（含 `box-sizing: border-box`）
- [ ] 适配方案已确定（vw / rem / rpx）
- [ ] `overflow-x: hidden` 已设置
- [ ] iOS 安全区域已适配（`env(safe-area-inset-*)`）
- [ ] 1px 边框使用 transform scale 方案
- [ ] 图片 `max-width: 100%`
- [ ] PostCSS 插件已配置（vw 方案）

### 建议项
- [ ] 公共工具类已引入（安全区域、1px 边框）
- [ ] `-webkit-overflow-scrolling: touch`
- [ ] `-webkit-font-smoothing: antialiased`
- [ ] `apple-mobile-web-app-capable` meta
- [ ] `format-detection telephone=no` meta
- [ ] 字体大小无奇数
- [ ] fixed 元素均已适配安全区域

### 禁止项
- [ ] 无 px 写移动端具体尺寸（固定值除外）
- [ ] 无 fixed 元素缺少安全区域适配
- [ ] 无横向 overflow-x 遗漏
- [ ] 无字体大小使用奇数
- [ ] 无 viewport 缺少 `user-scalable=no`

---

## PC 端

### 必选项
- [ ] CSS Reset 已引入（PC 专用版）
- [ ] 响应式断点已定义（CSS 变量）
- [ ] 内容区域 `max-width` + 居中已设置
- [ ] 最小宽度已设置（纯桌面端后台 >= 1024px）
- [ ] CSS 变量体系已建立（主题色、字号、间距）
- [ ] 字体栈正确（Windows 微软雅黑 / macOS 苹方）

### 建议项
- [ ] 滚动条已美化（Windows 下必需）
- [ ] 阴影/圆角使用 CSS 变量
- [ ] 表格横向滚动已处理
- [ ] 大屏（>=1920px）布局已优化

### 禁止项
- [ ] 无硬编码颜色值（应使用 CSS 变量）
- [ ] 无硬编码字号（应使用 CSS 变量）
- [ ] 无小于 1024px 的 min-width（桌面端后台）
- [ ] 无忽略大屏适配（1920+）

---

## 通用项（双端共有）

### 必选项
- [ ] 全局 `box-sizing: border-box`
- [ ] 全局 margin/padding 已 reset
- [ ] a 标签样式已重置
- [ ] img 标签 `display: block` + `max-width: 100%`
- [ ] ESlint + Prettier 已配置
- [ ] Git Hooks（husky + lint-staged）已配置

### Code Review 重点
- 新人 PR 必须检查 CSS Reset 是否引入
- 新人 PR 必须检查适配方案是否正确
- 新人 PR 必须检查安全区域是否适配
- 新人 PR 必须检查是否有硬编码颜色/字号
*（内容由AI生成，仅供参考）*
