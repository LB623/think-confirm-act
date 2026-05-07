---
name: think-confirm-act
description: Use when the user wants approval-first collaboration for AI programming, asks to think before acting, wants a plan or implementation approach before code changes, or says things like "先思考再行动", "先告诉我怎么做", "让我确认后再改", "思考完再动手", "做完代码修改后自己检查". Follow a cautious, confirmation-first workflow and avoid making code edits before explicit approval.
---

# Think Confirm Act

Use this skill when the user explicitly wants a confirmation-first workflow before edits or execution.

Typical trigger phrases include:

- 先思考再行动
- 先告诉我怎么做
- 思考完让我确认
- 经过我同意再做
- 先别改
- 改动大就先算了
- 不要破坏当前布局
- 做完代码修改后自己检测
- 先分析
- 先给方案

## Core behavior

When this skill is active, do not jump straight into edits.

Follow this order:

1. Understand the request and restate it briefly in plain language.
2. Inspect the relevant code or files first without modifying anything.
3. Think through the likely implementation approach and risks.
4. Present the proposed approach before editing.
5. Ask for confirmation when the user has explicitly requested confirmation-first behavior.
6. Only after approval, make the smallest reasonable change.
7. After changes, run self-verification and report the result clearly.

## Approval-first rules

If the user has asked to confirm before action, treat that as binding for code edits and other meaningful modifications.

Before editing, provide:

- what you think the user wants
- what files or areas you plan to touch
- whether the change is small or potentially structural
- whether there are risks such as layout breakage, behavior regressions, or unclear requirements

Then stop and wait for approval.

Do not use approval-first behavior as an excuse to avoid useful inspection. It is still good to gather context first. The restriction is mainly on changing files or taking impactful actions.

## When to ask instead of assume

Ask the user before proceeding if any of these are true:

- the change has non-obvious product or UX tradeoffs
- the request could be implemented in multiple materially different ways
- the change may affect layout, data flow, or architecture beyond a small local patch
- the codebase contains conflicting patterns and choosing one would be risky
- you discover ambiguity that could lead to the wrong outcome

If the change is clearly small and the user has not asked for confirmation-first behavior, normal autonomous execution is fine.

If the user only says something like "做完自己检查" or "自己检测一下" without asking to confirm before edits, treat it as a self-verification request only. Do not automatically activate the full confirmation-first workflow.

## Release scope

If the user later says something like "好，你自己判断" or "不用问我了，直接改", treat that as a temporary release from confirmation-first behavior for the current task only. Resume confirmation-first behavior for the next distinct task unless told otherwise.

If the user says something broader like "这个项目你就直接改吧，我信任你", you may treat that as permission to work autonomously within the current project and continuous task context. Still pause and ask before high-impact actions such as large refactors, architecture changes, deleting files, installing dependencies, changing external services, committing, pushing, or publishing.

For a new project, new thread, or clearly separate task, return to the default confirmation-first behavior unless the user renews the release.

## Communication style

Use short, clear, low-pressure language.

Preferred structure before edits:

1. Brief understanding of the request
2. What you inspected
3. Proposed implementation
4. What will and will not change
5. Request for confirmation

Good examples:

- 我理解你的意思是让聊天区内部滚动、页面不要继续被消息撑长。我先只查看布局和样式，不改代码，确认原因后把改法告诉你。
- 我看过了，主要会动 `App.jsx` 和 `styles.css`。这是一个小改动，风险低；如果你同意，我就按这个方案改。
- 我准备只压缩参数卡片，不改右侧其他结构。会收紧字段间距、slider 间距和说明文字占位。你确认后我再动手。

## Editing constraints while active

When the skill is active:

- prefer the smallest local change that satisfies the confirmed request
- preserve the current page structure unless the user explicitly agrees to structural change
- avoid opportunistic refactors
- do not silently broaden scope
- if new issues are discovered, surface them before expanding the change
- if the user says "只改这里", honor that strictly

## Self-verification (mandatory after every change)

After every implementation, always self-verify before reporting back. This is not optional.

Self-verification must cover:

**1. Correctness check**
- Re-read every changed line and confirm it does what was intended
- Check for typos, wrong variable names, off-by-one errors, or missing edge cases

**2. Scope check**
- Confirm no files or sections were changed beyond what was approved
- If anything extra was touched, call it out explicitly

**3. Consistency check**
- Verify the change is consistent with surrounding code style, naming conventions, and existing patterns
- Check that imports, exports, or dependencies are not broken

**4. Regression check**
- Think through adjacent logic that could be affected by the change
- If a build or test command is available, run it and report the result
- If no automated check is available, manually trace the affected code path and confirm expected behavior

**5. Self-assessment**
- Rate your own confidence: high / medium / low
- If confidence is medium or low, explain why and what the user should double-check manually

Preferred reporting format after changes:

```text
改动摘要：[简述改了什么]
检查结果：
- 正确性：✅ / ⚠️ [说明]
- 改动范围：✅ 只改了约定范围 / ⚠️ [说明额外改动]
- 一致性：✅ / ⚠️ [说明]
- 回归影响：✅ 无影响 / ⚠️ [说明可能受影响的地方]
置信度：高 / 中（建议你确认 XX） / 低（建议人工复查）
```

## Anti-patterns

Avoid these behaviors when the skill is active:

- editing immediately after the user's request when they explicitly asked for confirmation first
- presenting a vague plan without inspecting the actual code
- asking the user broad open-ended questions when a concrete proposal is possible
- making extra cleanup or refactor changes without approval
- treating "先思考再行动" as a request for endless analysis without producing a clear proposal
- skipping self-verification or only doing a superficial read-through after making changes
- reporting "done" without explicitly stating what was checked

## Default decision heuristic

If unsure whether to act immediately or ask first:

- inspect first
- propose second
- confirm third (if user requested confirmation-first)
- edit fourth
- self-verify last — always

In short: think, confirm, act, verify.
