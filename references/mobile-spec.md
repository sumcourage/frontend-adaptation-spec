---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: b21004edebe357441e3d410f977e7c81_d30af1e8753711f1b2f55254006c9bbf
    ReservedCode1: 1QWUUjmoCp7OIlqqLY/j6mh3jBNfstYz6xNHbPrqByFlHmrE4R/UfJSWv+QlmO0o2pauLaoqfydsp9C7KGBVI2fYrbVFMyg1qXapNeBdShi65OZfWxHslewpLewvtpPC6ITb7yfd6nU4yaxv606duSgKFk6X2nh0+R7LH2IpsdODtnF7Cmj3Vtmfj1k=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: b21004edebe357441e3d410f977e7c81_d30af1e8753711f1b2f55254006c9bbf
    ReservedCode2: 1QWUUjmoCp7OIlqqLY/j6mh3jBNfstYz6xNHbPrqByFlHmrE4R/UfJSWv+QlmO0o2pauLaoqfydsp9C7KGBVI2fYrbVFMyg1qXapNeBdShi65OZfWxHslewpLewvtpPC6ITb7yfd6nU4yaxv606duSgKFk6X2nh0+R7LH2IpsdODtnF7Cmj3Vtmfj1k=
---

# 移动端 H5 适配完整规范

## 一、适配方案选择

| 场景 | 方案 | 说明 |
|------|------|------|
| 新项目 H5 | vw | postcss-px-to-viewport 自动转换，设计稿 px 值直接写 |
| 老项目 / 组件库 | rem | 统一基准，便于管理 |
| 微信/支付宝小程序 | rpx | 原生支持 |
| uni-app 多端 | upx | 全端兼容 |

### vw 方案 PostCSS 配置（推荐）

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-px-to-viewport': {
      viewportWidth: 375,      // 设计稿宽度
      viewportHeight: 812,     // 设计稿高度
      unitPrecision: 5,        // 精度
      viewportUnit: 'vw',
      fontViewportUnit: 'vw',
      selectorBlackList: ['.ignore', '.hairlines'],
      minPixelValue: 1,
      mediaQuery: false
    }
  }
}
```

### rem 方案（基准 375 设计稿）

```css
html {
  font-size: calc(100vw / 3.75);
}
```

## 二、viewport meta 配置

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
```

附加 meta：
```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="format-detection" content="telephone=no">
```

## 三、项目初始化模板

### Vite + Vue3（最推荐）

```bash
npm create vite@latest my-h5 -- --template vue
npm install postcss-px-to-viewport -D
```

入口文件 main.js：
```js
import { createApp } from 'vue'
import App from './App.vue'
import './styles/reset.css'
import './styles/common.css'
import './styles/utils.css'
createApp(App).mount('#app')
```

### uni-app

pages.json 全局样式配置：
```json
{
  "globalStyle": {
    "navigationBarTextStyle": "black",
    "navigationBarTitleText": "项目名称",
    "navigationBarBackgroundColor": "#ffffff",
    "backgroundColor": "#f5f5f5"
  }
}
```

uni-app 安全区域样式：
```css
page {
  background-color: #f5f5f5;
}
.safe-area-top {
  padding-top: constant(safe-area-inset-top);
  padding-top: env(safe-area-inset-top);
}
.safe-area-bottom {
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
}
.fixed-bottom {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
}
```

## 四、1px 边框方案

使用伪元素 + transform scale：

```css
.border-bottom {
  position: relative;
}
.border-bottom::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 1px;
  background: #eee;
  transform: scaleY(0.5);
  transform-origin: bottom;
}

.border-top {
  position: relative;
}
.border-top::before {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  height: 1px;
  background: #eee;
  transform: scaleY(0.5);
  transform-origin: top;
}
```

## 五、避坑指南

1. `box-sizing: border-box` 必须全局设置，否则 padding 会撑大盒子
2. `overflow-x: hidden` 必须加，防止横向滚动条
3. `-webkit-font-smoothing: antialiased` 让苹果设备字体渲染更清晰
4. `-webkit-overflow-scrolling: touch` 开启 iOS 惯性滚动
5. `-webkit-text-size-adjust: 100%` 禁止 iOS 横屏时字体自动放大
*（内容由AI生成，仅供参考）*
