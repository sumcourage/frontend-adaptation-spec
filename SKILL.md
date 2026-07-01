---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: b21004edebe357441e3d410f977e7c81_d20b68b7753711f1897e5254002afed2
    ReservedCode1: y40U1N5cA9yv++G4DlfLj7Og+XSXrRl3667pyMNqkdA0d//E9pFPRcGFuhTQh+k8FkRVxygiJmJbzXnqkz8Q3Iq/wTNGh0RSK5YxAjbV7ZPhRQQT7PtkarSEOmw4L5wujv1vLm7XEt5Y5pcOkPtSCbnHOaGWrdGvzEYTl/1mt1vBWjHgAfxZJvf2Qoo=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: b21004edebe357441e3d410f977e7c81_d20b68b7753711f1897e5254002afed2
    ReservedCode2: y40U1N5cA9yv++G4DlfLj7Og+XSXrRl3667pyMNqkdA0d//E9pFPRcGFuhTQh+k8FkRVxygiJmJbzXnqkz8Q3Iq/wTNGh0RSK5YxAjbV7ZPhRQQT7PtkarSEOmw4L5wujv1vLm7XEt5Y5pcOkPtSCbnHOaGWrdGvzEYTl/1mt1vBWjHgAfxZJvf2Qoo=
---



# 前端项目统一适配规范（移动端 + PC 端）

为 AI Agent 提供前端适配的完整知识库与可直接注入的代码模板。

## 触发条件

- 新建前端项目 / 初始化 H5 项目 / 搭建 PC 后台
- 询问移动端适配方案 / rem / vw / rpx / 响应式
- 需要 CSS Reset / 安全区域适配 / 1px 边框
- 询问 PC 端响应式断点 / 桌面端布局规范
- 团队代码审查 / 适配规范检查

## 执行流程

### 场景一：新建项目
1. 确认目标平台：仅移动端 / 仅 PC 端 / 全平台
2. 确认技术栈：Vite+Vue3 / uni-app / 纯 H5 / React / 其他
3. 从 `assets/` 目录读取对应 CSS 文件注入到项目中
4. 根据 `references/` 中的详细规范配置 PostCSS / viewport meta 等

### 场景二：代码审查
1. 读取 `references/checklist.md` 获取完整自查清单
2. 逐项对照检查用户代码
3. 按 severity 分级输出问题（必须修复 / 建议优化 / 禁止项）

### 场景三：适配方案咨询
1. 根据用户平台和技术栈，从 `references/` 中匹配最佳方案
2. 给出方案对比表格和推荐理由
3. 提供对应的代码模板路径

## 适配方案决策树

```
用户平台？
├── 移动端 H5（新项目）     → vw 方案 + postcss-px-to-viewport
├── 移动端 H5（老项目）     → rem 方案（基准 375 设计稿）
├── 微信/支付宝小程序       → rpx 方案
├── uni-app 多端            → upx 方案
├── PC 端后台系统           → px + CSS 变量 + 响应式断点
└── 全平台项目              → 移动端 vw + PC 端响应式，两套 CSS 独立
```

## 核心规范速查

### 移动端核心规则
- viewport meta 必须含 `viewport-fit=cover`
- 全局 `overflow-x: hidden`
- 全局 `box-sizing: border-box`
- iOS 安全区域必须适配（`env(safe-area-inset-*)`）
- 1px 边框用 `transform: scaleY(0.5)`
- 图片 `max-width: 100%`
- 字体大小禁止用奇数

### PC 端核心规则
- 响应式断点：1920+ / 1280-1919 / 1024-1279 / <1024
- 设计基准推荐 1440px
- 内容最大宽度 1200-1400px 且居中
- 纯桌面端后台最小宽度 1024px
- 使用 CSS 变量统一管理主题色、字号、间距
- Windows 下滚动条统一美化
- 字体栈：`-apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif`

### 全平台禁止项
- 禁止用 px 写移动端具体尺寸（固定值除外）
- 禁止 fixed 元素不加安全区域
- 禁止横向 overflow 未设置
- 禁止字体大小使用奇数（移动端）
- 禁止硬编码颜色值（PC 端建议用 CSS 变量）

## 文件索引

详细规范和代码模板请按需读取：

| 文件 | 用途 | 读取时机 |
|------|------|----------|
| `references/mobile-spec.md` | 移动端完整适配规范 | 移动端项目初始化 / 问题排查 |
| `references/pc-spec.md` | PC 端完整适配规范 | PC 端项目初始化 / 问题排查 |
| `references/checklist.md` | 适配自查清单（双端） | 代码审查 / 上线前检查 |
| `assets/mobile/reset.css` | 移动端 CSS Reset | 移动端项目初始化时注入 |
| `assets/mobile/common.css` | 移动端公共样式（安全区域/1px边框/布局） | 移动端项目初始化时注入 |
| `assets/mobile/utils.css` | 移动端工具类 | 移动端项目初始化时注入 |
| `assets/pc/reset.css` | PC 端 CSS Reset | PC 端项目初始化时注入 |
| `assets/pc/common.css` | PC 端公共样式（布局/滚动条/字体） | PC 端项目初始化时注入 |
| `assets/pc/utils.css` | PC 端工具类（间距/弹性布局/文字） | PC 端项目初始化时注入 |
*（内容由AI生成，仅供参考）*
