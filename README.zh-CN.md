# think-confirm-act

[English](README.md) | [中文](README.zh-CN.md)

面向编程 agent 的“先思考、确认后行动”协作流程。

当你希望 agent 先检查代码、说明实现方案、等你确认后再进行有意义的代码修改时，使用这个 skill。

## 什么时候使用

- 你希望 agent 修改前先思考。
- 你希望先看到实现方案。
- 你希望先批准文件改动。
- 你担心布局、行为或架构被改坏。
- 你希望 agent 改完后自己检查。

常见触发句：

- `先思考再行动`
- `先告诉我怎么做`
- `让我确认后再改`
- `先别改`
- `先分析`
- `先给方案`

## 它会做什么

这个 skill 会让 agent 按下面流程工作：

1. 理解你的请求。
2. 先检查相关代码，不修改文件。
3. 说明计划采用的实现方式和风险。
4. 在你明确要求确认优先时，等待你确认。
5. 确认后做最小合理改动。
6. 自检正确性、改动范围和一致性。

## 语言切换

默认跟随用户语言。用户用中文，agent 用中文回复；用户用英文，agent 用英文回复。

你也可以明确要求切换语言：

- `切换中文`
- `用中文说`
- `Switch to English`
- `Use English`

## 安装

使用 Skills CLI 全局安装：

```bash
npx skills add LB623/think-confirm-act -g
```

只安装到 Codex：

```bash
npx skills add LB623/think-confirm-act -g --agent codex
```

## 仓库结构

```text
think-confirm-act/
├── README.md
├── README.zh-CN.md
├── LICENSE
├── .gitignore
└── SKILL.md
```

## 许可证

MIT
