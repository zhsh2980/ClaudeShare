---
description: 生成iOS SwiftUI视图组件
argument-hint: [视图名称]
allowed-tools: Write(*), Edit(*)
---

# 🍎 SwiftUI 视图生成

创建 $ARGUMENTS SwiftUI视图：

## 1. 视图结构
```swift
import SwiftUI

struct $ARGUMENTS: View {
    // 状态属性
    @State private var isLoading = false

    var body: some View {
        // 视图内容
        VStack {
            // UI组件
        }
        .navigationTitle("$ARGUMENTS")
        .padding()
    }
}

struct ${ARGUMENTS}_Previews: PreviewProvider {
    static var previews: some View {
        $ARGUMENTS()
    }
}
```

## 2. 功能特性
- 声明式UI设计
- 状态绑定和数据流
- 动画和过渡效果
- 导航和路由处理

## 3. 平台适配
- iPhone和iPad适配
- 深色模式支持
- 动态类型支持
- VoiceOver可访问性

视图名称：$ARGUMENTS