---
description: 初始化HarmonyOS应用项目
argument-hint: [应用名称]
allowed-tools: Bash(*), Write(*), Edit(*)
---

# 🌸 HarmonyOS 应用初始化

创建 $ARGUMENTS 鸿蒙应用：

## 1. 开发环境检查
!`node --version`
!`npm list @ohos/hvigor -g`

## 2. 项目创建
```bash
# 使用DevEco Studio模板或hvigor工具
hvigor create $ARGUMENTS --template=stage
cd $ARGUMENTS
npm install
```

## 3. 项目配置
- 配置应用签名
- 设置权限申请
- 配置构建脚本

## 4. 目录结构
```
src/main/
├── ets/           # ArkTS源码
├── resources/     # 资源文件
└── module.json5   # 模块配置
```

## 5. 基础代码
```typescript
// Index.ets
@Entry
@Component
struct Index {
  @State message: string = 'Hello $ARGUMENTS'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

应用名称：$ARGUMENTS