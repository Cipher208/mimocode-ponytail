# mimocode-ponytail

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MiMoCode](https://img.shields.io/badge/MiMoCode-%3E%3D0.38.0-blue.svg)](https://github.com/nicepkg/mimocode)

> Lazy senior dev mode for MiMoCode — YAGNI rules injected automatically via file hooks.

*He says nothing. He writes one line. It works.*

## What it does

Ponytail forces the laziest solution that actually works. Before writing code, the agent stops at the first rung that holds:

1. Does this need to exist at all? → skip (YAGNI)
2. Stdlib does it? → use it
3. Native platform feature? → use it
4. Already-installed dependency? → use it
5. One line? → one line
6. Only then: the minimum that works

## Installation

```bash
# Clone and copy
git clone https://github.com/Cipher208/mimocode-ponytail.git /tmp/mimocode-ponytail
mkdir -p ~/.config/mimocode/hooks
mkdir -p ~/.config/mimocode/ponytail/skills
cp /tmp/mimocode-ponytail/hooks/ponytail.ts ~/.config/mimocode/hooks/
cp /tmp/mimocode-ponytail/skills/*.md ~/.config/mimocode/ponytail/skills/
```

Or one-liner:

```bash
mkdir -p ~/.config/mimocode/hooks ~/.config/mimocode/ponytail/skills && \
git clone https://github.com/Cipher208/mimocode-ponytail.git /tmp/mimocode-ponytail && \
cp /tmp/mimocode-ponytail/hooks/ponytail.ts ~/.config/mimocode/hooks/ && \
cp /tmp/mimocode-ponytail/skills/*.md ~/.config/mimocode/ponytail/skills/
```

Then restart MiMoCode.

## How it works

MiMoCode's file hooks system loads `~/.config/mimocode/hooks/ponytail.ts`. This hook:

1. **Injects YAGNI rules** into the system prompt via `experimental.chat.system.transform`
2. **Handles `/ponytail` commands** via `tool.execute.before`
3. **Persists mode** to `~/.config/mimocode/ponytail/mode`

The rules are injected before every LLM call — not just once. This means the agent stays in ponytail mode across the entire session.

## Commands

| Command | What it does |
|---------|-------------|
| `/ponytail` | Show current mode |
| `/ponytail lite` | Set lite mode — name lazier alternative, user picks |
| `/ponytail full` | Set full mode (default) — ladder enforced |
| `/ponytail ultra` | Set ultra mode — YAGNI extremist |
| `/ponytail off` | Disable ponytail |
| `/ponytail review` | Review diff for over-engineering |
| `/ponytail audit` | Audit repo for bloat |
| `/ponytail debt` | List deferred shortcuts |
| `/ponytail gain` | Show impact scoreboard |
| `/ponytail help` | Quick reference |

## Intensity levels

| Level | Behavior |
|-------|----------|
| **lite** | Build what's asked, but name the lazier alternative. User picks. |
| **full** | The ladder enforced. Stdlib and native first. Shortest diff. Default. |
| **ultra** | YAGNI extremist. Deletion before addition. Ship the one-liner. |

## Skills

6 bundled skills in `skills/`:

- `ponytail.md` — Main rules (YAGNI ladder)
- `ponytail-review.md` — Review for over-engineering
- `ponytail-audit.md` — Audit repo for bloat
- `ponytail-debt.md` — Track deferred shortcuts
- `ponytail-gain.md` — Impact scoreboard
- `ponytail-help.md` — Quick reference

## Based on

This is an adaptation of [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) (Hermes plugin) for MiMoCode's file hooks system.

Key differences:
- Hermes: `pre_llm_call` + `pre_gateway_dispatch` hooks → MiMoCode: `experimental.chat.system.transform` + `tool.execute.before`
- Mode persistence: Hermes in-memory → MiMoCode file-based (`~/.config/mimocode/ponytail/mode`)
- Skills: Hermes `register_skill()` → MiMoCode file-based skills in `ponytail/skills/`

## License

MIT
