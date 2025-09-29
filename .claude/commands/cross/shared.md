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