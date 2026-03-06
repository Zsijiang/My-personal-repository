# 提交工作流技能

暂存更改、提交、创建 PR 并合并到 main。用于标准的提交-PR-合并循环。

## 使用场景

当完成一轮工作，需要提交代码时使用。输入可选的提交消息。

---

## 工作步骤

### 第 1 步：检查当前状态

```bash
git status
git diff --stat
git log --oneline -5
```

### 第 2 步：创建分支

```bash
git checkout -b <简短描述性分支名>
```

### 第 3 步：暂存文件

```bash
git add <file1> <file2> ...
```

**不要暂存**：
- 包含密钥/凭证的文件
- 本地配置文件
- 大型二进制文件（除非必要）

### 第 4 步：提交

如果提供了提交消息，使用它。否则分析暂存的更改，编写解释**为什么**而非仅仅**什么**的消息。

```bash
git commit -m "提交消息"
```

### 第 5 步：推送并创建 PR

```bash
git push -u origin <分支名>
gh pr create --title "<简短标题>" --body "## 摘要
- 变更点 1
- 变更点 2

## 测试计划
- [ ] 检查项 1
- [ ] 检查项 2
"
```

### 第 6 步：合并并清理

```bash
gh pr merge <pr-number> --merge --delete-branch
git checkout main
git pull
```

### 第 7 步：报告 PR URL 和合并内容

---

## 重要原则

- 始终创建**新分支** — 不要直接提交到 main
- 排除敏感文件
- 使用 `--merge`（非 `--squash` 或 `--rebase`），除非另行要求
- 如果用户提供了提交消息，原样使用
