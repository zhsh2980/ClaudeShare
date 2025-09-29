---
description: 创建ArkTS自定义组件
argument-hint: [组件名称]
allowed-tools: Write(*), Edit(*)
---

# 🎨 ArkTS 组件开发

构建 $ARGUMENTS ArkTS组件：

## 1. 组件定义
```typescript
@Component
export struct $ARGUMENTS {
  // 组件属性
  @Prop data: string = '';
  @State isVisible: boolean = true;

  build() {
    Column() {
      // 组件UI结构
      if (this.isVisible) {
        Text(this.data)
          .fontSize(16)
          .fontColor(Color.Black)
          .margin(10)
      }
    }
    .width('100%')
    .height('auto')
    .padding(12)
  }
}
```

## 2. 生命周期
- aboutToAppear()
- aboutToDisappear()
- onPageShow()
- onPageHide()

## 3. 状态管理
- @State 组件内部状态
- @Prop 父组件传递属性
- @Link 双向数据绑定
- @Provide/@Consume 跨组件通信

## 4. 事件处理
- 点击事件
- 触摸事件
- 滑动手势
- 长按操作

## 5. 动画效果
```typescript
.animation({
  duration: 300,
  curve: Curve.EaseInOut
})
```

组件名称：$ARGUMENTS