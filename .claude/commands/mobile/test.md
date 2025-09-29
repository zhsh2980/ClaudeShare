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