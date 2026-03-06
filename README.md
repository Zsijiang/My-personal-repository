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

## 🚀 快速开始

### 使用 Copilot 技能

1. 在 VS Code 中打开本仓库。
2. 打开 GitHub Copilot Chat 面板。
3. 点击 **Attach** 按钮，选择 **Prompt...**，然后选择需要的技能文件。
4. 在聊天框中描述你的需求，Copilot 将根据技能配置提供专业的输出。

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

## 📄 许可证

本项目供个人使用。