# think-confirm-act

[English](README.md) | [中文](README.zh-CN.md)

Approval-first collaboration workflow for coding agents.

Use this skill when you want the agent to inspect code, explain the intended implementation, and wait for confirmation before making meaningful code changes.

## When to use

- You want the agent to think before editing.
- You want a plan before implementation.
- You want to approve file changes first.
- You are worried about layout, behavior, or architecture regressions.
- You want the agent to self-check after code changes.

Typical trigger phrases:

- `先思考再行动`
- `先告诉我怎么做`
- `让我确认后再改`
- `先别改`
- `先分析`
- `先给方案`

## What it does

This skill makes the agent follow this workflow:

1. Understand the request.
2. Inspect the relevant code without modifying files.
3. Explain the proposed implementation and risks.
4. Wait for explicit confirmation when requested.
5. Make the smallest reasonable change after approval.
6. Self-verify correctness, scope, and consistency.

## Language switching

The skill follows the user's language by default. If the user writes in Chinese, the agent should respond in Chinese. If the user writes in English, the agent should respond in English.

The user can switch languages explicitly with requests such as:

- `切换中文`
- `用中文说`
- `Switch to English`
- `Use English`

## Install

Install globally with the Skills CLI:

```bash
npx skills add LB623/think-confirm-act -g
```

Install for Codex specifically:

```bash
npx skills add LB623/think-confirm-act -g --agent codex
```

## Repository structure

```text
think-confirm-act/
├── README.md
├── LICENSE
├── .gitignore
└── SKILL.md
```

## License

MIT
