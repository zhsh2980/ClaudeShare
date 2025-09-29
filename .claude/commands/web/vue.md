---
description: 创建Vue 3组合式API组件
argument-hint: [组件名称]
allowed-tools: Write(*), Edit(*)
---

# 🎨 Vue 3 组合式API组件

开发 $ARGUMENTS Vue组件：

## 1. 组件结构
```vue
<template>
  <div class="${ARGUMENTS}">
    <!-- 组件模板 -->
    <h2>{{ title }}</h2>
    <slot />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'

// Props定义
interface Props {
  title?: string
}

const props = withDefaults(defineProps<Props>(), {
  title: '$ARGUMENTS'
})

// 响应式数据
const count = ref(0)
const isLoading = ref(false)

// 计算属性
const displayText = computed(() => {
  return `${props.title} - ${count.value}`
})

// 生命周期
onMounted(() => {
  console.log('$ARGUMENTS mounted')
})

// 方法
const handleClick = () => {
  count.value++
}

// 暴露给父组件
defineExpose({
  reset: () => count.value = 0
})
</script>

<style scoped>
.${ARGUMENTS} {
  /* 组件样式 */
}
</style>
```

## 2. TypeScript支持
- Props类型定义
- Emits事件类型
- 组合式函数类型

## 3. 性能优化
- defineAsyncComponent
- v-memo 指令
- keep-alive 缓存

组件名称：$ARGUMENTS