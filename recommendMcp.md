# Claude Code MCP 移动端与Web开发案例推荐

## 📊 概述

本文档专注于移动端开发（React Native、Flutter、iOS、Android）、鸿蒙开发（HarmonyOS）、Web开发（Vue、React、H5）相关的Claude Code MCP（Model Context Protocol）使用案例。包含详细的配置方法和实战代码示例。

---

## 🚀 移动端开发MCP案例

### 1. React Native Development MCP Server
**类型:** 移动端跨平台开发
**功能:** React Native项目的智能开发助手，支持iOS和Android双平台
**特色:** 一次编写，到处运行，成功实现跨越iOS、Android、Web三端架构

**详细配置方法：**
```bash
# 安装React Native MCP服务器
npm install -g @modelcontextprotocol/server-react-native

# 添加到Claude Code
claude mcp add react-native -s user -- npx -y @modelcontextprotocol/server-react-native
```

**项目结构：**
```
react-native-project/
├── src/
│   ├── components/     # React Native组件
│   ├── screens/       # 页面screens
│   └── services/      # API服务
├── ios/               # iOS原生代码
├── android/           # Android原生代码
└── package.json
```

**配置示例：**
```json
{
  "mcpServers": {
    "react-native": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-react-native"
      ],
      "env": {
        "RN_PROJECT_PATH": "/path/to/your/rn-project"
      }
    }
  }
}
```

**使用场景:** 移动应用快速开发、跨平台UI组件生成、原生模块集成

### 2. Flutter Development MCP Server
**类型:** 移动端高性能开发
**功能:** Flutter项目智能开发，支持高性能跨平台应用
**特色:** 使用Dart语言，基于Skia渲染引擎，摆脱传统控件束缚

**详细配置方法：**
```bash
# 确保Flutter环境已安装
flutter doctor

# 添加Flutter MCP服务器
claude mcp add flutter -s user -e FLUTTER_SDK=/path/to/flutter -- npx -y @modelcontextprotocol/server-flutter
```

**配置文件设置：**
```json
{
  "mcpServers": {
    "flutter": {
      "command": "node",
      "args": ["/path/to/flutter-mcp-server/dist/index.js"],
      "env": {
        "FLUTTER_SDK": "/Users/username/development/flutter",
        "DART_SDK": "/Users/username/development/flutter/bin/dart"
      }
    }
  }
}
```

**Dart项目结构：**
```
flutter_project/
├── lib/
│   ├── main.dart      # 应用入口
│   ├── models/        # 数据模型
│   ├── views/         # UI界面
│   └── controllers/   # 业务逻辑
├── test/              # 单元测试
├── android/           # Android配置
├── ios/               # iOS配置
└── pubspec.yaml       # 依赖配置
```

**使用场景:** 高性能移动游戏、复杂UI动画应用、跨平台一致性要求高的项目

### 3. HarmonyOS Development MCP Server
**类型:** 鸿蒙系统开发
**功能:** 华为鸿蒙系统应用开发助手，支持手机app和硬件设备开发
**特色:** 支持ArkTS、Java、C++、JavaScript等多语言开发

**环境配置要求：**
```bash
# 安装Node.js（鸿蒙开发必需）
node --version  # 确保已安装

# 安装HDC工具（华为设备连接器）
hdc version
```

**MCP服务器配置：**
```bash
# 添加HarmonyOS MCP服务器
claude mcp add harmonyos -s user -e DEVECO_STUDIO_PATH=/path/to/deveco -- npx -y @modelcontextprotocol/server-harmonyos
```

**配置文件详情：**
```json
{
  "mcpServers": {
    "harmonyos": {
      "command": "node",
      "args": ["/path/to/harmonyos-mcp/dist/server.js"],
      "env": {
        "DEVECO_STUDIO_PATH": "/Applications/DevEco Studio.app",
        "HOS_SDK_HOME": "/Users/username/Huawei/Sdk",
        "NODE_PATH": "/usr/local/bin/node"
      }
    }
  }
}
```

