# My Personal Repository

这是我的个人项目仓库，用于管理代码项目和学术论文写作。本仓库集成了 GitHub Copilot 自定义技能（Skills），可以辅助完成代码开发和论文撰写。

## 📁 仓库结构

```
.
├── README.md                              # 本说明文件
└── .github/
    ├── copilot-instructions.md            # Copilot 通用指令配置
    └── prompts/
        ├── write-code.prompt.md           # 代码编写技能
        └── write-paper.prompt.md          # 论文写作技能
```

## 🚀 快速开始

### 使用 Copilot 技能

本仓库配置了两个 Copilot 自定义 Prompt 技能，可以在 GitHub Copilot Chat 中通过选择对应的 prompt 文件来使用：

1. **代码编写技能** (`write-code.prompt.md`)：辅助生成高质量、结构清晰的代码，支持多种编程语言。
2. **论文写作技能** (`write-paper.prompt.md`)：辅助撰写学术论文，包括摘要、引言、方法、实验、结论等部分。

### 如何使用

1. 在 VS Code 中打开本仓库。
2. 打开 GitHub Copilot Chat 面板。
3. 点击 **Attach** 按钮，选择 **Prompt...**，然后选择需要的技能文件。
4. 在聊天框中描述你的需求，Copilot 将根据技能配置提供专业的输出。

## 📝 自定义说明

- 通用编码指令位于 `.github/copilot-instructions.md`，Copilot 在本仓库中交互时会自动加载这些指令。
- 如需自定义或扩展技能，可在 `.github/prompts/` 目录下添加新的 `.prompt.md` 文件。

## 📄 许可证

本项目供个人使用。