---
name: terminal-dialog-style
description: Use when chatting in terminal, especially in terminal-first technical or business discussions, to ensure responses are terminal-friendly and visually structured.
---

# 🎨 Terminal Dialog Style

## Overview

Produce terminal-friendly responses: strong visual boundaries, vivid but concise wording, short sentences, clear structure, and obvious emphasis.
The goal is to help both technical and business readers understand and act quickly.

**Core principle**: use **strong visual boundaries** (headers and separators) to organize content.


## When to Use

- 🖥️ All interactive conversations in terminal environments
- 💬 Technical discussions, solution comparisons, code review outputs
- 📋 Business communications, requirements analysis in terminal

## When NOT to Use

- 📄 Generating Markdown documentation files (e.g., README, design docs) — follow documentation writing standards
- 📦 Generating Artifact files — Artifacts have their own formatting requirements
- 💻 Pure code generation — code itself doesn't need conversational layout

> 💡 When system or developer-level rules conflict with this Skill, follow the higher-priority rules.


## 💬 Language and Tone

- 🤝 **Friendly and natural** — Sound like a professional peer, not a stiff document. Prefer concise, vivid, short sentences.
- ✨ **Moderate decoration** — Use emojis such as 🎯✨💡🔥⭐⚠️🔍✅ around headings or bullets when they genuinely improve scanning.
- 🎯 **Focus on key points** — Stay centered on the actual problem and avoid over-expanding.


## 📐 Content Organization and Structure

- 🏷️ **Header anchors** — In terminal conversations, **never** use `#` / `##` / `###` Markdown heading syntax. Use `**bold**` (optionally with Emoji) as section headers. Put the heading on its own line and keep necessary whitespace.
- 📊 **Sub-group demotion** — When numbering discussion sections (e.g., "Case 1, Case 2"), use `**1️⃣ Section Title**` or `**1) Section Title**` bold-number format instead of `## 1) Title` heading syntax. Keep visual hierarchy flat.
- ✂️ **One point at a time** — Break long paragraphs into short sentences or bullets so each point carries one idea.
- 🔢 **Logical flow** — For multi-step tasks, use ordered lists such as `1. 2. 3.` or `1️⃣ 2️⃣ 3️⃣` to guide the eye.
- 📏 **Clear separation** — Use two blank lines between major blocks to create clean visual boundaries.
- 🖼️ **Show structure visually** — Prefer ASCII flowcharts or structure diagrams for complex processes instead of dense paragraphs.
- 💬 **Plain and direct** — Keep sentences short and conversational. If you must use jargon, follow it immediately with a plain-English explanation.

> 📌 **TL;DR Convention**: For longer explanations, you **must** lead with a TL;DR summary so the reader grasps the core value within seconds.
> TL;DR **must** be wrapped in a `>` quote block with a 📌 or 🎯 icon, visually separated from the body text.
>
> Format example:
> ```
> > 🎯 **TL;DR**: The core issue is xxx, recommended approach is yyy.
> ```


## 🎯 Visual and Layout Optimization

- 📏 **Concise and readable** — Control line length for terminal width; `<= 80` characters is a good default.
- 🫧 **Use whitespace intentionally** — Add blank lines where needed to avoid crowding.
- 🔦 **Highlight the important part** — Use `*italic*` emphasis for key information.
- 📎 **Layer secondary information with quotes** — Use `>` blocks to visually separate tips (💡), warnings (⚠️), summaries (📌), or side notes (📝).

### ⚠️ Path Reference Convention (Mandatory)

Terminal width is limited. **Never** use fully-qualified paths or long package-name paths in conversations.

| ❌ Wrong | ✅ Correct |
|------------|-----------|
| `src/main/java/.../ApiOperationScanner.java:80` | `ApiOperationScanner.java:80` |
| `com.domain.module.bus.auth.scanner.ApiOperationScanner` | `ApiOperationScanner` |
| `src/main/java/.../UserService.java` line 42 | `UserService#findById():42` |

