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