# Claude Code 自定义命令推荐大全 (20个中文案例)

基于网络搜集和实战经验，整理了 Claude Code 自定义命令的完整资源库。

## 📚 资源来源

### 官方文档
- [斜杠命令文档](https://docs.claude.com/zh-CN/docs/claude-code/slash-commands)
- [Claude Code 快速开始](https://docs.claude.com/zh-CN/docs/claude-code/quickstart)

### 中文博客资源
- [榨干 Claude Code 的 16 个实用小技巧](https://www.cnblogs.com/javastack/p/18978280)
- [Claude Code 用法全面拆解！26 项核心功能](https://zhuanlan.zhihu.com/p/1928918331810886674)
- [全面掌控 Claude Code：命令 + 参数 + 快捷键一文全整理](https://aicoding.csdn.net/6871255fa6db534ba2b8686f.html)
- [Claude Code 最佳实践指南](https://www.xuanyuanli.cn/pages/claude-code-best-practices/)

### 开源项目
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code)
- [claude-code-guide](https://github.com/Joseph19820124/claude-code-guide)

## 🎯 自定义命令概述

### 目录结构
```
.claude/commands/          # 项目级命令 (前缀 /project:)
├── dev/                   # 开发相关
├── git/                   # Git工作流
├── test/                  # 测试相关
├── deploy/                # 部署运维
├── docs/                  # 文档相关
├── security/              # 安全检查
├── data/                  # 数据分析
├── web/                   # Web开发
└── devops/                # 运维部署

~/.claude/commands/        # 用户级命令 (前缀 /user:)
```

### 命令文件格式
```markdown
---
description: 命令描述
argument-hint: [参数格式]
allowed-tools: Bash(*), Edit(*)
model: claude-3-5-haiku-20241022
---

# 命令标题
命令内容，支持 $ARGUMENTS 参数占位符

## 执行步骤
1. 步骤一
2. 步骤二

!`bash命令示例`
@文件引用示例
```

## 🔧 20个推荐自定义命令

### 🚀 开发效率类 (5个)

#### 1. 性能优化命令 (`dev/optimize.md`)
```markdown
---
description: 分析代码性能并提供优化建议
argument-hint: [文件路径]
---

# 性能优化分析

请分析 $ARGUMENTS 的性能，并提供：

1. **性能瓶颈识别**
   - 找出执行时间较长的代码段
   - 分析时间复杂度和空间复杂度

2. **优化建议**
   - 提供3-5个具体的优化方案
   - 评估优化后的性能提升

3. **代码重构**
   - 如需要，提供重构后的代码
   - 保证功能不变的前提下提升性能
```

**使用方式**: `/project:dev:optimize src/utils.js`

#### 2. 错误修复命令 (`dev/fix.md`)
```markdown
---
description: 智能诊断并修复代码错误
argument-hint: [错误描述或文件]
---

# 🔍 错误诊断与修复

针对 $ARGUMENTS，请执行：

## 诊断步骤
1. 分析错误类型和原因
2. 定位具体问题代码
3. 评估影响范围

## 修复方案
1. 提供修复代码
2. 解释修复原理
3. 预防类似问题的建议

## 测试验证
- 提供测试用例
- 确保修复不引入新问题
```

**使用方式**: `/project:dev:fix LoginError`

#### 3. 代码审查命令 (`dev/review.md`)
```markdown
---
description: 全面的代码审查和质量评估
argument-hint: [文件或目录路径]
---

# 📋 代码审查报告

对 $ARGUMENTS 进行全面审查：

## 代码质量评估
- **可读性**：变量命名、注释、结构
- **maintainability**：代码复用性、模块化
- **性能**：算法效率、资源使用

## 安全性检查
- 输入验证
- 数据泄露风险
- 访问控制

## 改进建议
- 优先级排序的改进点
- 具体的重构建议
- 最佳实践推荐
```

**使用方式**: `/project:dev:review src/components/`

#### 4. 任务分解命令 (`dev/task.md`)
```markdown
---
description: 将大任务分解为可执行的小任务
argument-hint: [任务描述]
---

# 📋 任务分解

将 $ARGUMENTS 分解为可执行任务：

## 任务分析
1. 理解核心需求
2. 识别依赖关系
3. 评估复杂度

## 分解结果
- **阶段1**：基础准备
- **阶段2**：核心开发
- **阶段3**：测试验证
- **阶段4**：部署发布

## 时间评估
- 各阶段预期工期
- 关键路径识别
- 风险点标记

## 执行计划
- 优先级排序
- 里程碑设定
- 验收标准
```

**使用方式**: `/project:dev:task 实现用户认证功能`

#### 5. 架构分析命令 (`dev/arch.md`)
```markdown
---
description: 分析项目架构并提供改进建议
argument-hint: [项目路径]
---

# 🏛️ 架构分析

对 $ARGUMENTS 进行架构分析：

## 当前架构评估
- 目录结构分析
- 模块依赖关系
- 设计模式识别

## 技术栈评估
- 框架和库使用情况
- 技术选型合理性
- 版本兼容性检查

## 改进建议
- 架构优化方案
- 可扩展性增强
- 性能提升策略

## 迁移计划
- 渐进式改进步骤
- 风险评估与缓解
- 实施时间线
```

**使用方式**: `/project:dev:arch ./`

### 🌿 Git工作流类 (3个)

#### 6. 智能提交命令 (`git/commit.md`)
```markdown
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
```

**使用方式**: `/project:git:commit feat`

#### 7. 分支管理命令 (`git/branch.md`)
```markdown
---
description: 智能分支创建和切换
allowed-tools: Bash(git branch:*), Bash(git checkout:*)
argument-hint: [分支名称]
---

# 🌿 分支管理

智能管理Git分支：

## 当前分支状态
!`git branch -a`

## 分支操作
- 创建新分支：$ARGUMENTS
- 检查分支命名规范
- 自动设置上游分支

## 工作流建议
- feature/功能名 - 新功能开发
- hotfix/问题描述 - 紧急修复
- release/版本号 - 发布准备
```

**使用方式**: `/project:git:branch feature/new-auth`

#### 8. 发布准备命令 (`git/release.md`)
```markdown
---
description: 准备项目发布版本
allowed-tools: Bash(git log:*), Bash(git tag:*)
---

# 🚀 发布准备

准备版本发布：

## 1. 版本检查
- 检查当前版本号
- 生成版本更新日志
- 验证所有测试通过

## 2. 文档更新
- 更新 CHANGELOG.md
- 检查 README.md
- 确认API文档最新

## 3. 构建验证
- 执行完整构建流程
- 运行所有测试
- 检查构建产物

版本号：$ARGUMENTS
```

**使用方式**: `/project:git:release v1.2.0`

### 🧪 测试质量类 (2个)

#### 9. 测试生成命令 (`test/test.md`)
```markdown
---
description: 自动生成单元测试和集成测试
argument-hint: [测试目标]
---

# 🧪 测试自动生成

为 $ARGUMENTS 生成完整测试：

## 单元测试
- 正常流程测试
- 边界条件测试
- 异常情况测试
- Mock对象使用

## 集成测试
- API接口测试
- 数据库交互测试
- 第三方服务集成

## 测试数据
- 创建测试数据集
- 设置和清理步骤
- 数据隔离策略

## 覆盖率目标
- 代码覆盖率分析
- 覆盖率改进建议
- 测试质量评估
```

**使用方式**: `/project:test:test src/services/api.js`

#### 10. 测试运行命令 (`test/runtest.md`)
```markdown
---
description: 运行测试并生成详细报告
allowed-tools: Bash(npm test:*), Bash(pytest:*), Bash(mvn test:*)
---

# 🏃‍♂️ 测试执行

执行完整测试流程：

## 1. 环境检查
- 测试依赖确认
- 配置文件验证
- 数据库连接测试

## 2. 测试执行
- 运行所有测试套件
- 并行执行优化
- 失败测试重试

## 3. 结果分析
- 测试通过率统计
- 失败用例详细分析
- 性能基准对比

## 4. 报告生成
- HTML测试报告
- 覆盖率报告
- 趋势分析图表

测试范围：$ARGUMENTS
```

**使用方式**: `/project:test:runtest integration`

### 🔒 安全检查类 (2个)

#### 11. 安全扫描命令 (`security/security.md`)
```markdown
---
description: 全面的安全漏洞扫描和分析
argument-hint: [扫描范围]
---

# 🔒 安全扫描

对 $ARGUMENTS 执行安全检查：

## 代码安全审计
- SQL注入风险检查
- XSS漏洞扫描
- CSRF防护验证
- 输入验证分析

## 依赖安全检查
- 第三方库漏洞扫描
- 版本安全性评估
- 许可证合规检查

## 配置安全审核
- 敏感信息泄露检查
- 访问控制配置
- 加密实现验证

## 安全加固建议
- 漏洞修复方案
- 安全最佳实践
- 防护措施推荐
```

**使用方式**: `/project:security:security ./`

#### 12. 代码扫描命令 (`security/scan.md`)
```markdown
---
description: 静态代码分析和质量检查
argument-hint: [文件或目录]
---

# 🔍 代码质量扫描

对 $ARGUMENTS 进行静态分析：

## 代码规范检查
- 编码风格一致性
- 命名规范遵循
- 注释完整性

## 潜在问题检测
- 死代码识别
- 未使用变量/方法
- 循环复杂度分析
- 重复代码检测

## 性能分析
- 算法复杂度评估
- 内存使用优化点
- 并发安全问题

## 改进建议
- 优先级排序的问题列表
- 具体修复建议
- 重构推荐方案
```

**使用方式**: `/project:security:scan src/`

### 📚 文档生成类 (2个)

#### 13. 文档生成命令 (`docs/doc.md`)
```markdown
---
description: 为代码自动生成详细文档
argument-hint: [文件路径]
---

# 📚 自动文档生成

为 $ARGUMENTS 生成完整文档：

## API 文档
- 函数/方法签名
- 参数说明
- 返回值描述
- 使用示例

## 代码注释
- 添加必要的行内注释
- 复杂逻辑的解释
- 注意事项和限制

## README 更新
- 功能概述
- 安装和使用方法
- 配置选项说明
```

**使用方式**: `/project:docs:doc src/utils/helper.js`

#### 14. 注释优化命令 (`docs/comment.md`)
```markdown
---
description: 优化代码注释质量
argument-hint: [文件路径]
---

# 💬 注释优化

对 $ARGUMENTS 的注释进行优化：

## 注释规范化
- 统一注释风格
- 补充缺失注释
- 移除冗余注释

## 内容优化
- 解释"为什么"而不只是"是什么"
- 添加复杂逻辑的思路说明
- 标注重要的设计决策

## 多语言支持
- 提供中英文注释版本
- 保持注释的专业性和准确性
```

**使用方式**: `/project:docs:comment src/main.js`

### 📊 数据分析类 (2个)

#### 15. 日志分析命令 (`data/log.md`)
```markdown
---
description: 智能分析应用日志
argument-hint: [日志文件路径]
---

# 📊 日志分析

分析 $ARGUMENTS 的日志文件：

## 日志概览
- 总记录数统计
- 时间范围分析
- 日志级别分布

## 异常检测
- 错误和异常统计
- 异常模式识别
- 频繁异常分析

## 性能分析
- 响应时间统计
- 资源使用趋势
- 性能瓶颈识别

## 可视化报告
- 时间序列图表
- 异常分布图
- 性能趋势分析

## 优化建议
- 日志配置优化
- 监控告警设置
- 问题解决方案
```

**使用方式**: `/project:data:log logs/app.log`

#### 16. 数据库优化命令 (`data/db.md`)
```markdown
---
description: 数据库性能分析和优化
argument-hint: [数据库连接或表名]
---

# 🗄️ 数据库优化

优化 $ARGUMENTS 的数据库性能：

## 查询分析
- 慢查询识别
- 执行计划分析
- 索引使用情况

## 结构优化
- 表结构设计审查
- 索引优化建议
- 分区策略评估

## 性能调优
- 查询重写建议
- 参数配置优化
- 缓存策略设计

## 监控设置
- 关键指标监控
- 告警阈值设定
- 性能基线建立
```

**使用方式**: `/project:data:db user_table`

### 🌐 Web开发类 (2个)

#### 17. 前端组件命令 (`web/component.md`)
```markdown
---
description: 生成前端组件代码和文档
argument-hint: [组件名称]
---

# ⚛️ 前端组件生成

创建 $ARGUMENTS 组件：

## 组件结构
- React/Vue/Angular组件代码
- 样式文件(CSS/SCSS)
- 类型定义(TypeScript)

## 功能实现
- Props接口定义
- 状态管理逻辑
- 事件处理方法
- 生命周期钩子

## 测试文件
- 单元测试用例
- 快照测试
- 交互测试

## 文档示例
- Storybook故事
- 使用示例代码
- Props说明表格

## 最佳实践
- 可访问性支持
- 性能优化
- 响应式设计
```

**使用方式**: `/project:web:component UserCard`

#### 18. API接口命令 (`web/api.md`)
```markdown
---
description: 生成RESTful API接口代码
argument-hint: [接口名称]
---

# 🔌 API接口生成

创建 $ARGUMENTS 接口：

## 接口定义
- 路由配置
- 请求/响应模型
- 参数验证规则
- 错误处理逻辑

## 数据层
- 数据模型定义
- 数据库操作
- 缓存策略
- 事务管理

## 安全实现
- 身份认证
- 权限验证
- 输入校验
- 输出过滤

## 文档生成
- OpenAPI规范
- 接口文档
- 使用示例
- 测试用例

## 性能优化
- 查询优化
- 响应压缩
- 并发控制
- 监控指标
```

**使用方式**: `/project:web:api /users`

### 🚀 DevOps类 (2个)

#### 19. 部署命令 (`devops/deploy.md`)
```markdown
---
description: 自动化部署流程
allowed-tools: Bash(docker:*), Bash(kubectl:*)
argument-hint: [环境名称]
---

# 🚀 自动化部署

部署到 $ARGUMENTS 环境：

## 预部署检查
- 代码质量验证
- 测试覆盖率检查
- 安全扫描通过
- 依赖兼容性确认

## 构建流程
- 应用打包构建
- Docker镜像创建
- 镜像安全扫描
- 制品库推送

## 部署执行
- 环境配置更新
- 服务滚动更新
- 健康检查验证
- 流量切换控制

## 部署验证
- 功能测试验证
- 性能基准检查
- 监控告警设置
- 回滚方案准备

## 通知报告
- 部署结果通知
- 变更记录更新
- 运维文档同步
```

**使用方式**: `/project:devops:deploy production`

#### 20. 监控设置命令 (`devops/monitor.md`)
```markdown
---
description: 设置应用监控和告警
argument-hint: [服务名称]
---

# 📈 监控告警设置

为 $ARGUMENTS 设置完整监控：

## 基础监控
- 系统资源监控(CPU/内存/磁盘)
- 应用性能指标(响应时间/吞吐量)
- 错误率和可用性监控
- 业务关键指标跟踪

## 日志监控
- 应用日志收集
- 错误日志聚合
- 关键事件跟踪
- 日志告警规则

## 告警配置
- 阈值告警设置
- 异常检测规则
- 通知渠道配置
- 升级策略定义

## 仪表板
- 实时监控大屏
- 趋势分析图表
- 性能对比报告
- 故障影响分析

## 自动化响应
- 自动扩缩容
- 故障自愈机制
- 预警处理流程
- 应急响应预案
```

**使用方式**: `/project:devops:monitor user-service`

## 🛠️ 配置指南

### 快速部署
```bash
# 1. 创建命令目录结构
mkdir -p .claude/commands/{dev,git,test,deploy,docs,security,data,web,devops}
mkdir -p ~/.claude/commands

# 2. 复制命令文件到对应目录
# 3. 在 Claude Code 中使用 /project:分类:命令名 调用
```

### 命令组织建议
```
.claude/commands/
├── dev/           # 开发相关 - 优化、修复、审查、任务、架构
├── git/           # Git工作流 - 提交、分支、发布
├── test/          # 测试相关 - 生成测试、运行测试
├── security/      # 安全检查 - 漏洞扫描、代码扫描
├── docs/          # 文档生成 - API文档、注释优化
├── data/          # 数据分析 - 日志分析、数据库优化
├── web/           # Web开发 - 组件生成、API接口
└── devops/        # 运维部署 - 自动部署、监控设置
```

## 🎯 使用技巧

### 1. 参数化命令
- 使用 `$ARGUMENTS` 接收用户输入
- 支持位置参数 `$1`, `$2`, `$3`
- 提供默认值 `${1:-默认值}`

### 2. Bash集成
- `!`bash命令`` - 执行并显示结果
- `@文件路径` - 读取文件内容
- 条件执行和管道操作

### 3. 工具权限控制
```yaml
---
allowed-tools:
  - "Bash(git *)"
  - "Edit(*)"
disabled-tools:
  - "WebSearch"
---
```

### 4. 模型指定
```yaml
---
model: "claude-3-5-haiku-20241022"
---
```

## 🔧 故障排除

### 常见问题
1. **命令无法识别** - 检查文件路径和 `.claude/commands` 目录
2. **参数传递失败** - 验证 `$ARGUMENTS` 语法
3. **权限不足** - 确认 `allowed-tools` 配置

### 调试方法
- 使用简单命令测试基础功能
- 逐步增加复杂度和功能
- 查看 Claude Code 执行日志

## 📈 最佳实践

1. **命令设计原则**
   - 单一职责，功能聚焦
   - 参数化设计，提高复用性
   - 清晰的文档和示例

2. **团队协作**
   - 统一命名规范
   - 版本控制管理
   - 定期审查更新

3. **性能优化**
   - 避免重复操作
   - 合理使用缓存
   - 并行处理优化

通过合理配置和使用这些自定义命令，可以显著提升 Claude Code 的开发效率和用户体验！