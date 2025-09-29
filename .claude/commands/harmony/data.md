---
description: 实现鸿蒙应用数据存储和管理
argument-hint: [数据模型名称]
allowed-tools: Write(*), Edit(*)
---

# 💾 鸿蒙数据管理

为 $ARGUMENTS 实现数据管理：

## 1. 数据模型定义
```typescript
// $ARGUMENTS.ets
export class $ARGUMENTS {
  id: string;
  name: string;
  createTime: number;

  constructor(id: string, name: string) {
    this.id = id;
    this.name = name;
    this.createTime = Date.now();
  }
}
```

## 2. 首选项存储
```typescript
import preferences from '@ohos.data.preferences';

class ${ARGUMENTS}Storage {
  private static instance: ${ARGUMENTS}Storage;
  private pref: preferences.Preferences | null = null;

  static getInstance(): ${ARGUMENTS}Storage {
    if (!${ARGUMENTS}Storage.instance) {
      ${ARGUMENTS}Storage.instance = new ${ARGUMENTS}Storage();
    }
    return ${ARGUMENTS}Storage.instance;
  }

  async save$ARGUMENTS(data: $ARGUMENTS): Promise<void> {
    await this.pref?.put('${ARGUMENTS}_' + data.id, JSON.stringify(data));
    await this.pref?.flush();
  }
}
```

## 3. 关系型数据库
```typescript
import relationalStore from '@ohos.data.relationalStore';

const SQL_CREATE_TABLE = `
  CREATE TABLE IF NOT EXISTS ${ARGUMENTS} (
    id TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    createTime INTEGER
  )
`;
```

## 4. 分布式数据
- 设备间数据同步
- 分布式对象管理
- 数据权限控制

数据模型：$ARGUMENTS