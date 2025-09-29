# Claude Code Hooks 实用案例大全 (20个中文案例)

基于网络搜集的资源，整理了 Claude Code hooks 的实用案例和配置示例。

## 📚 资源来源

### 官方文档
- [Claude Code hooks 入门指南](https://docs.claude.com/zh-CN/docs/claude-code/hooks-guide)
- [Hooks 参考文档](https://docs.claude.com/zh-CN/docs/claude-code/hooks)

### 中文博客资源
- [轩辕李的博客 - Claude Code 最佳实践](https://www.xuanyuanli.cn/pages/claude-code-best-practices/)
- [Java技术栈 - 榨干 Claude Code 的 16 个实用小技巧](https://www.cnblogs.com/javastack/p/18978280)
- [知乎 - Claude Code Hooks：变革你 2025 年的开发工作流程](https://zhuanlan.zhihu.com/p/1926228119695655955)
- [腾讯云 - Claude Code 从入门到精通：最全配置指南](https://cloud.tencent.com/developer/article/2566484)

### 开源项目
- [EvanL1/claude-code-hooks](https://github.com/EvanL1/claude-code-hooks)
- [aliceric27/claude-code-hooks](https://github.com/aliceric27/claude-code-hooks)
- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery)

## 🎯 Hook 事件类型

- **PreToolUse**: 工具使用前执行
- **PostToolUse**: 工具使用后执行
- **UserPromptSubmit**: 用户提交提示时执行
- **Notification**: Claude 需要许可或等待输入时执行
- **Stop**: 主 Claude Code 代理完成响应时执行
- **SessionStart**: 会话开始时执行
- **SessionEnd**: 会话结束时执行

## 🔧 20个实用 Hooks 案例

### 1. Bash 命令日志记录
**用途**: 记录所有执行的 Bash 命令，便于审计和调试

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '\"\\(.tool_input.command) - \\(.tool_input.description // \"No description\")\"' >> ~/.claude/bash-command-log.txt"
          }
        ]
      }
    ]
  }
}
```

### 2. TypeScript 自动格式化
**用途**: 在编辑 TypeScript 文件后自动执行 Prettier 格式化

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -q '\\.ts$'; then npx prettier --write \"$file_path\"; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 3. 桌面通知系统
**用途**: 当 Claude 需要用户输入时发送桌面通知

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' '等待您的输入'"
          }
        ]
      }
    ]
  }
}
```

### 4. 敏感文件保护
**用途**: 阻止对敏感配置文件的修改操作

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "python3 -c \"import json, sys; data=json.load(sys.stdin); path=data.get('tool_input',{}).get('file_path',''); sys.exit(2 if any(p in path for p in ['.env', 'package-lock.json', '.git/']) else 0)\""
          }
        ]
      }
    ]
  }
}
```

### 5. 自动 ESLint 检查
**用途**: 在编辑 JavaScript/TypeScript 文件后自动运行 ESLint

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(js|ts|jsx|tsx)$'; then npx eslint \"$file_path\" --fix; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 6. Git 分支保护
**用途**: 防止意外删除主分支

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.command' | grep -q 'git.*branch.*-d.*\\(main\\|master\\)' && echo '警告：尝试删除主分支！' >&2 && exit 2 || exit 0"
          }
        ]
      }
    ]
  }
}
```

