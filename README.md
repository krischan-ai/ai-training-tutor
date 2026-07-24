# AI Training Tutor

一个面向零基础学习者的 Codex Skill，用清晰、循序渐进的方式讲解 AI/机器学习模型训练、实验设计、监控、评估与故障排查。

## 能做什么

- 解释 SFT、LoRA、QLoRA、DPO、checkpoint、loss 等概念
- 设计从数据检查、dry-run、smoke run 到正式训练和评估的学习路径
- 解读训练日志、指标与报错，并给出安全的排查步骤
- 指导使用 MLflow、TensorBoard 等工具观察实验
- 编写适合初学者的模型训练教程
- 区分工程验证、课堂实验、基准测试与生产就绪

## 设计原则

这个 Skill 不只给出命令，而是先说明每一步的目的，再告诉学习者要观察什么，以及如何解释结果。默认由学习者亲自操作，帮助其建立独立分析和排错能力。

## 项目结构

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── training-tutor-guide.md
```

## 安装

将仓库克隆到 Codex 的 Skills 目录：

```bash
git clone <repository-url> ~/.codex/skills/ai-training-tutor
```

重新启动 Codex 或刷新 Skills 后即可使用。

## 使用示例

```text
请用 ai-training-tutor 给零基础学习者解释 LoRA 微调的完整流程。
```

```text
这段训练日志中的 validation loss 为什么持续上升？请带我一步步排查。
```

```text
帮我把现有模型训练文档改写成适合初学者的教程。
```

## License

本项目暂未指定开源许可证。公开可见不等于自动授予复制、修改或再分发权限。
