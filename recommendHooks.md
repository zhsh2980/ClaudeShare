# Claude Code Hooks 移动端/Web/鸿蒙开发实用案例大全 (20个专业案例)

基于最新的移动端开发、鸿蒙开发、Web和H5开发需求，整理了针对性的 Claude Code hooks 实用案例。

## 📚 资源来源

### 官方文档
- [Claude Code hooks 入门指南](https://docs.claude.com/zh-CN/docs/claude-code/hooks-guide)
- [Hooks 参考文档](https://docs.claude.com/zh-CN/docs/claude-code/hooks)

### 移动端开发资源
- [Claude加速Android App开发 - Jetpack与Compose结合](https://blog.csdn.net/u011897062/article/details/142264912)
- [Claude Code 中文开发套件](https://github.com/hifoxdot/claude-init-CN)
- [React Native app with Claude AI](https://designcode.io/react-native-ai/)
- [深度使用Claude code移动开发心得](https://blog.csdn.net/kof820/article/details/149313531)

### 鸿蒙开发资源
- [HarmonyOS ArkUI 框架实现原理](https://zhuanlan.zhihu.com/p/679207951)
- [跟老卫学HarmonyOS开发教程](https://gitee.com/waylau/harmonyos-tutorial)
- [ArkTS语法和鸿蒙组件实战](https://github.com/hi-dhl/HarmonyPractice)
- [华为开发者联盟 ArkUI文档](https://developer.huawei.com/consumer/cn/arkui/)

### Web/H5开发资源
- [最强Coding Agent: Claude Code权威实践指南](https://zhuanlan.zhihu.com/p/1920263182062163086)
- [Claude Code深度实战完整开发指南](https://aicoding.csdn.net/68872aac080e555a88d2f7f7.html)
- [Claude Code前端开发工作流自动化](https://mcp.csdn.net/686e9470080e555a88ce6b04.html)
- [Taro多端开发框架教程](https://coding.imooc.com/class/306.html)

## 🎯 Hook 事件类型

- **PreToolUse**: 工具使用前执行
- **PostToolUse**: 工具使用后执行
- **UserPromptSubmit**: 用户提交提示时执行
- **Notification**: Claude 需要许可或等待输入时执行
- **Stop**: 主 Claude Code 代理完成响应时执行
- **SessionStart**: 会话开始时执行
- **SessionEnd**: 会话结束时执行

## 📱 移动端开发 Hooks (6个)

### 1. React Native 自动构建检查
**用途**: 在修改RN组件后自动检查语法和构建

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(jsx?|tsx?)$' && echo \"$file_path\" | grep -q 'src/'; then npx react-native start --reset-cache --dry-run; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 2. Android Gradle 同步触发
**用途**: 在修改Android配置文件时自动触发Gradle同步

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '(build\\.gradle|gradle\\.properties|settings\\.gradle)$'; then echo '需要执行 Gradle 同步' && ./gradlew --refresh-dependencies; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 3. iOS Pod 依赖更新
**用途**: 在修改Podfile时自动更新iOS依赖

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -q 'Podfile$'; then cd ios && pod install --repo-update; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 4. Flutter 热重载触发
**用途**: 在修改Flutter Dart文件时触发热重载

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.dart$'; then flutter hot-reload 2>/dev/null || echo 'Flutter 热重载触发'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 5. 移动端资源优化检查
**用途**: 在添加图片资源时自动进行压缩和格式检查

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(png|jpg|jpeg)$' && echo \"$file_path\" | grep -qE '(assets|images)/'; then imageoptim \"$file_path\" 2>/dev/null || echo \"图片资源已添加: $file_path\"; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 6. 移动端测试设备检查
**用途**: 在启动移动端开发时检查连接的设备

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo '检查移动设备连接状态:' && adb devices && echo '--- iOS设备 ---' && xcrun simctl list devices | grep Booted || true"
          }
        ]
      }
    ]
  }
}
```

## 🌸 鸿蒙开发 Hooks (4个)

### 7. ArkTS 语法检查
**用途**: 在编辑ArkTS文件时自动进行语法检查

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.ets$'; then echo 'ArkTS语法检查:' && tsc --noEmit \"$file_path\" 2>/dev/null || echo \"ArkTS文件已更新: $file_path\"; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 8. HarmonyOS 构建检查
**用途**: 在修改鸿蒙项目配置时检查构建环境

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '(build-profile\\.json5|module\\.json5)$'; then echo 'HarmonyOS配置更新，检查hvigor构建环境' && npx @ohos/hvigor --version; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 9. ArkUI 组件规范检查
**用途**: 在创建ArkUI组件时检查命名和结构规范

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE 'src/main/ets/.*\\.ets$'; then echo \"检查ArkUI组件规范: $(basename \"$file_path\")\"; grep -q '@Component\\|@Entry' \"$file_path\" && echo '✓ 组件装饰器已添加' || echo '⚠ 缺少组件装饰器'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 10. 鸿蒙签名检查
**用途**: 在构建鸿蒙应用前检查签名配置

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.command' | { read cmd; if echo \"$cmd\" | grep -q 'hvigor.*assembleHap'; then echo '检查HarmonyOS签名配置...' && test -f build-profile.json5 && grep -q 'signingConfig' build-profile.json5 && echo '✓ 签名配置已设置' || echo '⚠ 请配置应用签名'; fi; }"
          }
        ]
      }
    ]
  }
}
```

## 🌐 Web开发 Hooks (5个)

### 11. 前端构建工具自动选择
**用途**: 根据项目配置自动选择Webpack、Vite或其他构建工具

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if [ \"$file_path\" = \"package.json\" ]; then echo '检测前端构建工具:'; test -f vite.config.js && echo '使用 Vite' || test -f webpack.config.js && echo '使用 Webpack' || echo '使用默认构建工具'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 12. CSS预处理器自动编译
**用途**: 在修改SCSS/LESS文件时自动编译为CSS

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(scss|sass)$'; then sass \"$file_path\" \"${file_path%.*}.css\" --no-source-map 2>/dev/null || echo \"SCSS文件已更新: $file_path\"; elif echo \"$file_path\" | grep -q '\\.less$'; then lessc \"$file_path\" \"${file_path%.*}.css\"; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 13. Vue/React 组件模板验证
**用途**: 在创建Vue或React组件时验证模板结构

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.vue$'; then echo '验证Vue组件结构' && grep -q '<template>' \"$file_path\" && echo '✓ Vue模板正确' || echo '⚠ Vue组件缺少template'; elif echo \"$file_path\" | grep -qE '\\.(jsx|tsx)$'; then echo '验证React组件' && grep -qE '(export default|export const)' \"$file_path\" && echo '✓ React组件导出正确'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 14. Web性能监控
**用途**: 在运行Web应用时启动性能监控

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.command' | { read cmd; if echo \"$cmd\" | grep -qE '(npm run|yarn|pnpm).*dev'; then echo '启动Web开发服务器，开启性能监控...'; lighthouse --version >/dev/null 2>&1 && echo '✓ Lighthouse可用于性能测试' || echo 'ℹ 建议安装lighthouse进行性能测试'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 15. 响应式设计检查
**用途**: 在修改CSS时检查响应式断点

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(css|scss|less)$'; then echo '检查响应式断点:'; grep -E '@media.*\\((max|min)-width' \"$file_path\" >/dev/null && echo '✓ 包含响应式断点' || echo 'ℹ 考虑添加移动端适配'; fi; }"
          }
        ]
      }
    ]
  }
}
```

## 📲 H5开发 Hooks (3个)

### 16. H5兼容性检查
**用途**: 在编辑H5代码时检查移动端兼容性

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(js|ts)$' && grep -qE '(navigator\\.|window\\.)' \"$file_path\"; then echo 'H5兼容性提醒: 检查移动端浏览器API支持'; grep -q 'touchstart\\|touchend' \"$file_path\" && echo '✓ 包含触摸事件处理' || echo 'ℹ 考虑添加触摸事件支持'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 17. 移动端视口配置检查
**用途**: 在编辑HTML文件时检查移动端视口配置

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.html$'; then echo '检查移动端视口配置:'; grep -q 'viewport.*width=device-width' \"$file_path\" && echo '✓ 视口配置正确' || echo '⚠ 建议添加移动端视口配置'; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 18. H5缓存策略检查
**用途**: 在部署H5应用时检查缓存配置

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '(service-worker|sw)\\.js$'; then echo 'H5缓存策略检查:'; grep -q 'caches\\|cache' \"$file_path\" && echo '✓ Service Worker缓存已配置' || echo 'ℹ 考虑添加离线缓存策略'; fi; }"
          }
        ]
      }
    ]
  }
}
```

## 🔄 跨平台开发 Hooks (2个)

### 19. 多端构建状态同步
**用途**: 在跨平台项目中同步各端构建状态

```json
{
  "hooks": {
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo '多端构建状态检查:'; test -d android && echo '✓ Android端可用' || echo '- Android端未配置'; test -d ios && echo '✓ iOS端可用' || echo '- iOS端未配置'; test -f index.html && echo '✓ Web端可用' || echo '- Web端未配置'"
          }
        ]
      }
    ]
  }
}
```

### 20. 统一代码规范检查
**用途**: 在提交代码前统一检查各端代码规范

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.command' | { read cmd; if echo \"$cmd\" | grep -qE 'git.*commit'; then echo '多端代码规范检查:'; find . -name '*.js' -o -name '*.ts' -o -name '*.jsx' -o -name '*.tsx' -o -name '*.dart' -o -name '*.ets' | head -5 | xargs -I {} sh -c 'echo \"检查: {}\" && head -1 \"{}\"' 2>/dev/null || true; fi; }"
          }
        ]
      }
    ]
  }
}
```

## 📝 配置说明

### 配置文件位置
- 用户级配置：`~/.claude/settings.json`
- 项目级配置：`.claude/settings.json`

### Hook 配置结构
```json
{
  "hooks": {
    "事件名称": [
      {
        "matcher": "工具匹配模式",
        "hooks": [
          {
            "type": "command",
            "command": "要执行的命令"
          }
        ]
      }
    ]
  }
}
```

### 移动端特定匹配器
- `"Edit|MultiEdit|Write"` - 文件编辑操作
- `"Bash"` - 命令行操作
- `"Write"` - 新文件创建
- 文件扩展名匹配：`\\.ets$`（鸿蒙）、`\\.dart$`（Flutter）、`\\.jsx?$`（React Native）

## 🛡️ 移动端开发安全注意事项

1. **API密钥保护** - 检查移动端配置文件中的敏感信息
2. **签名验证** - 确保应用签名配置正确
3. **权限检查** - 验证移动端权限申请的合理性
4. **网络安全** - 检查HTTPS和证书绑定配置
5. **代码混淆** - 生产环境启用代码保护

## 🔧 移动端特定故障排除

### React Native
```bash
# 清理缓存
npx react-native start --reset-cache
# 重新链接
npx react-native unlink && npx react-native link
```

### Flutter
```bash
# 清理构建
flutter clean && flutter pub get
# 重新生成
flutter packages pub run build_runner build
```

### HarmonyOS
```bash
# 清理hvigor构建
npx @ohos/hvigor clean
# 重新构建
npx @ohos/hvigor assembleHap
```

## 🚀 移动端开发最佳实践

1. **性能优化** - 针对移动设备优化代码和资源
2. **内存管理** - 注意移动端内存限制
3. **网络优化** - 考虑弱网环境和流量消耗
4. **用户体验** - 遵循各平台UI设计规范
5. **测试覆盖** - 在多种设备和系统版本上测试

通过这些专门针对移动端、鸿蒙、Web和H5开发的hooks配置，可以显著提升跨平台开发的效率和质量！