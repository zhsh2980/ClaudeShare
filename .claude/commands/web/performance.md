---
description: 实施Web应用性能优化策略
argument-hint: [优化目标]
allowed-tools: Bash(*), Edit(*), Write(*)
---

# 🚀 Web性能优化

优化 $ARGUMENTS 的性能：

## 1. 构建优化
```javascript
// vite.config.ts
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          router: ['react-router-dom']
        }
      }
    },
    chunkSizeWarningLimit: 1000
  },
  plugins: [
    // 压缩插件
    viteCompression(),
    // 预加载
    preloadPlugin()
  ]
});
```

## 2. 代码分割
```typescript
// 路由懒加载
const HomePage = lazy(() => import('./pages/Home'));
const AboutPage = lazy(() => import('./pages/About'));

// 组件懒加载
const HeavyComponent = lazy(() =>
  import('./components/HeavyComponent')
);
```

## 3. 缓存策略
- Service Worker实现
- HTTP缓存配置
- CDN资源优化
- 本地存储利用

## 4. 监控工具
```bash
# 性能分析
npm install -D lighthouse
npm install -D webpack-bundle-analyzer

# 运行分析
npm run build
npm run analyze
lighthouse http://localhost:3000 --output html
```

## 5. 优化指标
- First Contentful Paint (FCP)
- Largest Contentful Paint (LCP)
- Cumulative Layout Shift (CLS)
- Time to Interactive (TTI)

优化目标：$ARGUMENTS