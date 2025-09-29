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