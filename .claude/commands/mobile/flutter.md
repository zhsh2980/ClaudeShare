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