### 7. 自动测试运行
**用途**: 在修改测试文件或源文件后自动运行相关测试

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(test|spec)\\.(js|ts)$'; then npm test \"$file_path\"; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 8. Docker 构建验证
**用途**: 在修改 Dockerfile 后自动验证语法

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -q 'Dockerfile'; then docker build --dry-run -f \"$file_path\" .; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 9. 代码复杂度检查
**用途**: 检查代码复杂度，超过阈值时警告

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(js|ts)$'; then complexity=\"$file_path\" --threshold 10; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 10. 自动 Git 暂存
**用途**: 在文件编辑后自动添加到 Git 暂存区

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | xargs git add"
          }
        ]
      }
    ]
  }
}
```

### 11. 语音通知系统
**用途**: 使用 TTS 语音通知任务完成

```json
{
  "hooks": {
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "say '任务已完成' || espeak '任务已完成' || echo '任务已完成'"
          }
        ]
      }
    ]
  }
}
```

### 12. 数据库备份触发
**用途**: 在修改数据库相关文件时触发备份

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE '\\.(sql|migration)$'; then ./scripts/backup-db.sh; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 13. 包管理器安全检查
**用途**: 在修改 package.json 时检查安全漏洞

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if [ \"$file_path\" = \"package.json\" ]; then npm audit; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 14. 代码覆盖率检查
**用途**: 运行测试后检查代码覆盖率

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.command' | grep -q 'npm test' && npm run coverage || true"
          }
        ]
      }
    ]
  }
}
```

### 15. 文档自动更新
**用途**: 在修改代码后自动更新相关文档

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -qE 'src/.*\\.(js|ts)$'; then npm run docs:generate; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 16. 环境变量验证
**用途**: 在会话开始时验证必要的环境变量

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "python3 -c \"import os; required=['NODE_ENV','API_KEY']; missing=[var for var in required if not os.getenv(var)]; exit(1 if missing else 0)\""
          }
        ]
      }
    ]
  }
}
```

### 17. 自动代码压缩
**用途**: 在编辑生产代码时自动进行代码压缩

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|MultiEdit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | { read file_path; if echo \"$file_path\" | grep -q 'dist/'; then npm run minify \"$file_path\"; fi; }"
          }
        ]
      }
    ]
  }
}
```

### 18. 性能监控启动
**用途**: 在运行性能相关命令时启动监控

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.command' | grep -q 'npm run benchmark' && ./scripts/start-monitoring.sh || true"
          }
        ]
      }
    ]
  }
}
```

### 19. 团队通知系统
**用途**: 在完成重要任务时通知团队

```json
{
  "hooks": {
    "Stop": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "curl -X POST 'https://hooks.slack.com/your/webhook/url' -H 'Content-type: application/json' -d '{\"text\":\"Claude Code 任务已完成\"}'"
          }
        ]
      }
    ]
  }
}
```

### 20. 会话清理
**用途**: 在会话结束时清理临时文件

```json
{
  "hooks": {
    "SessionEnd": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "find /tmp -name 'claude-code-*' -type f -delete 2>/dev/null || true"
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

### 常用匹配器模式
- `"Bash"` - 匹配所有 Bash 命令
- `"Edit|MultiEdit|Write"` - 匹配文件编辑操作
- `".*"` - 匹配所有工具
- `"Read"` - 匹配文件读取操作

## 🛡️ 安全注意事项

1. **谨慎使用 PreToolUse hooks** - 可能会阻止重要操作
2. **验证命令安全性** - 避免执行危险的 shell 命令
3. **测试配置** - 在非生产环境先测试 hooks
4. **备份配置** - 定期备份 hooks 配置
5. **权限控制** - 确保 hooks 脚本有适当的执行权限

## 🔧 故障排除

### 禁用 Hooks
- 临时禁用：`claude-code --no-hooks`
- 环境变量：`export CLAUDE_CODE_NO_HOOKS=1`

### 调试 Hooks
- 查看 hooks 执行日志
- 使用 `echo` 命令输出调试信息
- 检查脚本执行权限

### 常见问题
1. **Hook 不执行** - 检查匹配器模式是否正确
2. **权限错误** - 确保脚本有执行权限
3. **路径问题** - 使用绝对路径或正确的相对路径

## 🚀 最佳实践

1. **从简单开始** - 先实现基本的 hooks，再逐步增加复杂功能
2. **错误处理** - 在 hooks 中添加适当的错误处理
3. **性能考虑** - 避免在 hooks 中执行耗时操作
4. **文档记录** - 为每个 hook 添加清晰的注释和说明
5. **团队协作** - 将项目级 hooks 纳入版本控制

通过合理配置和使用这些 hooks，可以显著提升 Claude Code 的开发体验和工作效率！