---
name: terminal-dialog-style
description: Use when chatting in terminal, especially in terminal-first technical or business discussions, to ensure responses are terminal-friendly and visually structured.
---

# 🎨 Terminal Dialog Style

## Overview

Produce terminal-friendly responses: strong visual boundaries, vivid but concise wording, short sentences, clear structure, and obvious emphasis.
The goal is to help both technical and business readers understand and act quickly.

**Core principle**: Use **strong visual boundaries** (headings and separators) to organize content.


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
- 🎯 **Focus on key points** — Stay centered on the actual problem and avoid over-expanding. Focus on the core issue.


## 📐 Content Organization and Structure

- 🏷️ **Header anchors** — In terminal conversations, **never** use `#` / `##` / `###` Markdown heading syntax. Use `**bold**` (optionally with Emoji) as section headers. Put the heading on its own line and keep necessary whitespace.
- 📊 **Sub-group demotion** — When numbering discussion sections (e.g., "Case 1, Case 2"), use `**1️⃣ Section Title**` or `**1) Section Title**` bold-number format instead of `## 1) Title` heading syntax. Keep visual hierarchy flat.
- ✂️ **One point at a time** — Break long paragraphs into short sentences or bullets so each point carries one idea.
- 🔢 **Logical flow** — For multi-step tasks, use ordered lists such as `1. 2. 3.` or `1️⃣ 2️⃣ 3️⃣` to guide the eye.
- 📏 **Clear separation** — Use two blank lines between major blocks to create clean, "hard visual boundaries."
- 🖼️ **Show structure visually** — Prefer ASCII flowcharts or structure diagrams for complex processes instead of dense paragraphs.
- 💬 **Plain and direct** — Keep sentences short and conversational. Avoid jargon where possible; if you must use it, follow it immediately with a plain-English explanation.

> 📌 **TL;DR Convention**: For longer explanations, you **must** lead with a TL;DR summary so the reader grasps the core value within seconds.
> TL;DR **must** be wrapped in a `>` quote block with a 📌 or 🎯 icon, visually separated from the body text.
> **After the TL;DR block ends, you must leave one blank line before starting the body text** to ensure clear visual separation.
>
> Format example:
> ```
> > 🎯 **TL;DR**
> > The core issue is xxx, recommended approach is yyy.
>
> (One blank line before the body)
>
> Detailed explanation follows...
> ```


## 📍 Path Reference Convention (Mandatory)

> ⚠️ **This is a hard constraint.** In terminal conversations, any path containing directory prefixes (e.g., `src/`, `com/`, `main/java/`) is a violation.
> Whether the path is inline, in a list, or on its own line, it **must** be abbreviated to its short name.

**Allowed Formats (Three and only three)**:

```
  +----------------------+--------------------+----------------------------------------------+
  | Format               | Purpose            | Example                                      |
  +----------------------+--------------------+----------------------------------------------+
  | FileName.ext:Lline   | General reference  | TrainCourseManager.kt:L335                   |
  | FileName.ext:Lrange  | Range reference    | TrainCourseManager.kt:L335-356               |
  | File#method():Lline  | Method-level loc   | TrainCourseManager#calcCurProgress():L362    |
  +----------------------+--------------------+----------------------------------------------+
```

**Forbidden Formats (Avoid at all costs)**:

```
❌ src/main/java/com/mxwis/puait/bus/train/manager/TrainCourseManager.kt:335-356
❌ com.mxwis.puait.bus.train.manager.TrainCourseManager
❌ - src/main/java/.../UserService.java line 42
```

**Side-by-Side Comparison**:

```
  +---------------------------------------------------+------------------------------------+
  | ❌ Wrong                                          | ✅ Correct                         |
  +---------------------------------------------------+------------------------------------+
  | src/main/java/.../ApiOperationScanner.java:80      | ApiOperationScanner.java:L80       |
  | com.domain.module.bus.auth.scanner.ApiOperation... | ApiOperationScanner                |
  | - src/main/java/.../UserService.java:42-60         | UserService.java:L42-60            |
  | List: - src/.../TrainCourseManager.kt:335-356      | TrainCourseManager.kt:L335-356     |
  +---------------------------------------------------+------------------------------------+
```

**Recommended templates for locating source code in dialogue**:

```
Query Video Records:
  - TrainCourseManager#getVideoRecord():L335-356
Logic for 99% progress cap:
  - TrainCourseManager#calcCurProgress():L362-370
```

> 📌 **Rule Summary**:
> - Use only the filename, **never** include directory prefixes.
> - Use the `L` prefix for line numbers (`L42`, `L335-356`) to avoid ambiguity.
> - Use short class names: `UserCore` instead of `com.xxx.UserCore`.
> - Paths on their own line must also follow these abbreviation rules. No exceptions.


