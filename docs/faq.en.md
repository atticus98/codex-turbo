# FAQ

## 1) Does enabling `multi_agent` always make things faster?
No. Only when tasks are divisible and have no write conflicts will you see significant speedup.

## 2) What are the benefits of enabling sub-agents?

- **Context Isolation** — Sub-agents have independent contexts, avoiding main agent context explosion
- **Focused Responsibility** — Each sub-agent handles a single task, producing more precise output
- **Parallel Efficiency** — Independent tasks can run in parallel, reducing overall time

## 3) Will multi-agent increase costs?
Yes. Enabling sub-agents may increase costs by **20%~30%**, depending on project scale and task complexity.

## 4) How many agents should I run in parallel?
Start with 5, observe quality and cost, then adjust gradually.

## 5) What if sub-agent model differs from main agent model?
Specify the model via the `model` field in `worker.toml` or `explorer.toml`.

## 6) Is this template suitable for everyone?
No. It's a starting template, best tailored to your team's habits through gradual pruning.
