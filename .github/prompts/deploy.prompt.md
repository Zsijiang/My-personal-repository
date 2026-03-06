# 部署技能

渲染幻灯片并同步到 docs/ 目录，用于 GitHub Pages 部署。

## 使用场景

当需要将修改后的幻灯片部署到 GitHub Pages 时使用。输入讲座名称（如 "Lecture4"）或"全部"。

---

## 工作步骤

### 第 1 步：运行同步脚本

```bash
# 部署特定讲座
./scripts/sync_to_docs.sh [讲座名]

# 部署全部
./scripts/sync_to_docs.sh
```

### 第 2 步：验证部署
- 检查 HTML 文件是否存在于 `docs/slides/`
- 检查 `_files/` 目录是否已复制（RevealJS 资源）
- 检查 `docs/Figures/` 是否已同步

### 第 3 步：验证交互图表（如适用）
- 在渲染的 HTML 中搜索交互控件数量
- 确认数量与预期匹配

### 第 4 步：浏览器中验证
```bash
# macOS
open docs/slides/[讲座文件名].html
# Linux
xdg-open docs/slides/[讲座文件名].html
```
- 确认幻灯片渲染正常
- 图片正确显示
- 导航功能正常

### 第 5 步：向用户报告结果

## 同步脚本的功能
- 渲染 `Quarto/` 中所有 `.qmd` 文件（跳过 `*_backup*`）
- 将 HTML 和 `_files/` 目录复制到 `docs/slides/`
- 将 Beamer PDF 从 `Slides/` 复制到 `docs/slides/`
- 使用 rsync 同步 `Figures/` 到 `docs/Figures/`
