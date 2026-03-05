# KDBP — Khujta Deep Behavior Protocol

A behavioral tracking and introspection framework for Claude Code workflows.

**Handle:** "The bones don't change. The nervous system adapts."

## What It Does

KDBP adds three capabilities to any Claude Code project:

1. **Lightweight recording** — Automatic ledger entries and cost tracking at workflow completion
2. **Dynamic injection** — Project-specific knowledge and values modify workflow behavior at designated points
3. **On-demand introspection** — Human-triggered alignment checks, story/epic checkpoints, and behavior evolution

## Architecture

```
Static core (ECC workflows)     → dev, review, deploy, create-story
  + Dynamic injection (KDBP)    → values/knowledge modify behavior at injection points
  + On-demand introspection     → /khujta-dbp EA, SC, EC, EB when human decides
```

Development workflows are structurally identical across all projects.
What changes between projects is the values and knowledge loaded at injection points.

## Installation

```bash
# 1. Copy KDBP into your project
cp -r _kdbp/ <project>/_kdbp/

# 2. Install hooks (shared base + KDBP custom)
cp _kdbp/hooks/shared/* <project>/.claude/hooks/
cp _kdbp/hooks/*.{py,sh} <project>/.claude/hooks/

# 3. Copy commands to .claude/commands/
cp _kdbp/commands/*.md <project>/.claude/commands/

# 4. Initialize behaviors
# Run /kdbp-init in the project to set up behaviors/
```

## Directory Structure

```
_kdbp/
  agents/           — khujta-dbp behavioral agent (20 protocols)
  behaviors/        — Template structure (REGISTRY, trajectory, stories, epics)
  commands/         — 12 slash commands (/kdbp-dev-story, /kdbp-init, etc.)
  core/             — Workflow engine + PROTOCOL-v2.md (historical reference)
  hooks/
    shared/         — 10 common hooks (Tier 1 enforcement, shared with ECC)
    *.py, *.sh      — 2 KDBP-specific hooks (P1 infra, P6 orphan refs)
  knowledge/        — 7 reference documents (loaded on-demand by workflows)
  workflows/        — 11 workflows (95 step files)
```

## Workflows

### Development (static core + injection points)
| Command | Steps | Purpose |
|---------|-------|---------|
| `/kdbp-dev-story` | 11 | TDD-first development with ledger recording |
| `/kdbp-code-review` | 9 | Adaptive multi-agent review |
| `/kdbp-create-story` | 9 | Story creation from epic |
| `/kdbp-create-epics` | 13 | Epic + story batch generation |

### Planning (KDBP-only, A/P/C menus)
| Command | Steps | Purpose |
|---------|-------|---------|
| `/kdbp-prd` | 10 | Product requirements document |
| `/kdbp-architect` | 8 | Architecture design |
| `/kdbp-ux-design` | 7 | UX specification |
| `/kdbp-brainstorm` | 6 | Ideation (target 100 ideas) |

### Behavioral Management
| Command | Steps | Purpose |
|---------|-------|---------|
| `/kdbp-init` | 9 | One-time behavioral bootstrap |
| `/kdbp-evolve-behavior` | 7 | Evolution engine (The Roast, triple loop) |
| `/kdbp-alignment-check` | 6 | On-demand reflection checkpoint |

### On-Demand Agent
| Command | Purpose |
|---------|---------|
| `/khujta-dbp` | 20-item behavioral agent menu (full) |
| `/khujta-dbp reflect` | 5-item reflection menu |

## Knowledge Files

| File | Purpose | Loaded When |
|------|---------|-------------|
| quick-reference.md | Agent default load (~240 tokens) | Agent activation |
| format-reference.md | Block templates (Value, Gabe, Intent) | Writing blocks |
| dbp-workflow-integration.md | Integration architecture | Workflow step-00 |
| code-review-patterns.md | 16 code review heuristics | Code review step-00 |
| hardening-patterns.md | 6 proactive debt reduction patterns | Epic creation |
| adversarial-patterns.md | 12 recurring structural blind spots | Evolution, review |
| infrastructure-manifest.md | Required files per directory type | Pre-write hook |

## Key Design Decisions

- **Record always, evaluate on demand.** Ledger entries are automatic and cheap (~500 tokens). Alignment evaluation is human-triggered and thorough.
- **PROTOCOL-v2.md is historical reference.** Operational content lives in knowledge files and workflow steps. Agent loads quick-reference.md (~240 tokens), not the full protocol (~3,800 tokens).
- **Hooks are Tier 1 (automatic).** Everything else is Tier 2 at best. "If it's not a hook, it's a suggestion."
- **Graceful degradation.** If behaviors/ doesn't exist, all KDBP checks become no-ops. Zero overhead.
