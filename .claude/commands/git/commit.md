---
description: 生成规范的Git提交信息并提交
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
argument-hint: [提交类型]
---

# 📤 智能Git提交

执行规范化Git提交流程：

## 1. 检查状态
!`git status`

## 2. 生成提交信息
根据变更内容生成符合约定式提交的消息：
- feat: 新功能
- fix: 错误修复
- docs: 文档更新
- style: 代码格式
- refactor: 重构
- test: 测试相关

## 3. 执行提交
使用生成的提交信息执行 `git add .` 和 `git commit`

提交类型：$ARGUMENTS