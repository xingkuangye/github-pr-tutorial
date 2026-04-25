# GitHub Pull Request 完整教程

> 本教程将帮助你从零开始掌握 GitHub Pull Request（PR）的使用，无论你是开源社区的贡献者还是团队开发者，都能在这里找到你需要的内容。

## 目录

- [什么是 Pull Request？](#什么是-pull-request)
- [Pull Request 的工作流程](#pull-request-的工作流程)
- [准备工作：Fork 与 Clone](#准备工作fork-与-clone)
- [创建你的第一个 Pull Request](#创建你的第一个-pull-request)
- [Pull Request 模板](#pull-request-模板)
- [代码审查与协作](#代码审查与协作)
- [高级技巧](#高级技巧)
- [常见问题与解决方案](#常见问题与解决方案)

---

## 什么是 Pull Request？

Pull Request（简称 PR）是 GitHub 协作工作流的核心功能。它允许你：

- **提出修改建议**：将你的代码更改提交给目标仓库
- **协作讨论**：在代码合并之前进行审查和讨论
- **追踪变更历史**：记录每一次提议的修改内容
- **自动化集成**：结合 CI/CD 实现自动化测试和部署

### PR 与 Merge Request 的区别

| 平台 | 名称 |
|------|------|
| GitHub | Pull Request (PR) |
| GitLab | Merge Request (MR) |
| Bitbucket | Pull Request |

虽然名称不同，但核心概念是相同的。

---

## Pull Request 的工作流程

```
┌─────────────────────────────────────────────────────────────────┐
│                      Pull Request 工作流程                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│   Fork 仓库 ──► Clone 到本地 ──► 创建分支 ──► 提交更改            │
│        │                                                        │
│        │                                                        │
│        ▼                                                        │
│   Push 到远程 ──► 创建 PR ──► 代码审查 ──► 修改完善               │
│        │                                                        │
│        │                                                        │
│        ▼                                                        │
│   合并到主分支 ◄─── 审批通过                                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 准备工作：Fork 与 Clone

### 步骤 1：Fork 目标仓库

1. 打开你想贡献的 GitHub 仓库
2. 点击页面右上角的 **Fork** 按钮
3. 选择你的账号作为 Fork 的目标位置
4. 等待仓库复制完成

### 步骤 2：Clone 你的 Fork 到本地

```bash
# 使用 HTTPS
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git

# 或使用 SSH
git clone git@github.com:YOUR_USERNAME/REPO_NAME.git
```

### 步骤 3：添加上游仓库的远程链接

```bash
# 添加上游仓库作为远程源
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPO.git

# 验证远程仓库配置
git remote -v
```

### 步骤 4：保持 Fork 同步

```bash
# 获取上游仓库的最新代码
git fetch upstream

# 切换到主分支
git checkout main

# 合并上游的更改
git merge upstream/main

# 推送到你的 Fork
git push origin main
```

---

## 创建你的第一个 Pull Request

### 步骤 1：创建功能分支

```bash
# 创建并切换到新分支
git checkout -b feature/add-new-feature

# 或者
git switch -c feature/add-new-feature
```

### 分支命名规范

| 类型 | 示例 | 说明 |
|------|------|------|
| feature/ | feature/user-auth | 新功能开发 |
| fix/ | fix/login-bug | Bug 修复 |
| hotfix/ | hotfix/critical-security | 紧急修复 |
| refactor/ | refactor/api-structure | 代码重构 |
| docs/ | docs/readme-update | 文档更新 |

### 步骤 2：进行代码修改

```bash
# 查看当前修改状态
git status

# 查看具体修改内容
git diff

# 暂存修改的文件
git add .

# 提交更改
git commit -m "feat: 添加用户认证功能"
```

### 提交信息规范

推荐使用 **Conventional Commits** 格式：

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

**类型（type）**：

| 类型 | 说明 |
|------|------|
| feat | 新功能 |
| fix | Bug 修复 |
| docs | 文档更改 |
| style | 代码格式（不影响功能）|
| refactor | 代码重构 |
| test | 测试相关 |
| chore | 构建/工具相关 |

### 步骤 3：推送分支到远程

```bash
# 推送分支到你的 Fork
git push origin feature/add-new-feature
```

### 步骤 4：在 GitHub 上创建 PR

1. 访问你的 GitHub Fork 仓库
2. 你会看到 "Compare & pull request" 按钮，点击它
3. 填写 PR 标题和描述
4. 选择目标分支（通常是 main 或 master）
5. 点击 "Create pull request"

### PR 描述示例

```markdown
## 概述
简要描述你做了什么修改，为什么要做这个修改。

## 改动内容
- 新增了用户认证功能
- 添加了登录页面
- 集成了第三方登录

## 测试情况
- [ ] 本地测试通过
- [ ] 新增了相关单元测试
- [ ] 测试账号：test@example.com

## 截图（可选）
![截图描述](image-url)

## 相关 Issue
Fixes #123
```

---

## Pull Request 模板

### 创建 PR 模板

在仓库根目录创建 `.github/PULL_REQUEST_TEMPLATE.md`：

```markdown
## 描述
<!-- 简要描述你的修改内容和目的 -->

## 修改类型
- [ ] 🐛 Bug 修复 (bug fix)
- [ ] ✨ 新功能 (new feature)
- [ ] 📖 文档更新 (documentation)
- [ ] 🎨 代码格式 (code style)
- [ ] ♻️ 代码重构 (refactoring)
- [ ] ✅ 测试 (tests)
- [ ] 🔧 构建/工具 (build/tooling)

## 涉及的文件
<!-- 列出你修改或新增的文件 -->
- 

## 测试步骤
<!-- 说明如何测试你的修改 -->
1. 
2. 
3. 

## 检查清单
- [ ] 我的代码遵循这个项目的代码规范
- [ ] 我已经进行了自我代码审查
- [ ] 我已经添加了必要的注释，特别是复杂的逻辑
- [ ] 文档已经更新（如需要）

## 其他说明
<!-- 其他需要审查者注意的事项 -->
```

### 自动关闭 Issue

在你的 PR 描述中使用以下关键词可以自动关闭相关 Issue：

| 关键词 | 示例 |
|--------|------|
| closes #123 | 关闭 Issue #123 |
| fixes #123 | 关闭并标记为已修复 |
| resolves #123 | 关闭并标记为已解决 |
| Closes #123, #456 | 关闭多个 Issue |

---

## 代码审查与协作

### 审查者视角

#### 如何进行代码审查

1. **理解修改目的**：先看 PR 描述，理解为什么要做这个修改
2. **检查代码质量**：
   - 代码是否清晰易懂？
   - 是否有适当的注释？
   - 是否遵循项目的代码规范？
3. **验证功能正确性**：
   - 逻辑是否正确？
   - 边界情况是否处理？
   - 是否有潜在的 Bug？
4. **考虑安全因素**：
   - 是否有安全漏洞？
   - 输入是否经过验证？

#### 审查评论规范

```
💡 建议：可以用这个符号开头表示改进建议
❓ 问题：可以用这个符号开头表示需要澄清的问题
✅ 认可：可以用这个符号表示对某处代码的肯定
🔴 重要：可以用这个符号标记需要重点关注的问题
```

#### 审查状态

| 状态 | 说明 |
|------|------|
| Approve | 批准合并 |
| Request Changes | 需要修改后再审 |
| Comment | 仅评论，不阻止合并 |

### PR 作者视角

#### 如何响应审查意见

1. **认真对待每条意见**：不要急于反驳，先理解审查者的意图
2. **及时回复**：对每条意见给予回应
3. **区分优先级**：
   - 阻塞性问题必须解决
   - 建议性问题可以考虑
4. **保持礼貌**：即使不同意，也要礼貌地解释你的考虑

#### 修改并更新 PR

```bash
# 在同一分支上继续修改
git add .
git commit -m "fix: 响应审查意见进行修改"
git push origin feature/add-new-feature
```

### 保持 PR 精简

**小而专注的 PR 更好**：

✅ **好的做法**：
- 每个 PR 只做一件事
- 控制在 400 行代码以内
- 易于审查和理解

❌ **不好的做法**：
- 一个 PR 包含多个不相关的改动
- 修改量太大难以审查
- 引入了难以排查的问题

---

## 高级技巧

### 1. Draft Pull Request（草稿 PR）

当你还在开发中，不希望立即接受审查时：

- 点击 "Create draft pull request" 而不是 "Create pull request"
- 草稿 PR 不会触发 CI 要求
- 可以随时转换为正式 PR

### 2. PR 链接与引用

```markdown
# 在 PR 中引用其他 Issue 或 PR
- Related to #123
- Blocks #456
- Part of #789
```

### 3. 强制推送注意事项

```bash
# ⚠️ 谨慎使用！会重写远程历史
git push --force origin feature-branch

# ✅ 更好的方式是创建新的 commit
# ⚠️ 强制推送会覆盖远程分支的所有内容
```

### 4. 使用 Rebase 保持提交历史整洁

```bash
# 将你的分支 rebase 到主分支
git fetch origin
git rebase origin/main

# 如果有冲突，解决后继续
git add .
git rebase --continue

# 如果想放弃 rebase
git rebase --abort
```

### 5. Squash Merge（压缩合并）

将一个 PR 中的所有提交合并为一个：

1. 在 Merge 按钮下拉菜单中选择 **Squash and merge**
2. 编辑合并后的提交信息
3. 确认合并

### 6. 设置 PR 模板

在 `.github/` 目录下创建：

```
.github/
├── PULL_REQUEST_TEMPLATE.md    # PR 模板
├── ISSUE_TEMPLATE/
│   ├── bug_report.md           # Bug 报告模板
│   └── feature_request.md     # 功能请求模板
└── CONTRIBUTING.md             # 贡献指南
```

### 7. 保护分支设置

在仓库 Settings > Branches 中：

- ✅ 启用 "Require pull request reviews before merging"
- ✅ 启用 "Require status checks to pass before merging"
- ✅ 设置 "Required number of approvals"
- ✅ 启用 "Dismiss stale approvals"

### 8. 自动更新 PR

当上游仓库有新的更改时：

```bash
# 方法一：Merge
git checkout feature-branch
git merge upstream/main

# 方法二：Rebase（推荐，保持历史整洁）
git checkout feature-branch
git rebase upstream/main

# 然后推送到你的 Fork
git push --force-with-lease origin feature-branch
```

### 9. 使用 GitHub CLI

```bash
# 安装 GitHub CLI
# macOS: brew install gh
# Linux: see https://github.com/cli/cli#installation

# 登录
gh auth login

# 从命令行创建 PR
gh pr create --title "添加新功能" --body "详细的描述"

# 查看 PR 状态
gh pr status

# 审查 PR
gh pr review 123 --approve

# 合并 PR
gh pr merge 123
```

---

## 常见问题与解决方案

### Q1: 合并冲突（Merge Conflict）

**问题**：PR 与目标分支存在冲突，无法自动合并。

**解决方案**：

```bash
# 1. 确保你的 Fork 是最新的
git fetch upstream

# 2. 切换到主分支
git checkout main

# 3. 合并上游更改
git merge upstream/main

# 4. 切换回你的分支
git checkout feature-branch

# 5. 合并主分支（会触发冲突）
git merge main

# 6. 手动解决冲突
# 编辑冲突文件，保留需要的代码

# 7. 标记冲突已解决
git add .
git commit -m "resolve merge conflict"

# 8. 推送
git push origin feature-branch
```

### Q2: 不小心提交到了主分支

**问题**：你的修改提交到了 main 分支而不是功能分支。

**解决方案**：

```bash
# 1. 查看提交历史，找到错误的提交
git log

# 2. 创建功能分支
git checkout -b feature-branch

# 3. 重置主分支到远程状态
git checkout main
git reset --hard origin/main
```

### Q3: PR 被锁定了

**问题**：显示 "This branch is out-of-date with the base branch"。

**解决方案**：

```bash
# 更新你的分支
git checkout feature-branch
git merge origin/main
# 或者
git pull origin main

# 推送更新
git push origin feature-branch
```

### Q4: 如何撤销已提交的 PR

**在 GitHub 上**：

1. 点击 PR 页面下方的 "Merge" 按钮
2. 点击 "Revert" 创建回退 PR

**使用命令行**：

```bash
# 克隆仓库
git clone https://github.com/...git

# 创建回退分支
git checkout -b revert-pr-123

# 撤销提交
git revert [commit-hash]

# 推送并创建 PR
git push origin revert-pr-123
```

### Q5: 如何修改 PR 的目标分支

**问题**：想把 PR 从一个分支改到另一个分支。

**解决方案**：

1. 在 PR 页面，点击 "Edit" 按钮
2. 在 "base" 下拉菜单中选择新的目标分支
3. 保存修改

### Q6: PR 合并后如何清理本地分支

```bash
# 删除已合并的分支
git branch -d feature-branch

# 删除远程分支
git push origin --delete feature-branch

# 清理已删除的远程分支引用
git fetch --prune
```

---

## 最佳实践总结

### 给贡献者的建议

1. **保持 PR 小而专注**：每次只做一件事
2. **写清楚提交信息**：方便回溯和理解
3. **详细填写 PR 描述**：让审查者快速理解意图
4. **及时响应审查意见**：保持沟通畅通
5. **遵守项目规范**：遵循 CONTRIBUTING.md 中的要求
6. **测试你的代码**：确保修改不会破坏现有功能
7. **保持耐心**：审查可能需要时间，不要催促

### 给维护者的建议

1. **及时响应 PR**：给贡献者积极的反馈
2. **提供建设性的反馈**：指出问题的同时给出改进建议
3. **自动化检查**：设置 CI/CD 减少手动检查
4. **文档化流程**：让贡献变得简单透明
5. **感谢贡献者**：开源社区需要认可和鼓励

---

## 更多资源

- [GitHub 官方文档](https://docs.github.com/cn/pull-requests)
- [Git 官方文档](https://git-scm.com/doc)
- [Conventional Commits 规范](https://www.conventionalcommits.org/)
- [GitHub CLI 文档](https://cli.github.com/)

---

## 许可证

本教程采用 [MIT 许可证](LICENSE)。

---

*本教程由 MiniMax Agent 创建 last update 2026-04-25*
