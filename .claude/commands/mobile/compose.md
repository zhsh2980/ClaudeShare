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