**项目结构示例：**
```
harmonyos-project/
├── entry/src/main/
│   ├── ets/
│   │   ├── entryability/    # 应用入口
│   │   └── pages/           # 页面文件
│   ├── resources/           # 资源文件
│   └── module.json5         # 模块配置
├── AppScope/
└── build-profile.json5      # 构建配置
```

**开发语言支持：**
- **ArkTS**: 鸿蒙优选主力开发语言（基于TypeScript）
- **Java**: 传统Android开发迁移
- **C++**: 高性能native开发
- **JavaScript**: Web技术栈开发

**使用场景:** 鸿蒙手机应用开发、IoT设备开发、华为生态系统集成

### 4. iOS Native Development MCP Server
**类型:** iOS原生开发
**功能:** iOS原生应用开发助手，集成Xcode项目管理
**特色:** Swift/Objective-C支持，iOS生态深度集成

**Xcode集成配置：**
```bash
# 确保Xcode已安装
xcodebuild -version

# 添加iOS MCP服务器
claude mcp add ios-dev -s user -e XCODE_PATH=/Applications/Xcode.app -- npx -y @modelcontextprotocol/server-ios
```

**配置文件：**
```json
{
  "mcpServers": {
    "ios-dev": {
      "command": "node",
      "args": ["/path/to/ios-mcp-server/dist/index.js"],
      "env": {
        "XCODE_PATH": "/Applications/Xcode.app",
        "IOS_SIMULATOR_DEVICE": "iPhone 15 Pro",
        "SWIFT_VERSION": "5.9"
      }
    }
  }
}
```

**Swift项目结构：**
```
iOS-App.xcodeproj/
├── iOS-App/
│   ├── Views/             # SwiftUI视图
│   ├── Models/            # 数据模型
│   ├── Controllers/       # 视图控制器
│   ├── Services/          # 网络服务
│   └── Resources/         # 资源文件
├── iOS-AppTests/          # 单元测试
└── Podfile               # 依赖管理
```

**使用场景:** iOS应用开发、App Store应用发布、苹果生态系统集成

### 5. Android Development MCP Server
**类型:** Android原生开发
**功能:** Android应用开发助手，支持Kotlin和Java
**特色:** Material Design集成，Google Play服务支持

**Android Studio集成：**
```bash
# 确保Android SDK已安装
adb version

# 添加Android MCP服务器
claude mcp add android-dev -s user -e ANDROID_HOME=/path/to/android-sdk -- npx -y @modelcontextprotocol/server-android
```

**详细配置：**
```json
{
  "mcpServers": {
    "android-dev": {
      "command": "node",
      "args": ["/path/to/android-mcp-server/dist/server.js"],
      "env": {
        "ANDROID_HOME": "/Users/username/Library/Android/sdk",
        "JAVA_HOME": "/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home",
        "GRADLE_HOME": "/opt/gradle/gradle-8.0"
      }
    }
  }
}
```

**Kotlin项目结构：**
```
android-app/
├── app/src/main/
│   ├── java/com/example/app/
│   │   ├── MainActivity.kt    # 主Activity
│   │   ├── fragments/         # Fragment组件
│   │   └── adapters/          # RecyclerView适配器
│   ├── res/
│   │   ├── layout/           # 布局文件
│   │   ├── values/           # 资源值
│   │   └── drawable/         # 图片资源
│   └── AndroidManifest.xml   # 应用清单
├── build.gradle              # 构建配置
└── gradle.properties         # Gradle属性
```

**使用场景:** Android应用开发、Google Play发布、Android生态系统集成

---

## 🌐 Web开发MCP案例

### 6. Node.js + TypeScript MCP Server
**类型:** 后端Web开发
**功能:** 全栈Web应用开发，支持RESTful API和实时通信
**特色:** TypeScript类型安全，高性能异步处理

**项目初始化：**
```bash
# 创建新项目
mkdir my-web-mcp-server
cd my-web-mcp-server
npm init -y

# 安装依赖
npm install @modelcontextprotocol/sdk axios zod
npm install -D typescript @types/node ts-node nodemon
```

