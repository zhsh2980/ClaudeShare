# Claude Code 移动端/Web/鸿蒙开发自定义命令大全 (20个专业案例)

基于最新的移动端开发、鸿蒙开发、Web和H5开发需求，整理了针对性的 Claude Code 自定义命令实用案例。

## 📚 资源来源

### 官方文档
- [斜杠命令文档](https://docs.claude.com/zh-CN/docs/claude-code/slash-commands)
- [Claude Code 快速开始](https://docs.claude.com/zh-CN/docs/claude-code/quickstart)

### 移动端开发资源
- [Claude加速Android App开发实战](https://blog.csdn.net/u011897062/article/details/142264912)
- [Cursor+Claude-3.5生成Android app](https://blog.csdn.net/weixin_41688410/article/details/146430386)
- [Claude Code 中文开发套件](https://github.com/hifoxdot/claude-init-CN)
- [React Native with Claude AI 完整教程](https://designcode.io/react-native-ai/)

### 鸿蒙开发资源
- [HarmonyOS ArkUI 框架实现原理和落地实践](https://zhuanlan.zhihu.com/p/679207951)
- [跟老卫学HarmonyOS开发教程](https://gitee.com/waylau/harmonyos-tutorial)
- [ArkTS语法和鸿蒙组件实战项目](https://github.com/hi-dhl/HarmonyPractice)
- [华为开发者联盟 ArkUI声明式UI开发框架](https://developer.huawei.com/consumer/cn/arkui/)

### Web/H5开发资源
- [Claude Code权威实践指南](https://zhuanlan.zhihu.com/p/1920263182062163086)
- [Claude Code深度实战完整开发指南](https://aicoding.csdn.net/68872aac080e555a88d2f7f7.html)
- [Claude Code前端开发工作流自动化](https://mcp.csdn.net/686e9470080e555a88ce6b04.html)
- [Taro多端开发框架实战教程](https://coding.imooc.com/class/306.html)

## 🎯 自定义命令概述

### 目录结构
```
.claude/commands/          # 项目级命令 (前缀 /project:)
├── mobile/                # 移动端开发
├── harmony/               # 鸿蒙开发
├── web/                   # Web开发
├── h5/                    # H5开发
├── cross/                 # 跨平台开发
└── tools/                 # 开发工具

~/.claude/commands/        # 用户级命令 (前缀 /user:)
```

### 命令文件格式
```markdown
---
description: 命令描述
argument-hint: [参数格式]
allowed-tools: Bash(*), Edit(*), Read(*)
model: claude-3-5-haiku-20241022
---

# 命令标题
命令内容，支持 $ARGUMENTS 参数占位符

## 执行步骤
1. 检查项目环境
2. 执行核心功能
3. 验证结果

!`命令示例`
@配置文件引用
```

## 📱 移动端开发命令 (6个)

### 1. React Native 项目初始化 (`mobile/rn-init.md`)
```markdown
---
description: 快速初始化React Native项目并配置开发环境
argument-hint: [项目名称]
allowed-tools: Bash(*), Write(*), Edit(*)
---

# 🚀 React Native 项目初始化

为 $ARGUMENTS 创建完整的RN项目：

## 1. 环境检查
!`node --version && npm --version`
!`npx react-native doctor`

## 2. 项目创建
- 使用最新RN模板创建项目
- 配置TypeScript支持
- 设置导航和状态管理

## 3. 开发环境配置
- Android开发环境设置
- iOS开发环境配置
- 调试工具配置

## 4. 依赖安装
```bash
npx react-native init $ARGUMENTS --template react-native-template-typescript
cd $ARGUMENTS
npm install @react-navigation/native @react-navigation/stack
npm install react-native-reanimated react-native-gesture-handler
```

## 5. 项目结构优化
- 创建标准目录结构
- 配置路径别名
- 设置代码规范

项目名称：$ARGUMENTS
```

**使用方式**: `/project:mobile:rn-init MyAwesomeApp`

### 2. Android Jetpack Compose 组件生成 (`mobile/compose.md`)
```markdown
---
description: 生成Android Jetpack Compose组件代码
argument-hint: [组件名称]
allowed-tools: Write(*), Edit(*)
---

# 🎨 Jetpack Compose 组件生成

创建 $ARGUMENTS Compose组件：

## 1. 组件结构
- Composable函数定义
- 状态管理设置
- UI预览配置

## 2. 代码生成
```kotlin
@Composable
fun $ARGUMENTS(
    modifier: Modifier = Modifier,
    // 参数定义
) {
    // 组件实现
    Surface(
        modifier = modifier,
        // 组件内容
    ) {
        // UI结构
    }
}

@Preview(showBackground = true)
@Composable
fun ${ARGUMENTS}Preview() {
    MyAppTheme {
        $ARGUMENTS()
    }
}
```

## 3. 最佳实践
- Material Design 3规范
- 响应式布局设计
- 可访问性支持
- 性能优化建议

组件名称：$ARGUMENTS
```

**使用方式**: `/project:mobile:compose UserProfileCard`

### 3. iOS SwiftUI 视图生成 (`mobile/swiftui.md`)
```markdown
---
description: 生成iOS SwiftUI视图组件
argument-hint: [视图名称]
allowed-tools: Write(*), Edit(*)
---

# 🍎 SwiftUI 视图生成

创建 $ARGUMENTS SwiftUI视图：

## 1. 视图结构
```swift
import SwiftUI

struct $ARGUMENTS: View {
    // 状态属性
    @State private var isLoading = false

    var body: some View {
        // 视图内容
        VStack {
            // UI组件
        }
        .navigationTitle("$ARGUMENTS")
        .padding()
    }
}

struct ${ARGUMENTS}_Previews: PreviewProvider {
    static var previews: some View {
        $ARGUMENTS()
    }
}
```

## 2. 功能特性
- 声明式UI设计
- 状态绑定和数据流
- 动画和过渡效果
- 导航和路由处理

## 3. 平台适配
- iPhone和iPad适配
- 深色模式支持
- 动态类型支持
- VoiceOver可访问性

视图名称：$ARGUMENTS
```

**使用方式**: `/project:mobile:swiftui ProductDetailView`

### 4. Flutter Widget 开发 (`mobile/flutter.md`)
```markdown
---
description: 创建Flutter Widget组件
argument-hint: [Widget名称]
allowed-tools: Write(*), Edit(*)
---

# 🎯 Flutter Widget 开发

构建 $ARGUMENTS Flutter Widget：

## 1. Widget类型选择
- StatelessWidget（无状态）
- StatefulWidget（有状态）
- 自定义绘制Widget

## 2. 代码生成
```dart
class $ARGUMENTS extends StatefulWidget {
  const $ARGUMENTS({Key? key}) : super(key: key);

  @override
  State<$ARGUMENTS> createState() => _${ARGUMENTS}State();
}

class _${ARGUMENTS}State extends State<$ARGUMENTS> {
  @override
  Widget build(BuildContext context) {
    return Container(
      // Widget实现
      child: Column(
        children: [
          // UI组件
        ],
      ),
    );
  }
}
```

## 3. 特性实现
- 响应式布局
- 主题适配
- 状态管理（Provider/Bloc）
- 手势处理

## 4. 测试配置
- Widget测试
- 集成测试
- 性能测试

Widget名称：$ARGUMENTS
```

**使用方式**: `/project:mobile:flutter CustomAnimatedButton`

### 5. 移动端API集成 (`mobile/api.md`)
```markdown
---
description: 生成移动端API请求和数据处理代码
argument-hint: [API名称]
allowed-tools: Write(*), Edit(*)
---

# 🔌 移动端API集成

为 $ARGUMENTS 创建API集成：

## 1. 网络请求层
```typescript
// React Native / TypeScript
interface ${ARGUMENTS}Response {
  // 响应类型定义
}

class ${ARGUMENTS}Service {
  private baseURL = 'https://api.example.com';

  async get$ARGUMENTS(): Promise<${ARGUMENTS}Response> {
    try {
      const response = await fetch(`${this.baseURL}/$ARGUMENTS`);
      return response.json();
    } catch (error) {
      throw new Error(`Failed to fetch $ARGUMENTS: ${error}`);
    }
  }
}
```

## 2. 状态管理
- Redux Toolkit配置
- Context API使用
- 错误处理机制
- 缓存策略

## 3. 安全考虑
- HTTPS强制使用
- Certificate Pinning
- Token安全存储
- 请求加密

## 4. 性能优化
- 请求缓存
- 分页加载
- 图片懒加载
- 网络状态监听

API名称：$ARGUMENTS
```

**使用方式**: `/project:mobile:api UserAuthentication`

### 6. 移动端测试套件 (`mobile/test.md`)
```markdown
---
description: 生成移动端自动化测试代码
argument-hint: [测试目标]
allowed-tools: Write(*), Bash(*)
---

# 🧪 移动端测试套件

为 $ARGUMENTS 创建测试套件：

## 1. 单元测试
```javascript
// Jest + React Native Testing Library
import { render, fireEvent } from '@testing-library/react-native';
import $ARGUMENTS from '../$ARGUMENTS';

describe('$ARGUMENTS', () => {
  test('renders correctly', () => {
    const { getByText } = render(<$ARGUMENTS />);
    // 测试断言
  });

  test('handles user interaction', () => {
    const { getByTestId } = render(<$ARGUMENTS />);
    fireEvent.press(getByTestId('button'));
    // 验证行为
  });
});
```

## 2. 集成测试
- API集成测试
- 导航流程测试
- 数据持久化测试

## 3. UI测试
- Detox (React Native)
- Espresso (Android)
- XCUITest (iOS)

## 4. 性能测试
- 启动时间测试
- 内存使用监控
- CPU使用率检查
- 电池消耗评估

测试目标：$ARGUMENTS
```

**使用方式**: `/project:mobile:test LoginFlow`

## 🌸 鸿蒙开发命令 (4个)

### 7. HarmonyOS 应用初始化 (`harmony/init.md`)
```markdown
---
description: 初始化HarmonyOS应用项目
argument-hint: [应用名称]
allowed-tools: Bash(*), Write(*), Edit(*)
---

# 🌸 HarmonyOS 应用初始化

创建 $ARGUMENTS 鸿蒙应用：

## 1. 开发环境检查
!`node --version`
!`npm list @ohos/hvigor -g`

## 2. 项目创建
```bash
# 使用DevEco Studio模板或hvigor工具
hvigor create $ARGUMENTS --template=stage
cd $ARGUMENTS
npm install
```

## 3. 项目配置
- 配置应用签名
- 设置权限申请
- 配置构建脚本

## 4. 目录结构
```
src/main/
├── ets/           # ArkTS源码
├── resources/     # 资源文件
└── module.json5   # 模块配置
```

## 5. 基础代码
```typescript
// Index.ets
@Entry
@Component
struct Index {
  @State message: string = 'Hello $ARGUMENTS'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

应用名称：$ARGUMENTS
```

**使用方式**: `/project:harmony:init MyHarmonyApp`

### 8. ArkTS 组件开发 (`harmony/component.md`)
```markdown
---
description: 创建ArkTS自定义组件
argument-hint: [组件名称]
allowed-tools: Write(*), Edit(*)
---

# 🎨 ArkTS 组件开发

构建 $ARGUMENTS ArkTS组件：

## 1. 组件定义
```typescript
@Component
export struct $ARGUMENTS {
  // 组件属性
  @Prop data: string = '';
  @State isVisible: boolean = true;

  build() {
    Column() {
      // 组件UI结构
      if (this.isVisible) {
        Text(this.data)
          .fontSize(16)
          .fontColor(Color.Black)
          .margin(10)
      }
    }
    .width('100%')
    .height('auto')
    .padding(12)
  }
}
```

## 2. 生命周期
- aboutToAppear()
- aboutToDisappear()
- onPageShow()
- onPageHide()

## 3. 状态管理
- @State 组件内部状态
- @Prop 父组件传递属性
- @Link 双向数据绑定
- @Provide/@Consume 跨组件通信

## 4. 事件处理
- 点击事件
- 触摸事件
- 滑动手势
- 长按操作

## 5. 动画效果
```typescript
.animation({
  duration: 300,
  curve: Curve.EaseInOut
})
```

组件名称：$ARGUMENTS
```

**使用方式**: `/project:harmony:component UserCard`

### 9. 鸿蒙数据管理 (`harmony/data.md`)
```markdown
---
description: 实现鸿蒙应用数据存储和管理
argument-hint: [数据模型名称]
allowed-tools: Write(*), Edit(*)
---

# 💾 鸿蒙数据管理

为 $ARGUMENTS 实现数据管理：

## 1. 数据模型定义
```typescript
// $ARGUMENTS.ets
export class $ARGUMENTS {
  id: string;
  name: string;
  createTime: number;

  constructor(id: string, name: string) {
    this.id = id;
    this.name = name;
    this.createTime = Date.now();
  }
}
```

## 2. 首选项存储
```typescript
import preferences from '@ohos.data.preferences';

class ${ARGUMENTS}Storage {
  private static instance: ${ARGUMENTS}Storage;
  private pref: preferences.Preferences | null = null;

  static getInstance(): ${ARGUMENTS}Storage {
    if (!${ARGUMENTS}Storage.instance) {
      ${ARGUMENTS}Storage.instance = new ${ARGUMENTS}Storage();
    }
    return ${ARGUMENTS}Storage.instance;
  }

  async save$ARGUMENTS(data: $ARGUMENTS): Promise<void> {
    await this.pref?.put('${ARGUMENTS}_' + data.id, JSON.stringify(data));
    await this.pref?.flush();
  }
}
```

## 3. 关系型数据库
```typescript
import relationalStore from '@ohos.data.relationalStore';

const SQL_CREATE_TABLE = `
  CREATE TABLE IF NOT EXISTS ${ARGUMENTS} (
    id TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    createTime INTEGER
  )
`;
```

## 4. 分布式数据
- 设备间数据同步
- 分布式对象管理
- 数据权限控制

数据模型：$ARGUMENTS
```

**使用方式**: `/project:harmony:data Product`

### 10. 鸿蒙服务开发 (`harmony/service.md`)
```markdown
---
description: 创建鸿蒙后台服务
argument-hint: [服务名称]
allowed-tools: Write(*), Edit(*)
---

# ⚙️ 鸿蒙服务开发

开发 $ARGUMENTS 后台服务：

## 1. ServiceExtensionAbility
```typescript
import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';
import Want from '@ohos.app.ability.Want';

export default class ${ARGUMENTS}Service extends ServiceExtensionAbility {
  onCreate(want: Want): void {
    console.info(`${ARGUMENTS}Service onCreate`);
    // 服务初始化
  }

  onRequest(want: Want, startId: number): void {
    console.info(`${ARGUMENTS}Service onRequest`);
    // 处理服务请求
  }

  onDestroy(): void {
    console.info(`${ARGUMENTS}Service onDestroy`);
    // 服务销毁清理
  }
}
```

## 2. 模块配置
```json5
// module.json5
{
  "extensionAbilities": [
    {
      "name": "${ARGUMENTS}Service",
      "srcEntry": "./ets/services/${ARGUMENTS}Service.ts",
      "type": "service",
      "exported": true
    }
  ]
}
```

## 3. 后台任务
- 长时运行任务
- 延时任务调度
- 工作调度器

## 4. 系统能力调用
- 位置服务
- 推送通知
- 设备管理
- 网络监听

服务名称：$ARGUMENTS
```

**使用方式**: `/project:harmony:service LocationTracker`

## 🌐 Web开发命令 (5个)

### 11. 现代Web应用脚手架 (`web/app.md`)
```markdown
---
description: 创建现代Web应用项目脚手架
argument-hint: [项目名称]
allowed-tools: Bash(*), Write(*), Edit(*)
---

# 🌐 现代Web应用脚手架

构建 $ARGUMENTS Web应用：

## 1. 技术栈选择
- React 18 + TypeScript
- Vite 构建工具
- TailwindCSS 样式框架
- React Router 路由管理

## 2. 项目初始化
```bash
npm create vite@latest $ARGUMENTS -- --template react-ts
cd $ARGUMENTS
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## 3. 开发工具配置
- ESLint + Prettier
- Husky Git hooks
- VSCode 配置
- 环境变量管理

## 4. 项目结构
```
src/
├── components/    # 组件
├── pages/        # 页面
├── hooks/        # 自定义Hook
├── utils/        # 工具函数
├── styles/       # 样式文件
└── types/        # 类型定义
```

## 5. 核心配置
- 路由配置
- 状态管理设置
- API 客户端配置
- 主题系统

项目名称：$ARGUMENTS
```

**使用方式**: `/project:web:app ModernDashboard`

### 12. Vue 3 组合式API组件 (`web/vue.md`)
```markdown
---
description: 创建Vue 3组合式API组件
argument-hint: [组件名称]
allowed-tools: Write(*), Edit(*)
---

# 🎨 Vue 3 组合式API组件

开发 $ARGUMENTS Vue组件：

## 1. 组件结构
```vue
<template>
  <div class="${ARGUMENTS}">
    <!-- 组件模板 -->
    <h2>{{ title }}</h2>
    <slot />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'

// Props定义
interface Props {
  title?: string
}

const props = withDefaults(defineProps<Props>(), {
  title: '$ARGUMENTS'
})

// 响应式数据
const count = ref(0)
const isLoading = ref(false)

// 计算属性
const displayText = computed(() => {
  return `${props.title} - ${count.value}`
})

// 生命周期
onMounted(() => {
  console.log('$ARGUMENTS mounted')
})

// 方法
const handleClick = () => {
  count.value++
}

// 暴露给父组件
defineExpose({
  reset: () => count.value = 0
})
</script>

<style scoped>
.${ARGUMENTS} {
  /* 组件样式 */
}
</style>
```

## 2. TypeScript支持
- Props类型定义
- Emits事件类型
- 组合式函数类型

## 3. 性能优化
- defineAsyncComponent
- v-memo 指令
- keep-alive 缓存

组件名称：$ARGUMENTS
```

**使用方式**: `/project:web:vue DataTable`

### 13. React Hook 开发 (`web/hook.md`)
```markdown
---
description: 创建自定义React Hook
argument-hint: [Hook名称]
allowed-tools: Write(*), Edit(*)
---

# ⚡ React Hook 开发

构建 use$ARGUMENTS Hook：

## 1. Hook实现
```typescript
import { useState, useEffect, useCallback } from 'react';

interface Use${ARGUMENTS}Options {
  // 配置选项
  autoStart?: boolean;
  interval?: number;
}

interface Use${ARGUMENTS}Return {
  // 返回值类型
  data: any;
  loading: boolean;
  error: Error | null;
  refetch: () => void;
}

export function use$ARGUMENTS(
  options: Use${ARGUMENTS}Options = {}
): Use${ARGUMENTS}Return {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState<Error | null>(null);

  const fetchData = useCallback(async () => {
    try {
      setLoading(true);
      setError(null);
      // 数据获取逻辑
      const result = await fetch('/api/$ARGUMENTS');
      setData(result);
    } catch (err) {
      setError(err as Error);
    } finally {
      setLoading(false);
    }
  }, []);

  useEffect(() => {
    if (options.autoStart) {
      fetchData();
    }
  }, [fetchData, options.autoStart]);

  return {
    data,
    loading,
    error,
    refetch: fetchData
  };
}
```

## 2. Hook测试
```typescript
import { renderHook, act } from '@testing-library/react';
import { use$ARGUMENTS } from './use$ARGUMENTS';

describe('use$ARGUMENTS', () => {
  test('should fetch data correctly', async () => {
    const { result } = renderHook(() => use$ARGUMENTS());

    act(() => {
      result.current.refetch();
    });

    // 测试断言
  });
});
```

## 3. 最佳实践
- 依赖数组优化
- 内存泄漏防护
- 错误边界处理

Hook名称：$ARGUMENTS
```

**使用方式**: `/project:web:hook useLocalStorage`

### 14. Web性能优化 (`web/performance.md`)
```markdown
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
```

**使用方式**: `/project:web:performance CoreWebVitals`

### 15. PWA开发套件 (`web/pwa.md`)
```markdown
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
```

**使用方式**: `/project:web:pwa MyProgressiveApp`

## 📲 H5开发命令 (3个)

### 16. 移动端H5应用 (`h5/mobile.md`)
```markdown
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
```

**使用方式**: `/project:h5:mobile ShoppingMall`

### 17. 微信小程序H5 (`h5/wechat.md`)
```markdown
---
description: 开发微信生态H5应用
argument-hint: [应用名称]
allowed-tools: Write(*), Edit(*), Bash(*)
---

# 💬 微信小程序H5

构建 $ARGUMENTS 微信H5应用：

## 1. 微信JS-SDK集成
```javascript
// 微信配置
import wx from 'weixin-js-sdk';

class WeixinHelper {
  constructor() {
    this.config = {
      debug: false,
      appId: process.env.WECHAT_APP_ID,
      timestamp: '',
      nonceStr: '',
      signature: '',
      jsApiList: [
        'chooseImage',
        'uploadImage',
        'getLocation',
        'onMenuShareTimeline',
        'onMenuShareAppMessage'
      ]
    };
  }

  async init() {
    // 获取签名
    const signature = await this.getSignature();
    this.config.timestamp = signature.timestamp;
    this.config.nonceStr = signature.nonceStr;
    this.config.signature = signature.signature;

    wx.config(this.config);

    return new Promise((resolve, reject) => {
      wx.ready(() => resolve(wx));
      wx.error((err) => reject(err));
    });
  }

  shareToTimeline(title, link, imgUrl) {
    wx.onMenuShareTimeline({
      title: title,
      link: link,
      imgUrl: imgUrl
    });
  }
}
```

## 2. 微信支付集成
```javascript
class WeixinPay {
  async pay(orderInfo) {
    const payData = await this.getPayParams(orderInfo);

    return new Promise((resolve, reject) => {
      wx.chooseWXPay({
        timestamp: payData.timestamp,
        nonceStr: payData.nonceStr,
        package: payData.package,
        signType: payData.signType,
        paySign: payData.paySign,
        success: (res) => resolve(res),
        fail: (err) => reject(err)
      });
    });
  }
}
```

## 3. 授权登录
```javascript
class WeixinAuth {
  getAuthUrl() {
    const params = new URLSearchParams({
      appid: process.env.WECHAT_APP_ID,
      redirect_uri: encodeURIComponent(window.location.href),
      response_type: 'code',
      scope: 'snsapi_userinfo',
      state: 'STATE'
    });

    return `https://open.weixin.qq.com/connect/oauth2/authorize?${params}#wechat_redirect`;
  }

  async getUserInfo(code) {
    const response = await fetch('/api/wechat/userinfo', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ code })
    });

    return response.json();
  }
}
```

## 4. 小程序跳转
```javascript
// 跳转到小程序
wx.miniProgram.navigateTo({
  url: '/pages/index?param=value'
});

// 返回小程序
wx.miniProgram.navigateBack();
```

应用名称：$ARGUMENTS
```

**使用方式**: `/project:h5:wechat EcommerceStore`

### 18. H5游戏开发 (`h5/game.md`)
```markdown
---
description: 创建H5游戏项目
argument-hint: [游戏名称]
allowed-tools: Write(*), Edit(*), Bash(*)
---

# 🎮 H5游戏开发

开发 $ARGUMENTS H5游戏：

## 1. 游戏引擎选择
```javascript
// Phaser 3游戏引擎
import Phaser from 'phaser';

class GameScene extends Phaser.Scene {
  constructor() {
    super({ key: '${ARGUMENTS}Scene' });
  }

  preload() {
    // 加载游戏资源
    this.load.image('player', 'assets/player.png');
    this.load.image('enemy', 'assets/enemy.png');
    this.load.audio('bgm', 'assets/background.mp3');
  }

  create() {
    // 创建游戏对象
    this.player = this.add.sprite(400, 300, 'player');
    this.enemies = this.add.group();

    // 设置物理效果
    this.physics.add.collider(this.player, this.enemies, this.hitEnemy, null, this);

    // 输入控制
    this.cursors = this.input.keyboard.createCursorKeys();
  }

  update() {
    // 游戏循环更新
    this.handleInput();
    this.updateEnemies();
  }

  handleInput() {
    if (this.cursors.left.isDown) {
      this.player.x -= 5;
    }
    if (this.cursors.right.isDown) {
      this.player.x += 5;
    }
  }
}

// 游戏配置
const config = {
  type: Phaser.AUTO,
  width: 800,
  height: 600,
  physics: {
    default: 'arcade',
    arcade: {
      gravity: { y: 300 },
      debug: false
    }
  },
  scene: GameScene
};

const game = new Phaser.Game(config);
```

## 2. 移动端适配
```javascript
// 响应式游戏布局
class ResponsiveGame {
  constructor() {
    this.setupResize();
    this.setupTouch();
  }

  setupResize() {
    window.addEventListener('resize', () => {
      this.resizeGame();
    });
  }

  setupTouch() {
    // 虚拟手柄
    this.virtualGamepad = new VirtualGamepad();
  }

  resizeGame() {
    const canvas = document.querySelector('canvas');
    const windowWidth = window.innerWidth;
    const windowHeight = window.innerHeight;

    // 计算缩放比例
    const scale = Math.min(windowWidth / 800, windowHeight / 600);
    canvas.style.transform = `scale(${scale})`;
  }
}
```

## 3. 性能优化
- 对象池管理
- 纹理图集优化
- 音频压缩
- 帧率控制

## 4. 发布配置
```javascript
// 构建优化
const gameConfig = {
  // 生产环境配置
  physics: {
    default: 'arcade',
    arcade: {
      debug: false // 关闭调试模式
    }
  },
  // 资源预加载
  preloader: {
    showProgressBar: true,
    progressBarColor: '#ff6b6b'
  }
};
```

游戏名称：$ARGUMENTS
```

**使用方式**: `/project:h5:game FlappyBird`

## 🔄 跨平台开发命令 (2个)

### 19. 多端统一开发 (`cross/unified.md`)
```markdown
---
description: 创建多端统一开发项目
argument-hint: [项目名称]
allowed-tools: Bash(*), Write(*), Edit(*)
---

# 🔄 多端统一开发

构建 $ARGUMENTS 跨平台项目：

## 1. Taro多端框架
```bash
# 安装Taro CLI
npm install -g @tarojs/cli

# 创建项目
taro init $ARGUMENTS
cd $ARGUMENTS

# 安装依赖
npm install
```

## 2. 项目配置
```javascript
// config/index.js
const config = {
  projectName: '$ARGUMENTS',
  date: '2025-1-1',
  designWidth: 750,
  deviceRatio: {
    640: 2.34 / 2,
    750: 1,
    828: 1.81 / 2
  },
  sourceRoot: 'src',
  outputRoot: 'dist',
  plugins: [],
  defineConstants: {},
  copy: {
    patterns: [],
    options: {}
  },
  framework: 'react',
  compiler: 'webpack5',
  mini: {
    postcss: {
      pxtransform: {
        enable: true,
        config: {}
      }
    }
  },
  h5: {
    publicPath: '/',
    staticDirectory: 'static',
    postcss: {
      autoprefixer: {
        enable: true
      }
    }
  }
}
```

## 3. 多端组件
```typescript
// src/components/UniversalButton.tsx
import Taro from '@tarojs/taro';
import { Button } from '@tarojs/components';
import { FC } from 'react';

interface UniversalButtonProps {
  text: string;
  onClick: () => void;
  type?: 'primary' | 'default';
}

const UniversalButton: FC<UniversalButtonProps> = ({ text, onClick, type = 'default' }) => {
  const handleClick = () => {
    // 不同平台的反馈
    if (process.env.TARO_ENV === 'weapp') {
      Taro.vibrateShort();
    }
    onClick();
  };

  return (
    <Button
      className={`universal-btn universal-btn--${type}`}
      onClick={handleClick}
    >
      {text}
    </Button>
  );
};
```

## 4. 平台差异处理
```typescript
// src/utils/platform.ts
export const getPlatform = () => {
  return process.env.TARO_ENV;
};

export const isWeapp = () => process.env.TARO_ENV === 'weapp';
export const isH5 = () => process.env.TARO_ENV === 'h5';
export const isRN = () => process.env.TARO_ENV === 'rn';

// 平台特定代码
if (isWeapp()) {
  // 小程序特定逻辑
} else if (isH5()) {
  // H5特定逻辑
}
```

## 5. 构建发布
```bash
# 构建小程序
npm run build:weapp

# 构建H5
npm run build:h5

# 构建React Native
npm run build:rn
```

项目名称：$ARGUMENTS
```

**使用方式**: `/project:cross:unified MultiPlatformApp`

### 20. 代码共享库 (`cross/shared.md`)
```markdown
---
description: 创建跨平台代码共享库
argument-hint: [库名称]
allowed-tools: Write(*), Edit(*), Bash(*)
---

# 📚 代码共享库

构建 $ARGUMENTS 共享代码库：

## 1. Monorepo架构
```bash
# 使用Lerna管理多包
npm install -g lerna
lerna init

# 项目结构
packages/
├── shared-core/        # 核心逻辑
├── shared-ui/          # UI组件
├── shared-utils/       # 工具函数
├── mobile-app/         # 移动端应用
├── web-app/           # Web应用
└── h5-app/            # H5应用
```

## 2. 核心共享代码
```typescript
// packages/shared-core/src/api/$ARGUMENTS.ts
export interface ${ARGUMENTS}Config {
  baseURL: string;
  apiKey: string;
  timeout: number;
}

export class ${ARGUMENTS}API {
  private config: ${ARGUMENTS}Config;

  constructor(config: ${ARGUMENTS}Config) {
    this.config = config;
  }

  async request<T>(endpoint: string, options?: RequestInit): Promise<T> {
    const url = `${this.config.baseURL}${endpoint}`;
    const response = await fetch(url, {
      ...options,
      headers: {
        'Authorization': `Bearer ${this.config.apiKey}`,
        'Content-Type': 'application/json',
        ...options?.headers
      },
      timeout: this.config.timeout
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    return response.json();
  }
}
```

## 3. 平台适配层
```typescript
// packages/shared-core/src/platform/index.ts
export interface PlatformAdapter {
  storage: {
    get(key: string): Promise<string | null>;
    set(key: string, value: string): Promise<void>;
    remove(key: string): Promise<void>;
  };
  network: {
    isConnected(): Promise<boolean>;
  };
  device: {
    getInfo(): Promise<DeviceInfo>;
  };
}

// React Native适配器
export class ReactNativeAdapter implements PlatformAdapter {
  storage = {
    async get(key: string) {
      return AsyncStorage.getItem(key);
    },
    async set(key: string, value: string) {
      return AsyncStorage.setItem(key, value);
    },
    async remove(key: string) {
      return AsyncStorage.removeItem(key);
    }
  };

  network = {
    async isConnected() {
      const state = await NetInfo.fetch();
      return state.isConnected;
    }
  };
}

// Web适配器
export class WebAdapter implements PlatformAdapter {
  storage = {
    async get(key: string) {
      return localStorage.getItem(key);
    },
    async set(key: string, value: string) {
      localStorage.setItem(key, value);
      return Promise.resolve();
    },
    async remove(key: string) {
      localStorage.removeItem(key);
      return Promise.resolve();
    }
  };

  network = {
    async isConnected() {
      return navigator.onLine;
    }
  };
}
```

## 4. 构建配置
```javascript
// packages/shared-core/rollup.config.js
export default {
  input: 'src/index.ts',
  output: [
    {
      file: 'dist/index.cjs.js',
      format: 'cjs'
    },
    {
      file: 'dist/index.esm.js',
      format: 'esm'
    }
  ],
  external: ['react', 'react-native'],
  plugins: [
    typescript(),
    resolve(),
    commonjs()
  ]
};
```

## 5. 发布管理
```bash
# 版本管理
lerna version

# 发布到npm
lerna publish

# 本地链接测试
lerna link
```

库名称：$ARGUMENTS
```

**使用方式**: `/project:cross:shared MySharedLibrary`

## 📝 配置和部署指南

### 快速部署所有命令
```bash
# 1. 创建完整的命令目录结构
mkdir -p .claude/commands/{mobile,harmony,web,h5,cross,tools}

# 2. 复制所有命令文件到对应目录
# (将上述20个命令的markdown内容保存到对应路径)

# 3. 在Claude Code中使用命令
# 移动端: /project:mobile:rn-init MyApp
# 鸿蒙: /project:harmony:init HarmonyApp
# Web: /project:web:app ReactApp
# H5: /project:h5:mobile H5App
# 跨平台: /project:cross:unified MultiApp
```

### 命令分类说明

| 分类 | 命令数量 | 主要功能 |
|------|---------|----------|
| 📱 移动端 | 6个 | React Native、Android、iOS、Flutter开发 |
| 🌸 鸿蒙 | 4个 | HarmonyOS、ArkTS、ArkUI开发 |
| 🌐 Web | 5个 | React、Vue、PWA、性能优化 |
| 📲 H5 | 3个 | 移动端H5、微信生态、游戏开发 |
| 🔄 跨平台 | 2个 | 多端统一、代码共享 |

### 最佳实践建议

1. **技术栈一致性** - 在同一项目中保持技术栈的一致性
2. **性能优先** - 移动端开发特别注意性能和内存管理
3. **平台适配** - 充分考虑不同平台的特性和限制
4. **代码复用** - 最大化跨平台代码的复用率
5. **测试覆盖** - 确保在目标平台上进行充分测试

通过这些专业的移动端、鸿蒙、Web和H5开发命令，可以显著提升跨平台开发的效率和质量！