## 🎯 Visual and Layout Optimization

- 📏 **Concise and readable** — Control line length for terminal width; `<= 80` characters is recommended.
- 🫧 **Appropriate whitespace** — Use blank lines intentionally to avoid information crowding.
- 🔦 **Highlight the important part** — Use `*italic*` emphasis for key information.
- 📎 **Layer information with quotes** — Use `>` blocks to visually "frame" auxiliary information. When encountering **tips (💡), warnings (⚠️), core summaries (📌), or side notes (📝)**, use `>` to separate them from the body for better visibility.


## 🧩 Code and Data Display

- 📝 **Code blocks** — Use fenced Markdown code blocks with a language identifier for multi-line code, config, or logs.
- 🎯 **Focus on the core** — Omit irrelevant surrounding code (like imports) to highlight the critical logic.
- ✏️ **Diff markers** — Use `+` / `-` in diff blocks to make changes easy to spot.
- 🔢 **Line number assistance** — Add line numbers when necessary (e.g., in debugging scenarios).


## 📊 Structured Data and Diagrams

Focus on the **visual organization of information** for comparisons, flows, hierarchies, and other non-code content.

> ⚠️ **Priority Note**: This Skill intentionally places ASCII tables ahead of lists.
> In terminal environments, monospace fonts are naturally suited for table alignment. Multi-dimensional comparisons are far more readable in tables than in lists.
> This priority differs from general Markdown documentation standards and is a deliberate design for terminal scenarios.

> 🚫 **HARD PROHIBITION: Markdown Table Syntax**
> Terminal environments (like Codex CLI) **cannot render** Markdown tables (`| xxx | yyy |` syntax).
> Unrendered Markdown tables look messy and have extremely poor readability.
> **In terminal conversations, always use plain-text ASCII tables with box-drawing characters (`+---+`), and never use `|---|---|` Markdown table syntax.**

**Presentation Priority**:

1. 📊 **Plain-text ASCII Tables** — Use them when data features multi-dimensional comparisons and cell content is concise.
     - ✅ 4 columns or fewer, short cell content (core principle).
     - ✅ Suitable for: option comparisons, command parameter descriptions, status checklists, multi-dimensional evaluations.
     - ❌ Not suitable for: single-dimension explanations, long-form text, nested hierarchies.

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

2. 🌳 **Plain-text ASCII Diagrams** — Use them when text alone cannot clearly express structure, flow, or hierarchy.
     - ✅ Suitable for: architecture diagrams, file trees, state machines, flowcharts, class diagrams, dependency graphs.
     - 🔧 Common symbols: `├──`, `└──`, `│`, `→`, `┌┐└┘`, `[node]`, `●`.
     - 📏 Keep it concise (usually ≤20 lines, max 35 for complex cases). **Must accompany with text explanation.**

Example:
```
  🔴 High Risk (Direct code modification or command execution)
  ├── execute_shell_command  ← arbitrary command execution, highest risk
  ├── create_text_file       ← may overwrite files

  🟡 Medium Risk (Add/Modify with some control)
  ├── insert_after_symbol    ← add code
  └── switch_modes           ← mode switching may bypass safeguards

  🟢 Low Risk (Knowledge handling, no code edits)
  ├── write_memory           ← write knowledge
  └── onboarding             ← project analysis
```

3. 📋 **Lists** — The default fallback for most scenarios.


## ✅ Suggested Ending Style

- 📝 **Brief Summary** — Attach a short summary after complex content to reiterate core points.
- 👉 **Next-Step Guidance** — End with practical advice, action plans, or encouragement for further questions.


## ❌ Common Mistakes

- 🚫 **Using `##` heading syntax in conversation** — Terminal conversations should use bold grouping. `##` headers are visually too heavy and break the flat flow of dialogue.
- 🚫 **Using Markdown tables in terminal** — **Hard Violation.** The `| xxx | yyy |` syntax does not render in terminal, showing up as scattered text. You must use `+---+` ASCII tables.
- 🚫 **Using overly wide tables** — Long content, code, or narrative inside tables will lead to catastrophic line wrapping in the terminal.
- 🚫 **Paths containing directory prefixes** — **Hard Violation.** Whether inline or in lists, you must only use the filename (see "📍 Path Reference Convention").
- 🚫 **Dense blocks of pure text** — Lack of visual anchors makes it impossible for readers to locate information quickly.
- 🚫 **Decorative ASCII diagrams** — Diagrams should serve understanding, not just aesthetics.
- 🚫 **Missing TL;DR** — Long content without a `>` quote block summary forces the reader to scan the entire message to grasp the point.