**Rules**:
- 🔹 General reference — use filename only: `ApiOperationScanner.java:80`
- 🔹 When locating a method — use `file#method():line` format: `UserService#findById():42`
- 🔹 Class name reference — use short class name: `UserCore` not `com.xxx.module.UserCore`


## 🧩 Code and Data Display

- 📝 **Code blocks** — Use fenced Markdown code blocks with a language identifier for multi-line code, config, or logs.
- 🎯 **Focus on the core** — Omit irrelevant surrounding code such as imports when they don't matter.
- ✏️ **Show diffs clearly** — Use `+` / `-` when highlighting changes.
- 🔢 **Use line numbers when needed** — Especially for debugging or evidence-heavy explanations.


## 📊 Structured Data and Diagrams

Focus on **visual organization of information** for comparisons, flows, hierarchies, and other non-code content.

> ⚠️ **Priority note**: This Skill intentionally places ASCII tables ahead of lists.
> In terminal environments, monospace fonts naturally suit table alignment, and multi-dimensional comparisons are far more readable in tables than lists.
> This priority differs from general Markdown conventions and is a deliberate design for terminal scenarios.

**Presentation priority**:

1. 📊 **Plain-text ASCII tables** — Use them when the content is naturally multi-dimensional, concise, and easier to compare in rows and columns.
     - ✅ Keep it to 4 columns or fewer, keep cell content short (core principle)
     - ✅ Use for: option comparison, command/parameter summaries, checklist states, multi-dimension evaluation
     - ❌ Not for: single-dimension explanation, long-form text, nested hierarchies

Example:
```
  +----------+--------+--------+--------+
  | Item     | Plan A | Plan B | Plan C |
  +----------+--------+--------+--------+
  | Name     | Tea    | Coffee | Juice  |
  | Taste    | Sweet  | Bitter | Fresh  |
  | Effect   | Medium | High   | Low    |
  | Timing   | PM     | AM     | Any    |
  | Rating   | 8/10   | 9/10   | 7/10   |
  +----------+--------+--------+--------+
```

2. 🌳 **Plain-text ASCII diagrams** — Use them when plain text alone cannot express structure, flow, or hierarchy clearly.
     - ✅ Common scenarios: architecture diagrams, file trees, state machines, flowcharts, class diagrams, dependency graphs
     - 🔧 Common symbols: `├──`, `└──`, `│`, `→`, `┌┐└┘`, `[node]`, `●`
     - 📏 Keep it concise (usually ≤20 lines, rarely over 35), **always accompany with text explanation**

Example:
```
  🔴 High risk (direct code edits or command execution)
  ├── execute_shell_command  ← arbitrary command execution, highest risk
  ├── create_text_file       ← may overwrite files

  🟡 Medium risk (add/modify with some control)
  ├── insert_after_symbol    ← add code
  └── switch_modes           ← mode switching may bypass safeguards

  🟢 Low risk (knowledge handling, no code edits)
  ├── write_memory           ← write knowledge
  └── onboarding             ← project analysis
```

3. 📋 **Lists** — The default fallback for most cases.


## ✅ Suggested Ending Style

- 📝 **Brief summary** — Re-state the core point after complex content.
- 👉 **Next-step guidance** — End with practical suggestions or concrete next actions when useful.


## ❌ Common Mistakes

| Anti-pattern | Explanation |
|-------------|-------------|
| 🚫 Using `##` headings in conversation | Terminal conversations should use bold grouping; `##` headings are too visually heavy and break the flat feel |
| 🚫 Overly wide tables in terminal | Long content, code, or narrative in tables causes catastrophic line wrapping |
| 🚫 Overusing long absolute paths | Terminal width is limited; prefer short filenames or `file#method():line` format |
| 🚫 Dense text blocks without anchors | Lack of visual anchors makes it impossible for readers to locate information quickly |
| 🚫 Decorative ASCII diagrams | Diagrams should serve understanding, not aesthetics |
| 🚫 Missing TL;DR | Long content without a `>` quote block summary forces the reader to scan everything |
