---
description: 创建鸿蒙后台服务
argument-hint: [服务名称]
allowed-tools: Write(*), Edit(*)
---

# ⚙️ 鸿蒙服务开发

开发 $ARGUMENTS 后台服务：

## 1. ServiceExtensionAbility
```typescript
import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';
import Want from '@ohos.app.ability.Want';

export default class ${ARGUMENTS}Service extends ServiceExtensionAbility {
  onCreate(want: Want): void {
    console.info(`${ARGUMENTS}Service onCreate`);
    // 服务初始化
  }

  onRequest(want: Want, startId: number): void {
    console.info(`${ARGUMENTS}Service onRequest`);
    // 处理服务请求
  }

  onDestroy(): void {
    console.info(`${ARGUMENTS}Service onDestroy`);
    // 服务销毁清理
  }
}
```

## 2. 模块配置
```json5
// module.json5
{
  "extensionAbilities": [
    {
      "name": "${ARGUMENTS}Service",
      "srcEntry": "./ets/services/${ARGUMENTS}Service.ts",
      "type": "service",
      "exported": true
    }
  ]
}
```

## 3. 后台任务
- 长时运行任务
- 延时任务调度
- 工作调度器

## 4. 系统能力调用
- 位置服务
- 推送通知
- 设备管理
- 网络监听

服务名称：$ARGUMENTS