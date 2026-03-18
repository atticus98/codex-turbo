# codex-turbo

English | [简体中文](./README.md)

This repository is a personal Codex CLI template set. It aims to make better
use of native CLI capabilities and support parallel task orchestration with
multiple agents.

> 💡 **Not sure how to apply it?** You can send this repository URL to an AI
> assistant such as Claude Code CLI or Codex CLI and let it help merge the
> templates into your local setup.

> Current compatible version: **Codex CLI v0.115.0**
>
> The original post
> [Codex CLI 多智能体并行调度配置分享](https://linux.do/t/topic/1603762)
> can no longer be edited. This repository is the maintained version going
> forward.

## Key Points

- 💡 **Parallel Workflow**: `multi_agent = true` for high parallelism with
  minimal blocking
- 🔧 **System-level Contract**: inject agent workflow rules through
  `developer_instructions` in `config.toml`, with higher priority than
  `AGENTS.md`
- 🧠 **Native Memory**: `memories = true` to extract and consolidate
  conversation memory automatically
- 🔌 **WebSocket Support**: `responses_websockets_v2 = true` enables realtime
  streaming responses with no automatic fallback
- 🎯 **Conversation Style**: strong visual boundaries, emoji markers, and
  short direct terminal-friendly output
- 📝 **Dynamic Contract**: the main agent dynamically sends clear task
  instructions with goal/action/result
- ⚙️ **Concurrency Control**: `max_threads = n` for custom per-round parallel
  limits
- ⚠️ **Risk Management**: dangerous operation confirmation and immutable
  principles
- 🤖 **Custom Agents**: manually configure sub-agent model, reasoning effort,
  and role description
- 📋 **Reusable Templates**: ready-to-copy `AGENTS.template.en.md` and
  `config.toml.en.example`

## Directory Structure

```text
.
├── README.md                  # Chinese documentation
├── README.en.md               # English documentation (this page)
└── templates/
    ├── cn/                        # Chinese templates
    │   ├── AGENTS.template.md
    │   ├── config.template.toml
    │   ├── agents/
    │   │   ├── explorer.toml
    │   │   └── worker.toml
    │   └── skills/
    │       └── terminal-dialog-style/
    └── en/                        # English templates
        ├── AGENTS.template.en.md
        ├── config.toml.en.example
        ├── agents/
        └── skills/
```

## Quick Start (5 Minutes)

Goal: switch your Codex CLI into a "parallel + templated" workflow.

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd codex-turbo
```

### 2. Copy the template configuration

This repository provides the following template files:

| File | Purpose | Target Location |
|------|---------|-----------------|
| `templates/en/config.toml.en.example` | Core system configuration, including `developer_instructions` for the parallel workflow | `~/.codex/config.toml` |
| `templates/en/AGENTS.template.en.md` | Development principles and output style guide | `~/.codex/AGENTS.md` |
| `templates/en/agents/` | Sub-agent configuration (`explorer`, `worker`) | `~/.codex/agents/` |
| `templates/en/skills/` | Skill templates such as `terminal-dialog-style` | `~/.codex/skills/` |

> Complete `config.toml` with your own provider-specific key and environment
> settings.

**First-time use (direct copy)**:

```bash
# Create target directory if needed
mkdir -p ~/.codex

# Copy the core configuration files
cp templates/en/AGENTS.template.en.md ~/.codex/AGENTS.md
cp templates/en/config.toml.en.example ~/.codex/config.toml

# Copy agent and skill directories
cp -r templates/en/agents ~/.codex/
cp -r templates/en/skills ~/.codex/
```

**Existing configuration (manual merge)**:

Do not overwrite your existing `~/.codex` directly. Merge it step by step.

> - Your current files: `~/.codex/config.toml`, `~/.codex/AGENTS.md`
> - Repository templates: `templates/en/config.toml.en.example`,
>   `templates/en/AGENTS.template.en.md`

1. **Back up your current configuration first**

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.bak
cp ~/.codex/AGENTS.md ~/.codex/AGENTS.md.bak
[ -d ~/.codex/agents ] && cp -R ~/.codex/agents ~/.codex/agents.bak
[ -d ~/.codex/skills ] && cp -R ~/.codex/skills ~/.codex/skills.bak
```

> If `~/.codex/agents.bak` or `~/.codex/skills.bak` already exists, clean up
> the old backup first. Otherwise `cp -R` may create nested backup
> directories.

2. **Review the diff before deciding how to merge**

```bash
diff -u ~/.codex/config.toml templates/en/config.toml.en.example
diff -u ~/.codex/AGENTS.md templates/en/AGENTS.template.en.md
```

3. **At minimum, merge these key blocks in `config.toml`**

- `developer_instructions`
- `[agents.explorer]`
- `[agents.worker]`
- `[features]`
- `[agents]`
- `[memories]`

4. **Sync the related files too. Do not update only the main config**

These two lines in `[agents.explorer]` and `[agents.worker]` are mandatory:

- `config_file = "agents/explorer.toml"`
- `config_file = "agents/worker.toml"`

So the following files must also exist:

```bash
mkdir -p ~/.codex/agents ~/.codex/skills/terminal-dialog-style
cp templates/en/agents/explorer.toml ~/.codex/agents/explorer.toml
cp templates/en/agents/worker.toml ~/.codex/agents/worker.toml
cp templates/en/skills/terminal-dialog-style/SKILL.md ~/.codex/skills/terminal-dialog-style/SKILL.md
```

5. **Run a quick self-check after the merge**

```bash
# Check key blocks in config.toml and the config_file declarations
rg -n "developer_instructions|\\[agents\\.explorer\\]|\\[agents\\.worker\\]|\\[features\\]|\\[agents\\]|\\[memories\\]|config_file" ~/.codex/config.toml

# Check whether the related files exist
test -f ~/.codex/agents/explorer.toml && echo "OK: agents/explorer.toml"
test -f ~/.codex/agents/worker.toml && echo "OK: agents/worker.toml"
test -f ~/.codex/skills/terminal-dialog-style/SKILL.md && echo "OK: skills/terminal-dialog-style/SKILL.md"

# Optional: inspect the directory tree
ls -R ~/.codex/agents ~/.codex/skills
```

Expected results:

- The first command should match at least these blocks or fields:
  `developer_instructions`, `[agents.explorer]`, `[agents.worker]`,
  `[features]`, `[agents]`, `[memories]`, `config_file`
- Each `test -f` command should print its corresponding `OK: ...` line
- If `ls -R` reports `No such file or directory`, the related directories were
  not prepared correctly and you should go back to the previous step

6. **If you need to roll back, restore it like this**

First confirm that these backup files or directories exist:

- `~/.codex/config.toml.bak`
- `~/.codex/AGENTS.md.bak`
- `~/.codex/agents.bak`
- `~/.codex/skills.bak`

Then run:

```bash
cp ~/.codex/config.toml.bak ~/.codex/config.toml
cp ~/.codex/AGENTS.md.bak ~/.codex/AGENTS.md

rm -rf ~/.codex/agents
rm -rf ~/.codex/skills

cp -R ~/.codex/agents.bak ~/.codex/agents
cp -R ~/.codex/skills.bak ~/.codex/skills
```

> ⚠️ `rm -rf ~/.codex/agents` and `rm -rf ~/.codex/skills` will delete the
> current directories immediately. Before running them, make sure
> `~/.codex/agents.bak` and `~/.codex/skills.bak` both exist and really contain
> the old configuration you want to restore.

> Do not blindly overwrite your existing provider configuration, API keys, MCP
> server configuration, or any other environment-dependent fields. The
> templates define the workflow; your local configuration defines the runtime.

> ⚠️ **Important**: `developer_instructions` in `config.toml.en.example` is a
> system-level contract with higher priority than `AGENTS.md`. Make sure it is
> merged.

> Note: this document is adapted for Codex CLI `v0.115.0`. Field names may
> still differ across versions or providers, so always confirm against your
> local CLI.

## Disclaimer

This repository provides methodology and template references, verified against
Codex CLI `v0.115.0`.

**Cost note**: multi-agent mode may increase token usage by around 20% to 30%.
Evaluate the cost based on your actual workload.

**Risk note**: an LLM can still make wrong decisions and may delete data or
modify code incorrectly. Recommended precautions:

- configure sandbox permissions and confirmation rules carefully
- test in a controllable environment first
- keep backups for important data

You are responsible for any consequences caused by using these templates.
