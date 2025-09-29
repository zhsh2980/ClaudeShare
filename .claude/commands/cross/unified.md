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