---
description: 将Web应用转换为PWA
argument-hint: [应用名称]
allowed-tools: Write(*), Edit(*)
---

# 📱 PWA开发套件

将 $ARGUMENTS 转换为PWA：

## 1. Manifest配置
```json
{
  "name": "$ARGUMENTS",
  "short_name": "$ARGUMENTS",
  "description": "A Progressive Web App",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#000000",
  "icons": [
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

## 2. Service Worker
```javascript
// sw.js
const CACHE_NAME = '${ARGUMENTS}-v1';
const urlsToCache = [
  '/',
  '/static/css/main.css',
  '/static/js/main.js'
];

self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then((cache) => cache.addAll(urlsToCache))
  );
});

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then((response) => {
        return response || fetch(event.request);
      }
    )
  );
});
```

## 3. 离线功能
- 缓存策略实现
- 离线页面设计
- 数据同步机制
- 后台同步

## 4. 推送通知
```javascript
// 推送订阅
const subscription = await registration.pushManager.subscribe({
  userVisibleOnly: true,
  applicationServerKey: publicKey
});

// 通知显示
self.addEventListener('push', (event) => {
  const options = {
    body: event.data.text(),
    icon: '/icons/icon-192x192.png',
    badge: '/icons/badge.png'
  };

  event.waitUntil(
    self.registration.showNotification('$ARGUMENTS', options)
  );
});
```

应用名称：$ARGUMENTS