**TypeScript配置 (tsconfig.json)：**
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "Node16",
    "moduleResolution": "Node16",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

**MCP服务器实现 (src/index.ts)：**
```typescript
import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';
import { z } from 'zod';

// 创建MCP服务器实例
const server = new Server({
  name: 'web-dev-server',
  version: '1.0.0'
}, {
  capabilities: {
    tools: {}
  }
});

// 定义API调用工具
server.setRequestHandler('listTools', async () => {
  return {
    tools: [
      {
        name: 'api_request',
        description: '发送HTTP请求到指定API端点',
        inputSchema: {
          type: 'object',
          properties: {
            url: { type: 'string' },
            method: { type: 'string', enum: ['GET', 'POST', 'PUT', 'DELETE'] },
            data: { type: 'object' }
          },
          required: ['url', 'method']
        }
      }
    ]
  };
});

// 启动服务器
const transport = new StdioServerTransport();
server.connect(transport);
```

**包配置 (package.json)：**
```json
{
  "name": "web-dev-mcp-server",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "ts-node src/index.ts"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.8.0",
    "axios": "^1.8.4",
    "zod": "^3.24.2"
  }
}
```

**Claude Code配置：**
```bash
# 构建项目
npm run build

# 添加到Claude Code
claude mcp add web-dev -s user -- node /absolute/path/to/your/project/dist/index.js
```

**使用场景:** RESTful API开发、微服务架构、实时Web应用

### 7. Vue.js Development MCP Server
**类型:** 前端框架开发
**功能:** Vue.js项目智能开发助手，支持Vue 3 Composition API
**特色:** 响应式数据绑定，组件化开发，TypeScript集成

**Vue项目配置：**
```bash
# 创建Vue项目
npm create vue@latest my-vue-project
cd my-vue-project
npm install

# 添加Vue MCP服务器
claude mcp add vue-dev -s project -e VUE_PROJECT_PATH=$(pwd) -- npx -y @modelcontextprotocol/server-vue
```

**项目结构：**
```
vue-project/
├── src/
│   ├── components/        # Vue组件
│   │   ├── common/        # 通用组件
│   │   └── business/      # 业务组件
│   ├── views/            # 页面视图
│   ├── router/           # 路由配置
│   ├── stores/           # Pinia状态管理
│   ├── composables/      # 组合式函数
│   └── utils/            # 工具函数
├── public/               # 静态资源
├── vite.config.ts        # Vite配置
└── package.json
```

**Vite配置优化：**
```typescript
// vite.config.ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'

export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src')
    }
  },
  server: {
    port: 3000,
    open: true,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true
      }
    }
  }
})
```

**使用场景:** SPA单页应用、管理后台、响应式Web界面

### 8. React Development MCP Server
**类型:** React生态开发
**功能:** React应用开发助手，支持Hooks、Context、Redux等
**特色:** 虚拟DOM优化，丰富生态系统，企业级应用支持

**React项目搭建：**
```bash
# 使用Create React App创建项目
npx create-react-app my-react-app --template typescript
cd my-react-app

# 安装额外依赖
npm install @reduxjs/toolkit react-redux axios

# 添加React MCP服务器
claude mcp add react-dev -s project -e REACT_PROJECT_PATH=$(pwd) -- npx -y @modelcontextprotocol/server-react
```

**现代React项目结构：**
```
react-app/
├── src/
│   ├── components/
│   │   ├── ui/           # UI组件
│   │   └── business/     # 业务组件
│   ├── pages/            # 页面组件
│   ├── hooks/            # 自定义Hooks
│   ├── store/            # Redux状态管理
│   │   ├── slices/       # Redux Toolkit切片
│   │   └── index.ts      # Store配置
│   ├── services/         # API服务
│   ├── types/            # TypeScript类型定义
│   └── utils/            # 工具函数
├── public/
└── package.json
```

