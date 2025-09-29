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