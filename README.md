# Personal LLM Wiki Skill

A reusable AI skill for maintaining a local, Git-backed knowledge base across conversations.

The skill helps an AI agent preserve project context, decisions, research, implementation status, and handoff notes without re-investigating the same topic in every session.

## Features

- Maintains durable context across AI sessions.
- Separates raw evidence from current knowledge.
- Tracks goals, progress, blockers, and next actions for development work.
- Uses Git history for review, synchronization, and recovery.
- Loads only the context needed for the current task.
- Supports project-specific development wikis and long-lived topic knowledge.
- Includes platform-neutral initialization guidance.

## Repository Structure

```text
personal-llm-wiki/
├── SKILL.md
├── references/
│   ├── initialize-wiki.md
│   └── initialize-agent.md
├── .gitignore
├── LICENSE
└── README.md
```

This repository contains the **skill instructions**, not your personal knowledge.

Your actual Wiki should live in a separate Git repository:

```text
llm-wiki/
├── AGENTS.md
├── SCHEMA.md
├── index.md
├── dev/
├── knowledge/
├── scripts/
└── templates/
```

Keeping the skill and Wiki in separate repositories prevents personal or project data from being published with the reusable skill.

## Requirements

- Git
- Python 3
- An AI agent or coding assistant that supports reusable skill instructions

## Installation

Clone the repository:

```bash
git clone https://github.com/Mars-yyds/personal-llm-wiki-skill.git
```

Install or copy the directory using the skill mechanism supported by your AI agent. The directory name must remain:

```text
personal-llm-wiki
```

The required entry file is:

```text
personal-llm-wiki/SKILL.md
```

## Usage

Example requests:

```text
Create a development Wiki for this project and keep tracking its goals,
progress, blockers, and next actions.
```

```text
Load the project context from my LLM Wiki and continue the current task.
```

```text
Update the Wiki with this document and revise any conclusions that changed.
```

```text
Organize this Wiki, remove duplicated current knowledge, and identify gaps.
```

The user does not need to edit Wiki files manually. The agent reads the repository rules, selects relevant evidence, updates the appropriate pages, and records execution state.

## Knowledge Model

The recommended Wiki separates information by responsibility:

| Location | Purpose |
| --- | --- |
| `raw/` | Original evidence such as documents, conversations, code snapshots, and test results |
| `wiki/` | Current knowledge and confirmed conclusions |
| `work/` | Development status, environment values, blockers, and handoff actions |
| `index.md` | Navigation and reading guidance |
| `log.md` | Traceable read, use, update, and verification activity |

Development work belongs under `dev/`. Long-lived reusable knowledge belongs under `knowledge/`.

## Initialization

- To create a new Wiki, see [references/initialize-wiki.md](references/initialize-wiki.md).
- To configure a personal Agent that starts from the Wiki, see [references/initialize-agent.md](references/initialize-agent.md).

The initialization guides are platform-neutral. They do not assume a specific messaging provider, AI CLI, hosting service, or private infrastructure.

## Privacy and Security

- Keep personal and project knowledge in a separate repository.
- Review the repository visibility before pushing.
- Do not store credentials, access tokens, cookies, private keys, or authentication state.
- Avoid committing organization-only URLs or confidential project material to public repositories.
- Use a private or organization-approved remote for sensitive knowledge.
- Publish only sanitized content when maintaining a public Wiki.

## Development

Before committing changes:

```bash
git diff --check
git status --short
```

Verify that:

- `SKILL.md` has valid YAML frontmatter.
- The frontmatter `name` matches the directory name.
- Referenced files exist.
- Local IDE metadata is not staged.
- No credentials, personal absolute paths, or private service URLs are present.

## License

Licensed under the Apache License 2.0. See [LICENSE](LICENSE).
