# 初始化 LLM Wiki

初始化前只确认存放位置。推荐使用独立目录，避免与代码仓库或 Skill 源码混在同一个 Git 仓库中。

> 我会创建一个独立的、由 Git 管理的 LLM Wiki。
>
> **请确认存放位置**
>
> - 推荐位置：`~/work/llm-wiki`
>
> 可以按这个位置初始化吗？需要调整时只需提供新路径。

## 1. 检查目标目录

- 目标不存在：继续初始化。
- 目标已存在：禁止覆盖。先检查是否含 `AGENTS.md`、`SCHEMA.md`、`index.md`、`dev/` 和 `knowledge/`。
- 已是可用 Wiki：直接复用。
- 结构冲突或目录非空：停止并报告，不自动移动、删除或覆盖。

## 2. 选择初始化来源

优先级：

1. 用户明确提供的 Wiki 仓库 URL。
2. 当前环境已配置的可信模板仓库。
3. 没有可用模板时，在目标目录创建最小 Wiki 结构。

克隆已有模板：

```bash
mkdir -p "$(dirname "$WIKI_DIR")"
git clone "$WIKI_TEMPLATE_REPO" "$WIKI_DIR"
```

`WIKI_DIR` 和 `WIKI_TEMPLATE_REPO` 必须先解析成真实值；禁止原样执行占位符。

没有模板时创建最小结构：

```bash
mkdir -p "$WIKI_DIR"/{dev,knowledge}
git -C "$WIKI_DIR" init -b main
```

随后创建：

```text
AGENTS.md
SCHEMA.md
index.md
dev/index.md
knowledge/index.md
```

`AGENTS.md` 定义启动、读取、写入、Git 和安全规则；`SCHEMA.md` 定义 Wiki 页面、原始来源和研发状态格式。内容应保持平台中立，不写入凭据、组织专用地址或个人绝对路径。

## 3. 验证

进入目标目录后检查：

```bash
git status --short --branch
test -f AGENTS.md
test -f SCHEMA.md
test -f index.md
```

读取 `AGENTS.md`，按其中流程继续初始化个人资料或项目 Wiki。初始化成功不等于必须立即提交；提交或推送前先检查隐私信息和远端可见性。