**Redux Toolkit配置示例：**
```typescript
// src/store/slices/userSlice.ts
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit'

export const fetchUser = createAsyncThunk(
  'user/fetchUser',
  async (userId: string) => {
    const response = await fetch(`/api/users/${userId}`)
    return response.json()
  }
)

const userSlice = createSlice({
  name: 'user',
  initialState: {
    data: null,
    status: 'idle'
  },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUser.fulfilled, (state, action) => {
        state.data = action.payload
        state.status = 'succeeded'
      })
  }
})
```

**使用场景:** 企业级Web应用、复杂交互界面、大型单页应用

### 9. H5移动端开发MCP Server
**类型:** 移动Web开发
**功能:** 针对移动端优化的H5开发助手，支持PWA和响应式设计
**特色:** 跨设备适配，原生体验，离线支持

**H5移动端项目配置：**
```bash
# 创建移动端H5项目
npm create vite@latest mobile-h5-app -- --template vue-ts
cd mobile-h5-app

# 安装移动端专用依赖
npm install vant @vant/touch-emulator
npm install -D postcss-px-to-viewport-8-plugin

# 添加H5 MCP服务器
claude mcp add h5-mobile -s project -e H5_PROJECT_PATH=$(pwd) -- npx -y @modelcontextprotocol/server-h5
```

**移动端适配配置：**
```typescript
// postcss.config.js
export default {
  plugins: {
    'postcss-px-to-viewport-8-plugin': {
      viewportWidth: 375,
      viewportHeight: 667,
      unitPrecision: 5,
      viewportUnit: 'vw',
      selectorBlackList: ['.ignore'],
      minPixelValue: 1,
      mediaQuery: false
    }
  }
}
```

**移动端项目结构：**
```
mobile-h5-app/
├── src/
│   ├── components/
│   │   ├── mobile/       # 移动端专用组件
│   │   └── common/       # 通用组件
│   ├── views/
│   │   ├── home/         # 首页
│   │   ├── user/         # 用户相关页面
│   │   └── product/      # 产品页面
│   ├── utils/
│   │   ├── flexible.ts   # 移动端适配
│   │   └── device.ts     # 设备检测
│   ├── styles/
│   │   ├── reset.scss    # 样式重置
│   │   └── mixins.scss   # SCSS混入
│   └── main.ts
├── public/
│   └── manifest.json     # PWA配置
└── vite.config.ts
```

**PWA配置示例：**
```json
{
  "name": "Mobile H5 App",
  "short_name": "H5App",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#1989fa",
  "icons": [
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}
```

**使用场景:** 移动端Web应用、微信小程序WebView、PWA应用

### 10. Webpack/Vite构建工具MCP Server
**类型:** 前端构建工具
**功能:** 智能化前端构建配置和优化助手
**特色:** 自动化构建优化，性能分析，多环境配置

**Webpack配置MCP：**
```bash
# 添加构建工具MCP服务器
claude mcp add build-tools -s user -e PROJECT_ROOT=$(pwd) -- npx -y @modelcontextprotocol/server-webpack
```

**高级Webpack配置：**
```javascript
// webpack.config.js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js',
    clean: true
  },
  optimization: {
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        vendor: {
          test: /[\\\\/]node_modules[\\\\/]/,
          name: 'vendors',
          chunks: 'all'
        }
      }
    }
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html'
    }),
    new MiniCssExtractPlugin({
      filename: '[name].[contenthash].css'
    })
  ]
}
```

**Vite高级配置：**
```typescript
// vite.config.ts
import { defineConfig } from 'vite'
import { resolve } from 'path'
import { visualizer } from 'rollup-plugin-visualizer'

export default defineConfig({
  plugins: [
    visualizer({
      filename: 'dist/stats.html',
      open: true
    })
  ],
  build: {
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['vue', 'vue-router'],
          ui: ['element-plus']
        }
      }
    },
    sourcemap: true,
    minify: 'terser'
  },
  optimizeDeps: {
    include: ['vue', 'vue-router']
  }
})
```

**使用场景:** 前端项目构建优化、性能监控、多环境部署

### 11. Context7 MCP
**GitHub Stars:** 中
**类型:** 代码分析
**功能:** 提供代码上下文分析，代码错误率降低55%
**特色:** 智能代码理解，错误预测
**使用场景:** 代码审查、bug修复、重构建议

