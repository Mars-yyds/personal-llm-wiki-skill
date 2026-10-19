---
name: personal-llm-wiki
version: 1.0.1
description: Maintain a local Git-backed wiki for reusable context across AI sessions. Use for long-running projects, durable decisions, research notes, and structured handoffs. Do not use for temporary scratch notes.
metadata: {"requires":{"bins":["git","python3"],"skills":[]}}
---

# LLM Wiki

LLM Wiki 是由 AI 自主维护的本地 Git 知识仓库。它把原始资料、跨会话形成的当前知识和研发状态持续保留下来，让后续 Agent 先复用已有理解，必要时再回到原始证据，而不是每次从头调查。

## 默认入口

- 本地路径：`~/work/llm-wiki`
- 使用规则：`~/work/llm-wiki/AGENTS.md`

用户初始化时可以选择其他路径；之后使用已确认的 Wiki 路径及其中的 `AGENTS.md`，不要再次要求改回默认位置。

## 日常使用

使用者不需要理解 Wiki 的文件结构，也不需要手工编辑。只需在工作中告诉 Agent 读取、记录、恢复或整理；Agent 按仓库规则自主维护。

### 常见入口

| 场景 | 可以直接对 Agent 说 |
| --- | --- |
| 开始一项新研发或长期关注一个主题 | “为 `<任务或主题>` 新建 Wiki，之后持续记录。” |
| 新会话了解某个主题或继续上次工作 | “从 LLM Wiki 获取 `<主题或任务>` 的上下文，确认当前状态后继续。” |
| 有新的资料、讨论结论或决定 | “把这些内容更新到 `<Wiki>`，同步修正受影响的结论。” |
| 内容重复、冲突、过时或入口混乱 | “整理 `<Wiki>`，处理重复、冲突、过时内容和知识空白。” |

个人 Agent 已固定从 Wiki 启动时，直接说任务即可。

### Agent 的最小工作循环

1. 先读根索引和目标 Wiki 的入口，只加载当前任务需要的页面。
2. 当前知识足够时直接使用；不足时再回到原始资料、文档、代码或真实系统核对。
3. 有明确结束条件和执行状态的工作进入 `dev/`；跨任务复用的主题知识进入 `knowledge/`。
4. 新资料保留为原始证据，并整合进受影响的当前页面；发现冲突时标记矛盾并保留纠正来源。
5. 修改完成后按仓库规则检查、记录和提交。

## 初始化

- 本地还没有 LLM Wiki：读取[初始化 LLM Wiki](references/initialize-wiki.md)。
- 需要初始化个人资料并创建个人全局 Agent：读取[初始化个人全局 Agent](references/initialize-agent.md)。
