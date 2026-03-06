# My Personal Repository

这是我的个人项目仓库，用于管理代码项目和学术论文写作。本仓库集成了 GitHub Copilot 自定义技能（Skills），可以辅助完成代码开发、论文撰写、学术研究等工作。

> 💡 本仓库的 Copilot 工作流设计参考了 [pedrohcgs/claude-code-my-workflow](https://github.com/pedrohcgs/claude-code-my-workflow)，并将其 Claude Code 的 skills/agents/rules 体系适配为 GitHub Copilot 的 prompt 文件格式。

## 📁 仓库结构

```
.
├── README.md                                    # 本说明文件
└── .github/
    ├── copilot-instructions.md                  # Copilot 通用指令配置
    └── prompts/                                 # Copilot 可复用技能
        ├── write-code.prompt.md                 # 📝 代码编写
        ├── write-paper.prompt.md                # 📄 论文撰写
        ├── proofread.prompt.md                  # 🔍 校对审查
        ├── review-paper.prompt.md               # 📋 论文审稿（裁判式）
        ├── review-code.prompt.md                # 🔧 代码质量审查
        ├── data-analysis.prompt.md              # 📊 端到端数据分析
        ├── lit-review.prompt.md                 # 📚 文献综述
        ├── research-ideation.prompt.md          # 💡 研究构思
        ├── interview-me.prompt.md               # 🎤 研究访谈
        ├── compile-latex.prompt.md              # 🔨 LaTeX 编译
        ├── validate-bib.prompt.md               # 📖 参考文献验证
        ├── devils-advocate.prompt.md            # 😈 魔鬼代言人审查
        ├── slide-excellence.prompt.md           # 🎯 幻灯片卓越审查
        ├── create-lecture.prompt.md             # 🎓 讲座创建
        ├── visual-audit.prompt.md               # 👁️ 视觉审计
        ├── pedagogy-review.prompt.md            # 📐 教学法审查
        ├── deploy.prompt.md                     # 🚀 部署幻灯片
        ├── deep-audit.prompt.md                 # 🔬 深度审计
        └── commit.prompt.md                     # 💾 提交工作流
```

## 🚀 三种使用方式

---

### 📦 方式一：存到 GitHub 仓库

你可以将这些 Copilot 工作流文件**放到任何 GitHub 仓库**中使用。有以下几种方法：

#### 方法 A：直接使用本仓库（最简单）

本仓库本身就是可用的！只需：

```bash
# 克隆本仓库到本地
git clone https://github.com/Zsijiang/My-personal-repository.git

# 用 VS Code 打开
code My-personal-repository
```

打开后 Copilot 会自动读取 `.github/copilot-instructions.md` 中的指令。

#### 方法 B：复制到已有项目中

如果你已经有一个项目仓库，把 `.github` 文件夹复制进去即可：

```bash
# 假设你有一个项目叫 my-research-project
cd my-research-project

# 创建 .github 目录（如果不存在）
mkdir -p .github/prompts

# 从本仓库复制文件
# 方法 1：手动下载后复制
cp -r /path/to/My-personal-repository/.github/copilot-instructions.md .github/
cp -r /path/to/My-personal-repository/.github/prompts/ .github/prompts/

# 方法 2：使用 git 命令直接拉取
git clone https://github.com/Zsijiang/My-personal-repository.git /tmp/copilot-workflow
cp /tmp/copilot-workflow/.github/copilot-instructions.md .github/
cp -r /tmp/copilot-workflow/.github/prompts/* .github/prompts/
rm -rf /tmp/copilot-workflow
```

#### 方法 C：只选择需要的技能文件

你不必复制所有技能。根据需要选择：

```bash
# 只复制代码开发相关的技能
cp write-code.prompt.md review-code.prompt.md data-analysis.prompt.md .github/prompts/

# 只复制学术写作相关的技能
cp write-paper.prompt.md review-paper.prompt.md proofread.prompt.md lit-review.prompt.md .github/prompts/
```

#### 提交到 GitHub

```bash
cd your-project
git add .github/
git commit -m "添加 Copilot 自定义技能和指令"
git push
```

> ⚠️ **重要**：`.github/copilot-instructions.md` 是**通用指令**，Copilot 每次对话会自动加载。`.github/prompts/*.prompt.md` 是**可选技能**，需要手动附加使用。

#### 文件结构要求

```
你的项目/
├── .github/
│   ├── copilot-instructions.md        # ← 必须：通用指令（自动加载）
│   └── prompts/                        # ← 可选：技能文件目录
│       ├── write-code.prompt.md        # ← 按需添加技能
│       ├── write-paper.prompt.md
│       └── ...
├── src/                                # 你的项目代码
├── paper/                              # 你的论文文件
└── ...
```

---

### 💻 方式二：在 VS Code 中使用

#### 前提条件

1. **安装 VS Code**：从 [code.visualstudio.com](https://code.visualstudio.com/) 下载安装
2. **安装 GitHub Copilot 扩展**：
   - 打开 VS Code
   - 点击左侧栏的扩展图标（或按 `Ctrl+Shift+X` / `Cmd+Shift+X`）
   - 搜索 `GitHub Copilot` 并安装
   - 同时安装 `GitHub Copilot Chat`
3. **登录 GitHub 账号**：确保你有 Copilot 订阅（个人版、企业版或学生免费版）

#### 第 1 步：打开含有技能文件的项目

```bash
# 克隆并打开
git clone https://github.com/Zsijiang/My-personal-repository.git
code My-personal-repository
```

或者在 VS Code 中：**文件** → **打开文件夹** → 选择你的项目目录。

#### 第 2 步：打开 Copilot Chat 面板

- **快捷键**：`Ctrl+Shift+I`（Windows/Linux）或 `Cmd+Shift+I`（macOS）
- **或者**：点击左侧活动栏的 Copilot Chat 图标
- **或者**：按 `Ctrl+Shift+P` 打开命令面板，输入 `Copilot Chat`

#### 第 3 步：使用通用指令（自动生效）

`.github/copilot-instructions.md` 文件会**自动加载**，无需任何操作。当你在 Copilot Chat 中提问时，Copilot 会自动遵循其中定义的：
- 编码规范（PEP 8、tidyverse 等）
- 回复语言（默认中文）
- 质量门禁（80 分以上才提交）
- 学术写作标准

#### 第 4 步：使用技能文件（手动附加）

这是核心操作步骤：

1. 在 Copilot Chat 输入框中，点击 📎 **Attach** 按钮（回形针图标）
2. 在弹出菜单中选择 **Prompt...**
3. 会显示 `.github/prompts/` 中所有可用的技能文件列表
4. **选择你需要的技能**，例如 `write-code`
5. 技能内容会被附加到你的对话上下文中
6. 在输入框中描述你的需求，发送即可

#### 使用示例

**示例 1：写代码**
```
📎 附加 → write-code.prompt.md

然后输入：
"帮我写一个 Python 函数，读取 CSV 文件并计算每列的平均值"
```

**示例 2：审查论文**
```
📎 附加 → review-paper.prompt.md
📎 附加 → #file:paper/my-paper.tex    （附加你的论文文件）

然后输入：
"请审查我的论文"
```

**示例 3：校对幻灯片**
```
📎 附加 → proofread.prompt.md
📎 附加 → #file:slides/lecture01.tex

然后输入：
"校对这个幻灯片文件"
```

**示例 4：数据分析**
```
📎 附加 → data-analysis.prompt.md
📎 附加 → #file:data/experiment.csv

然后输入：
"对这个数据集进行探索性分析并建立回归模型"
```

#### VS Code 中的 Copilot Chat 模式

| 模式 | 快捷键 | 说明 |
|------|--------|------|
| **Chat 面板** | `Ctrl+Shift+I` | 侧边栏对话，适合长对话 |
| **内联 Chat** | `Ctrl+I` | 在编辑器内直接提问，适合快速代码修改 |
| **终端 Chat** | 在终端中 `Ctrl+I` | 在 VS Code 内置终端中使用 |

#### 确认 Copilot 指令已加载

在 Copilot Chat 中输入以下内容来验证：

```
你好，请告诉我你当前加载了哪些自定义指令？默认回复语言是什么？
```

如果正常工作，Copilot 应该会用**中文**回复，并提到质量门禁、先规划再执行等原则。

---

### 🖥️ 方式三：在终端中使用

#### 前提条件

1. **安装 GitHub CLI**：
   ```bash
   # macOS
   brew install gh

   # Windows (通过 winget)
   winget install GitHub.cli

   # Ubuntu/Debian
   sudo apt install gh

   # 或从 https://cli.github.com/ 下载
   ```

2. **登录 GitHub**：
   ```bash
   gh auth login
   ```

3. **安装 Copilot CLI 扩展**：
   ```bash
   gh extension install github/gh-copilot
   ```

#### 使用 Copilot CLI

安装完成后，你可以在终端中直接使用 Copilot：

```bash
# 向 Copilot 提问
gh copilot suggest "如何用 git 撤销最后一次提交"

# 让 Copilot 解释命令
gh copilot explain "git rebase -i HEAD~3"
```

#### 配合技能文件在终端中使用

虽然终端版 Copilot 不能直接"附加" prompt 文件，但你可以通过以下方式利用技能内容：

**方法 1：将技能内容作为上下文传入**

```bash
# 读取技能文件内容，配合你的问题一起传给 Copilot
cat .github/prompts/write-code.prompt.md | gh copilot suggest "按照以上规范，帮我写一个排序算法"
```

**方法 2：在 VS Code 内置终端中使用**

VS Code 内置终端可以享受 Copilot Chat 的完整功能：

1. 在 VS Code 中按 `` Ctrl+` `` 打开内置终端
2. 在终端中按 `Ctrl+I` 启动 Copilot 内联对话
3. 此时 `.github/copilot-instructions.md` 中的指令仍然会自动加载

**方法 3：使用 shell 别名快速调用**

在你的 `~/.bashrc` 或 `~/.zshrc` 中添加便捷命令：

```bash
# 添加到 ~/.bashrc 或 ~/.zshrc
alias copilot='gh copilot suggest'
alias copilot-explain='gh copilot explain'

# 使用示例
copilot "用 Python 写一个 Web 爬虫"
copilot-explain "awk '{print $1}' file.txt"
```

添加后执行 `source ~/.bashrc` 或 `source ~/.zshrc` 使其生效。

#### 终端使用对比

| 方式 | 技能文件自动加载 | 适合场景 |
|------|-----------------|---------|
| `gh copilot suggest` | ❌ 不自动加载 | 快速命令行问题 |
| VS Code 内置终端 + `Ctrl+I` | ✅ 自动加载 copilot-instructions | 项目内开发 |
| VS Code Chat 面板 + 附加 prompt | ✅ 完整功能 | 使用完整技能 |

> 💡 **推荐**：对于完整的技能体验（如论文审稿、代码审查等复杂任务），建议使用 VS Code 中的 Copilot Chat 面板 + 手动附加 prompt 文件的方式。终端版 Copilot 更适合快速的命令行问题。

---

### ⚡ 快速参考卡片

| 你想做什么 | 推荐方式 | 步骤 |
|-----------|---------|------|
| 写代码 | VS Code Chat | 附加 `write-code` → 描述需求 |
| 审查论文 | VS Code Chat | 附加 `review-paper` + 论文文件 → "请审查" |
| 校对文档 | VS Code Chat | 附加 `proofread` + 文件 → "校对" |
| 数据分析 | VS Code Chat | 附加 `data-analysis` + 数据文件 → 描述目标 |
| 查命令行 | 终端 | `gh copilot suggest "如何..."` |
| 解释命令 | 终端 | `gh copilot explain "命令"` |
| 文献综述 | VS Code Chat | 附加 `lit-review` → 描述主题 |
| 研究构思 | VS Code Chat | 附加 `research-ideation` → 描述方向 |

### 通用指令自动加载

`.github/copilot-instructions.md` 文件中的指令会在 Copilot 交互时**自动加载**，无需手动附加。它包含：
- 核心工作原则（先规划再执行、执行后验证、质量门禁）
- 编码规范（Python PEP 8、R tidyverse、JS/TS ESLint）
- 学术写作规范
- 工作流协议

## 📋 技能分类

### 🖥️ 代码开发

| 技能 | 文件 | 说明 |
|------|------|------|
| 代码编写 | `write-code.prompt.md` | 高质量代码生成，支持 Python、R、JS/TS、Java、C++、Go、Rust |
| 代码审查 | `review-code.prompt.md` | 代码质量、可重现性、安全性审查，生成评分报告 |
| 数据分析 | `data-analysis.prompt.md` | 端到端分析：探索 → 回归 → 出版级表格和图表 |
| 提交工作流 | `commit.prompt.md` | 标准的 git 分支 → 提交 → PR → 合并 流程 |

### 📝 学术写作

| 技能 | 文件 | 说明 |
|------|------|------|
| 论文撰写 | `write-paper.prompt.md` | 按标准结构撰写论文（摘要到参考文献） |
| 论文审稿 | `review-paper.prompt.md` | 顶级期刊裁判式审查，含 6 维度评分 |
| 校对审查 | `proofread.prompt.md` | 语法、拼写、一致性和学术质量检查 |
| 参考文献验证 | `validate-bib.prompt.md` | 交叉验证引用键与 .bib 条目 |

### 🔬 研究辅助

| 技能 | 文件 | 说明 |
|------|------|------|
| 文献综述 | `lit-review.prompt.md` | 结构化文献搜索，识别研究空白 |
| 研究构思 | `research-ideation.prompt.md` | 生成研究问题、假设和识别策略 |
| 研究访谈 | `interview-me.prompt.md` | 交互式访谈，将想法转化为研究方案 |

### 🎓 教学与演示

| 技能 | 文件 | 说明 |
|------|------|------|
| 讲座创建 | `create-lecture.prompt.md` | 从论文到 Beamer 幻灯片的完整流程 |
| 幻灯片卓越审查 | `slide-excellence.prompt.md` | 多维度综合审查 |
| 视觉审计 | `visual-audit.prompt.md` | 溢出、字体、间距、布局检查 |
| 教学法审查 | `pedagogy-review.prompt.md` | 叙事弧线、认知负荷、符号一致性 |
| 魔鬼代言人 | `devils-advocate.prompt.md` | 批判性的 5-7 个教学挑战 |
| LaTeX 编译 | `compile-latex.prompt.md` | XeLaTeX 3 次编译 + bibtex |
| 部署 | `deploy.prompt.md` | 渲染并同步到 GitHub Pages |

### 🔧 项目管理

| 技能 | 文件 | 说明 |
|------|------|------|
| 深度审计 | `deep-audit.prompt.md` | 仓库一致性审计（4 维度并行检查） |

## 🔄 与 Claude Code 工作流的对应关系

本仓库将 `pedrohcgs/claude-code-my-workflow` 的核心功能适配为 Copilot 格式：

| Claude Code 概念 | Copilot 对应 | 说明 |
|---|---|---|
| `CLAUDE.md` (项目指令) | `.github/copilot-instructions.md` | 自动加载的全局指令 |
| `.claude/skills/*/SKILL.md` (技能) | `.github/prompts/*.prompt.md` | 可复用的 prompt 文件 |
| `.claude/rules/*.md` (规则) | 嵌入到 `copilot-instructions.md` | 合并为通用指令 |
| `.claude/agents/*.md` (子智能体) | 模拟为 prompt 文件 | Copilot 无直接子智能体概念 |
| `MEMORY.md` (持久记忆) | 嵌入到 `copilot-instructions.md` | 关键模式已记录 |
| `.claude/hooks/*` (钩子) | 无直接对应 | Copilot 暂无钩子机制 |
| `.claude/settings.json` | 无直接对应 | Copilot 使用 VS Code 设置 |

## 📝 自定义指南

### 添加新技能
在 `.github/prompts/` 目录下创建新的 `.prompt.md` 文件。建议包含：
1. **技能标题** — 清晰的角色定义
2. **使用场景** — 何时使用
3. **工作步骤** — 详细的步骤指引
4. **输出格式** — 期望的输出结构
5. **重要原则** — 注意事项

### 修改通用指令
编辑 `.github/copilot-instructions.md` 以调整：
- 编码规范偏好
- 学术写作风格
- 质量门禁阈值
- 回复语言设置

---

## ❓ 常见问题

### Q: Copilot 是免费的吗？
**A:** GitHub Copilot 有以下方案：
- **学生/教师**：通过 [GitHub Education](https://education.github.com/) 申请可**免费使用**
- **个人版**：$10/月 或 $100/年
- **企业版**：$19/用户/月
- **免费版（Copilot Free）**：2024 年起提供有限的免费额度

### Q: 我需要把这些文件放到每个项目里吗？
**A:** 是的，`.github/copilot-instructions.md` 和 `.github/prompts/` 需要放在你想使用这些技能的项目仓库中。Copilot 会从当前打开的项目中读取这些文件。

### Q: 可以只用部分技能吗？
**A:** 当然可以！你可以只复制你需要的 `.prompt.md` 文件到 `.github/prompts/` 目录。`copilot-instructions.md` 建议始终复制，因为它定义了基础行为规范。

### Q: 这些文件会影响 Copilot 的代码补全吗？
**A:** `copilot-instructions.md` 会影响 Copilot Chat 的行为（包括通用补全建议的风格），但不会影响编辑器内的 Tab 补全功能。`.prompt.md` 文件只在你手动附加时才会影响对话。

### Q: 我能修改这些技能文件吗？
**A:** 完全可以！这些文件就是普通的 Markdown 文件，你可以根据自己的需要修改、删除或添加新的技能。建议你根据自己的工作流程定制这些技能。

### Q: 终端 Copilot 和 VS Code Copilot 有什么区别？
**A:** 
| 特性 | 终端 (`gh copilot`) | VS Code Copilot Chat |
|------|---------------------|---------------------|
| 自动加载项目指令 | ❌ | ✅ |
| 附加技能文件 | ❌ (需手动传入) | ✅ |
| 附加项目文件 | ❌ | ✅ |
| 代码补全 | ❌ | ✅ |
| 适合场景 | 快速命令行问题 | 完整开发工作流 |

## 📄 许可证

本项目供个人使用。