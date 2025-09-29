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