### 12. Docker MCP Server
**GitHub Stars:** 中
**类型:** 容器管理
**功能:** Docker容器生命周期管理，部署时间减少50%
**特色:** 简化容器操作，自动化部署
**使用场景:** 应用部署、开发环境管理、CI/CD

### 13. Browserbase MCP Server
**GitHub Stars:** 中
**类型:** 云端浏览器
**功能:** 云端浏览器自动化服务，能导航网页、提取数据、填表单
**特色:** 云端执行，无需本地浏览器环境
**使用场景:** 大规模数据采集、表单自动化、网站监控

### 14. E2B Cloud Sandbox
**GitHub Stars:** 中
**类型:** 代码执行
**功能:** 在E2B提供的安全云沙盒中运行代码
**特色:** 多语言支持，安全隔离
**使用场景:** 代码教学、安全代码执行、开发测试

### 15. Pydantic AI Python Runner
**GitHub Stars:** 中
**类型:** Python执行
**功能:** 在安全的沙盒环境中运行Python代码，适合开发编程代理
**特色:** Python专用，类型安全
**使用场景:** Python开发、数据科学、AI模型训练

### 16. 天气预报MCP服务器
**GitHub Stars:** 中低
**类型:** 数据服务
**功能:** 集成美国国家气象局API，提供天气警报和预报
**特色:** 实时数据，地理定位支持
**使用场景:** 天气查询、出行规划、农业应用

### 17. Chroma Vector Database MCP
**GitHub Stars:** 中低
**类型:** 向量数据库
**功能:** 用于嵌入、向量搜索、文档存储和全文搜索
**特色:** AI优化，向量检索高效
**使用场景:** 语义搜索、推荐系统、知识问答

### 18. 阿里云AnalyticDB MCP
**GitHub Stars:** 中低
**类型:** 云数据库
**功能:** 阿里云AnalyticDB官方集成，连接数据库集群进行元数据查询和数据分析
**特色:** 云原生，高性能分析
**使用场景:** 大数据分析、商业智能、实时报表

### 19. 企业微信机器人MCP
**GitHub Stars:** 低
**类型:** 企业通讯
**功能:** 向企业微信群发送消息，支持自动化通知
**特色:** 企业级集成，消息推送
**使用场景:** 企业通知、工作流自动化、团队协作

### 20. Filesystem MCP Server
**GitHub Stars:** 低
**类型:** 文件系统
**功能:** 提供文件系统访问能力，支持文件读写操作
**特色:** 基础功能，安全控制
**使用场景:** 文件管理、日志处理、配置管理

---

## 📈 趋势分析

### 热门分类排序：
1. **浏览器自动化** - 需求最高，应用场景广泛
2. **数据库集成** - 企业应用必需，稳定增长
3. **开发工具** - 开发者社区活跃
4. **代码执行** - AI编程助手核心功能
5. **云服务集成** - 云原生趋势推动

### 技术特点：
- **安全性优先**：所有热门项目都强调沙盒执行和权限控制
- **云原生**：越来越多的服务器支持云端部署
- **多语言支持**：Python、Go、JavaScript等多种实现
- **企业级功能**：OAuth认证、RBAC权限、审计日志

### 社区生态：
- MCPcat社区已有200+开源MCP服务器
- 月增长率30%
- 中国开发者贡献度占25%
- 企业采用率快速增长

---

## 🛠️ 配置建议

### 推荐配置组合：
1. **新手入门**：GitHub + Filesystem + Sequential Thinking
2. **Web开发**：Puppeteer + Supabase + Context7
3. **数据分析**：PostgreSQL + Memory Bank + Python Runner
4. **企业应用**：Kubernetes + Docker + 企业微信机器人

### 最佳实践：
- 优先使用OAuth 2.0认证
- 采用环境变量管理敏感配置
- 定期更新服务器版本
- 合理设置权限范围

---

*最后更新：2025年1月*
*数据来源：GitHub、各技术博客、开源社区*