---
description: 创建移动端优化的H5应用
argument-hint: [应用名称]
allowed-tools: Write(*), Edit(*), Bash(*)
---

# 📲 移动端H5应用

开发 $ARGUMENTS 移动端H5应用：

## 1. 移动端适配
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="format-detection" content="telephone=no">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <title>$ARGUMENTS</title>
</head>
```

## 2. 触摸事件处理
```javascript
// 移动端手势库
import { createGesture } from '@ionic/core';

class TouchHandler {
  constructor(element) {
    this.setupGestures(element);
  }

  setupGestures(element) {
    // 滑动手势
    const swipeGesture = createGesture({
      el: element,
      threshold: 15,
      onMove: (ev) => this.onSwipe(ev),
      gestureName: 'swipe'
    });

    swipeGesture.enable();
  }

  onSwipe(event) {
    const deltaX = event.deltaX;
    const deltaY = event.deltaY;
    // 处理滑动逻辑
  }
}
```

## 3. 性能优化
```css
/* 硬件加速 */
.accelerated {
  transform: translateZ(0);
  will-change: transform;
}

/* 触摸优化 */
.touch-element {
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
}

/* 字体优化 */
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

## 4. 兼容性处理
- iOS Safari适配
- Android浏览器兼容
- 微信内置浏览器优化
- 各种WebView适配

## 5. 调试工具
```javascript
// vConsole移动端调试
import VConsole from 'vconsole';

if (process.env.NODE_ENV === 'development') {
  new VConsole();
}

// 性能监控
const observer = new PerformanceObserver((list) => {
  list.getEntries().forEach((entry) => {
    console.log('Performance:', entry);
  });
});
observer.observe({entryTypes: ['measure', 'navigation']});
```

应用名称：$ARGUMENTS