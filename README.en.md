# codex-turbo

English | [简体中文](./README.md)

This repository is a set of personal Codex CLI configuration templates. Adhering to the principle of **"Lightweight & Efficient,"** it aims to deeply leverage **native CLI capabilities** without introducing complex dependencies, enabling high-performance task orchestration through multi-agent collaboration. This setup is shared as a personal practice and is intended as a **starting point** to help you build your own ideal AI workflow.

> 💡 **Not sure how to apply it?** You can send this repository URL to an AI
> assistant such as Claude Code CLI or Codex CLI and let it help merge the
> templates into your local setup.

> Current compatible version: **Codex CLI v0.120.0**



## Key Points

- 💡 **Parallel Workflow**: `multi_agent = true` for maximum parallelism with
  minimal blocking
- 🔧 **System-level Contract**: inject agent workflow rules through
  `developer_instructions` in `config.toml`, with higher priority than
  `AGENTS.md`
- 🧠 **Native Memory**: `memories = true` to extract and consolidate
  conversation memory automatically, improving context continuity
- 🔌 **WebSocket Support**: `supports_websockets = true` is configured under
  `[provider]`. You need to verify whether your model provider supports it;
  do not enable it if unsupported, to avoid errors
- 🧩 **Model Selection**: model and reasoning depth can be adjusted to fit your
  actual project requirements — the current template is a reference starting
  point for general development
- 🎯 **Interaction Style**: Solves the "terminal reading disaster" of native Codex
  (cramped text, long sentences, and path clutter) by aligning with the `Claude Code`
  style. Features **forced line breaks, visual anchors, and concise brevity** to turn
  chaotic logs into structured, vivid dialog.
- 📝 **Dynamic Contract**: the main agent dynamically sends clear task
  instructions with goal/action/result structure
- ⚙️ **Concurrency Control**: `max_threads = n` for custom per-round parallel
  limits
- ⚠️ **Risk Management**: dangerous operation confirmation and immutable
  principles
- 🤖 **Custom Agents**: manually configure sub-agent model, reasoning effort,
  and role description
- 📋 **Reusable Templates**: ready-to-copy `AGENTS.template.en.md` and
  `config.toml.en.example`

## Core Files and Directories

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

**Related Docs**

- [CHANGELOG](./CHANGELOG.md)

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
|------|---------|--------------------|
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

**Existing configuration (manual merge)**: → See [Migration Guide](./docs/manual-merge.en.md)

> Note: this document is adapted for Codex CLI `v0.116.0`. Field names may
> differ across versions or providers, so always confirm against your local CLI.


## FAQ

**Q1: Does enabling `multi_agent` always speed things up?**

Not necessarily. Parallel execution only provides a clear benefit when tasks can
be broken down independently and have no write conflicts.

**Q2: What are the benefits of enabling sub-agents?**

- **Context isolation** — sub-agents run in their own context, preventing the
  main agent's context from bloating
- **Focused responsibility** — each sub-agent handles a single task, producing
  more precise output
- **Parallel efficiency** — independent tasks can run concurrently, reducing
  overall elapsed time

**Q3: Will sub-agents increase my costs?**

Yes. Enabling sub-agents may increase costs by **20%–30%**, depending on
project scale and task complexity.

**Q4: How many sub-agents should I run?**

Start with the default, observe quality and cost, then adjust gradually.

**Q5: What if the sub-agent model differs from the main agent model?**

Specify the model separately via the `model` field in `worker.toml` or
`explorer.toml`.

**Q6: Is this template suitable for everyone?**

No. It is a starting-point template — best tailored progressively to your
team's own conventions.


## Disclaimer

This repository provides configuration methodology and template references,
verified against Codex CLI `v0.116.0`.

**Cost note**: multi-agent mode may increase token usage by around 20% to 30%.
Evaluate the cost based on your actual workload.

**Risk note**: an LLM can still make wrong decisions and may delete data or
modify code incorrectly. Recommended precautions:

- configure sandbox permissions and confirmation rules carefully
- test in a controllable environment first
- keep backups for important data

You are responsible for any consequences caused by using these templates.
